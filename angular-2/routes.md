# Routes

- służą do obsługi różnych widoków w aplikacji (tak jak w angularJS)
- pochdzą z modułu '@angular/router'

## Podstawowa konfiguracja

- każdy moduł powinien mieć swój plik route'ów
- plik nazywany zgodnie z nazwą modułu oraz rozszeżeniem nazwa.routes.ts
- plik router exportuje const typu  ModuleWithProviders który jest tworzony przez metodę forRoot modułu RouterModule z przekazanym paramentrem - tablicą route'ów modułu
- plik router importuje ModuleWithProviders oraz Routes, RouterModule
- plik tworzy const routes typu Routes, bedący tablicą obiektów route, zawierających ścieżkę oraz component który dany route obsługuje

#### Przykład podstawowej konfiguracji routera:

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

- kolejność routów w tablicy routów ma znaczenie, - im wyżej tym wyższy priortyter
  - wildecardy powinny być na dole,
  - spewcyficzne pathy na górze
-

## Debugowanie

- aby debugowac dokładnie co się dzieje w trakcie nawigacji miedyz routami, stosuj `{ enableTracing: true }` jako drugi parametr w `RouterModule.forRoot()`

## Tworzenie prostego rutowania - ściąga:

- utwórz plik routów dla modułu: app.routes.ts
- zaimportuj plik routów do modułu
- umieść zaimportowany obiekt routów w dekoratorze modułu w tablicy importów
- w templejcie componentu umieszczamy routerLink do nawigacji oraz router-outlet do wyświetlania

## Dostęp do stanu

- ścieżka oraz parametry routu są dostępne w componecie za pomocą serwisu ActivatedRoute
- popularne parametry serwisu: url, data, paramMap, queryParamMap, ...
- [podstawowa dokumentacja](https://angular.io/guide/router#activatedroute-the-one-stop-shop-for-route-information)
- [pełna dokumentacja](https://angular.io/api/router/ActivatedRoute)

## Tworzenie podwidoków - children views

- każdy widok może mieć swoje widoki-dzieci
- widoki dzieci będą wyświetlane w RouterOutlet templejtu rodzica
- widoki-dzieci tworzymy w pliku routów danego modułu, za pomocą właściwości `children`
- `children` przyjmuje tablicę obiektów routes, dokładnie takich samych jak normalnę nadrzędne routy
- scieżka do widoku-dziecka jest połączneniem ścieżki rodzica, / oraz scieżki dziecka

      export const routes: Routes = [
        { path: animals,
          children: [
            { path: 'cats', component: CatListComponent },
            { path: 'dogs', component: DogListComponent }
          ]
         }
      ];

## Widoki chronione (protected)

- na podstawie: https://blog.thoughtram.io/angular/2016/07/18/guards-in-angular-2.html
- są powszenie wykorzystywane do zabezpiecznie widoków (urli) przed określonymi userami (np. logowanie)
- w ng2 mamy 4 typy zabezpieczen widoków:
  - CanActivate
  - CanActivateChild
  - CanDeactivate
  - CanLoa
- zabezpiecznie (Strażnik) to tak naprawdę funkcje zwracjące:
  - Observabla<boolean>
  - Promis<boolean>
  - boolean

- implementować Strażników możemy za pomocą:
  - funkcji
  - classy

### Tworzenie za pomocą funkcji

- tworzymy prosty provider który jest funkcją zwracającą jakiś typ booleanu

      @NgModule({
        ...
        providers: [
          provide: 'CanAlwaysActivateGuard',
          useValue: () => {
            return true;
            }
          ],
          ...
      })

 - urzywanym w routech jako element tabli canActivate obiektu routu

       export const AppRoutes:RouterConfig = [
         {
           path: '',
           component: SomeComponent,
           canActivate: ['CanAlwaysActivateGuard']
         }
       ];

- dzieki tablicy możemy mieć wielu Strażników strzegących dany route

### Tworzenie za pomocą classy

- jeżeli dane Strażnik potrebuje mieć jakieś serwisy z naszej aplikacjie, to powinniśmy go trzyć jako klasę, do której wstrzykniemy serwisy
- taki Strażnik jest implementacją @Injectable(), czyli klasycznym providerem
- taki Strażnik musi posiadać jedną z medot których zabezpiecznie będzie realizował:
  - canActivate()
  - canActivateChild()
  - canDeactivate()

      import { Injectable } from '@angular/core';
      import { CanActivate } from '@angular/router';
      import { AuthService } from './auth.service';

      @Injectable()
      export class CanActivateViaAuthGuard implements CanActivate {

        constructor(private authService: AuthService) {}

        canActivate() {
          return this.authService.isLoggedIn();
        }
      }

- w module musi być zarejestrowany jak klasyczny provider:

      @NgModule({
        ...
        providers: [
          AuthService,
          CanActivateViaAuthGuard
        ]
      })
      export class AppModule {}

- a następnie może być użyty jako Strażnik

      {
        path: '',
        component: SomeComponent,
        canActivate: [
          'CanAlwaysActivateGuard',
          CanActivateViaAuthGuard
        ]
      }

### Daktywacja

- może być urzywana jako zabezpiecznie przed opuszczeniem danego routu
- może prosić o potwierdzenie gdy użytwkonik chce opuścić niezapisany formularz
