# Garage App - Anleitung

## Übersicht
Die Garage App verwaltet deine Fahrzeuge (Autos, Töffli, Töff). Alle Daten werden im Browser gespeichert.

## Funktionen

### Fahrzeuge hinzufügen
1. Wähle den Fahrzeugtyp (Auto, Töffli, Töff)
2. Fülle die Felder aus (Marke, Kennzeichen, Baujahr, etc.)
3. Klicke auf "Speichern"

### Fahrzeugdetails bearbeiten
- Klicke auf eine Fahrzeugkarte
- Wechsle zwischen "Infos" und "Teile"
- Ändere die Daten und klicke "Änderungen speichern"

### Service-Benachrichtigung
- Trage das Service-Datum im Format `TT.MM.JJJJ` ein (z.B. 15.03.2024)
- Die App warnt dich **30 Tage vor dem Service-Termin**
- Fällige Services werden rot markiert auf der Fahrzeugkarte
- Ein Banner oben zeigt alle fälligen Services an

### Teile verwalten
1. Öffne ein Fahrzeug
2. Klicke auf "Teile"
3. Wähle die Kategorie (Auto, Töffli, Töff)
4. Füge Teile mit Name und Anzahl hinzu

### Daten speichern (Export)
- Klicke auf "Daten exportieren"
- Es wird eine `garage_export_YYYY-MM-DD.json` Datei heruntergeladen
- Diese Datei enthält alle deine Fahrzeuge

### Daten laden (Import)
- Klicke auf "Daten importieren"
- Wähle eine zuvor exportierte JSON-Datei
- Wähle "OK" zum Überschreiben oder "Abbrechen" zum Hinzufügen

## Tipps
- Das Service-Datum muss im Format `TT.MM.JJJJ` eingegeben werden
- Die Daten bleiben im Browser gespeichert (localStorage)
- Exportiere regelmässig ein Backup deiner Daten
- Zum Löschen eines Fahrzeugs: Klicke auf "Löschen" auf der Fahrzeugkarte

## Dateien
- `index.html` - Die App (einfach im Browser öffnen)
- `ANLEITUNG.md` - Diese Anleitung
