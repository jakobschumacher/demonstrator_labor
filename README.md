# IfSG-Demonstrator (Labor + Klinik)

Ein einfacher Frontend-Demonstrator zur Erfassung von Informationen zu meldepflichtigen
Infektionskrankheiten (IfSG).

Der Demonstrator orientiert sich an der Erfassung meldepflichtiger Infektionskrankheiten
nach IfSG und zeigt den Ansatz einer erweiterbaren Liste statt rein flacher Checkbox-Eingaben.

## Projektstatus

- Aktueller Stand: Einzelne statische HTML-Datei mit eingebettetem CSS und JavaScript
- Einstiegspunkt: `index.html`
- Persistenz/Backend: keines (nur In-Memory im Browser)
- Fokus aktuell: Vier erweiterbare Listen fuer Labor, Klinik, Risikofaktoren und Exposition

## Aktueller Funktionsumfang (Labor)

- Verwaltung mehrerer Labortest-Zeilen (hinzufuegen, duplizieren, loeschen)
- Erregerabhaengige Konfiguration fuer:
  - Methoden
  - Materialien
  - hierarchische Erregerauswahl
- Modal fuer Sequenzierungsergebnis (ID und Kommentar)
- Modal fuer Resistenzprofil mit dynamischer Resistenz-ID
- Beispielkonfigurationen fuer:
  - Enterobacterales
  - Campylobacter
  - Tuberkulose

## Zielbild Funktionsumfang (Labor + Klinik)

- Erweiterbare Laborliste (bereits umgesetzt)
- Erweiterbare klinische Liste fuer Symptome (bereits umgesetzt)
- Erweiterbare Liste fuer Risikofaktoren (bereits umgesetzt)
- Erweiterbare Liste fuer Expositionen (bereits umgesetzt)
- Einheitliche Interaktionen ueber beide Listen hinweg

## Ausfuehrung

Da es ein statischer Demonstrator ist, reicht das Oeffnen der Datei im Browser:

1. `index.html` direkt im Browser oeffnen
2. Optional lokal via einfachem HTTP-Server bereitstellen (z. B. `python -m http.server`)

## Struktur

- `index.html`: komplette App (Markup, Styles, Logik)

## Umgesetzte Erweiterung: Klinische Informationen

Neben den Laborangaben ist eine zweite erweiterbare Liste fuer klinische Informationen
(Symptome des Patienten) umgesetzt.

Beispiel-Felder je klinischem Eintrag:

- Symptom
- Datum Beginn
- Datum Ende
- Sicherheit der Informationsermittlung

Auswahl fuer die Sicherheit der Informationsermittlung:

- vermutet
- von der betroffenen Person erfragt
- von weiterer Person erfragt

### Umsetzung

- Eigene klinische Datenstruktur getrennt von `rows` angelegt
- Erregerabhaengige Symptomlisten in `PATHOGEN_CONFIG` hinterlegt
- Eigene UI-Sektion mit den Aktionen hinzufuegen, duplizieren, loeschen umgesetzt
- Datumsvalidierung eingebaut (`Datum Ende` darf nicht vor `Datum Beginn` liegen)

### Erfuellte Kriterien

- Klinische Eintraege sind als erweiterbare Liste pflegbar
- Bestehende Laborfunktionen bleiben unveraendert nutzbar
- Erregerwechsel behandelt ungueltige klinische Auswahlwerte konsistent
- README und AGENTS werden bei Abschluss des Features gemeinsam aktualisiert

### Abgleich mit `survnet_variablen.csv`

- Breite Ueberschneidung mit dem gewuenschten Modell: `Symptome/Kriterien` + Datumsbezug (`Erkrankungsbeginn`, teils `am`)
- Fuer Enterobacterales und Tuberkulose existieren zusaetzliche klinische Kontextfelder
  (z. B. `infiziert/kolonisiert`, organbezogene Angaben, Diagnose-/Behandlungskontext), die nicht symptomzeilenbasiert sind
- Diese Kontextfelder bleiben fuer den Demonstrator bewusst ausserhalb der neuen Symptomliste

## Umgesetzte Erweiterung: Risikofaktoren und Expositionen

- Risikofaktoren als erweiterbare Liste mit Spalten: `Risikofaktor`, `Datum Beginn`, `Datum Ende`, `Sicherheit`
- Expositionen als erweiterbare Liste mit Spalten: `Exposition`, `Art des Kontaktes`, `Datum Beginn`, `Datum Ende`, `Sicherheit`, `Nachweis in der Quelle`
- Beide Listen nutzen dieselben Interaktionsmuster wie die klinische Liste (hinzufuegen, duplizieren, loeschen)
- Datumsvalidierung aktiv: `Datum Ende` bleibt optional, darf aber nicht vor `Datum Beginn` liegen
- Expositionsoptionen wurden aus `survnet_variablen.csv` fuer Enterobacterales, Campylobacter und Tuberkulose in `PATHOGEN_CONFIG` hinterlegt
- Exposition wurde erweitert um Lebensmittel-Optionen und Kontakt-zu-Menschen inkl. Kontaktarten
- Nachweis in der Quelle wird als Auswahl gepflegt: `gesichert`, `vermutet`

## Umgesetzte Erweiterung: Erregerbezogene Vorauswahl

- Beim Erregerwechsel werden fuer Labor und klinische Informationen passende Beispielzeilen vorausgefuellt
- Campylobacter startet u. a. mit Symptomen zu Bauchschmerzen und Durchfall sowie PCR-Labortest
- Enterobacterales und Tuberkulose erhalten ebenfalls erregerpassende Vorauswahlen fuer Labor und Klinik
- Fuer Enterobacterales und Tuberkulose werden zudem passende Risikofaktoren und Expositionen vorausgewaehlt
- Campylobacter startet bei Risikofaktoren und Expositionen weiterhin mit leeren Zeilen
