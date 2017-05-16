Componenty w angular-2
--------
Podstawowym bytem składającym się na moduły ng2 są komponent

- składają się z plików: .ts (obowiązkowo) .html, .css

Tworzyć komponenty możemy za pomocą angular-cli:
- ng generate component example-component
- taki component jest automatycznie rejestrownay w module
  - w pliku modułu (np app.module.ts) w obiekcjie konfiguracji modułu jest właściwość declarations (tablica), gdzie deklarujemy zaimportowane componenty

Składania podstawowa komponentu ng2:

      import {Component} from '@angular/core';

      @Component({
        selector: 'selektor-nazwa-komponentu',
        template:  '<p>markup componentu<p>',
        styles: []
      })
      export class NazwaKomponentuComponent {
        constructor () { }
      }

Obsługa metod componentów w html:
- do obsługi zdarzenia w html, należy podać w () nazwę zadażenia, następnie = oraz metodę która zostanie wywołana przy zdażeniu
- najprostrzy przykład, klikanie buttona z wywołaniem medoty componentu:
  - html:
        <input #myInput type="text" />
        <button (click)="passInputToConsole(myInput.value)">Show</button>
  - ts:
        passInputToConsole(input: String) {
          console.log('passInputToConsole', input);
        }
- referencja danych z input poprzez nadanie nazwy elementowi #nazwa oraz referencja do jego wartości nazwa.value
- aby przekzać obiekt eventu, można w html w wywołaniu metody przekzać $event:
      <button (click)="passInputToConsole($event, myInput.value)">Show</button>
  - dzięki temu mamy w componentcie infomcaje o evencie i możemy ją użyć:
        passInputToConsole(event: Event, input: String) {
          console.log(event);
          console.log('passInputToConsole', input);
        }
