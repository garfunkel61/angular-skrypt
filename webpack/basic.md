Web-pack
========

- czym jest? narzędzie buildujące, które doładowywuje biblioteki oraz łączy plik w aplikacjach
- polega na konfiguracji
- różni się tym, że wszystkie dołącznae źródła (css'y, fonty itp) traktuje jak moduły JS'owe
- dzięki temu dla poszczególnych stron może tworzyć tylko takie asety które są im potrzebne (a nie wszystko ładować)

Jak zacząć?
-----------

- instalujemy jak npm modul, bo nim jest
- tworzymy plik webpack.config.js - w nim bedziemy mieli konfurację
- setupujemy konfiguracje
- uruchamiamy webpacka który zbuduje aplikacjie: node node_modules/.bin/webpack
  - z wypisanie wszystkich modułów (wewnetrzynch i zewnetrznych) node node_modules/.bin/webpack --display-modules
  - z automatyczną obserwacją zmian i przebudową node node_modules/.bin/webpack --watch

Prosta konfiguracja
-------------------

Obiekt konfiguracyjny musi być eksportowany a pliku konfiguracyjnego, oraz określać conajmniej:
- punkt wejścia entry
- punkt wyjścia output


    module.exports = {
        entry:  './src',
        output: {
            path:     'builds',
            filename: 'bundle.js',
        },
    };

Transpilacja plików
-------------------

- w pliku konfiguracyjnym możemy okreslić jakie pliki mają być przetwarzane
- konieczne jest zainstalowanie loader'a oraz transpilatora
- loader to moduly npm umozliwijące transpilacje danych plików
- transpilatoru to moduly npm transpilujące stosowne pliki

Transpliacja ES6 -> ES5

- zainstaluj transpilatory babel-core babel-preset-es2015
- skonfiguruj transpilatroy .babelrc { "presets": ["es2015"] }
- zainstaluj loader: babel-loader
- skonfiguruj loader w webpack.config.js, przez dodanie klucza module do obiektu konfiguracji


    module: {
        loaders: [
            {
                test:   /\.js/,
                loader: 'babel',
                include: __dirname + '/src',
            }
        ]
    }

- test: jakie pliki wchodą do loadera - podajemy regexp
- loader: jaki loader jest stosowany dla tych plików
- loaders: seria loaderów stsowanych dla plików (tablica lub str!str!str) czytane od P do L
- includ: skąd brać pliki do loadera
- exclud: których plików nie brać do loadera

Server developerski
-------------------

- jest w webpacku prosty server developerski, który nalezy dociagnąć jako zewnętrzny modył npm:
  - webpack-dev-server
- uruchomienie serwera bedzie serwowało pliki z lokalizacji jego uruchomienia lub możemy podać określone pliki parametrem:
  - node node_modules/.bin/webpack-dev-server --content-base podana-lokacja-plików/
- dwa tryby uruchomienia: z nagłówkiem (defaultowy, aplikacja jako iframe), czysty (sama aplikacjia bez dodatków) 'inline'
  - node node_modules/.bin/webpack-dev-server --inline

Pytania?
--------

- co podajemy jako test? (path?) - wildcard, path, regexp
- czy można jako include dawać wildcard'a po prostu?
- jakiego servera urzywać? co z webpack-dev-server?
- czy sosowac kilka loaderów dla jednych plików?
- czy jakoś fajnie można stosować 'chunks' przy aplikacjia angularowych?
