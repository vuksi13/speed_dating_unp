# Analiza skupa podataka Speed Dating

Seminarski rad iz predmeta **Uvod u nauku o podacima**, PMF Kragujevac.

**Autori:** Luka Vuksanovic (39-2022), Janko Josovic (58-2022)

## O projektu

Analiziramo podatke iz eksperimenta brzih sastanaka koji su sproveli Ray Fisman i Sheena Iyengar na Univerzitetu Kolumbija (2002–2004): 551 učesnik, 21 događaj, 8.378 sastanaka. Cilj je da predvidimo da li će učesnik posle sastanka poželeti ponovni susret sa partnerom (`dec`) i da ispitamo šta zaista određuje tu odluku.

Rad obuhvata:

- opis i čišćenje podataka (duplikati, tipovi, nedosledno šifrovane vrednosti, vrednosti van skale);
- analizu nedostajućih i ekstremnih vrednosti;
- eksplorativnu analizu (univarijantnu, bivarijantnu i multivarijantnu);
- statističke testove četiri hipoteze (α = 0,05);
- pravljenje novih promenljivih;
- modele klasifikacije: logistička regresija, ridge, lasso, kNN, PCA + logistička regresija, uz unakrsnu validaciju po učesniku, iteracije modela i bootstrap;

## Podaci

- Izvor: [Speed Dating Experiment, Kaggle](https://www.kaggle.com/datasets/annavictoria/speed-dating-experiment)
- Sirovi podaci: `data/raw/Speed Dating Data.csv` (kodiranje latin-1)
- Očišćeni podaci: `data/clean/sd_clean.rds` i `data/clean/sd_clean.csv`
- Podaci sa novim promenljivim: `data/clean/sd_fe.rds`

## Struktura repozitorijuma

```
data/
  raw/Speed Dating Data.csv
  clean/                     očišćeni podaci
Seminarski.Rmd               izveštaj - kod, rezultati i tumačenje
Seminarski.docx / .html      izveštaj nakon pokretanja
README.md
```

## Pokretanje

1. Otvoriti projekat u RStudio-u, tako da je radni direktorijum koren repozitorijuma.
2. Jednom instalirati pakete:

   ```r
   install.packages(c("tidyverse", "broom", "glmnet", "car", "boot"))
   ```

   Paketi `class` i `cluster` dolaze uz R.
3. Otvoriti `Seminarski.Rmd` i pokrenuti **Knit**.Ceo dokument se izvršava za nekoliko minuta, najduže traju postupni izbor promenljivih i unakrsna validacija.

Svi slučajni koraci koriste `set.seed(2026)`, pa su rezultati ponovljivi.
