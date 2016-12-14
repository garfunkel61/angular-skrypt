Components
==========

Sa prostrza wersja dyrektywy, o uporszczonej konfiguracji.
Służa do tworzenia aplikacji zbilizonych do Angular2 o architekturze komponentowej.

Tworzenie komponentów
---------------------

- za pomoca metody .component() modułu angularowego
- metoda przyjmuje dwa argumenty - nazwe componentu oraz obiekt konfiguracji
- w html musi zostac utworzony element z nazwy componentu w kebab-case (jak dyrektywa)

JS

    angular.module('heroApp').component('heroDetail', {
      templateUrl: 'heroDetail.html',
      controller: HeroDetailController,
      bindings: {
        hero: '='
      }
    });

###### Obiekt konfiguracji componentu

- bindings - obiekt zawierajacy wstrzykniete (w html) z rodzica lub innych komponentow zmienne
- controller - kod kontrolera (np zaimportowana funkcja)
- controllerAs - string, nadana nazwa kontrolera, defaultowo $ctrl
- require
- template - string html
- templateUrl - url string do templajtu
- transclude - boolean, wszystkie zmienne rodzica wpadaja do scope componentu, defaultowo na false

###### Bindings

- obiekt zmiennych danego componentu pochodzacych z componentu nadrzednego
- kazdy z kluczy obiektu jest zmienna na componencie, i zawiera podana w html componentu zmienna z rodzica
- zmienne bindowane do compoentu moga miec 2-way-bindign lub 1-way-bindign

typy bindingów:
- < - zmienne nie sa obserwowane, co znaczy ze przypisanie nowej wlasciwosci w componecie nie zmieni wlasciwosci w rodzicu (! chyba ze jest to obiekt lub tablica - wtedy poprzez referencje do tego samego obiektu zmiany beda nanoszone u rodzica) Dlatego nie nalezy nigdy zmieniac obiektu lub tablicy w componecie na zmiennej bindowanej z <
- = - standardowe 2-way-binding
- @ - używane dla niezmininych stringow przychodzacych z rodzica
- & - używane dla funkcji z rodzica ktore beda wykonywane jako callbacki okreslony eventow componentu:
  - onDelete
  - onUpdate

  ***

  # ToDo:
  - egghead sprawdzic componenty i zaktualizowac co tu napisane
  - components lifecycle z dokumentacji https://docs.angularjs.org/guide/component
