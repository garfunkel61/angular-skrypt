Style w componentach ng2
---------

- są umieszczane w tablic styles obietku konfiguracji componentu @Component
- tablica przyjmuje stringa ktroy jest zbioerm selektorów i reguł css'owych
- można podawać jako tablice do style, właściwość 'styles'
- można podawać jako tablic z url do pliku, właściwość 'styleUrls'

### Specjalne selekotory

- w ng2 występują specjalne selektory, między innymi:
  - :host { ... } - wybiera element główny (root) componentu
  - :host(...) - warkunkowe nadanie dodatkowych styli gdy root posiada podaną jako argument .class'e
        :host(.active) { ... }
  - :host-context(...) - warkunkowe nadanie styli gdy root jest potomkiem podanej jako argument .class'y
        :host-contex(.smaller) h1 { ... }
  - /deep/ - dostęp do stylowania elementów pochodzących z componetów bedądzych dziećmi componentu root (z defaultu style nie zostaną nadane na zagniezdzone w componecie componenty)
  - nazw-componentu - można dostać się do componentu dziecka przez jego nazwę

### Enkapsulacja styli

- component z defaultu zostaje zasilony globalnymi stylami projektu, i można stosować te style na elementach componetu
- component posiada właściwość 'encapsulation', która przyjmuje obiekt ViewEncapsulation z 3 właściwościami:
  - Native - component nie bedzie zasiolony stylami globalnymi (odizolowanie styli komponentu)
  - Emulated - style globalne są dostępne, style componentu nie wchodzą do styli globalnych
  - None - style globalne są dostępne, style componentu zasilają style globalne i działają w całym projekcie
- defaultowo component bez nadawani wartości właściwości 'encapsulation' bedzie miał: ViewEncapsulation.Emulated
