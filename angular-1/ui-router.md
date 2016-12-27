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
-'miejsca' tworzymy za pomoca metody state(), przyjujacej obiekt konfiguracyjny 'miejsca'
- miejsca (stany) moga być aktywowane przez przejscie w przegladarce do nazwy stanu poprzedzonego #:
- stany sa renderowane w miejscu dyrektywy w templajcie <ui-view></ui-view>


      www.aplikacja.com/#/app

        $stateProvider.state('app', {
          url: '/app',
          abstract: false,
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

- templejt 'miejsca' jest wyswietlany za pomoca dyrektywy ui-view
- uruchomienie stany moze nastapic w jeden ze sposobow:
  - wywołanie $state.go()
  - klikniecie w ui-sref dyrektywe atrybutu
  - navigacje standardowa do wstazanego url

- 'miejsca' maja czesto wstpolne czesci w aplikacji, dla tego celu stosowane sa 'nested-states'
  - templejt stanu może mieć swój <ui-view></ui-view> i wyswietlać w nim swoje 'podstany' ('nested-states')


    .state('about', {
      url: 'about',
      template: '<h3>about</h3>
                    <ui-view></ui-view>'
    })
    .state('about.sub', {
      url: '/sub',
      template: '<h4>sub</h4>'
    })

- stan sub jest dzieckiem about, i bedzi wysietlony w ui-view templejtu about w przypadku aktywacji tego stanu

$urlRouterProvider
------------------

- umozliwia obsluge dodatkowa podanych adresów url
- posiada dwie podstawowe metodyL .when() i .otherwise()

- .when() -sluzy do przekierowan, przyjuje dwa parametry
  - 1 parametr: - wpisany url (moze byc regexp)
  - 2 parametr: - url na ktory przeikerujemy
- .otherwise() - słuzy do przekirewoania wszystkich niezdefiniowanych w state'ach lub .when()'ach url na podany url


***

Stany w sub-modułowej aplikacji
-------------------------------

- każdy moduł aplikacji złorzonej może definiować routy w metodzie .config() submodułów, analogicznie jak w przypadku konfiguracji pojedynczego modułu
- Przykład sub-modułowych routów: https://plnkr.co/edit/0b9CpultcnH5yhuXdTLH?p=preview


Routy oparte o componenty
-------------------------

- w miejsce controllera i templejtu w routach możemy podawać nazwe componentu injectowanego do modulu


    ...
    .state('main-component', {
      url: '/main',
      component: 'component-name'
    })
    ...


Paramentry stanów
------------------

- w przypadku gdy chcemy generowac stany na podstawie listy jakis obiektow, mozemy w url stanu podawac parametr ktory bedzie dostepny w kontrolerzez tego stanu
- w urlu stanu podajemy parametr zapisany w pojedynczej interpolacji
- paramentr mamy dostepny zarowno w controlerze jak i resolvie stanu

    ...
    .state('single-elem', {
      url: '/elem-list/{elemId}',
      component: 'component-name'
    })
    ...

- linkowanie do parametryzowanego stanu jest mozliwe poprzez wywolanie ui-sref z nazwia stanu i jako paramter podana wartoscia parametru


    ... ui-sref='single-elem({ elemId: 123 })' ...

- przyklad aplikacji z list-item patternem i nested-view: https://plnkr.co/edit/zRXmod?p=preview

Resolvovanie zmiennych w stanie
-------------------------------

- dzieki wlasciwosci resolve mozemy przekazywac do stanu rozne dane zanim stan zostanie wywolany
- gowlnie slurzy do pobierania danych servisem z rest api gdy na dany stan wchodzimy
- dane sa dostepne w controllerze / componedzie pod podana w obikcie resolve nazwa


    .state('main-component', {
      url: '/main',
      component: 'component-name',
      resolve: {
        items: () => {
          return $http.get('url-po-dane')
        }
      }
    })
