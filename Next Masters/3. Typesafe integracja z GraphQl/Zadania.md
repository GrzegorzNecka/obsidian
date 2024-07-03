
# 3.11: Zadania 3

## Zadania

Implementacja poniższych zadań zależy od wybranego serwera GraphQL:

- Użycie naszego API: [https://graphql.hyperfunctor.com/graphql](https://graphql.hyperfunctor.com/graphql)
- Użycie Hygraph – gotowego CMS-a z darmowym planem, który udostępnia możliwość komunikacji po GraphQL.
- Postawienie instancji Strapi – CMS/CMS Open Source do hostowania na swoim serwerze.
- Napisanie własnego serwera GraphQL w dowolnej technologii (nasz wybór to oczywiście TypeScript).

1. Zaimplementuj widok pojedynczego produktu na podstawie danych pobieranych z GraphQL.
2. Dodaj podstrony kategorii pod adresem `/categories/[nazwa kategorii]/[numer strony]`
3. Popraw komponent `ActiveLink` tak, że będąc na stronie `/categories/t-shirts/2` aktywny jest link `/categories` w navbarze.
4. Dodaj podstrony kolekcji pod adresem `/collections/[nazwa kolekcji]`. Kolekcje znajdziesz w schemie GraphQL.
5. Zaimplementuj komponent z sugerowanymi **czterema** produktami na podstawie GraphQL. Kryteria wyboru produktów ustal sam(a). Dodaj do kontenera tego komponentu atrybut `data-testid="related-products"`
6. Zaimplementuj wybór wariantu produktu (kolor, rozmiar) na podstawie pól, które znajdziesz w GraphQL w schemie produktów.
7. Popraw paginację tak, aby pobierała dane z GraphQL. Dodaj prerenderowanie kilku pierwszych stron.
8. Zaimplementuj prostą wyszukiwarkę używając GraphQL. Wyszukiwarka powinna być widoczna w navbarze (input), a po wyszukaniu użytkownik powinien być na stronie `/search?query=(WPISANE SŁOWA)` Ręczna zmiana ?query=… lub odświeżenie strony powinny również powodować wyszukanie i działać. Opcjonalnie, użyj do tego `@apollo/experimental-nextjs-app-support`.
9. Zaimplementuj wyszukiwanie, które jest automatycznie (bez naciśnięcia ENTER) wyzwalane po 500 ms od momentu skończenia pisania treści zapytania przez użytkownika. Upewnij się, że nie wykonujesz niepotrzebnie zapytań gdy użytkownik jest w trakcie pisania.

⚠️ **Uwaga**: Jeśli używasz plików `loading.tsx` to pamiętaj, aby znalazł się w nich element z atrybutem `aria-busy="true"`.