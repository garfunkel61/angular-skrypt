Patterny tworzenia componentów w Angular
========================================

Klasyczny - register + inject, function
--------------------------------------

    angular
      .module('app.dashboard')
      .controller('Dashboard', ['common', 'data', Dashboard]);

    function Dashboard(common, data) { ... }

Odwórcony - function, inject, register
-----------------

    function Dashboard(common, data) { ... }

    Dashboard.$inject = ['common', 'data'];

    angular
      .module('app.dashboard')
      .controller('Dashboard', Dashboard);

- w stosunku do klasycznego pozbywa sie tablicy dependecji z metdoy controller, a stosuje DI bezpośrednio na konstruktorze controloera


Wariacja - register, inject, function
-------------------------------------

    angular
      .module('app.dashboard')
      .controller('Dashboard', Dashboard);

    Dashboard.$inject = ['common', 'data'];

    function Dashboard(common, data) { ... }


Automatyzacja
--------------

- za pomocą ngAnnotate, możemy pominać $inject, a np gulp przy budowie bedzie za nas uzupelniał tę cześć

np.

    angular
      .module('app.dashboard')
      .controller('Dashboard', Dashboard);

    /* @ngInject */
    function Dashboard(common, data) { ... }
