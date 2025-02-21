
# Projekt interop z nowościami:

https://web.dev/blog/interop-2023?hl=pl
https://web.dev/blog/interop-2025?hl=pl

Part of new ==containment spec==. Partial implementation in Firefox and Safari

# Control rendering with `content-visibility`

- [https://infrequently.org/2020/12/content-visibility-scroll-fix/](https://infrequently.org/2020/12/content-visibility-scroll-fix/)
- [https://web.dev/articles/content-visibility](https://web.dev/articles/content-visibility)

content-visibility to nowoczesna właściwość CSS, która pozwala na znaczącą optymalizację renderowania poprzez kontrolę nad tym, czy element ma być renderowany.

Podstawowe wartości:
- **auto** - przeglądarka pomija renderowanie elementów poza viewport
- **hidden** - element jest ukryty (podobnie jak display: none), ale zachowuje style
- **visible** - domyślne zachowanie, zawartość jest zawsze renderowana

Przykład użycia:
```css
.section {
  content-visibility: auto;
  contain-intrinsic-size: 0 500px; /* Sugerowany placeholder size */
}
```

**Najlepsze zastosowania:**

- Długie listy elementów
- Sekcje poniżej "fold" (poza początkowym viewport)
- Komponenty w nieskończonym scrollowaniu
- Tabowe interfejsy
- Rozbudowane layouty z dużą ilością contentu

**Kluczowe zalety:**

- Dramatyczna poprawa wydajności pierwszego renderowania
- Redukcja zużycia pamięci
- Automatyczne zarządzanie renderowaniem podczas scrollowania
- Zachowanie scroll-barów (w przeciwieństwie do display: none)

Warto łączyć z **contain-intrinsic-size** aby uniknąć "skakania" layoutu podczas scrollowania. Wsparcie jest dobre w nowoczesnych przeglądarkach (Chrome, Edge, Opera), ale brak w Safari i Firefox.

# `contain: strict`

Specify that the children of a DOM element will not, in any way, affect the rendering of DOM content outside the element, to improve rendering performance.


```css
div { 
contain: none; /* no containment on element */ 
contain: layout; /* influences how element relates to other elements in the document */ 
contain: paint; /* influences how element is painted to screen */ 
contain: size; /* influences how element affects size calculations for the page */ 
contain: style; /* is considered at-risk for removal from spec */   contain: content; /* combines layout and paint */ 
contain: strict; /* combines layout, paint, and size */ 
}
```


### Oto zwięzłe podsumowanie właściwości CSS contain:

**contain** to właściwość CSS, która informuje przeglądarkę, że dany element i jego potomkowie są niezależni od reszty drzewa dokumentu. Głównym celem jest optymalizacja wydajności renderowania strony.

Podstawowe wartości:

- **layout** - izoluje wpływ elementu na układ innych elementów
- **paint** - ogranicza renderowanie do granic kontenera, pomija renderowanie niewidocznych elementów
- **size** - ignoruje potomków przy obliczaniu wymiarów (wymaga zdefiniowania width i height)

Wartości skrótowe:

```css
.element {
  contain: content; /* równoważne z: layout paint */
  contain: strict;  /* równoważne z: layout paint size */
}

```

Najlepsze zastosowania:

- Kontenery z dynamiczną zawartością (np. widgety)
- Elementy z treścią third-party (np. reklamy)
- Obszary grid w CSS Grid
- Elementy ze scrollowaniem (szczególnie paint dla lepszej wydajności)
- Komponenty SPA z dynamicznie zmienianą zawartością

Właściwość jest szczególnie przydatna w aplikacjach z dużą ilością dynamicznych zmian w DOM, gdzie może znacząco zredukować obliczenia związane z layoutem i renderowaniem. Wsparcie przeglądarek jest dobre, z wyjątkiem Safari.

### co dzieje się pod spodem

- Przeglądarka tworzy tzw. "containment context" - wyizolowany kontekst renderowania
- Element z contain staje się "boundary box" - granicą dla operacji layoutu i renderowania
- Przeglądarka może zoptymalizować proces renderowania poprzez:
- Pominięcie przeliczania layoutu dla elementów poza kontenerem
- Ograniczenie obszaru repaintingu tylko do granic kontenera
- Cachowanie rezultatów renderowania

contain to mechanizm optymalizacyjny działający w głównym wątku renderowania, który pomaga przeglądarce lepiej zarządzać zasobami poprzez izolację wpływu zmian w określonych częściach DOM.


## for isolating rendering layers

## Offscreen Canvas
### Performant Three.js on separate thread

- [https://github.com/pmndrs/react-three-offscreen](https://github.com/pmndrs/react-three-offscreen)
- [https://www.fricze.com/demo/three](https://www.fricze.com/demo/three)
- [https://offscreen.pmnd.rs/](https://offscreen.pmnd.rs/)
- [https://blog.stackademic.com/optimizing-3d-model-rendering-in-next-js-by-reducing-blocking-time-using-react-fiber-offscreen-11bd39ca7a67](https://blog.stackademic.com/optimizing-3d-model-rendering-in-next-js-by-reducing-blocking-time-using-react-fiber-offscreen-11bd39ca7a67)