ng-annotate
==========

Czym jest?
----------

- narzędzie umożliwiające bezpieczną minifikację kodu angularowego, w przypadku gdy używane jest DI w aplikcji (nie w zapisie tablicowym lub za pomocą metody $inject)

Jak przekazywać zależności w anularze? 3 metody
----------

#### Function arguments - 'zapis argumentowy',

- zapis polega na przekazaniu do metody komponentu (np controller lub servis) czystej funkcji z zależności jako argumentami tej funkcji
- w takim zapisie przy minifikacji następuje zamiana argumentów przkazywanych do funkcji komponentu (np. controllera) na jednoliterowe wartości.
- w takim przypadku zależności injectowane zostają zmienione z orinalnych nazw na nazwy robocze, jednoliterowe (a, b, c ..)

      function Ct ($scope) { ... }

      angular.module('app', [])
          .controller('ControllerName', Ct);

- w tym kodzie po minifikacji argument funkcji Ct $scope zostanie zmieniony na 'a', przez co zminifikowany kod nie będzie działał


#### Array notation - zapis tablicowy

- zapis polega na przekazaniu do metody komponentu (np controller lub service) tablicy zawierającej stringi będące nazwami injektowanych zależności oraz jako ostatniego elementu tablicy funkcji z zależności jako argumentami tej funkcji zgodnie z kolejnością elementów tablicy
-  takim zapisie przy minifikacji następuje zamiana argumentów przkazywanych do funkcji komponentu (np. controllera) na jednoliterowe wartości
-  takim przypadku zależności injectowane zostają zmienione z orinalnych nazw na nazwy robocze, jednoliterowe (a, b, c ..) ale dzięki stringom w tablicy, minifikacja nie psuje kodu gdyż strinig nie zostają zmienione


      function Ct ($scope) { ... }

      angular.module('app', [])
        .controller('ControllerName', ['$scope',  Ct]);

- w tym kodzie po minifikacji argument funkcji Ct $scope zostanie zmieniony na 'a', ale dzięki stringowi '$scope' będzie wiadomo czym to 'a' jest


#### Indirect injection - pośrednie wstrzyknięcie

- zapis polega na przekazaniu do metody komponentu (np controller lub servis) czystej funkcji z zależności jako argumentami tej funkcji oraz przypisaniu właściwości .$inject tej fukncji, o wartości równej tablicy zależności
-  takim przypadku zależności injectowane zostają zmienione z orinalnych nazw na nazwy robocze, jednoliterowe (a, b, c ..) ale dzięki właściwości $inject z tablicą zależności, minifikacja nie psuje kodu gdyż strinig w tablicy nie zostają zmienione


      function Ct ($scope) { ... }

      Ct.$inject = ['$scope'];

      angular.module('app', [])
          .controller('ControllerName', Ct);

- w tym kodzie po minifikacji argument funkcji Ct $scope zostanie zmieniony na 'a', ale dzięki stringowi '$scope' w właściwości $inject będzie wiadomo czym to 'a' jest
