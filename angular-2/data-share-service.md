# Serwisy do dzielenia danych

- serwisy możemy wykorzystywać do dzielenia danych
- dane dzielone tworzymyj jako specjalne Observable - Subject

## Tworzenie observabla w serwisie:

- na klasie serwisu tworzymy dwie zmienne:
    - `private obserwowanaNazwa` - jest to obiekt Subject lub BehaviorSubject
    - `public obserwowanaNazwa$` - jest to wywołanie obserwowanaNazwa.asObservable() - stworzenie obserwabla
- na klasie serwisu tworzymy prywantą metodę, która jako parametr przyuje nową wartość observabla, a w ciele wywołuje .next() z nową wartością:
    - `private updateObserwowanaNazwa(nowaWartość) { ... }`

- gdzieś w metodach / konstruktorze / naszego serwisu, wywołujemy metodę `update...` z podaniem wartość - w ten sposób tworzymy nową wartość observabla

- słuchanie na observablu - w komponecie lub innym serwisie:
    - injectiujemy nasz serwis do komponenty i w konstruktorze / metodzie wykorzystujemy publiczną właściwość serwisu injectowanego `obserwowanaNazwa$` z wywołaniem metody .subscribe() na tymże
    - w metodzie .subscribe jako parametr otrzymujemy obserwowaną nową wartość z metody updateObserwowanaNazwa(...)
