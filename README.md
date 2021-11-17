# Docs
Repozytorium zawierające dokumentacje dotyczącą projektu PSS na przedmiocie Inżynieria Oprogramowania (AGH))
## Aby otworzyć podsumowanie dokumentacji danej sekcji projektu należy wybrać jeden w poniższych linków:
1. [api](https://profi-sales-system.github.io/Docs/api/index.html)
2. [database](https://profi-sales-system.github.io/Docs/database/index.html)
3. [gui](https://profi-sales-system.github.io/Docs/gui/index.html)
4. [ERD](https://profi-sales-system.github.io/Docs/ERD.png)


## INTERFEJSY DLA:
## 1.API:

### Pobieranie kursów walut:
``` 
RatesConnector ratesConnector = new RatesConnector();
```
pobranie
```
ratesConnector.ratesRequest(kod, RateType).getRates()[0].getMid());
```
gdzie:
- kod -> String np."EUR"
- RateType -> typ wyliczeniowy, jaki typ kursu oczekujemy, np {MID,ASK,BID}.
