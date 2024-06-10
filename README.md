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

## Arduino Kód

```arduino
#include <MIDI.h>

// Definice pinů pro tlačítka
#define PIN_TLACITKO_PREHRAT 2
#define PIN_TLACITKO_ZASTAVIT 3
#define PIN_TLACITKO_CUE 4

// Definice pinů pro posuvníky hlasitosti
#define PIN_POSUVNIK_1 A0
#define PIN_POSUVNIK_2 A1

MIDI_CREATE_DEFAULT_INSTANCE();

void setup() {
  // Inicializace MIDI
  MIDI.begin(MIDI_CHANNEL_OMNI);

  // Nastavení pinů pro tlačítka jako vstupy
  pinMode(PIN_TLACITKO_PREHRAT, INPUT_PULLUP);
  pinMode(PIN_TLACITKO_ZASTAVIT, INPUT_PULLUP);
  pinMode(PIN_TLACITKO_CUE, INPUT_PULLUP);
}

void loop() {
  // Kontrola stisknutých tlačítek
  if (digitalRead(PIN_TLACITKO_PREHRAT) == LOW) {
    MIDI.sendNoteOn(0x3C, 127, 1); // MIDI nota pro tlačítko Přehrát
    delay(100); // Omezení pro odstranění bouncingu
  }

  if (digitalRead(PIN_TLACITKO_ZASTAVIT) == LOW) {
    MIDI.sendNoteOn(0x3D, 127, 1); // MIDI nota pro tlačítko Zastavit
    delay(100); // Omezení pro odstranění bouncingu
  }

  if (digitalRead(PIN_TLACITKO_CUE) == LOW) {
    MIDI.sendNoteOn(0x3E, 127, 1); // MIDI nota pro tlačítko Cue
    delay(100); // Omezení pro odstranění bouncingu
  }

  // Čtení hodnot z analogových pinů pro posuvníky hlasitosti a odesílání MIDI zpráv
  int hlasitost1 = analogRead(PIN_POSUVNIK_1) / 8; // Mapování rozsahu 0-1023 na 0-127
  MIDI.sendControlChange(0x07, hlasitost1, 1); // MIDI zpráva pro posuvník 1

  int hlasitost2 = analogRead(PIN_POSUVNIK_2) / 8; // Mapování rozsahu 0-1023 na 0-127
  MIDI.sendControlChange(0x08, hlasitost2, 1); // MIDI zpráva pro posuvník 2
}
