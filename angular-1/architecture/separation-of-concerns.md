Separation of concerns - rozdzielenie odpowiedzialnosci
========================================================

- przeciwienstwo kodu typu 'spagetti'
- kazdy z komponentow aplikacji wykonuje tylko 1 rzecz
- komponent musi wykonowyac te rzecz dobrze

- potocznie nazywane kodem RAVIOLI

np.
- controller tylko i wyłącznie obsługuję logikę danego widoku, nie wykonuje calli, bordcastuje eventow etc

Zasada jedności 'Rule of 1'
---------------------------

- aby dobrze realizować Separation of concerns nalezy posługiwać sie zasadą jedności, która mówi:
  - kompontne może pełnić tylko 1 rolę (spełniać jedną funkcję, np serwis pobierający dane)
  - komponent może być tylko w 1 pliku, i 1 plik może mieć tylko 1 komponent
  - komponent tworzony jest tylko w 1 celu


  Jak separate concerns?
  ----------------------

  - podziel aplikacje na moduly
  - moduly podziel na componenty (serwisy, controllery, widgety (directives, components))
