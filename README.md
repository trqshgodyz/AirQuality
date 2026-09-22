# Analiza poluării cu NO₂ în orașele din România

Acest proiect analizează concentrația de dioxid de azot (NO₂) din România pentru perioada **2024–2025**, folosind imagini satelitare Sentinel-5P și platforma Google Earth Engine.

Analiza urmărește cinci orașe:

* București
* Galați
* Craiova
* Constanța
* Brașov

Pentru fiecare oraș este analizată o zonă cu raza de **10 km** în jurul centrului său.

## Obiective

Proiectul urmărește:

* cartografierea distribuției NO₂ în România;
* compararea valorilor mediane din 2024 și 2025;
* extragerea mediilor lunare pentru fiecare oraș;
* observarea variațiilor sezoniere;
* compararea nivelurilor din timpul iernii și verii;
* calcularea schimbării procentuale dintre 2024 și 2025;
* clasificarea orașelor în funcție de nivelul mediu al poluării.

## Sursa datelor

Datele provin din colecția:

```text
COPERNICUS/S5P/OFFL/L3_NO2
```

Aceasta este disponibilă prin [Google Earth Engine](https://earthengine.google.com/) și conține observații Sentinel-5P privind concentrația troposferică de NO₂.

Pentru delimitarea României este utilizată colecția:

```text
FAO/GAUL_SIMPLIFIED_500m/2015/level0
```

## Tehnologii utilizate

* Python
* Google Earth Engine Python API
* geemap
* pandas
* matplotlib
* Jupyter Notebook sau Google Colab

## Instalare

Clonează repository-ul:

```bash
git clone https://github.com/USERNAME/NUME-REPOSITORY.git
cd NUME-REPOSITORY
```

Instalează bibliotecile necesare:

```bash
pip install earthengine-api geemap pandas matplotlib
```

Alternativ, dacă repository-ul conține un fișier `requirements.txt`, poți rula:

```bash
pip install -r requirements.txt
```

## Configurarea Google Earth Engine

Pentru rularea proiectului este necesar:

1. Un cont Google Earth Engine.
2. Un proiect Google Cloud asociat contului.
3. Autentificarea din Python.

Codul folosește:

```python
ee.Authenticate()
ee.Initialize(project='airquality-508516')
```

Dacă rulezi proiectul din propriul cont, înlocuiește `airquality-508516` cu ID-ul proiectului tău Google Cloud:

```python
ee.Initialize(project='ID-UL-PROIECTULUI-TAU')
```

La prima rulare, Earth Engine va deschide procesul de autentificare în browser.

## Metodologie

### 1. Selectarea zonei de studiu

Granița României este extrasă din baza de date FAO GAUL.

### 2. Definirea zonelor urbane

Pentru fiecare dintre cele cinci orașe este creat un buffer circular cu raza de 10 km.

### 3. Filtrarea datelor satelitare

Sunt păstrați doar pixelii care îndeplinesc următoarele condiții:

* fracția de nori este mai mică sau egală cu 40%;
* valoarea NO₂ este pozitivă sau egală cu zero.

Banda analizată este:

```text
tropospheric_NO2_column_number_density
```

Valorile sunt exprimate în:

```text
mol/m²
```

### 4. Agregarea datelor

Pentru fiecare lună din 2024 și 2025:

* se calculează imaginea mediană lunară;
* se extrage media NO₂ din bufferul fiecărui oraș;
* rezultatele sunt salvate într-un DataFrame pandas.

Lunile fără pixeli valizi sunt eliminate din analiză.

## Rezultate generate

Proiectul generează:

### Hartă interactivă

Harta conține:

* valoarea mediană NO₂ pentru anul 2024;
* valoarea mediană NO₂ pentru anul 2025;
* diferența dintre 2025 și 2024;
* conturul României;
* zonele de analiză de 10 km din jurul orașelor.

În harta diferențelor:

* nuanțele de albastru indică o scădere a NO₂;
* nuanțele de roșu indică o creștere a NO₂.

### Grafice

Sunt generate următoarele grafice:

1. Evoluția lunară a NO₂ în perioada 2024–2025.
2. Comparația dintre iarnă și vară.
3. Comparația mediilor anuale din 2024 și 2025.

### Tabele

Codul afișează:

* mediile anuale pentru fiecare oraș;
* schimbarea procentuală dintre 2024 și 2025;
* mediile sezoniere;
* raportul dintre valorile de iarnă și cele de vară;
* media generală pentru întreaga perioadă;
* mediile pentru fiecare lună calendaristică.

## Rulare

Proiectul poate fi rulat într-un Jupyter Notebook sau în Google Colab.

Într-un notebook, execută celulele în ordine. Harta interactivă este afișată prin:

```python
Map
```

Extragerea datelor din Google Earth Engine poate dura câteva minute, în funcție de conexiune și de timpul de procesare al serverelor.

## Structura recomandată a repository-ului

```text
air-quality-romania/
├── README.md
├── requirements.txt
├── no2_analysis.ipynb
├── LICENSE
└── images/
    ├── monthly_evolution.png
    ├── seasonal_comparison.png
    └── annual_comparison.png
```

## Fișierul requirements.txt

```text
earthengine-api
geemap
pandas
matplotlib
jupyter
```

## Limitări

* Sentinel-5P măsoară coloana troposferică de NO₂, nu concentrația directă la nivelul solului.
* Norii pot reduce numărul observațiilor disponibile.
* Mediile calculate într-o rază de 10 km nu reprezintă toate variațiile locale dintr-un oraș.
* Rezultatele nu înlocuiesc măsurătorile realizate de stațiile terestre de monitorizare.
* Comparația sezonieră combină datele din ambii ani.
* Valorile pentru iarnă includ lunile decembrie, ianuarie și februarie din fiecare an analizat.

## Posibile îmbunătățiri

Proiectul poate fi extins prin:

* exportarea rezultatelor într-un fișier CSV;
* salvarea automată a graficelor;
* includerea mai multor orașe;
* compararea datelor satelitare cu stațiile terestre;
* analiza separată a anotimpurilor pentru fiecare an;
* adăugarea unor indicatori meteorologici;
* publicarea hărții sub forma unei aplicații web.

## Autor

* Capp Sara-Cristiana
* Conțolenco Bianca - Maria
* Dăscălescu Ondina Ștefania
* Khan-Hamida Mariyam


## Licență

N-avem bani de așa ceva... :( 
