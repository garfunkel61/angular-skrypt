# Routes

- służą do obsługi różnych widoków w aplikacji (tak jak w angularJS)
- pochdzą z modułu '@angular/router'

## Podstawowa konfiguracja

- każdy moduł powinien mieć swój plik route'ów
- plik nazywany zgodnie z nazwą modułu oraz rozszeżeniem nazwa.routes.ts
- plik router exportuje const typu  ModuleWithProviders który jest tworzony przez metodę forRoot modułu RouterModule z przekazanym paramentrem - tablicą route'ów modułu
- plik router importuje ModuleWithProviders oraz Routes, RouterModule
- plik tworzy const routes typu Routes, bedący tablicą obiektów route, zawierających ścieżkę oraz component który dany route obsługuje

#### Przykłado podstawowej konfiguracji routera:

      // Buildin modules
      import { ModuleWithProviders }  from '@angular/core';
      import { Routes, RouterModule } from '@angular/router';

      // Custom Components
      import { CatListComponent } from './cats/cat-list.component';
      import { DogListComponent } from './dogs/dog-list.component';

      // Route Configuration
      export const routes: Routes = [
        { path: 'cats', component: CatListComponent },
        { path: 'dogs', component: DogListComponent }
      ];

      export const routing: ModuleWithProviders = RouterModule.forRoot(routes);

- moduł posiadający swój router musi ten router importować i dodać do konfiguracji w dekoratororze modułu w tablicy importów:
  - `imports: [... routing ...]`
- dzięki wykorzystaniu RouterModule w componencie mamy dostęp do dyrektyw routera, m-in:
  - RouterOutlet - wyświetla templejt rutowanego componentu
  - RouterLink - umozliwia nawigację miedzy routami

## Tworzenie rutowania - ściąga:

- utwórz plik routów dla modułu: app.routes.ts
- zaimportuj plik routów do modułu
- umieść zaimportowany obiekt routów w dekoratorze modułu w tablicy importów
- w templejcie componentu umieszczamy routerLink do nawigacji oraz router-outlet do wyświetlania  
