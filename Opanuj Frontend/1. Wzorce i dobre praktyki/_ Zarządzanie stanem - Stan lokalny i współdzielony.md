
## **Wprowadzenie do Zarządzania Stanem**

### **Czym jest stan w programowaniu?**

Stan w kontekście programowania to pojęcie odnoszące się do przechowywania informacji o bieżących warunkach lub sytuacji, w której znajduje się aplikacja lub jej część. **Jest to zbiór zmiennych, wartości, informacji, które aplikacja "pamięta" w trakcie swojego działania**.

Stan determinuje, w jaki sposób program reaguje na różne dane wejściowe lub zdarzenia w danym momencie.

### **Czym jest zarządzanie stanem?**

Zarządzanie stanem odnosi się do sposobu, w jaki przechowujemy stan i obsługujemy jego zmiany w naszym kodzie. Zmiany stanu w programie muszą być dokonywane w kontrolowany sposób, aby zapewnić spójność i poprawność działania programu. Na przykład, w aplikacji do zarządzania listą zadań, dodawanie, edycja czy usuwanie zadania to zmiana stanu listy zadań. Dobrze zaprojektowane zarządzanie stanem pozwala na łatwe śledzenie tych zmian, co ułatwia dalsze rozwijanie aplikacji, testowanie oraz debugowanie.

### **Przykłady stanu i jego zarządzania z prawdziwego życia**

Zanim przejdziemy do kontekstu programowania frontendowego, omówmy dwa przykłady stanu i jego zarządzania z prawdziwego życia.

**Przykład 1: Światła w Domu**

Wyobraźmy sobie system oświetlenia w domu. Każde światło może być w jednym z dwóch stanów: włączone lub wyłączone. Zarządzanie stanem światła odbywa się za pomocą przełącznika. Gdy naciskasz przełącznik, zmieniasz stan światła – z wyłączonego na włączone i odwrotnie.
![[Pasted image 20240313124250.png]]
Proste? Proste! Ale podobnie jak w programowaniu, możemy wpaść na różne usprawnienia tego jak postrzegamy stan świateł i jak nimi zarządzamy:

- **Automatyzacja**: Możesz zautomatyzować światła, aby zmieniały stan w zależności od innych warunków, np. czasu dnia czy wykrycia ruchu. Tutaj stan światła jest zarządzany przez system, który reaguje na zmienne warunki zewnętrzne.
    
- **Grupowanie**: Możesz też grupować światła, tak aby jednym przełącznikiem zarządzać stanem wielu świateł jednocześnie. W tym przypadku, zmiana stanu jednego elementu (przełącznika) wpływa na stan wielu elementów (świateł).
    
- **Zdalne sterowanie**: Rozważmy możliwość zdalnego sterowania światłami za pomocą aplikacji mobilnej. Twoje interakcje z aplikacją zmieniają stan świateł, nawet gdy jesteś poza domem.
    

**Przykład 2: Gra w szachy**

Stan gry w szachy jest definiowany przez położenie wszystkich pionków na planszy w danym momencie. Każdy ruch jednego z graczy zmienia ten stan.

Głębsza analiza stanu w szachach:

- **Możliwe ruchy**: Na podstawie aktualnego stanu planszy, gracz analizuje możliwe ruchy. Tutaj stan (pozycja pionków) determinuje przyszłe decyzje.
    
- **Strategia**: Gracze tworzą strategie oparte na obserwacji zmian stanu planszy. Każdy ruch przeciwnika wpływa na strategię drugiego gracza.
    
- **Historia gry**: W szachach ważna jest również historia zmian stanu – każdy poprzedni ruch ma wpływ na obecną sytuację na planszy. To jak w programowaniu, gdzie historia zmian stanu (np. logi) pomaga zrozumieć obecne zachowanie systemu.
    
- **Zakończenie gry**: Gra kończy się, gdy osiągnięty jest określony stan (szach-mat), co oznacza, że jeden z graczy nie ma już możliwych ruchów.
    

  
W obu przykładach zarządzanie stanem obejmuje monitorowanie, kontrolowanie i reagowanie na zmiany. W programowaniu, podobnie jak w tych przykładach, ważne jest, aby zarządzanie stanem było przewidywalne i kontrolowane, co zapewnia spójność i efektywność działania systemu.  

### Czym jest stan w kontekście aplikacji frontendowych?

Stan w kontekście interfejsu użytkownika (UI) aplikacji frontendowej to bieżący kontekst lub warunki, w których znajduje się interfejs. Obejmuje to wszystkie dane i ustawienia, które determinują, co jest wyświetlane na ekranie w danym momencie, jak aplikacja reaguje na interakcje użytkownika, oraz jak prezentuje się i zachowuje. Stan UI jest dynamiczny – zmienia się w odpowiedzi na działania użytkownika, komunikację z serwerem czy zmiany w środowisku przeglądarki.

![[Pasted image 20240313124324.png]]

**Co najczęściej wpływa na stan UI?**

1. **Interakcje użytkownika**: Każde kliknięcie, wpisanie tekstu, przewinięcie strony itp. może zmienić stan UI.
    
2. **Dane zewnętrzne**: Dane z API, odpowiedzi z serwera, aktualizacje w czasie rzeczywistym z WebSockets.
    
3. **Stan przeglądarki:** Takie jak silnik i wersja przeglądarki, wielkość okna, ustawienia prywatności i dostępności, blokowanie elementów popup, mogą mieć wpływ na to, co użytkownik jest w stanie zobaczyć i zrobić w UI.
    
4. **Cache i pamięć lokalna**: Przechowywane dane mogą wpływać na to, co użytkownik widzi po ponownym otwarciu aplikacji lub po odświeżeniu strony, na przykład zachowane sesje użytkownika, zapisane preferencje w LocalStorage.
    
5. **Stan aplikacji**: Takie jak stan zalogowania użytkownika oraz jego uprawnienia, preferencje co do motywu (ciemny/jasny).
    

### **Przykłady stanu i zarządania stanem w aplikacjach frontendowych**

**Przykład 1: Wieloetapowy formularz zakupowy**

Podstawowy scenariusz

- **Stan**: Dane wprowadzone na każdym etapie formularza (np. wybór produktów, dane adresowe, opcje dostawy, dane płatności).
    
- **Zarządzanie**: Użytkownik przechodzi przez kolejne etapy formularza, wprowadzając wymagane informacje. Stan jest aktualizowany na każdym etapie i przechowywany do końcowego przesłania zamówienia.
    

Najczęstsze wyzwania

1. **Walidacja danych na każdym etapie**: Każdy etap formularza może wymagać swojej walidacji, co zwiększa złożoność zarządzania stanem, gdyż należy śledzić poprawność danych na różnych etapach.
    
2. **Zachowanie stanu przy powrocie do poprzednich etapów**: Użytkownik może chcieć wrócić do poprzedniego etapu, aby zmienić wprowadzone informacje. Zarządzanie stanem musi umożliwiać przechowywanie i przywracanie danych z poprzednich etapów bez ich utraty.
    
3. **Integracja z systemami zewnętrznymi**: Na przykład, integracja z systemami płatności lub zewnętrznymi API do sprawdzania dostępności produktów. Zarządzanie stanem musi uwzględniać asynchroniczne operacje i potencjalne zmiany dostępności produktów w trakcie procesu zakupowego.
    
4. **Odzyskiwanie stanu po odświeżeniu strony**: W przypadku przypadkowego odświeżenia strony, pożądane jest zachowanie dotychczas wprowadzonych danych. Może to wymagać zapisywania stanu w lokalnej pamięci przeglądarki lub w sesji.
    

### **Przykład 2: Interaktywna mapa (np. Google Maps)**

Podstawowy Wariant

- **Stan**: Pozycja na mapie, poziom powiększenia, wybrane punkty.
    
- **Zarządzanie**: Użytkownik przesuwa mapę lub zmienia poziom powiększenia, co aktualizuje stan.

Najczęstsze wyzwania

1. **Asynchroniczne ładowanie danych**: Wyświetlanie różnych danych w zależności od poziomu powiększenia i regionu mapy wymaga asynchronicznego ładowania danych.
    
2. **Zachowanie stanu podczas nawigacji**: Utrzymanie stanu mapy podczas nawigacji do innych części aplikacji i powrót do tego samego stanu.
    
3. **Reakcja na zmiany lokalizacji użytkownika**: Mapa powinna dynamicznie reagować na zmiany lokalizacji użytkownika w czasie rzeczywistym (np. w aplikacji mobilnej).  
    

W każdym z tych przykładów, zarządzanie stanem może szybko stać się złożone ze względu na różnorodne czynniki i wymagania interakcji użytkownika oraz integracji z zewnętrznymi systemami. Stąd dobór odpowiednich strategii i narzędzi do zarządzania stanem jest kluczowy.

### Trzy rodzaje stanu na frontendzie

W kontekście frontendowym, stan można generalnie podzielić na trzy główne kategorie: stan lokalny (stan UI), stan współdzielony oraz stan globalny. Każdy z tych typów stanu ma swoje specyficzne zastosowania, wady i zalety oraz najlepsze praktyki zarządzania:

![[Pasted image 20240313124337.png]]

** #Stan_lokalny (Stan UI)**: Dotyczy danych związanych bezpośrednio z danym komponentem interfejsu użytkownika. Jest to stan wewnętrzny, który kontroluje zachowanie i wygląd pojedynczego komponentu. Przykłady:

- Wartość wprowadzana w polu formularza.
    
- Stan rozwinięcia/zwinięcia akordeonu w interfejsie użytkownika.
    
- Informacja o tym, czy dany element UI, np. modal, jest aktualnie widoczny.  
    

** #Stan_współdzielony**: Odnosi się do danych, które są wykorzystywane przez kilka komponentów współtworzących bardziej złożoną funkcję, np. koszyk zakupowy. Przykłady:

- Stan wyboru w komponencie nawigacyjnym, który wpływa na zawartość wyświetlaną w głównym widoku.
    
- Dane wprowadzone przez użytkownika na poszczególnych etapach formularza, które są wymagane na kolejnych etapach.
    
- Stan ładowania danych
    
  
** #Stan_globalny**: Obejmuje dane, które są istotne dla wielu różnych części aplikacji i muszą być dostępne globalnie. Zarządzanie takim stanem często wymaga użycia specjalistycznych bibliotek takich jak Redux, NGRX czy Vuex. Przykłady:

- Status sesji użytkownika, to czy jest zalogowany i jakie ma uprawnienia dostępowe.
    
- Preferencje użytkownika, czyli ustawienia związane z motywem (ciemny/jasny).
    
- Kluczowe dane domenowe (np. lista zadań w Todo app), z których korzysta wiele funkcji aplikacji

Każdy z tych typów stanu pełni specyficzną rolę w aplikacjach frontendowych, pomagając w organizacji logiki aplikacji i zapewnianiu spójnego, reaktywnego doświadczenia użytkownika.

W tej lekcji skupimy się na zagadnieniach związanych ze stanem lokalnym oraz współdzielonym. Stan globalny omówimy w kolejnej lekcji.

### Frameworki UI a zarządzanie stanem

Manipulowanie Document Object Model (DOM) w sposób bezpośredni, zwłaszcza w nowoczesnych, interaktywnych aplikacjach internetowych, jest kosztowne pod względem wydajności. Każda zmiana w DOM, nawet tak prosta jak aktualizacja tekstu czy zmiana stylów, może spowodować konieczność ponownego renderowania i obliczania układu strony ( #reflow i #repaint), co jest procesem zasobożernym. W tradycyjnym podejściu, programista musiał ręcznie zarządzać tymi aktualizacjami, co jest nie tylko niewydajne, ale również podatne na błędy i trudne w utrzymaniu.

**Frameworki jako Abstrakcja nad DOM**

Frameworki frontendowe takie jak React, Vue i Angular, oferują warstwę abstrakcji nad bezpośrednią manipulacją #DOM. Pozwalają one na skupienie się na logice biznesowej i zarządzaniu stanem aplikacji, podczas gdy szczegóły dotyczące renderowania i aktualizacji DOM są obsługiwane przez framework.

![[Pasted image 20240313124350.png]]

Kluczowe zalety frameworków w kontekście zarządzania stanem:

1. **Efektywne zarządzanie aktualizacjami DOM**: Frameworki używają technik takich jak wirtualny DOM (React, Vue) lub mechanizmy detekcji zmian (Angular), które minimalizują ilość interakcji z prawdziwym DOM. To optymalizuje wydajność przez ograniczenie kosztownych operacji reflow i repaint.
    
2. **Deklaratywne UI**: Frameworki pozwalają na #deklaratywne opisywanie interfejsów użytkownika, co oznacza, że programiści określają „co” ma być wyświetlone, a nie „jak” to zrobić. Logika aktualizacji UI jest automatycznie zarządzana przez framework, co upraszcza proces tworzenia interfejsu.
    
3. **Reaktywność i wiązanie danych**: Zapewniają one reaktywne wiązanie danych, co oznacza, że interfejs użytkownika automatycznie aktualizuje się w odpowiedzi na zmiany w stanie aplikacji. To sprawia, że zarządzanie dynamicznym stanem staje się bardziej intuicyjne i mniej podatne na błędy.
    
4. **Skalowalność i utrzymanie**: Użycie tych frameworków upraszcza skalowanie aplikacji i jej utrzymanie. Dzięki wyraźnemu oddzieleniu logiki aplikacji od manipulacji UI, kod staje się bardziej modularny, czytelny i łatwiejszy w testowaniu.
    
5. **Społeczność i ekosystem**: Frameworki te mają rozbudowane ekosystemy i społeczności, oferując gotowe rozwiązania, biblioteki i narzędzia, które jeszcze bardziej ułatwiają zarządzanie stanem i interakcje z UI.
    

Podsumowując, frameworki frontendowe takie jak React, Vue i Angular, znacząco ułatwiają i optymalizują proces zarządzania stanem i interakcji z DOM w aplikacjach internetowych. Pozwalają one frontendowcom skupić się na budowaniu interaktywnych interfejsów użytkownika, delegując większość ciężaru pracy związanego z manipulacją DOM i aktualizacjami UI do frameworka.

## Zarządzanie stanem lokalnym

W ramach przypomnienia: stan lokalny służy do przechowywania i zarządzania danymi, które są istotne dla pojedynczego komponentu aplikacji. Umożliwia to komponentom reagowanie na interakcje użytkownika, aktualizacje danych oraz inne zmiany w aplikacji poprzez dynamiczne aktualizacje interfejsu użytkownika. Zarządzanie stanem lokalnym obejmuje zwykle dane formularzy, stan UI komponentu (np. czy dialog jest otwarty czy zamknięty), dane tymczasowe, które nie są częścią globalnego stanu aplikacji.

Zróbmy sobie teraz szybki przegląd podobieństw i różnic pomiędzy frameworkami na znanym i lubianym przykładzie komponentu _Counter_.

**React**

W Reactcie stan lokalny jest zarządzany za pomocą hooka [_useState_](https://react.dev/reference/react/useState) w komponentach funkcyjnych lub _this.state_ w komponentach klasowych. Dzięki jawnemu wywołaniu #setter zwróconego przez _useState_, React wie że doszło do aktualizacji stanu i samodzielnie dba o aktualizację DOM.

**Przykład z _useState_**:

```tsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Current count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**Angular**

W Angularze zarządzanie stanem lokalnym jest realizowane poprzez właściwość klasy komponentu. Angular automatycznie śledzi zależności między stanem aplikacji a DOM, zapewniając aktualizacje.

**Przykład z właściwością klasy**:

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-counter',
  template: `
    <div>
      <p>Current count: {{ count }}</p>
      <button (click)="increment()">Increment</button>
    </div>
  `
})
export class Counter {
  count = 0;

  increment() {
    this.count++;
  }
}
```

**Vue**

W Vue stan lokalny jest zarządzany przez reaktywne właściwości danych komponentu. Vue automatycznie śledzi zależności między stanem aplikacji a DOM, zapewniając aktualizacje.

**Przykład z Vue 3 Composition API**:

```html
<template>
  <div>
    <p>Current count: {{ count }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const count = ref(0);
    const increment = () => {
      count.value++;
    };

    return { count, increment };
  }
}
</script>
```

**  
Podobieństwa i różnice**

- **Podobieństwa**: Wszystkie trzy frameworki oferują proste mechanizmy do deklaratywnego zarządzania stanem lokalnym.

- **Różnice**: Główna różnica polega na sposobie, w jaki frameworki reagują na zmiany stanu i podchodzą do aktualizacji DOM. Wejdziemy w temat głębiej w sekcji poświęconej relacji pomiędzy zarządzaniem stanem a wydajnością. Tymczasem, wbrew obiegowej opinii, lecz zgodnie ze zdrowym rozsądkiem, uznamy to za nieistotne z punktu widzenia wzorców zarządzania stanem.

### Kiedy stan lokalny to za mało?

Rozumiemy już podstawy zarządzania stanem lokalnym, czas wykorzystać tę wiedzę w praktyce. Założmy, że Product Manager zleca nam budowę widoku, który pozwoli na wyszukiwanie i wyświetlanie postaci z serialu Rick and Morty na podstawie jej imienia oraz płci.

## Komponenty kontenerowe i prezentacyjne

Skorzystamy z prostego, lecz kluczowego wzorca jakim jest podzielenie komponentu _CharacterSearch na komponent kontenerowy i komponenty prezentacyjne._

Podział na komponenty kontenerowe i prezentacyjne to frontendowy wzorzec projektowy, który pomaga organizować kod i oddzielać logikę aplikacji od jej warstwy prezentacji.

**Komponenty kontenerowe** zajmują się logiką, taką jak pobieranie danych z API i obsługa stanu, podczas gdy **komponenty prezentacyjne** skupiają się na wyświetlaniu UI w oparciu o dane wejściowe ([_props_](https://react.dev/learn/passing-props-to-a-component)).

Do komponentu kontenerowego _CharacterSearchContainer_ wydzielimy nasze operacje związane z zarządzaniem stanem: pobieranie danych oraz sortowanie:

```ts
import { useState, useEffect } from 'react';

function CharacterSearchContainer() {
  const [name, setName] = useState('');
  const [gender, setGender] = useState('');
  const [characters, setCharacters] = useState([]);
  const [sortOption, setSortOption] = useState('');

  useEffect(() => {
    if (name || gender) {
      fetch(`https://rickandmortyapi.com/api/character/?name=${name}&gender=${gender}`)
        .then((response) => response.json())
        .then((data) => setCharacters(data.results || []))
        .catch((error) => console.error('Error fetching data:', error));
    }
  }, [name, gender]);

  const sortedCharacters = [...characters].sort((a, b) => {
    if (sortOption === 'name') {
      return a.name.localeCompare(b.name);
    } else if (sortOption === 'created') {
      return new Date(a.created) - new Date(b.created);
    }
    return 0;
  });

  // Nie wiemy jakich komponentów prezentacyjnych potrzebujemy :c
  return <div />
}
```

Aby prawidłowo wydzielić komponenty prezentacyjne, musimy spojrzeć na nasz UI i zadecydować jakich komponentów potrzebujemy:
![[Pasted image 20240313130345.png]]
Na dobry początek powinno wystarczyć, podzielimy więc naszą warstę prezentacyjną na trzy komponenty:

- SearchTitle
    

```javascript
function SearchTitle() {
  return <h1 className="pt-24 text-xl">Wyszukiwarka postaci Rick and Morty</h1>;
}
```

- SearchForm
    

```javascript
function SearchForm({ name, setName, gender, setGender, sortOption, setSortOption }) {
  return (
    <form className="space-x-4">
      <input
        type="text"
        placeholder="Insert name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <select value={gender} onChange={(e) => setGender(e.target.value)}>
        <option value="">Any Gender</option>
        <option value="female">Female</option>
        <option value="male">Male</option>
        <option value="genderless">Genderless</option>
        <option value="unknown">Unknown</option>
      </select>
      <select
        value={sortOption}
        onChange={(e) => setSortOption(e.target.value)}
      >
        <option value="" disabled>Sort by</option>
        <option value="name">Name</option>
        <option value="created">Created Date</option>
      </select>
    </form>
  );
}
```

Zauważ, że _SearchForm_ oczekuje od rodzica propsów _setName_, _setGender_ oraz _setSortOption_. Z punktu widzenia tego komponentu to funkcje przekazane jako wartość, które komponent wywołuje po wystąpieniu eventu [change](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event) w powiązanych polach formularza (nazwa, płeć i sortowanie). _SearchForm_ nie interesuje jak działa logika sortowania, deleguje tę odpowiedzialność do rodzica-kontenera _CharacterSearchContainer._

- CharacterList
    

```javascript
function CharacterList({ characters }) {
  return (
    <ol className="grid grid-cols-1 gap-4 list-none md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
      {characters.map((character) => (
        <li key={character.id} className="flex flex-col items-center">
          <h3>{character.name}</h3>
          <img src={character.image} alt={character.name} />
        </li>
      ))}
    </ol>
  );
}
```

Kod po zrealizowaniu podziału na komponenty kontenerowe i prezentacyjne znajdziesz w **examples/module1/lesson2/container-components**  

**💪 Ćwiczenie praktyczne z dalszej refaktoryzacji:**

1. Wydziel logikę wyszukiwania postaci do zewnętrznego modułu - zadecyduj czy potrzebujesz customowego hooka/serwisu czy zwykłej funkcji
    
2. Wydziel logikę sortowania postaci do zewnętrznego modułu - zadecyduj czy potrzebujesz customowego hooka/serwisu czy zwykłej funkcji
    
3. Zezwól na wyświetlanie dowolnej nazwy wyszukiwarki, np. _“Wyszukiwarka postaci Pokemon”_
    
4. Podziel komponent _CharacterList_ na _komponent listy oraz karty postaci_
    
5. Podziel komponent _SearchForm_ na komponenty dedykowane poszczególnym polom formularza
    

Moje rozwiązanie:

##   #Prop_drilling

Naszym punktem wyjścia jest **examples/module1/lesson2/prop-drilling-start** czyli wyszukiwarka po wykonaniu refaktoryzacji z ćwiczenia powyżej, dzięki czemu kod jest znacznie lepiej zorganizowany oraz czytelny.

Kod po zmianach z pozbyciem się prop drillingu znajdziesz w **examples/module1/lesson2/prop-drilling-finish.**  
  
**Pozbywanie się prop-drillingu dzięki Context API (React), serwisom (Angular) lub provide/inject (Vue)**

Każdy z frameworków oferuje nam wbudowany sposób na udostępnianie danych w dół drzewa komponentów bez konieczności prop-drillingu. Jednak warto mieć na uwadze jak działają te mechanizmy, aby uniknąć problemów z wydajnością aplikacji i reaktywnością danych.

### **Context API (React)**

[Context API](https://react.dev/learn/passing-data-deeply-with-context) w React to mechanizm, który umożliwia przekazywanie danych w dół drzewa komponentów, bez konieczności manualnego przekazywania propsów przez każdy poziom hierarchii.

Można to porównać do systemu poczty pneumatycznej, który bezpośrednio przesyła informacje z punktu A do punktu B, niezależnie od tego, ile pięter dzieli te dwa punkty w budynku.
![[Pasted image 20240313130404.png]]
Źródło ilustacji: [react.dev](https://react.dev/learn/passing-data-deeply-with-context)  

W skrócie, Context API składa się z trzech głównych elementów:

1. **React.createContext** - Tworzy obiekt Context. Kiedy React renderuje komponent, który subskrybuje ten Context, odczytuje on wartość kontekstu od najbliższego pasującego **Provider** powyżej w drzewie.
    
2. **Provider** - Komponent **Provider** "dostarcza" wartość kontekstu do komponentów potomnych, które tego potrzebują. Możesz mieć wielu Providerów w aplikacji i każdy z nich może przekazywać różne wartości.
    
3. **Consumer** - Komponenty, które potrzebują danych z kontekstu, mogą subskrybować kontekst i otrzymywać w ten sposób dane.
    

Korzystając z tej wiedzy moglibyśmy przebudować naszą aplikację, aby wykorzystywała context do zarządzania stanem i udostępniania go w dół drzewa komponentów:

```javascript
import { sortCharacters } from '../utils/sortCharacters';

interface CharacterContextValues {
  characters: Character[];
  name: string;
  setName: React.Dispatch<React.SetStateAction<string>>;
  gender: string;
  setGender: React.Dispatch<React.SetStateAction<string>>;
  sortOption: string;
  setSortOption: React.Dispatch<React.SetStateAction<string>>;
}

const defaultValues: CharacterContextValues = {
  characters: [],
  name: '',
  setName: () => {},
  gender: '',
  setGender: () => {},
  sortOption: '',
  setSortOption: () => {},
};

const CharacterContext = createContext<CharacterContextValues>(defaultValues);

export const CharacterProvider = ({
  children,
}: {
  children: React.ReactNode;
}) => {
  const [name, setName] = useState('');
  const [gender, setGender] = useState('');
  const [sortOption, setSortOption] = useState('');
  const characters = useCharacterSearch(name, gender);

  const value = {
    name,
    setName,
    gender,
    setGender,
    sortOption,
    setSortOption,
    characters: sortCharacters(characters, sortOption),
  };

  return (
    <CharacterContext.Provider value={value}>
      {children}
    </CharacterContext.Provider>
  );
};

export const useCharacterContext = () => useContext(CharacterContext);
```

Następnie podmienilibyśmy nasz komponent kontenerowy na _CharacterProvider_ i voila, każdy z komponentów dzieci mógłby uzyskać dostęp do stanu za pomocą customowego hooka _useCharacterContext_.

Jednak **zastosowanie kontekstu dla tego typu danych niesie za sobą konsekwencje związane z wydajnością aplikacji.**

### **C**o musisz wiedzieć zanim zastosujesz Context API?

**Zmiana wartości kontekstu => Re-renderowanie konsumentów**

Kiedy wartość stanu przechowywanego w **Context.Provider** zmienia się, wszystkie komponenty konsumujące ten kontekst są ponownie renderowane. W dużych drzewach komponentów, gdzie wielu komponentów konsumuje dane z kontekstu, może to prowadzić do znacznej liczby niepotrzebnych re-renderowań.

**Zbyt duży zakres kontekstu**

Z uwagi na mechanizm re-renderowanie komponentów przy zmianach w kontekście, używanie jednego kontekstu na samym szczycie drzewa komponentów, tak aby udostępnić zróżnicowane dane dla całej aplikacji, nie jest dobrą decyzją. W takim przypadku, nawet niewielka zmiana jednej części danych w kontekście może prowadzić do re-renderowania wszystkich komponentów konsumujących ten kontekst, niezależnie od tego, czy te konkretne dane są dla nich istotne.

###   
**Najlepsze praktyki stosowania Context API**

Aby uniknąć problemów z wydajnością, ważne jest, aby stosować się do kilku najlepszych praktyk przy używaniu React Context API:

**Rozdrobnienie kontekstów**

Zamiast tworzyć jeden, globalny kontekst dla całej aplikacji, lepiej jest tworzyć mniejsze, bardziej skoncentrowane konteksty dla różnych części danych. Pozwala to na bardziej precyzyjne kontrolowanie re-renderowania komponentów w oparciu o rzeczywiste zmiany stanu, które ich dotyczą.

**Rodzaje danych dla Context API**

Context API najlepiej nadaje się do przekazywania danych, które nie zmieniają się często, ale muszą być dostępne w wielu miejscach aplikacji. Oto kilka przykładów:

- **Ustawienia globalne** aplikacji, takie jak motyw, preferencje językowe czy preferencje dostępności.
    
- **Dane uwierzytelniające użytkownika**, takie jak status zalogowania i uprawnienia, które są potrzebne w różnych częściach aplikacji do zarządzania sesją i uprawnieniami dostępowymi użytkownika.
    
- **UI state**, który musi być dostępny globalnie, ale zmienia się rzadko, na przykład status połączenia internetowego, tryb ciemny/jasny.  
      
    

Wracając do naszej aplikacji, która jest prosta i nie posiada wielu poziomów zagnieżdżenia co uzasadniałoby wprowadzanie kontekstu. Dane formularza, które siłą rzeczy zmieniają się często, nie są rekomendowanym typem danych dla Context API. Czy z tego powodu mamy związane ręce i musimy chwytać za bibliotekę do zarządzania stanem? Bynajmniej! Więcej na ten temat w kolejnej lekcji.

Jak to wygląda w pozostałych frameworkach? Nie da się ukryć, że korzystniej 🙈

### Provide / inject we Vue 3

Vue oferuje podobny mechanizm do Context API o nazwie [Provide / Inject](https://vuejs.org/guide/components/provide-inject). Jednak API Vue jest prostsze, nie powoduje problemów związanych z wydajnością i daje większą kontrolę nad reaktywnością.

Jak sama nazwa wskazuje, provide / inject składa się z dwóch elementów:

1. **Provide:** Komponent "dostarczający" może udostępniać dane lub metody, wykorzystując opcję **provide**. Te dane stają się dostępne dla dowolnego komponentu potomnego, który zdecyduje się ich użyć. Dzięki metodom _ref()_ i _reactive()_ sprawiamy, że komponenty potomne wykorzystujące kontekst automatycznie zareagują na zmianę stanu _-_ bez tych metod będzie on statyczny_._
    

```javascript
// RandomParentComponent
<script>
import { provide } from 'vue';

export default {
  setup() {
    const theme = ref('material');
    const darkMode = ref(false);
    provide('theme', theme);
    provide('darkMode', darkMode);
  }
}
</script>
```

2. **Inject:** Komponenty potomne mogą "wstrzyknąć" te dane do swojego zakresu, korzystając z opcji **inject**, co pozwala im na dostęp do dostarczonych danych bez potrzeby przekazywania propsów przez każdy poziom drzewa komponentów.
    

```javascript
// RandomChildComponent
<script>
import { inject } from 'vue';

export default {
  setup() {
    const darkMode = inject('darkMode');
    return { darkMode };
  }
}
</script>
```

Co ważne zmiana _theme,_ którym nie jest zainteresowany _RandomChildComponent,_ nie spowoduje jego rerendera, jakby to się stało domyślnie przy zastosowaniu React Context API (bez zastosowania React.memo w _RandomChildComponent_).

Z tego powodu _provide / inject_ stanowią istotną alternatywę dla bibliotek do zarządzania stanem, które omówimy w kolejnej lekcji.

### **Serwisy w Angularze**

Serwis (ang. Service) w Angularze to klasa z dekoratorem **@Injectable**, która zapewnia sposób na dzielenie się danymi i logiką biznesową między różnymi częściami aplikacji. Angular wykorzystuje wstrzykiwanie zależności (Dependency Injection, DI), aby umożliwić łatwe i efektywne udostępnianie serwisów w różnych komponentach i modułach aplikacji. Serwisy mogą być używane do wielu celów, takich jak wykonywanie zapytań HTTP, zarządzanie stanem aplikacji, autentykacja użytkownika itd. Można powiedzieć, że łączą w sobie możliwości customowych hooków oraz Context API.

```javascript
// character-search.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { BehaviorSubject, Observable } from 'rxjs';
import { map } from 'rxjs/operators';
import { Character } from '../models/character.model'; 

@Injectable({
  providedIn: 'root'
})
export class CharacterSearchService {
  private nameSubject = new BehaviorSubject<string>('');
  private genderSubject = new BehaviorSubject<string>('');
  private sortOptionSubject = new BehaviorSubject<string>('');

  private apiBaseUrl = 'https://rickandmortyapi.com/api/character/';

  constructor(private http: HttpClient) {}

  setName(name: string) {
    this.nameSubject.next(name);
  }

  setGender(gender: string) {
    this.genderSubject.next(gender);
  }

  setSortOption(sortOption: string) {
    this.sortOptionSubject.next(sortOption);
  }

  getCharacters(): Observable<Character[]> {
    return this.http.get<{ results: Character[] }>(`${this.apiBaseUrl}?name=${this.nameSubject.value}&gender=${this.genderSubject.value}`)
      .pipe(
        map(response => response.results || [])
      );
  }
}
```

Następnie taki serwis możemy wstrzyknąć w dowolny komponent, który jest zainteresowany stanem i metodami obsługiwanymi przez ten serwis.

Podobnie jak Provide / Inject z Vue 3, serwisy z Angulara są wolne od wyzwań, które wymieniliśmy omawiając Context API i stanowią istotną alternatywę dla bibliotek do zarządzania stanem, które omówimy w kolejnej lekcji.

## Signals, czyli “nowe” podejście do zarządzania stanem lokalnym i współdzielonym

W ostatnich latach za sprawą frameworka [Solid.js](https://www.solidjs.com/) rosnącą popularność zyskują Sygnały (ang. Signals), czyli kolejne podejście do reaktywnego zarządzania stanem lokalnym i wspódzielonym.

Przyjrzyjmy prostemu przykładowi z zastosowaniem Angulara:

```javascript
// Inicjalizacja sygnału
const count = signal(0);

// Sygnały są getterami - wywołanie powoduje odczytanie ich wartości.
console.log('The count is: ' + count());

// Wartość sygnału możemy zaktualizować za pomocą metody set()
count.set(1);

// Lub za pomocą metody update, która udostępnia nam domknięcie na aktualnej wartości
count.update(value => value + 1);

// Inicjalizacja sygnału zależnego, automatycznie aktualizowanego przy zmianie wartości count
const doubleCount = computed(() => count() * 2);
```

Co raz więcej programistów jest przekonanych, że to właśnie TEN sposób za kilka lat stanie się standardem pośród frameworków frontendowych. Nie są to przypuszczenia bezzasadne, ponieważ w krótkim czasie oficjalnej implementacji sygnałów doczekały się: [Angular](https://angular.io/guide/signals), [Vue](https://vuejs.org/guide/extras/reactivity-in-depth.html#connection-to-signals), [Svelte](https://svelte.dev/blog/runes#signal-boost), [Qwik](https://qwik.dev/docs/components/state/#usesignal) i [Preact](https://preactjs.com/guide/v10/signals).

Ale o co chodzi i skąd te wszystkie zachwyty? Już tłumaczę!

Znaczna część bólu związanego z zarządzaniem stanem w JavaScript polega na reagowaniu na zmiany dla danej wartości, ponieważ wartości nie są bezpośrednio obserwowalne. Frameworki zazwyczaj obchodzą to poprzez przechowywanie wartości w zmiennej i ciągłe sprawdzanie, czy uległa one zmianie, co jest uciążliwe i suboptymalne pod kątem wydajności.

Najlepiej byłoby, gdybyśmy mieli sposób na wyrażenie wartości, który samodzielnie poinformuje nas o jej zmianie. To właśnie robią Sygnały.
![[Pasted image 20240313130416.png]]
Sygnał to wrapper wartości, który automatycznie powiadamia zainteresowanych konsumentów o zmianie tej wartości. Sygnały mogą zawierać dowolne wartości, od prostych prymitywów (string, number) po złożone struktury danych (obiekty). Wartość sygnału jest zawsze odczytywana za pomocą [gettera](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get), co pozwala frameworkom śledzić, czy i gdzie sygnał jest używany.

Implementacje Signals różnią się pomiędzy frameworkami, ale łączy je:

- **Domyślne lenistwo** - tylko sygnały, które faktycznie są używane przez jakikolwiek komponent są obserwowane i aktualizowane.
    
- **Optymalne aktualizacje** - jeśli wartość sygnału nie uległa zmianie, komponenty i efekty, które używają tej wartości, nie zostaną zaktualizowane, nawet jeśli zależności sygnału uległy zmianie.
    
- **Optymalne śledzenie zależności** - framework sam śledzi komponenty zależne od danego sygnału, w przeciwieństwie do architektury React Hooks, która opiera się na jawnych tablicach zależności.
    
- **Bezpośredni dostęp** - dostęp do wartości sygnału w komponencie automatycznie subskrybuje aktualizacje bez potrzeby stosowania selektorów lub hooków.
    

Dzięki temu Sygnały wyróżniają się niespotykaną wydajnością, prostotą użycia i świetną skalowalnością - można je stosować w małych i dużych aplikacjach bez doktoryzowania się z API konkretnego frameworka.

Co ciekawe tak naprawdę nie jest to żadna nowość, ponieważ takie podejście do reaktywności sięga lat 60’tych, a w świecie JavaScript z takiego rozwiązania korzystał zapomniany już Knockout.js (2010) - więcej o ewolucji sygnałów w JavaScript dowiesz się z tego [artykułu](https://dev.to/this-is-learning/the-evolution-of-signals-in-javascript-8ob).

### React, do you even signal?

Wielkim nieobecnym jeżeli chodzi o wsparcie dla Sygnałów jest React. Co prawda mamy do dyspozycji [@preact/signals-react](https://www.npmjs.com/package/@preact/signals-react), ale względu na brak przystosowania frameworka do obsługi sygnałów biblioteka ma swoje problemy (wymienione w readme) i nie cieszy się dużą popularnością. Dan Abramov, jeden z frontmanów Reacta, [wprost odradza korzystania z tej biblioteki](https://github.com/facebook/react/issues/26704#issuecomment-1522044060).

Nie ma żadnych oficjalnych zapowiedzi wsparcia sygnałów w React. [Wypowiedzi członków core team’u](https://twitter.com/acdlite/status/1628811935088013314?lang=en) wskazują na ich sceptyczne podejście do tego rozwiązania. Ich zdaniem sygnały kłócą się z “filozofią Reacta”, skoncentrowanej na tworzeniu frameworka, które nie wymaga od nas myślenia o wydajności - kto wie, obyśmy w przyszłości doczekali się takiej wersji Reacta 😉

### Angular jest za trudny? Sygnały na ratunek!

Anyways, zobaczmy jak sygnały potrafią uprościć kod w Angularze, pozwalając nam zrezygnować z części kodu opartego o RxJS, który w dużej części odpowiada za wysoki próg wejścia do tego frameworka.  
  
Punktem wyjścia dla tego przykładu jest kod **examples/module1/lesson2/signals-angular-start**

Sygnały to obiecująca “nowość”. To czy staną się nowym standardem w reaktywnym zarządzeniu stanem, będzie w dużej mierze zależne od popularności największych konkurentów Reacta czyli Angulara, Vue oraz Svelte. Czas pokaże!  

## 👨‍💻 Ćwiczenia praktyczne

1. **Zbuduj własną wyszukiwarkę z** [**REST Countries API**](https://restcountries.com/#endpoints-all) - wykorzystaj wiedzę zdobytą w tej lekcji do budowy wyszukiwarki w dowolnym frameworku. REST Countries pozwala na wiele możliwości filtrowania państw: waluta, język, stolica, nazwa państwa.
    
    1. Minimalne wymagania:
        
        1. Aplikacja pozwala na filtrowanie po wybranej właściwości: waluta, język, stolica lub nazwa państwa ← wybierz jedną, API nie pozwala filtrować po kilku właściwościach na raz :c.
            
        2. Aplikacja wyświetla: nazwę państwa oraz flagę.
            
        3. Aplikacja pozwalać na sortowanie: alfabetyczne, po wielkości populacji.
            
    2. Dla żądnych wrażeń: Tryb zgadywania na podstawie flagi!
        
        1. Minimalne wymagania:
            
            1. Aplikacja pozwala przełączać się pomiędzy “Tryb wyszukiwania” a “Tryb zgadywania” za pomocą radio inputa.
                
            2. Po aktywacji trybu zgadywania, aplikacja ukrywa formularz wyszukiwarki.
                
            3. Po aktywacji trybu zgadywania, aplikacja wybiera pseudolosowo jeden z wyników zapytania do [endpointa /all](https://restcountries.com/v3.1/all).
                
            4. Aplikacja ukrywa nazwę wylosowanego państwa, pokazuje jedynie jego flagę.
                
            5. Aplikacja wyświetla formularz z inputem tekstowym do zgadywania nazwy oraz dwoma przyciskami: “Sprawdź” i “Wylosuj ponownie”.
                
            6. Po kliknięciu “Sprawdź” aplikacja weryfikuje czy użytkownik podał poprawnę nazwę państwa i wyświetla adekwatny komunikat - sukces lub błąd.
                
            7. Po kliknięciu “Wylosuj ponownie” pseudolosowo wybiera inną flagę do zgadywania.
                
2. **Signal all the things** - skorzystaj z kodu **examples/module1/lesson2/signals-angular-finish** i dokonaj refaktoryzacji pozostałych subjectów (nameSubject, genderSubject, sortOptionSubject) obsługujacych formularz na sygnały.
    

## **📚 Materiały Dodatkowe**

1. [Sekcja “Observables & RxJS” w dokumentacji Angulara](https://angular.io/guide/observables)
    
2. [The Evolution of Signals in JavaScript](https://dev.to/this-is-learning/the-evolution-of-signals-in-javascript-8ob)
    
3. [Lifting State Up](https://reactjs.org/docs/lifting-state-up.html)
