Strukturyzowanie modułów
========================

- 'Level structure' tworzone sa 3 poziomy modułów, i wszystkie moduły korzystajć mogą z różnych modółów
- 'Exect structure' tworzone sa dependecje dla dokladnie i tylko dla okreslonego modulu

Level structure
---------------

- 3 typy modułów
  - Main App Module - główn, agregujący pozostałe moduł, rozruchamia aplikacjie
  - Cross App Modules - moduły posiadający reużywalne componenty (core + widgets)
  - App Feature Modules - moduły funkcjonalne aplikacji

np.

    // Main app module
    angular.module('main.app', [
      // corss app modules:
      'app.core',
      'app.widgets',

      // feature app modules:
      'app.avengers',
      'app.dashboard',
      'app.layout'
    ]);

    // Corss app module
    angular.module('app.core'. [
      // build in angular:
      'ngAnimate',

      // Reusable cross apps: (non widgets)
      'block.logger',
      'block.router',

      // external libs:
      'ui-router'
    ]);
    ...

    // Feature module
    angular.module('app.avengers', [])


- dzieki takiej strutkurze, 'app.avangers' ma dostep do wszystkiego z core i widgets, ale nie trzeba ich mu wstrzykiwac
