# WeatherAnalyser – Teilaufgabe 1: Analyse / Grobkonzept

## 1. Problemstellung (Was will Frau Walser?)

Frau Sandra Walser von den Bergbahnen Flumserberg AG hat ein Problem mit der Auswertung von Wetterdaten.

Aktuell:
- Wetterdaten werden stündlich gesammelt (Temperatur, Windgeschwindigkeit, Schneehöhe)
- Daten werden als CSV gespeichert
- Auswertung erfolgt manuell in Excel

Problem:
- Sehr zeitaufwendig bei vielen Daten
- Keine schnelle Übersicht über wichtige Kennzahlen

Ziel:
Ein Python-Programm, das:
- CSV-Dateien automatisch einliest
- Daten sortiert (mit MergeSort)
- Minimum, Maximum und Durchschnitt berechnet
- Ergebnisse übersichtlich im Terminal ausgibt
- zuverlässig mit Unit-Tests abgesichert ist

---

## 2. Datenstruktur der CSV-Datei

Die CSV-Datei enthält folgende Spalten:

| Feld                | Beschreibung                  |
|--------------------|------------------------------|
| datum              | Datum der Messung            |
| temperatur         | Temperatur in °C             |
| windgeschwindigkeit| Windgeschwindigkeit          |
| schneehoehe        | Schneehöhe in cm             |

Beispiel:
datum;temperatur;windgeschwindigkeit;schneehoehe
2024-01-15;-8.2;34;120

Nach dem Einlesen wird die Datei in eine Liste von Dictionaries umgewandelt.

---

## 3. Funktionsübersicht (Ein- und Ausgaben)

### csv_einlesen(dateipfad)
- Eingabe: Dateipfad (String)
- Ausgabe: Liste von Dictionaries

### merge_sort(liste, schluessel)
- Eingabe: Liste + Schlüssel
- Ausgabe: Sortierte Liste

### minimum(liste, schluessel)
- Ausgabe: Datensatz mit kleinstem Wert

### maximum(liste, schluessel)
- Ausgabe: Datensatz mit grösstem Wert

### durchschnitt(liste, schluessel)
- Ausgabe: Durchschnitt oder None

### auswertung(dateipfad)
- Ausgabe: Formatierte Terminal-Ausgabe

---

## 4. Fehlerfälle

- Datei existiert nicht → FileNotFoundError
- Datei leer → leere Liste
- Ungültige Werte → Fehler beim Parsen
- Leere Liste bei Durchschnitt → None

---

## 5. Landau-Notation (Big-O)

Beschreibt die Effizienz eines Algorithmus.

- O(n) → linear
- O(n²) → langsam
- O(n log n) → effizient

---

## 6. Laufzeitvergleich

MergeSort:
- O(n log n)
- effizient

Selectionsort:
- O(n²)
- langsam

---

## 7. User Stories

### 1
Automatische Temperaturauswertung (Min/Max/Ø)

### 2
Sortierte Schneehöhen anzeigen

### 3
Durchschnitt Windgeschwindigkeit berechnen

### 4
Code verständlich und erweiterbar

---

## Fazit

Ein Python-Programm zur effizienten Analyse von Wetterdaten mit Fokus auf:
- MergeSort
- Statistik
- Fehlerbehandlung
- Testbarkeit
