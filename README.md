# Docs
Repozytorium zawierające dokumentacje dotyczącą projektu PSS na przedmiocie Inżynieria Oprogramowania (AGH))
## Aby otworzyć podsumowanie dokumentacji danej sekcji projektu należy wybrać jeden w poniższych linków:
1. [api](https://profi-sales-system.github.io/Docs/api/index.html)
2. [database](https://profi-sales-system.github.io/Docs/database/index.html)
3. [gui](https://profi-sales-system.github.io/Docs/gui/index.html)
4. [ERD](https://profi-sales-system.github.io/Docs/ERD.png)

przykłady uzycia: 
```     DataForInvoice dataForInvoice = new DataForInvoice();
        dataForInvoice.putContractor(2);
        dataForInvoice.putSeller();
        Invoice.generateInvoice(dataForInvoice.data,1);
        
        RatesConnector ratesConnector = new RatesConnector();
        System.out.println(ratesConnector.ratesRequest("EUR", RateType.MID).getRates()[0].getMid());

        PrintService printer = Print.choosePrinter();
        Print.printPDF("src/main/resources/invoice.pdf",printer);
