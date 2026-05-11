
# WeatherAnalyser – Teilaufgabe 2: Design / Detailkonzept

## 1. Ablaufdiagramm merge_sort()

```text
Start
  |
  v
Ist Länge der Liste <= 1?
  | Ja
  v
Liste zurückgeben
  |
  Ende

  | Nein
  v
Liste in zwei Hälften teilen
  |
  v
merge_sort(linke Hälfte) aufrufen
  |
  v
merge_sort(rechte Hälfte) aufrufen
  |
  v
Beide sortierten Hälften mit merge() zusammenführen
  |
  v
Sortierte Liste zurückgeben
  |
 Ende
```

---

## 2. Ablaufdiagramm auswertung()

```text
Start
  |
  v
CSV-Datei einlesen
  |
  v
Sind Daten vorhanden?
  | Nein
  v
Fehlermeldung ausgeben
  |
 Ende

  | Ja
  v
Temperaturdaten sortieren
  |
  v
Minimum berechnen
  |
  v
Maximum berechnen
  |
  v
Durchschnitt berechnen
  |
  v
Ergebnisse formatiert ausgeben
  |
 Ende
```

---

# 3. Funktionstabelle

| Funktion | Parameter | Rückgabewert | Fehlerfälle |
|---|---|---|---|
| csv_einlesen(dateipfad) | dateipfad: str | list[dict] | Datei fehlt, Datei leer, fehlerhafte Werte |
| merge_sort(liste, schluessel) | liste: list, schluessel: str | sortierte Liste | Leere Liste |
| merge(liste_links, liste_rechts, schluessel) | zwei Listen + Schlüssel | zusammengeführte Liste | falscher Schlüssel |
| minimum(liste, schluessel) | liste, schluessel | Dict mit kleinstem Wert | leere Liste |
| maximum(liste, schluessel) | liste, schluessel | Dict mit grösstem Wert | leere Liste |
| durchschnitt(liste, schluessel) | liste, schluessel | float oder None | Division durch 0 vermeiden |
| auswertung(dateipfad) | dateipfad | keine Rückgabe (Ausgabe im Terminal) | Datei nicht vorhanden |

---

# 4. Dictionary-Format von csv_einlesen()

Die Funktion `csv_einlesen()` gibt eine Liste von Dictionaries zurück.

Beispiel:

```python
[
    {
        "datum": "2024-01-15",
        "temperatur": -8.2,
        "windgeschwindigkeit": 34,
        "schneehoehe": 120
    },
    {
        "datum": "2024-01-16",
        "temperatur": -3.1,
        "windgeschwindigkeit": 18,
        "schneehoehe": 118
    }
]
```

---

# 5. Erklärung Teile-und-herrsche (MergeSort)

MergeSort arbeitet nach dem Teile-und-herrsche-Prinzip aus Kapitel 4 des Lehrbuchs.  
Zuerst wird die Liste in zwei kleinere Hälften aufgeteilt („divide“). Danach werden beide Hälften rekursiv weiter aufgeteilt, bis nur noch Listen mit einem Element übrig bleiben („conquer“). Eine Liste mit einem Element gilt bereits als sortiert und bildet den Basisfall der Rekursion. Anschliessend werden die kleinen sortierten Listen Schritt für Schritt wieder zusammengesetzt („combine“). Dabei vergleicht die Funktion `merge()` die Werte der beiden Listen und fügt sie in der richtigen Reihenfolge zusammen. Dadurch entsteht am Ende eine vollständig sortierte Liste mit einer Laufzeit von O(n log n).

---

# 6. Basisfall und Rekursionsfall

## Basisfall
Der Basisfall tritt ein, wenn die Liste 0 oder 1 Element enthält.  
In diesem Fall ist die Liste bereits sortiert und wird direkt zurückgegeben.

```python
if len(liste) <= 1:
    return liste
```

## Rekursionsfall
Der Rekursionsfall tritt ein, wenn die Liste mehr als ein Element enthält.  
Die Liste wird halbiert und `merge_sort()` wird erneut auf beide Hälften angewendet.

```python
mitte = len(liste) // 2

links = merge_sort(liste[:mitte], schluessel)
rechts = merge_sort(liste[mitte:], schluessel)
```

---

# Fazit

Das Detailkonzept beschreibt den Aufbau des Programms und die Funktionsweise von MergeSort.  
Besonders wichtig sind:
- Rekursion
- Basisfall und Rekursionsfall
- Teile-und-herrsche-Prinzip
- klare Datenstruktur mit Dictionaries

Dadurch wird das Programm übersichtlich, erweiterbar und effizient.
