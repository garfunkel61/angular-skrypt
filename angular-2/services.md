Servisy w ng2
------

- podobnie jak w ng-1, serwisy służą do dzielenia funcjonalności między componentami applikacji
- towrozne mogą być z pomocą cli: ng g s nazwa-servisu
- ! serwis nie jest tworzony w swoim folderze, musimy go utworzyc maunaulnie, cd do niego i tam utworzyć serwis

### Prost obsłuba serwisu

Rejestrowanie serwisu:

- ! tworzony servis nie jest z definicji providerowany:
      WARNING Service is generated but not provided, it must be provided to be used
- należy go manualnie dostarczyć do modułu (zarejestrować w niej):
  - w pliku modułu (np app.module.ts) w obiekcjie konfiguracji modułu jest właściwość providers, która jest tablicą zarejestrownaych modułów. Importujemy do pliku nasz serwis, i umieszczamy go w tablicy providerów

Konsumowanie serwisu:

- zarejestrowany servis należy dołączyć do wybranuch componetów modułu na ktorym został zarejestrowany:
  - w construktorze komponentu dodajemy parament w którym przekazujemy serwis

        import { MailService } from './../mail-service/mail.service';
        ...
        constructor(private mail: MailService) {...}
- dzięki temu na obiekcie conponentu mamy dostępny obiekt serwisu pod zmienną mail, i możemy korzystać w kodzie oraz html'u:
       {{ mail.message }}

Tworzenie manualne serwisu:

- serwis jest classą 'injectowaną' (?) - musi być eksportowany z pliku jako klasa i korzystać z @Injectable
      import { Injectable } from '@angular/core';

      @Injectable()
      export class MailService {

      constructor() { }

      message: String = 'Message form service';

      }
- tworzenie zmiennych na klasie serwisy - po prostu dodajemy właściwość i po niej = z odpowiednią wartością

### Obsługa serwisu za pomocą injectora

#### Serwis typu KLASA

- tworzony analogicznie jak w prostej obsłudze (jeśli serwis typu obiekt)

Rejestrowanie serwisu:

- Importujemy do pliku nasz serwisu
- W tablicy providers umieszczamy obiekt z dwoma właściwościami: 'provide' i 'useClass'
  - provide zawiera nazwę jaką bedzimy urzywać dla serwisu w componentach, jest to string
  - useClass zawiera zaimportowaną klasę serwisu
        import { UserService } from './../user-service/user.service';
        providers: [
          ...
          { provide: 'userData', useClass: UserService },
          ...
        ],

Konsumowanie serwisu:

- ! nie musimy importować serwisu do componentu! - GŁÓWNA RÓŻNICA
- ! musimy zaimportować dekorator Inject z '@angular/core'
- w konstrukotrze komponentu korzystany z dekoratora @Inject('userData') z nazwą z tablicy providerów modułu (mówimy co injectujemy) oraz następnie nazwą zmiennej pod jaką bedziu dostępny serwis w componecie private userData
        constructor(
          ...
          @Inject('userData') private userData) { }
- teraz serwis jest wstrzykniety do obiektu componentu pod zmienna prywatną userData


#### Serwis typu VALUE

- towrzony jak serwis bezpośrednio w tablicy providerów, przez obiekt z własnościami 'provide' i 'useValue'
- do 'useValue' bezpośrenio przypisujemy wartość jaką bedzie miał serwis
      { provide: 'envType', useValue: 'http://localhost:1000/' }

- konsumowany tak samo jak serwis typu klasa:
        constructor(
          ...
          @Inject('envType') private envType) { }
- teraz serwis jest wstrzykniety do obiektu componentu pod zmienna prywatną envType
