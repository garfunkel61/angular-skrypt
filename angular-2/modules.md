Moduły w ng2
----

### Czym jest moduł ng2?

- podobnie jak w angJs, w ng2 podstawowym budulcem aplikacji są moduly
- służą do konfigurowania aplikacji
- aplikacja powinna mieć 1 główny moduł, na który składają sie komponenty i sub-moduły
- moduł jest towrzony za pomocą dekoratora @NgModule() do którego przekazujemy obiekt konfiguracyjny modułu

### Obiek konfiguracji modułu

Właściwości z opisami:

- imports - tablica zewnętrznych modułów budujących moduł
- declarations - tablic wewnętrznych komponetów budująch moduł
- bootsrtap - tablica komponentów uruchamiających aplikacjię
- providers - tablica serwisów dostępnych w module
- ...

      @NgModule({
        declarations: [
          AppComponent
        ],
        imports: [
          BrowserModule,
          FormsModule,
          HttpModule
        ],
        providers: [],
        bootstrap: [AppComponent]
      })


### Uruchamianie modułu głównego aplikacji

Do uruchamiania modułu służy metoda bootstrapModule

- tworzymy osobny plik uruchamiajacy aplikacjie - np. main.ts
- metoda bootstrapModule() pochodzi z obiektu platformBrowserDynamic() który importujemy z '@angular/platform-browser-dynamic'
- metoda bootstrapModule() jako prametr przyjmije główny moduł aplikacji

      import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
      import { AppModule } from './app.module';

      platformBrowserDynamic().bootstrapModule(AppModule);

- opisany powyżej przykład opisuje uruchamianie aplikacji ng2 a przeglądarce internetowej, są inne opcje i środowiska uruchominiowe ...
- ...
