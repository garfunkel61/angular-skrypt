Struktura plikow
================

- może być dowolna
- wiele różnych metod dzielenia aplikacji na pliki
- najwazniejsze aby byc spojnym w sposobie tworzenia strkutury plikow i folderow

***

Struktura funkcjonalna
----------------------

- zakłada podział folderów i plików aplikacji zgodnie z funkcjonalnościami aplikacji
- kazdy folder pownien byc odpowiednikiem funkcjonalności i posiadać moduł angularowy oraz posiadac swoje sub-moduły itp
- przykład na podstawie aplikacji CRUD ksiazek



      app/
          index.js
          categories/
              categories.module.js
              categories.html
              categories.spec.js
          books/
              list-books/
                  list-books.module.js
                  list-books.html
              create-book/
                  create-book.module.js
                  create-book.html
              edit-book/
                  edit-book.module.js
                  edit-book.html
              books.module.js
              books.html
              books.spec.js
          common/
            books-model/
            categories-model/


- nazwy modulow: [foldery.plik.typ] 'books.list-books.module'
