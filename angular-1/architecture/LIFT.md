LIFT
====

LIFT dla stkutury plików
------------------------

- paradygmat, zasady, którymi warto się kierować przy budowie aplikacji

- L - locating our code is easy - trzymaj pliki danej founcjonalności w 1 folderze
- I - identify code at glance -   nazwy plikow powinny miec rozszezenia takie jak typ komponentu, np nazwa.controller.js
- F - flat structer as long as possible - utzymuje plaską strultórę folderów aż do 7 plików na folder
- T - try to stey DRY - staraj sie pisać kod z reuzywalnymi komponentami, aby sie nie powtarzac

- najwazniejsze zaday są pierwsze, czyli L > I > F > T

LIFT dla pliku
--------------

- trzymaj interfejs komponentu na górze pliku (interfjes - dependencje oraz zmienne / właściwości)

np. interfejs dla controller'a

    angular
      .module('app.nazwa-modulu')
      .controller('Nazwa', ['common', 'data', Nazwa]);

    function Avengers(common, data) {
      this.title = '';
      this.list = [];
      this.user = 'asd';
    }
