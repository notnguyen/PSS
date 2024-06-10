# PSS

# Dokumentace DJ ovládacího boxu

## Přehled

Tento dokument poskytuje instrukce k použití DJ ovládacího boxu, který umožňuje ovládat DJ software, jako je Mixxx, pomocí tlačítek a posuvníků. Ovládací box je navržen tak, aby byl jednoduchý a efektivní, obsahuje tlačítka pro přehrávání, zastavení, označení místa (cue) a dva posuvníky hlasitosti. Je připojen k počítači pomocí rozhraní MIDI pomocí Arduina Leonardo.

## Komponenty

- Arduino Leonardo
- 2x Posuvné potenciometry (pro ovládání hlasitosti)
- 3x Tlačítka (pro funkce přehrávání, zastavení a označení místa)
- Dráty pro propojení

## Nastavení

1. **Propojení komponent**: Propojte komponenty podle následujících připojení:
   - Propojte posuvné potenciometry s analogovými piny A0 a A1 na Arduinu pro ovládání hlasitosti.
   - Propojte tlačítka s digitálními piny 2, 3 a 4 na Arduinu pro funkce přehrávání, zastavení a označení místa.

2. **Nahrání kódu**: Nahrajte kód pro Arduina (viz níže) do Arduina Leonardo.

3. **Připojení k DJ softwaru**: V DJ softwaru (např. Mixxx) nakonfigurujte MIDI mapování tak, aby odpovídalo tlačítkům a posuvníkům na ovládacím boxu.

## Funkce

- **Tlačítko Přehrávání**: Stisknutím tohoto tlačítka začne přehrávání skladby.
- **Tlačítko Zastavení**: Stisknutím tohoto tlačítka zastavíte přehrávání skladby.
- **Tlačítko Označení místa (Cue)**: Stisknutím tohoto tlačítka nastavíte označení místa v aktuální pozici skladby.
- **Posuvníky hlasitosti**: Posouváním těchto posuvníků upravíte hlasitost každého přehrávacího kanálu v DJ softwaru.

