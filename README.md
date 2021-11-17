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
#### pakiet -> pl.io.pss.api.exchange
Tworzymy objekt dla połączenia
``` 
RatesConnector ratesConnector = new RatesConnector();
```

pobranie kursu
```
ratesConnector.ratesRequest(kod, RateType).getRates()[0].getMid());
```
gdzie:
- ``` kod ``` -> String np."EUR"
- ``` RateType ``` -> typ wyliczeniowy, jaki typ kursu oczekujemy, np {MID,ASK,BID}.

### Pobieranie danych firm z GUS:
#### pakiet -> pl.io.pss.api.WsClient
Tworzymy objekt
```
CompanyApi companyApi = new CompanyApi(nip)
```
gdzie ``` nip ``` to String zawirający 10cyfr reprezentujacych firme której dane chcemy pobrać.
samo pobieranie danych:
```
companyApi.data().getFullName();
companyApi.data().getCountry();
companyApi.data().getStreet();
companyApi.data().getCity;
companyApi.data().getPostCode();
companyApi.data().getCity();
companyApi.data().getPhoneNumber();
companyApi.data().getEmail();
```

### Generowanie faktury wraz z formatem PDF:
#### pakiet -> pl.io.pss.api.invoice
Tworzymy obiekt
```
DataForInvoice dataForInvoice = new DataForInvoice();
```    
Ustalamy jaki kontrahent jest nabywcą
```
dataForInvoice.putContractor(idkontrahenta);    
```
Ustwiamy sprzedawce
```
dataForInvoice.putSeller();     
```
I generujemy fakture
```
Invoice.generateInvoice(dataForInvoice.data,idzamowienia);
```
gdzie ``` idzamowienia ``` to numer zamówienia jakiego faktura dotyczy

## 2. Obsługa bazy danych
### Pobieranie informacji

Klasa `DataGetter` pozwala na dostęp do zasobów bazy danych

#### pakiet -> pl.io.pss.api.database

Konstruktor bezargumentowy `public DataGetter()`

Funkcje:

`public Commodity getCommodity(String symbol)`
Pobiera informacje o towarze

`public Order getOrder(int orderID)`
Pobiera informacje o zamówieniu

`public Contractor getContractor(int contractorID)`
Pobiera informacje o kontrahencie

`public Invoice getInvoice(int invoiceID)`
Pobiera informacje potrzebne do wygenerowania faktury

`public ArrayList<Item> getItemsFromOrder(int orderID)`
Zwraca listę przedmiotów z danego zamówienia wraz z cenami i ilością

### Dodawanie i aktualizowanie informacji

Klasa `DataInserter` pozwala pozwala umieszczać/aktualizować informacje w bazie danych  

#### pakiet -> pl.io.pss.api.database

Konstruktor bezargumentowy `public DataGetter()`

Funkcje:

`public boolean insertCommodity(Commodity commodity)` Zapisuje dane towaru do bazy danych

`public boolean insertOrder(Order order)` Zapisuje dane zamówienia do bazy danych

`public boolean insertContractor(Contractor contractor)` Zapisuje dane kontrahenta do bazy danych

`public boolean insertInvoice(Invoice invoice)` Zapisuje dane faktury do bazy danych


### Użyte struktury reprezentacji danych

#### pakiet -> pl.io.pss.api.database.structures

`Commodity` reprezentuje towar (symbol, nazwa, typ, jednostka)   
Konstruktor:   
`public Commodity(String symbol, String  name, String  type, String unit)`  
Funkcje:  
`public String getSymbol()`  
`public String getName()`  
`public String getType()`  
`public String getUnit()`  
`public String toString()`  

`Item` reprezentuje towar wraz z ceną i ilością  
Konstruktor:   
`public Item(Commodity commodity, BigDecimal  count, BigDecimal totalPrice, BigDecimal price)`  
Funkcje:  
`public BigDecimal getCount()`  
`public BigDecimal getTotalPrice()`  
`public BigDecimal getPrice()`  
`public Commodity getCommodity()`  
`public String toString()`  

`Order` reprezentuje zamowienie, czyli listę `Item` oraz dane kontraktora, datę realizacji,
status(zrealizowano lub nie) oraz opis
Konstruktor:   
`public Order(Item[] items, String contractorID, String description, String realizationDate, String realized)`  
Funkcje:  
`public Item[] getItems()`  
`public String getContractorID()`  
`public String getDescription()`  
`public String getRealizationDate()`  
`public String getRealized()`  
`public String toString()`    

`Contractor` reprezentuje wszystkie dane kontrahenta  
Konstruktor:   
`public Order(Item[] items, String contractorID, String description, String realizationDate, String realized)`  
Funkcje:  
`public String getId()`  
`public String getType()`  
`public String getFullName()`  
`public String getSymbol()`  
`public String getStreet()`  
`public String getLocalNumber()`  
`public String getBuildingNumber()`  
`public String getPostCode()`  
`public String getCity()`  
`public String getProvince()`  
`public String getCountry()`  
`public String getNIP()`  
`public String getEmail()`  
`public String getPhoneNumber()`  
`public String toString()`  

`Invoice` reprezentuje dane potrzebne to generowania faktury    
Konstruktor:   
`public Order(Item[] items, String contractorID, String description, String realizationDate, String realized)`  
Funkcje:  
`public Contractor getSeller()`  
`public Contractor getBuyer()`  
`public Order getOrder()`  
`public String getSpecialist()`  
`public String getOrderNr()`  
`public String getDate()`  
`public String getConditions()`  
`public String getInvoiceNr()`  
`public String getDescription()`  
`public BigDecimal getPriceNoTax()`  
`public BigDecimal getTaxValue()`  
`public BigDecimal getTax()`  
`public BigDecimal getOther()`  
`public BigDecimal getPriceTotal()`  
`public String toString()`  

## 2. Interfejs Graficzny Użytkownika
### Widok aplikacji i wyświetlanie
Za całokształt interaktywnego okna aplikacji odpowiedzialna jest klasa `MainController` 
zawierająca następujące metody:

`public void selectLanguage(MouseEvent mouseEvent)` pozwalającą na zmianę języka aplikacji

`public void switchToNewWindow(MouseEvent mouseEvent)` pozwalającą zmienić okno aplikacji

`public void switchToMainWindow(MouseEvent mouseEvent)` umożliwiającą powrót do okna głównego

oraz metody wywoływane przy obsłudze rozwijanego menu kontekstowego, przeciążone przez `MenuController`

`public void showSalesCategoryButtons()` wyświetla dostępne sekcje w module Sprzedaż
`public void showPurchaseCategoryButtons()` wyświetla dostępne sekcje w module Zakup
`public void showWarehouseCategoryButtons()` wyświetla dostępne sekcje w module Magazyn
`public void showFinanceCategoryButtons()` wyświetla dostępne sekcje w module Finanse
`public void showOrganizationCategoryButtons()` wyświetla dostępne sekcje w module Organizacja
`public void showCatalogCategoryButtons()` wyświetla dostępne sekcje w module Kartoteki
`public void showAdministrationCategoryButtons()` wyświetla dostępne sekcje w module Administracja


### Reagowanie na akcje użytkownika
Użytkownik ma możliwość wyboru sekcji, którą chce wyświetlić, bądź edytować. Wybór każdej z nich wiąże się ze zmianą sposobu reakcji na poszczególne akcje.
Np. Przycisk "Dodaj" inaczej będzie działał dla sekcji Kontrahenci, a inaczej dla sekcji Faktury itd. 
Użytkownik może równocześnie mieć otworzonych kilka zakładek, a w każdej z nich inna sekcja, dlatego też aktualnie wybrane sekcje (dalej zwane "aktualnymi stanami") przechowywane są w liście stanów:
`public static ArrayList<MainController> actualStates` w klasie `MainController`
Obecnie wybrana zakładka zapamiętywana jest w `public static MainController currentState`

Każdy stan obsługiwany jest przez inną klasę, będącą kontrolerem.
`ContractorsController` dla Kontrahentów w module Kartoteki
`WaresController` dla Towarów w module Kartoteki
`OrdersFromSuppliersController` dla Zamówień od Dostawców w module Zakup
`PurchaseAjustmentController` dla Korekt w module Zakup
`PurchaseInvoicesController` dla Faktur w module Zakup
`CustomerOrdersController` dla Zamówień w module Sprzedaż
`SalesAjustmentController` dla Korekt w module Sprzedaż
`SalesInvoicesController` dla Faktur w module Sprzedaż
`InventoryController` dla Inwentaryzacji w module Magazyn
`StockLevelsController` dla Stanów Magazynowych w module Magazyn

Każdy kontroler jest klasą dziedziczącą po głównym kontrolerze `MainController` i zawiera następujące przeciążone metody, które definiują sposób reagowania na wybór konkretnego przycisku:

Obsługa przycisku „Dodaj”
`public void pressedAddButton(MouseEvent mouseEvent)`

Obsługa przycisku „Usuń”
`public void pressedRemoveButton(MouseEvent mouseEvent)`

Obsługa przycisku „Filtruj”
`public void pressedFilterButton(MouseEvent mouseEvent)`

Obsługa przycisku „Szukaj”
`public void pressedFindButton(MouseEvent mouseEvent)`

Obsługa przycisku „Drukuj”
`public void pressedPrintButton(MouseEvent mouseEvent)`

Obsługa przycisku „Zobacz”
`public void pressedViewButton(MouseEvent mouseEvent)`

Obsługa przycisku „Edytuj”
`public void pressedEditButton(MouseEvent mouseEvent)`

Ponadto klasy kontrolujące mają zdefiniowane medoty:

`public ContractorsController addNewBookmark(String title)` tworzy nową zakładkę o tytule: `String title`
`public ContractorsController setTheTable()` komunikuje się z bazą danych i generuje tabelę do wyświetlenia 
