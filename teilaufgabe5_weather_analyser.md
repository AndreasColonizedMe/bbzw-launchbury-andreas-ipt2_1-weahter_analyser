# WeatherAnalyser – Teilaufgabe 5: Unit-Tests mit pytest

## test_weather_analyser.py

```python
import pytest

from weather_analyser import (
    csv_einlesen,
    merge_sort,
    minimum,
    maximum,
    durchschnitt,
)


def test_csv_einlesen_normalfall():
    daten = csv_einlesen("test_wetterdaten.csv")

    assert len(daten) == 3
    assert daten[0]["datum"] == "2024-01-15"
    assert daten[0]["temperatur"] == -8.2


def test_csv_einlesen_datei_fehlt():
    with pytest.raises(FileNotFoundError):
        csv_einlesen("nicht_vorhanden.csv")


def test_merge_sort_normalfall():
    liste = [
        {"wert": 3},
        {"wert": 1},
        {"wert": 4},
        {"wert": 2},
    ]

    sortiert = merge_sort(liste, "wert")

    assert [x["wert"] for x in sortiert] == [1, 2, 3, 4]


def test_merge_sort_bereits_sortiert():
    liste = [
        {"wert": 1},
        {"wert": 2},
        {"wert": 3},
    ]

    sortiert = merge_sort(liste, "wert")

    assert [x["wert"] for x in sortiert] == [1, 2, 3]


def test_merge_sort_umgekehrt_sortiert():
    liste = [
        {"wert": 5},
        {"wert": 4},
        {"wert": 3},
    ]

    sortiert = merge_sort(liste, "wert")

    assert [x["wert"] for x in sortiert] == [3, 4, 5]


def test_merge_sort_leere_liste():
    assert merge_sort([], "wert") == []


def test_merge_sort_ein_element():
    liste = [{"wert": 42}]

    assert merge_sort(liste, "wert") == [{"wert": 42}]


def test_minimum_normalfall():
    daten = [
        {"temp": 5},
        {"temp": -3},
        {"temp": 10},
    ]

    result = minimum(daten, "temp")

    assert result == {"temp": -3}


def test_minimum_leere_liste():
    assert minimum([], "temp") is None


def test_maximum_normalfall():
    daten = [
        {"temp": 5},
        {"temp": -3},
        {"temp": 10},
    ]

    result = maximum(daten, "temp")

    assert result == {"temp": 10}


def test_maximum_leere_liste():
    assert maximum([], "temp") is None


def test_durchschnitt_normalfall():
    daten = [
        {"temp": 10},
        {"temp": 20},
        {"temp": 30},
    ]

    result = durchschnitt(daten, "temp")

    assert result == 20.0


def test_durchschnitt_gerundet():
    daten = [
        {"temp": 3.333},
        {"temp": 6.667},
    ]

    result = durchschnitt(daten, "temp")

    assert result == 5.0


def test_durchschnitt_leere_liste():
    assert durchschnitt([], "temp") is None
```

---

# test_wetterdaten.csv

```csv
datum;temperatur;windgeschwindigkeit;schneehoehe
2024-01-15;-8.2;34;120
2024-01-16;-3.1;18;118
2024-01-17;-12.5;52;125
```

---

# pytest-Befehl

```bash
pytest test_weather_analyser.py --cov=weather_analyser --cov-report=term-missing
```
