# Interceptory

Interceproty służą do przechwytywania wydarzeń i aplikowaniu zmian w związku z tymi wydarzeniami.
Podstawowym interceptorem jest http interceptor, który przechwytuje wszystkie zapytania http i może zmieniać obiekty wychodzące lub przychodzące w tychże.

## $http.interceptors

Privider serwisu $http, czyli $httpProvider, posiada właściwość .interceptors, która jest tablicą interceptorów. Każdy interceptor powinien
