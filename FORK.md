# PF2e Bestiary Tracking — fork stołu

Fork modułu [WBHarry/pf2e-bestiary-tracking](https://github.com/WBHarry/pf2e-bestiary-tracking) dla światów PF2e
stołu. Praca idzie na gałęzi `table`; `main` stoi tak jak u oryginału. Id modułu zostaje `pf2e-bestiary-tracking`, bo
pod nim świat trzyma bestiariusz (dziennik i ustawienia modułu). Motywy daje fork stołu PF2e Subsystem Theming
(`D:\Tabletop\Foundry\Development\pf2e-subsystem-theming`).

## Czym różni się od oryginału

- Napisy szablonów idą przez klucze językowe: pola biografii, "Recall Knowledge", obrona i zasięg zaklęcia — przez
  klucze systemu PF2e (`PF2E.Biography*`, `PF2E.RecallKnowledge.Label`, `PF2E.Item.Spell.Defense.Label`,
  `PF2E.TraitRange`), napisy menu powiązań aktorów — przez nowe klucze modułu (`PF2EBestiary.LinkMenu.*`,
  `PF2EBestiary.Miscellaneous.InvalidBestiaryLink`).
- ST Pozyskiwania Wiedzy istoty to etykiety systemu (`PF2E.Actor.NPC.Identification.Skills.Label`, `….Lore.Label`)
  z listą umiejętności w zapisie języka klienta (`game.i18n.getListFormatter`, alternatywa); oryginał składał je po
  angielsku i nie dawał "or" przed ostatnią umiejętnością.
- Typ obrażeń w ataku to zapis systemu w formule obrażeń (`CONFIG.PF2E.damageRollFlavors`), nie slug.
- `module.json` bez `manifest` i `download` oryginału, także w relacji wymagającej Theming, więc aktualizacja
  Foundry nie podmieni forka ani jego zależności oryginałem; wersja to wydanie oryginału z czwartym członem
  (`1.3.10.2`). Wersja danych (`currentVersion` w `scripts/setup.js`, migracje bestiariusza) zostaje wersją
  oryginału.

## Build i wdrożenie

```
npm ci
npm run package                      # BestiaryTracking.js, CSS, paczka kompendium → dist/pf2e-bestiary-tracking
foundry-server deploy dist/pf2e-bestiary-tracking
```

`BestiaryTracking.js` i `styles/pf2e-bestiary-tracking.css` to wynik builda, commitowany jak u oryginału; hook
`husky` przepuszcza commit przez prettiera, jak u oryginału. Środowisko testowe dowiązuje `dist/pf2e-bestiary-tracking`
w profilach `pl-pf2e-ui` i `pl-pf2e-malevolence`; polski widok sprawdza w workspace PF2e
`tests/foundry/bestiary-tracking.js` (profil `pl-pf2e-ui`). Angielski plik języka bierze z gałęzi `table` ekstraktor
przekładu (`tools/PackExtractor/config.json` w workspace PF2e).

## Nowe wydanie oryginału

`git fetch upstream`, merge jego tagu albo `main` na `table`, `npm run package`, wersja w `module.json` — nowe
wydanie oryginału z `.1` — scenariusz bestiariusza, deploy.
