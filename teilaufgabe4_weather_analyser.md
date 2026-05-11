
# WeatherAnalyser – Teilaufgabe 4

```python
"""
WeatherAnalyser – Teilaufgabe 4
Python-Implementierung
"""

import csv


def csv_einlesen(dateipfad):
    """
    Liest eine CSV-Datei ein und gibt eine Liste von Dictionaries zurück.

    Args:
        dateipfad (str): Pfad zur CSV-Datei.

    Returns:
        list: Liste mit Wetterdaten als Dictionaries.

    Raises:
        FileNotFoundError: Wenn die Datei nicht existiert.
        ValueError: Wenn Werte nicht korrekt umgewandelt werden können.
    """

    daten = []

    with open(dateipfad, mode="r", encoding="utf-8") as datei:
        reader = csv.DictReader(datei, delimiter=";")

        for zeile in reader:
            daten.append(
                {
                    "datum": zeile["datum"],
                    "temperatur": float(zeile["temperatur"]),
                    "windgeschwindigkeit": int(zeile["windgeschwindigkeit"]),
                    "schneehoehe": int(zeile["schneehoehe"]),
                }
            )

    return daten


def merge(linke_liste, rechte_liste, schluessel):
    """
    Führt zwei sortierte Listen zusammen.
    """

    sortierte_liste = []
    i = 0
    j = 0

    while i < len(linke_liste) and j < len(rechte_liste):
        if linke_liste[i][schluessel] <= rechte_liste[j][schluessel]:
            sortierte_liste.append(linke_liste[i])
            i += 1
        else:
            sortierte_liste.append(rechte_liste[j])
            j += 1

    while i < len(linke_liste):
        sortierte_liste.append(linke_liste[i])
        i += 1

    while j < len(rechte_liste):
        sortierte_liste.append(rechte_liste[j])
        j += 1

    return sortierte_liste


def merge_sort(liste, schluessel):
    """
    Sortiert eine Liste rekursiv mit MergeSort.
    """

    if len(liste) <= 1:
        return liste.copy()

    mitte = len(liste) // 2

    linke_haelfte = merge_sort(liste[:mitte], schluessel)
    rechte_haelfte = merge_sort(liste[mitte:], schluessel)

    return merge(linke_haelfte, rechte_haelfte, schluessel)


def minimum(liste, schluessel):
    """
    Findet den kleinsten Wert in der Liste.
    """

    if not liste:
        return None

    kleinster_wert = liste[0]

    for element in liste:
        if element[schluessel] < kleinster_wert[schluessel]:
            kleinster_wert = element

    return kleinster_wert


def maximum(liste, schluessel):
    """
    Findet den grössten Wert in der Liste.
    """

    if not liste:
        return None

    groesster_wert = liste[0]

    for element in liste:
        if element[schluessel] > groesster_wert[schluessel]:
            groesster_wert = element

    return groesster_wert


def durchschnitt(liste, schluessel):
    """
    Berechnet den Durchschnitt eines Wertes.
    """

    if not liste:
        return None

    summe = 0

    for element in liste:
        summe += element[schluessel]

    mittelwert = summe / len(liste)

    return round(mittelwert, 2)


def auswertung(dateipfad):
    """
    Führt die komplette Wetterdaten-Auswertung durch.
    """

    try:
        daten = csv_einlesen(dateipfad)

        if not daten:
            print("Die CSV-Datei ist leer.")
            return

        temperatur_min = minimum(daten, "temperatur")
        temperatur_max = maximum(daten, "temperatur")
        temperatur_durchschnitt = durchschnitt(daten, "temperatur")

        print("\n--- Wetterdaten-Auswertung ---\n")

        print(
            f"Temperatur: Min {temperatur_min['temperatur']} °C ({temperatur_min['datum']}) | "
            f"Max {temperatur_max['temperatur']} °C ({temperatur_max['datum']}) | "
            f"Ø {temperatur_durchschnitt} °C"
        )

    except FileNotFoundError:
        print("Fehler: Datei wurde nicht gefunden.")

    except ValueError:
        print("Fehler: Ungültige Werte in der CSV-Datei.")


if __name__ == "__main__":
    auswertung("wetterdaten.csv")
```
