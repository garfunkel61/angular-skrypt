Build in directives
===================

- angular posiada dużo wbudownaych dyrektyw
- tutaj znajdziesz notatki jak urzywać tychże

ng-class
--------

- służy do dynamicznego nadawania klasy elemntom
- działa jako atrypbut ng-class="..."
- przyjumje obiekt w ktorym kluczami sa nazwy klas, a wlasciwosciami wyrzazenie ewalujace do booleanow

HTML

    < div ng-class="{
      'warning': task.status == 'Hold' ,
      'success': task.status == 'Completed',
      'active': task.status == 'Started',
      'danger': task.status == 'Pending'
      } ">

ng-repeat
---------

- służy do iterowania po tablica / obiektach w i renderowaniu elementów zgodnie z elemetami / kluczami
- każdy wyrenderowany element otrzymoje swoj scope, posiadajacy wbudowane wlasciwosci:
  - $index (numer elementy)
  - $first (boolean, czy pierwszy)
  - $middle (boolean, czy środkowy)
  - $last (boolean, czy ostatni)
  - $even (boolean, czy parzysty)
  - $odd (boolean, czy nieparzysty)
- działa jako atrybut ng-repeat="..."
- przyjuje obiekt lub tablice

HTML - tablica

    <ul>
      <li ng-repeat='element in elemntsArray'>...</li>
    <ul>

HTML - obiekt

    <ul>
      <li ng-repeat='(key, val) in object'>...</li>
    <ul>
