
# Projekt interop z nowościami:

https://web.dev/blog/interop-2023?hl=pl
https://web.dev/blog/interop-2025?hl=pl

# Dynamic viewport units:

`height: 45dvh`

1. [https://web.dev/blog/viewport-units](https://web.dev/blog/viewport-units)
![[Pasted image 20250219150315.png]]
![[Pasted image 20250219150410.png]]

![[Pasted image 20250219150421.png]]


# Container Queries and Container Units

### Components ==responsive== in relation ==to container== not whole window

- [https://github.com/GoogleChromeLabs/container-query-polyfill](https://github.com/GoogleChromeLabs/container-query-polyfill)
- [https://developer.mozilla.org/en-US/blog/getting-started-with-css-container-queries/#nested_containers](https://developer.mozilla.org/en-US/blog/getting-started-with-css-container-queries/#nested_containers)![[container-query.svg]]
### ==One component adjusting== to given role and position
[https://codepen.io/wuuuuuuuuut/pen/RwOxVQe](https://codepen.io/wuuuuuuuuut/pen/RwOxVQe)


### Podstawowy syntax:

```css
.container {
  container-type: inline-size;
  /* lub */
  container: name-container / inline-size;
}

@container (min-width: 400px) {
  .child {
    /* style */
  }
}
```

### Kluczowe właściwości:

- **container-type**:
	- **inline-size** - queries bazujące na szerokości kontenera
	- **size** - queries bazujące na szerokości i wysokości
	- **normal -** tylko dla style queries
- **container-name** - nadaje nazwę kontenerowi (opcjonalne)
- **container** - skrócony zapis dla container-type i container-name

### Główne zastosowania:

- Komponenty wielokrotnego użytku (karty, widgety)
- Layouty z dynamiczną szerokością (grid, flex)
- Responsywne komponenty niezależne od viewportu
- Adaptywne interfejsy w systemach design

### Use case 

```css
.card-container {
  container-type: inline-size;
}

.card {
  display: grid;
  grid-template-columns: 1fr;
}


@container (min-width: 400px) {
  .card {
    grid-template-columns: 200px 1fr;
  }
}
```

### Kluczowe zalety:

- Responsywność bazująca na kontenerze, nie viewport
- Lepsza reużywalność komponentów
- Bardziej przewidywalne zachowanie
- Możliwość tworzenia prawdziwie modularnych komponentów

**Container Queries** są wspierane przez wszystkie nowoczesne przeglądarki i stanowią nowy standard w tworzeniu responsywnych interfejsów na poziomie komponentów
# Container queries ~~might be~~ are an alternative to listening to element resize

[https://codepen.io/chriscoyier/pen/jOeBzNN](https://codepen.io/chriscoyier/pen/jOeBzNN)
