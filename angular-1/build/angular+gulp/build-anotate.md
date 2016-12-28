Czym jest automatyzacja tasków
==============================

- automatyzacja zbierania wszystkich plików js'owych i wykonanie niezbednej pracy aby polaczyc je w dzialajaca aplikacje
- zewnętrzne narzędzia do wykonywania tych automatycznych tasków bildujących: grunt, gulp, webpack

Gulp
====

- bazuje na stremach
- instalowany za pomoca npm
- tworzymy taski które wykonują powiezone im zadania

Co zrobić gulpem?
-----------------

- doinstaluj gulp-ng-annotate
- zrob taska, ktory zbiera pliki js, przepuszcza je przez ngAnnotate, buduje plik jeden

np. - przepuszam wsystkie wkazane pliki przez ng-annotate, i zapisuje we wskazanym miejscu

      var source = ['./path/to/js/files/*.js'];

      gulp.task('build-with-annotate', function() {
        return gulp
          .src(source)
          .pipe(plug.ngAnnotate({add: true}))
          .pipe(plug.rename((path) => {
            path.extname = '.annotate.js';
          }))
          .pipe(gulp.dest('./build'));
      });
