# Busauslastungsprognose im öffentlichen Nahverkehr

## Projektübersicht

Dieses Data Science Projekt ist Teil der Bachelorarbeit von Christian Sawadogo an der Universität Münster. Ziel ist die kurzfristige Prognose der Auslastung von Bussen im städtischen Nahverkehr Münster mittels maschinellen Lernens. Das entwickelte Artefakt kombiniert drei Teilmodelle (Vorgängerbesetzung, Ein- und Aussteiger) in einer Meta-Regression, um die Busauslastung auf Haltestellenebene zuverlässig vorherzusagen.

## Forschungsfrage

Wie kann im Rahmen des Design-Science-Research ein erklärbares Artefakt auf Basis maschinellen Lernens entwickelt und evaluiert werden, das die Busauslastung auf Haltestellenebene für ausgewählte Buslinien in Münster kurzfristig prognostiziert und dabei gegenüber der angezeigten Ist-Auslastung eine praktisch relevante Reduktion von RMSE, MAE und \$R^2\$ erzielt?

## Datenbeschaffung

* **Fahrgastdaten**: Export aus dem FAN-System der Stadtwerke Münster (Bus-Kamerasystem)
* **Wetterdaten**: Historische Stundenwerte über Open-Meteo API
* **Veranstaltungsdaten**: Öffentliche Veranstaltungsdatenbank Münsterland (Open Data)

## Ausführung der Notebooks

1. `import_bus_data.ipynb`: Konsolidierung und Parquet-Export der Rohdaten
2. `clean_data.ipynb`: Datenbereinigung, Formatkorrekturen, Logikprüfungen
3. `import_weather_data.ipynb`: Abruf & Aufbereitung der Wetterdaten
4. `import_event_data.ipynb`: Abruf & Aufbereitung der Veranstaltungsdaten
5. `feature_engineering.ipynb`: Anreicherung um Wetter- und Event-Features, zeitliche und räumliche Aggregationen
6. `hyperparameter_tuning.ipynb`: Optimierung der Hyperparameter per RandomizedSearchCV
7. `train_ml_model.ipynb`: Training und Validierung der XGBoost-Teilmodelle

## Ergebnisse

* **Szenario 1 (historisch)**: Ohne Echtzeitdaten nur mäßige Genauigkeit (R²≈0.48)
* **Szenario 2 (unterwegs)**: Mit Vorgängerbesetzung und Verspätung nahezu gleiche Fehler wie Baseline
* **Szenario 3 (kurz vor Ankunft)**: MAE-Reduktion 12 %, RMSE-Reduktion 34 %, R²≈0.15 gegenüber Ist-Auslastung

SHAP-Analysen zeigen, dass ohne Echtzeitdaten räumliche und zeitliche Muster dominieren, während in Echtzeit-Szenarien die Vorgängerbesetzung den größten Einfluss hat.
