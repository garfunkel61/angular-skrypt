UI Router
=========

- jest dodakowa biblioteka dla Angulara
- slurzy do tworzenia stanow, widoków i przesc miedzy nimi, które sa dostepne pod adresami url
- musi byc dolaczony do aplikacji (np jako modul npm)

Definiowanie stanów
-------------------

- po zaimportowaniu ui-router do aplikacji, mozemy korzystac z $stateProvider, $urlRouterProvider, $locationProvider w callbacku metody .config() modułu aplikacji


        angular.module().config(($stateProvider,
          $urlRouterProvider, $locationProvider) => {
            ...
        })

$stateProvider
--------------

- pozwala na tworzenie 'miejsc' w aplikacji, ktore opisuja jak sie w tym miejscu zachowuje UI
- 'miejsca' tworzymy za pomoca metody state(), przyjujacej obiekt konfiguracyjny 'miejsca'


        $stateProvider.state({
          url: '/app',
          templateUrl: 'app/main/main-page.html',
          controller: 'MainPageCtrl',
          controllerAs: 'mainPageCtrl',
          resolve: {
            simpleVal: () => { return 'simpleVal'; }
          },
          data: {
            simpleData: 'data'
          }
        });

- templejt 'miejsca' jest wyswietlany za pomoca dyrektywy ui-state
- 'miejsca' maja czesto wstpolne czesci w aplikacji, dla tego celu stosowane sa 'nested-states'
- uruchomienie stany moze nastapic w jeden ze sposobow:
  - wywołanie $state.go()
  - klikniecie w ui-sref dyrektywe atrybutu
  - navigacje standardowa do wstazanego url

- dokładniej o $stateProvider: https://github.com/angular-ui/ui-router/wiki
