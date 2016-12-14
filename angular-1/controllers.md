Controllers
===========

- jest to obiekt tworzony za pomocą konstruktora JSoweg, i wykorzystany do inicjalizowania $scope oraz dodawanie zachowań do $scope
- dodawany do htlm jak dyrektwa ng-controller (lub za pomocą UI router - bedzie dalej)
- agular inicjalizuje nowy obiekt controllera gdy napotka ng-controller, tworzy również nowy $scope, możliwy do injectowania w funkcji konstrukcyjnej controllera (dalej na $scope tworzymy zmienne).
- powinien być używany w trybie 'controller as', to instancja controllera zostanie przypisana do nowopowstawłego scope (dalej na kontrolerze tworzymy zmienne)
- tworzymy controller za pomocą metody .controller() modułu angularowego:

JS:

    angular.module('moduleName', []).controller('ControlerName', [
      '$scope',
      function ($scope) {
        $scope.varName = 'abc';
      }
    ])

HTML:

    <... ng-controller='ControllerName'>
      {{ varName }}
    </...>

- contollery nie powinny robić zbyt dużo, jedynie zapewniać logikę dla 1 widoku
- controllery nie powinny !!!:
  - manipulować DOM (dyrektywy)
  - formatować input (controls)
  - filtrować output (filters)
  - dzielic kod miedzy modyly (serwisy)

***

Dziedziczenie w Controllers
---------------------------

- czesto kontrolery w dome są zagnieżdzone, dzięki temu controllery 'dzieci' mają dostęp do wszyskich zmiennyhc controllerów rodziców (z dołu do góry)

***

'Controller as ' syntax
-----------------------
[https://toddmotto.com/digging-into-angulars-controller-as-syntax/]

- zamiana polega na tym, że zmienne są tworzone na obiekcie controllera a nie bezpośrednio na $scope [obiekt controller jest na $scope]
- sam controller jest przypisany do zmiennej na scope $podanej jako 'as'

JS:

    angular.module('moduleName', []).controller('ControlerName', [
      '$scope',
      function ($scope) {
        this.varName = 'abc';
      }
    ])


HTML:

    <... ng-controller='ControllerName as ctrlName'>
      {{ ctrlName.varName }}
    </...>

- takim podejściu nie nadpisujemy wartości patent Scopów przy dziedziczeniu kontroloreów, (nie trzeba się odnosić zmiennej rodzica o tej samej nazwie za pomocą $parent.varName a tylko urzywamy ctrlName.varName) ( o ile damy rozne nazwy w 'controller as ')
- możemy korzystać z metod $scope (bordacts, on, itp) tylko gdy potrzebujemy (zainjectowany w naszym przykaladzie $scope nie jest obowiązkowy, lecz aby korzystac z ww. metod nalezy go injectowac)

***

'Controler as' w komponetach
----------------------------

- w dyrektywach, componentach lub UIrouterze urzywamy właściwości


    { ... 'controllerAs': 'ctrlName' ... } i tyle :)
