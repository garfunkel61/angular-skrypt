Services
========

- są wykorzustuwane do wstrzykiwania [DI] obiektów do komponentu aplikacji (controllerow, dyrektyw, filtrów)
- wyróżniamy 3 podstawowe typy, Value, Service, Factory
- tworzymy na module za pomocą jego metod, analogicznych do nazw serwisów

***

Value
-----
- najprosztrzy serwis jaki posiada Angular - szłuży do przekazywania do komponentu prostej wartości, np. object literal albo zwykly primityw
- po wstrzyknieciu do komponentu jest wykorzystywany bezpośrednio nazwaServisuValue.właściwość


Service
-------
- służy do przekazywania do komponentu obiektu pod postacią konstruktora (czyli taki co trzeba stworzyć za pomocą słowa new)
- dzięki metodzie .service nie trzeba tego obiektu w komponecie inicjalizwoać słowem new - zostaje automatycznie utworzony

Factory
-------
- służy do korzystania z 'module pattern' do tworzenia obiektów w JS || lub 'revealing module pattern' do tworzeni obiektów z prywatnymi wartościami w JS
- dzięki metodzie .factory  nie trzeba tego obiektu w komponecie inicjalizować wywołaniem funkcji ktora go zwraca - zostaje automatycznie zwrócony i gotowy do urzytku


- 'module pattern’ jest to funcja która zwraca object literal (prawie jak tworzenie obiektu konstruktorem, tylko że bez słowa 'new')

      function droidFactory () {
        return {
          name: 'a',
          age: 2
        }
      }

- 'revealing module pattern' jest to funkcja która zwraca object literal posiadający prywatne i publiczne wartości:
      - publiczne: gdy są w zwracanym object literal bezposrednio wpisane
      - prywatne:  gdy są w zwracanym object literal wpisane jako referencje do funkcji zwracających wartości zadeklarowanych w tworzonej funkcji

      function droidFactory () {
        function droidAgePrivate () { // niedostepne z zewnątrz //
          return 2;
        }

        return {
          name: 'a',
          age: droidAgePrivate;  //udostepniona wartość prywatnej wartości
        }
      }

***

Podsumowanie
============

- .value   - dla object literal, dostpne bezpośrenio pod injectowaną nazwą
- .service - dla object constructor, bez konieczności urzywania w komponecie 'new', dostpne bezpośrenio pod injectowaną nazwą
- .factory - dla object tworzyn z 'module pattern',  bez konieczności urzywania w komponecie wywołania funkcji zwracającej, dostpne bezpośrenio pod injectowaną nazwą
