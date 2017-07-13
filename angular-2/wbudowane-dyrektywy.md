Wbudowane componenty i dyrektywy
------

### ngFor - iterowanie w html

- poznwala na iteracje w html'u po danych itertowalnych (tablice, ...) z wyświetleniem elementów
          <ol>
            <li *ngFor="item of serviceName.itemsName">
              {{ item }}
            </li>
          </ol>

- można iterować po componentach, przekazując im dane
- można wyśiwetlić index, dodając w ngFor let i = index
        *ngFor="...; let i = index;"
- ..

### ngSwitch - warunkowe wyświetlanie elementów

- pozwala warunkowo wyświetlić elementu html zgodnie z wartością przypisaną dyrektywie
- nie wyswietlany elemnt nie jest totadny do DOM
      <p [ngSwitch]="item.value">
          <span *ngSwitchCase="yes">Yes</span>
          <span *ngSwitchCase="no">No</span>
          <span *ngSwitchDefault>Default</span>
      </p>

### ngModel - 2way data binding

- za pomocą ngModel możemy synchronizować dane miedzy widokiem a componentami
- na elemecie pobierającym dane możemy zdefiniować ngModel, dzięki temu bedziemy synchronizować dane przekazywane z widoku do komponentu
- na inpucie ustawiamy [(ngModel)]='zmienna', tak przekazemy dane do kody (compoentu)
- taka zmienna może być zmieniona w construktorze i html zostanie zakutalizowany, ale może też być zmieniona w html i w construktorze sie zmieni

### @Input - wstrzykiuwanie danych do componentów

- możemy przekazywać dane z componentu 'rodzinca' do jego dzieci, tak jak w AngJs
- służy do tego Input

- w html gdzie umieszczamy 'dziecko' compoent, podajemy w nawiasach kwadratowych nazwę zmiennej do ktorej wstzykujemy dane z 'rodzica'

        <component-name [zmiennaBioraca]="zmiennaDajacaZrodzica">

- w kodzie componentu 'dziecko' musimy zaimpontrować 'Input' z core/angular, oraz za pomocą @Input zdefiniować zmienną biorącą

        impornt { Input } form '@angular/core';

        ... klasa componentu

          @Input() zmiennaBiorąca;

        ...
- tak przekazujemy dane w komponentach z rodzica do dziecka

### @Output - przekazywanie danych z componentu do serwisu ?

- może być wykorzystany do aktualizacji danych zgodnie component <=> serwis
- do @Output możemy stworzyc zmienna z przypisanym obiektem new EventEmitter - który pozwala emitowac eventy
- metodę zmiennej @Output możemy wywoływać w html'u z przekazanymi parametrami, za pomocą właściwości .emit

- ToDo: dopisz jak lepiej zrozumiesz ... -> https://egghead.io/lessons/angular-2-pass-events-from-angular-2-components-with-output

### ngClass

- kondycyjne nadawanie class cssowych,
- jak w angJs,
- używamy jak wstrzykiwaną dyrektywę, czyli []
      [ngClass]="{nazwa-classy:warunke-boolean-nadania-classy-z-kodu}"

##### () - reperezntuje wywołanie eventów
##### [] - reprezentuje wstrzykiwane dane
##### [()] - 2way binding danych
