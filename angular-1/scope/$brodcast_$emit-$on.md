Metody scope
============

$broadcast $emit $on
--------------------

- metody propagujacę (b i e) oraz nasłuchjące (o) określonego EVENTU
- $broadcast - wywołanie EVENTU do wszystkich dzieci danego $scope lub $rootScope
- $emit - wywołanie EVENTU do wszystkich rodziców danego $scope

      $scoep|$rootScope.$emit|$brodcast('nazwa-eventu');
      //-> nazwa taka zeby wskazywkała na miejsce wykonania

- $on - metoda nasłuchująca podanego jako parametr EVENTU i wykonująca określony callback

      $scope|$rootScope.$on('nazwa-eventu', (event) => {});
