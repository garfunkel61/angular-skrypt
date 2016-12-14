Modules
=======

- są wykorzystawane jako kontenery dla komponentów aplikacji (controllerow, dyrektyw, filtrów, komponentow)
- tworzone za pomocą medoty .module, gdzie: nazwa - obowiazkowa, dependencje - opcjonalne

      angular.module('nazwa', ['dependencje']);

- posiadają metody: - komponetów (.controller etc.) - .run() - .config()

Metody modułów
--------------
- .config() -  przyjmuje callback, który może posiadać dependencies jako parametry. Kod wykonywnay jest w trakcie inicjalizajici modułów. Jako dependencje można injectować (providery, constanty)

- .run() - przyjmuje callback, który może posiadać dependencies jako parametry. Kod wykonywnay jest po inicjalizajici modułów. Jako dependencje można injectować instancje (seriwsy [service, factory, value], constanty)

      ! .run() jest wykonywane gdy wszystkie serwisy są już zainicjowane (po .config())

Dependencje modułu
------------------

Moduł może przymować inne moduły jako dependencje. Służy to dekompozycji aplikacji - może być ładnie podzielona na moduły funkcyjne.
- Metody .config() i .run() modułu nadrzędnego sa wykonywane przed motodami modółw injectowanych.
- Dependencje modułów sa trazytywne, tz że jeżeli moduł-A otrzymuje w dependecnij -B, a -B posiada w dependncjach -X i -Y, to -X i -Y sa odstępne w A

      angular.module('nazwa-modułu-A', ['nazwa-modułu-B', 'nazwa-modułu-C']);
      angular.module('nazwa-modułu-B', ['nazwa-modułu-X', 'nazwa-modułu-Y']);

- Moduł A posiada moduły B, C, X, Y (jako dependencje i sub-dependencje).

- Moduły musza być dołaczone do plikow ladownych przez strone

***

Moduły angularowe w ES6
=======================

- Składnia - jak klasyczna angularowa: angular.module('nazwa-modułu-A', []);
- Importowanie - moduly musza być hierarchicznie importowane, tz.:

      import 'path/module-B'
      angular.module('nazwa-modułu-A', ['nazwa-modułu-B']);
