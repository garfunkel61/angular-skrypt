Angular CLI - narzędzie terminala umożliwiające obsługę aplikacji angularowej
-----------

Podstawowe funkcje:

- dostępne jako npm-moduł
- posiada wbudownay serwer lokalny: ng serve
- możliwia stworzenie zasetupowanej aplikacji od 0: ng new nazwa-aplikacji --parametry
  - --prefix: jak prefixowane bedą componenty aplikacji
- pozwala tworzyć komponenty angularowe: ng generate component nazwa-komponentu --parametry
    - ng generate component example-component --inline-template --inline-style
    - ng g c example-componetnt -it -is
    - componenty tworzymy z root'u aplikacji
- tworzenie serwisów: ng generate service nazwa
  - ng g s nazwa-servisu

Konfiguracja:

- aplikacje towrzone z CLI posiadają plik konfiguracyjny w root'cie: .angular-cli.json
- wszelkie konfiguracje aplikacji znajudą się w tym pliku
- powszechne wartości kofiguracyjne:
  - 'prefix': - określa jak wszystkie componenty oraz sama aplikacji bedą miały prefix przed swoimi nazwami
