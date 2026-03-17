# AGENTS

Dieses Dokument enthaelt projektbezogene Arbeitsregeln fuer Agenten im Repository.

## Ziel des Projekts

Der Demonstrator soll Kolleginnen und Kollegen demonstrieren, wie eine Software aufgebaut sein könnte. Die Software dient der Eingabe von Informationen zu meldepflichtigen Infektionskrankheiten nach dem IfSG. 
Die bisherige Software erfasst viele Eingaben vor allem als Checkbox, die man an- und abhaken kann ("flache Eingabe"). Dieser Demonstrator zeigt die Möglichkeiten einer "erweiterbaren Liste".

## Ressourcen
- Screenshots der alten Software im ordner `survnet_screenshots/`
- Sammlung aller sichtbaren Variablen in `survnet_variablen.csv`
- Screenshot des Designs der zu entstehenden Software

## Bereits umgesetzt

### Laborangaben
- Erregerabhaengige Testkonfiguration
- Sequenzierungsinformationen
- Resistenzprofile inkl. abgeleiteter ID

### Klinische Informationen
- Erweiterbare Symptomliste umgesetzt
- Verbindliche Feldstruktur: Symptom, Datum Beginn, Datum Ende, Sicherheit
- Sicherheitswerte als Auswahl: vermutet, von der betroffenen Person erfragt,
  von weiterer Person erfragt

### Risikofaktoren
- Erweiterbare Liste umgesetzt
- Verbindliche Feldstruktur: Risikofaktor, Datum Beginn, Datum Ende, Sicherheit

### Expositionen
- Erweiterbare Liste umgesetzt
- Verbindliche Feldstruktur: Exposition, Art des Kontaktes, Datum Beginn, Datum Ende, Sicherheit, Nachweis in der Quelle
- Expositionsoptionen pro Erreger zentral in `PATHOGEN_CONFIG`

### In Planung
- Erweiterbare Liste fuer weitere klinische Kontextfelder (nicht symptomzeilenbasiert)

### Naechster Umsetzungsschritt
- Weitere klinische Kontextfelder fachlich priorisieren und als eigene Eingabebloecke modellieren


## Aktuelle technische Basis

- Reines Frontend in `index.html`
- Keine externen Abhaengigkeiten
- Kein Build- oder Testsystem eingerichtet

## Arbeitsprinzipien fuer kommende Aenderungen

- Bestehendes Verhalten nicht ungefragt aendern
- Bei neuen Features die bestehende Datenstruktur (`rows`, `PATHOGEN_CONFIG`) weiterverwenden
- Komplexe Logik in kleine, klar benannte Funktionen aufteilen
- UI-Anpassungen responsiv halten
- Deutsche Fachbegriffe im UI konsistent beibehalten
- Fuer neue erweiterbare Listen (z. B. klinische Informationen) dieselben Interaktionsmuster nutzen
  (hinzufuegen, duplizieren, loeschen, valide Default-Werte)
- Erregerabhaengige Optionen zentral in `PATHOGEN_CONFIG` halten, keine verteilten Hardcodings
- Bei klinischen Eintraegen die verbindliche Feldstruktur beibehalten
  (Symptom, Datum Beginn, Datum Ende, Sicherheit)
- Bei Risikofaktoren die verbindliche Feldstruktur beibehalten
  (Risikofaktor, Datum Beginn, Datum Ende, Sicherheit)
- Bei Expositionen die verbindliche Feldstruktur beibehalten
  (Exposition, Art des Kontaktes, Datum Beginn, Datum Ende, Sicherheit, Nachweis in der Quelle)
- Erregerwechsel muss ungueltige Auswahlwerte in allen Listen defensiv zuruecksetzen

## Dokumentationspflicht

Bei relevanten Projektfortschritten muessen beide Dateien aktualisiert werden:

- `README.md`: Nutzer- und Projektperspektive (Funktionen, Setup, Nutzung, Status)
- `AGENTS.md`: Umsetzungs- und Arbeitsregeln (Architekturhinweise, Konventionen, offene Leitlinien)

Wenn sich Scope, Architektur oder Workflows aendern, sollen diese Aenderungen hier explizit
nachgezogen werden.

Fuer dieses Projekt gilt: Nach jedem relevanten Feature-Schritt zuerst Dokumentation angleichen,
dann Implementierung fortsetzen.
