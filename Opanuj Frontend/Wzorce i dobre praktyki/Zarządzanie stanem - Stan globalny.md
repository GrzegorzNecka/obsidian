## Wprowadzenie

W tej lekcji przyjrzymy się koncepcji globalnego zarządzania stanem w aplikacjach frontendowych. Wyjaśnimy, jakie problemy rozwiązuje globalne zarządzanie stanem i omówimy architekturę Flux. Następnie, rozważymy jak zadecydować czy Twoja aplikacja potrzebuje biblioteki do globalnego zarządzania stanem (w zależności od frameworka). Na wypadek odpowiedzi twierdzącej, poznasz bibliotekę Redux-Toolkit, która stanowi nowoczesne i uproszczone podejście do zarządzania stanem globalnym. Na koniec przeanalizujemy alternatywne biblioteki do zarządzania stanem.

## Definicja i potrzeba globalnego zarządzania stanem

Zacznijmy od przypomnienia definicji przytoczonej w poprzedniej lekcji:

**Stan globalny**: Obejmuje dane, które są istotne dla wielu różnych części aplikacji i muszą być dostępne globalnie. Zarządzanie takim stanem czasami wymaga użycia specjalistycznych bibliotek takich jak Redux, NgRx czy Vuex. Przykłady:

- Status sesji użytkownika, to czy jest zalogowany i jakie ma uprawnienia dostępowe.
    
- Preferencje użytkownika, czyli ustawienia związane z motywem (ciemny/jasny).
    
- Kluczowe dane domenowe (np. lista zadań w Todo app), z których korzysta wiele funkcji aplikacji.
    
![[Pasted image 20240316220543.png]]
Aby podejmować świadome decyzje co do potrzeby i sposobu zarządzania stanem globalnym w 2024r., pozwól że przedstawię Ci rys historyczny.

Popularyzacja bibliotek do zarządzania stanem w ekosystemie frameworków frontendowych jest zjawiskiem, które można zrozumieć tylko w kontekście problemów, z jakimi zmagały się zespoły programistyczne dekadę temu.

Facebook, rozwijając swoje aplikacje, szczególnie te złożone jak Facebook Ads, napotykał na problem skomplikowanego przepływu danych i trudności w jego przewidywaniu. Narzędzia do zarządzania stanem, które były dostępne w tamtym czasie, nie oferowały wystarczającej przejrzystości i łatwości w debugowaniu. W rezultacie, utrzymanie jakości i wydajności kodu oraz szybkość wprowadzania nowych funkcji stawały się coraz większym wyzwaniem.

Redux, stworzony przez [Dana Abramova](https://twitter.com/dan_abramov2) i [Andrew Clarka](https://twitter.com/acdlite) w 2015 roku, został zaprezentowany na konferencji React Europe jako biblioteka do zarządzania stanem aplikacji. Kluczowe czynniki, które przyczyniły się do gwałtownej popularyzacji Reduxa, to:

1. problemy czasu dziecięcego Reacta, przede wszystkim braku wbudowanego API do udostępniania danych w dół drzewa komponentów. Context API zostało dodane do Reacta “dopiero” w 2018 roku, trzy lata po premierze Reduxa.
    
2. świetny dev-marketing ojców założycieli na Twitterze i konferencjach
    
3. wyzwania w budowaniu **wysoce dynamicznych i złożonych** interfejsów użytkownika (trzecia pozycja na liście nie jest tutaj przypadkowa, wrócimy do tego później).
    

Na fali popularyzacji Reduxa wyrosły analogiczne rozwiązania dla pozostałych frameworków: [NgRx](https://ngrx.io/) (Angular) oraz [Vuex](https://vuex.vuejs.org/) (Vue).

## Wprowadzenie do Architektury Flux

Skoro znamy już rys historyczny, możemy się zapoznać z kluczowymi zagadnieniami architektury Flux, w wariancie zaimplementowanym przez Redux. Jak to zwykle bywa z “frontendowymi wynalazkami”, i tym razem mamy do czynienia z podejsciem, które czerpie garściami z ugruntowanych metod i technik inżynierii oprogramowania, przede wszystkim: [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html), [CQRS](https://martinfowler.com/bliki/CQRS.html), oraz wzorca #Mediator [Mediator](https://sourcemaking.com/design_patterns/mediator).

Aby zrozumieć Flux, musimy zapoznać się z trzema kluczowymi koncepcjami: action, store oraz reducer.
![[Pasted image 20240316220606.png]]
### Action

Akcje to obiekty składające się z dwóch właściwości _type_ oraz _payload_:

```javascript
{
  type: 'ADD_PRODUCT_TO_CART',
  payload: { id: 2 }
}
```

Akcja służy nam do opisywania zdarzeń, które są istotne z punktu widzenia stanu naszej aplikacji. Pole _type_ pozwala zidentyfikować rodzaj zdarzenia, podczas gdy _payload_ to dane powiązane z tym zdarzeniem - w tym wypadku to id produktu, który powinien zostać dodany do koszyka.

Aby ułatwić sobie przesyłanie akcji z widoku oraz pisanie testowanie jednostkowych, korzystamy z **actions creators** czyli prostych funkcji zwracających akcje określonego typu:

```javascript
const addProductToCart = (productId) => ({
  type: 'ADD_PRODUCT_TO_CART',
  payload: { id: productId }
})
```

Dzięki temu kiedy chcemy przesłać (ang. dispatch) akcje _ADD_PRODUCT_TO_CART_ możemy to zrobić _w następujący sposób:_

```javascript
dispatch(addProductToCart(2);
```

### **Store**

Store jest sercem całej architektury Flux. Store jest niezmienialny (ang. immutable), co oznacza, że nie możemy bezpośrednio modyfikować przechowywanego w nim stanu. To podejście ma wiele zalet, w tym analizę zmian stanu, łatwość debugowania i możliwość implementacji funkcji takich jak "cofnij/zrób ponownie" (undo/redo).

Tworzenie store'u w Reduxie wymaga użycia funkcji **createStore** z paczki Redux. Do tej funkcji przekazujemy _reducer_ (lub kombinację reducerów, jeśli nasza aplikacja jest bardziej złożona), a także stan początkowy.

```tsx
import { createStore } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer);
```

Pierwotnie zachęcano, aby wynosić do Store cały stan aplikacji (lokalny, współdzielony i globalny) i uczynić z niego “single source of truth”. Niestety takie podejście sprawia, że nawet w prostych aplikacjach Store rozrasta się bardzo szybko, potrzebna jest duża ilość akcji oraz reducerów. Obecnie [dokumentacja Redux](https://redux.js.org/faq/organizing-state#do-i-have-to-put-all-my-state-into-redux-should-i-ever-use-reacts-usestate-or-usereducer) zostawia to do decyzji developerom, my rekomendujemy wykorzystywanie store’a jedynie do stanu globalnego.

**Reducer**

Reducer to czysta (_pure_) funkcja, która przyjmuje aktualny stan aplikacji i akcję jako argumenty, a następnie zwraca nowy stan. W Reduxie stan jest niezmienialny, co oznacza, że reducer musi zwrócić nowy obiekt stanu, jeśli stan ma zostać zmieniony. Kluczowe jest, aby każda funkcja reducer była #deterministyczna, co oznacza, że przy tych samych argumentach wejściowych zawsze zwróci ten sam wynik.

Struktura reducera jest następująca:

```tsx
function rootReducer(state = initialState, action) {
  switch (action.type) {
    case 'ADD_PRODUCT_TO_CART':
      // Logika dodawania produktu do koszyka
      return {
        ...state,
        cart: [...state.cart, state.products[action.payload]]
      };
    // inne case'y dla różnych akcji
    default:
      return state;
  }
}
```

Często stosuje się kilka mniejszych reducerów skoncentrowanych na określonej domenie (np. produkty, użytkownik, wysyłka), które zarządzają konkretnymi częściami stanu, a następnie łączy się je za pomocą funkcji **combineReducers** z Reduxa.  

Poznałeś już kluczowe założenia architektury Flux, teraz omówimy jej główne zalety.

### **Zalety Flux/Redux**

1. **Przewidywalność stanu**

Redux zapewnia jednokierunkowy przepływ danych, co czyni stan aplikacji bardziej przewidywalnym. Każda akcja jest opisana jako zwykły obiekt, a zmiany stanu są wykonywane przez czyste funkcje (reducery).  
  
**Przykład**: W aplikacji e-commerce, dodanie produktu do koszyka jest przewidywalną akcją, która zawsze prowadzi do takiego samego rezultatu w stanie aplikacji, niezależnie od kontekstu wykonania.

2. **Ułatwienie debugowania**

Dzięki jednokierunkowemu przepływowi danych i narzędziom takim jak [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd), debugowanie aplikacji staje się łatwiejsze. Możliwość przeglądania historii akcji, stanu przed i po akcjach oraz podróży w czasie (time travel debugging) przyspiesza identyfikację i rozwiązywanie problemów.  
  
**Przykład**: Możliwość cofnięcia stanu aplikacji do momentu przed wystąpieniem błędu ułatwia znalezienie przyczyny problemu w skomplikowanej logice biznesowej.

3. **Ułatwienie testowania**

Reducer w Reduxie to czyste funkcje, co ułatwia ich testowanie. Można łatwo przeprowadzać testy jednostkowe, przekazując określone stany początkowe i akcje, aby sprawdzić, czy wynik jest zgodny z oczekiwaniami.  
  
**Przykład**: Testowanie reducera odpowiedzialnego za kluczową logikę dodawania i usuwania produktów z koszyka może być wykonane jak dla zwykłej funkcji JS, bez potrzeby mockowania interfejsu użytkownika czy wykonywania testów e2e.

## Jak wszyscy “nabraliśmy się” na Reduxa?

W latach 2015-2017 doszło do niesamowitej popularyzacji Flux i Reduxa. Takie podejście do zarządzania stanem stało się domyślnym wyborem w niemal każdej aplikacji Reactowej.  
  
Obiegowa heurystyka była następująca: “Budujesz duży/złożony projekt? Skorzystaj z Reduxa!”.

Co oznacza duży/złożony projekt w tego typu heurystykach nie dowiedziałem się do dziś, a trochę już pracuję w tej branży. Ośmielę się stwierdzić, że to przede wszystkim skuteczna forma perswazji - w końcu każdy lubi myśleć o najbardziej wymagającej aplikacji, nad jaką pracował/pracuje/będzie pracować jako o dużej i/lub złożonej (ja też dałem się na to złapać).  
  
Upłynęło trochę wody w Wiśle, deadline’y w wielu projektach zostały przekroczone i co gorsza aplikacje nadal miały bugi, mimo że miało być jednokierunkowo, przewidywalnie i testowalnie.  
  
Tym oto sposobem w latach 2018-2019 skończyły się złote lata Reduxa - okazało się że biblioteka ma swoje wady i wielu projektach bardziej przeszkadza niż pomaga:

### **Wady Flux/Redux**

1. **Boilerplate i złożoność**

Redux wymaga pisania dużych ilości kodu boilerplate do obsługi akcji oraz reducerów. [Dokumentacja](https://redux.js.org/introduction/getting-started), mimo że świetnie napisana, przytłacza swoją objętością i ilością zasad, które musimy poznać oraz zapamiętać. Dla wielu aplikacji może to być nieproporcjonalnie dużo pracy w porównaniu z realnym zwrotem z zalet.

2. **Trudności z asynchronicznością**

Zarządzanie asynchronicznymi akcjami w Reduxie wymaga dodatkowych narzędzi jak [Redux Thunk](https://github.com/reduxjs/redux-thunk) czy [Redux Saga](https://redux-saga.js.org/), co dodatkowo podnosi złożoność aplikacji. Wspomniane biblioteki nie są szczególnie intuicyjne a obsługa asynchroniczności i efektów ubocznych jest w nich trudniejsza niż w czystym React.

3. **Nadmierna centralizacja**

W wielu projektach Redux przechowuje cały stan aplikacji w jednym globalnym obiekcie, co może prowadzić do przerośniętych struktur, ciężkich w analizie i zarządaniu. Dla niektórych typów stanu jest to na dodatek najzwyczajniej nieefektywne, np. dla stanu powiązanego jedynie z UI, który naturalnie lepiej zarządzać w lokalnym i współdzielonym stanie komponentów.  
  
**Przykład 1**: Stan formularza, który nie wpływa na resztę aplikacji, może być łatwiej zarządzany poza stanem globalnym.

**Przykład 2**: Stan widoczności modala z komunikatem o nowej wersji aplikacji, może być łatwiej zarządzany poza stanem globalnym.

4. **Skalowanie**

Mimo że Redux dobrze skaluje się w kontekście zarządzania stanem globalnym, to wraz z rozbudową aplikacji rośnie liczba potrzebnych akcji i reducerów, przez co zarządzanie nimi i utrzymanie czystości kodu staje się wyzwaniem.

---

Całkiem trafnie można podsumować powyższe wady za pomocą sformułowania “over-engineering”. Ale jak to się stało, że wszyscy “daliśmy się nabrać” - czyżby chodziło jedynie o skupienie się na zaletach, które nie były aż tak istotne dla wielu projektów i nieświadomości wad tej biblioteki zanim nauczyło nas doświadczenie? Nie do końca.

Większość aplikacji internetowych, to aplikacje typu #CRUD (tworzenie, odczyt, aktualizacja i usuwanie), które przede wszystkim synchronizują stan pomiędzy interfejsem użytkownika a backendem.

Wiąże się z tym szereg wyzwań: sposób pobierania, buforowania i synchronizacji danych ze stanem serwera, obsługa race conditions, unieważnianie nieaktualnych danych i ich ponowne pobieranie, usuwanie duplikatów zapytań, ponawianie nieudanych zapytań.

Czy Redux zauroczył społeczność Reacta, ponieważ pomaga poradzić sobie z synchronizacją stanu pomiędzy interfejsem użytkownika a backendem? Nie bardzo, co prawda Reduxa stosowano do tych celów, ale nie oferował on zbyt wiele pomocy i ułatwień - większość logiki trzeba było pisać samodzielnie.

Drugim problemem, z którym zmagają się CRUDy tworzone w React jest możliwość udostępniania danych w dół drzewa komponentów bez konieczności prop drillingu.

Czy Redux zauroczył społeczność Reacta, ponieważ zapewniał upragniony mechanizm dependency injection? Jak najbardziej, ta biblioteka bardzo dobrze radzi sobie z tym zagadnieniem i przed pojawieniem się Context API w 2018 roku nie miała “oficjalnej konkurencji”.

Trzecim problemem, z którym zmagały się aplikacje tworzone w React był brak jasnych praktyk oraz wzorców zarządzania stanem (i w wielu innych obszarach).

Czy Redux zauroczył społeczność Reacta, ponieważ oferował porządek, którego każdy potrzebował a mało kto bał się przyznać, bo w końcu elastyczność jest lepsza, niż “nudy znane z Angulara”? Śmiem twierdzić, że tak - aczkolwiek to moja czysto subiektywna opinia.

I tutaj dochodzimy do morału całej historii. W programowaniu (i życiu) często są dwa rodzaje powodów: **_dobre powody_** (jednokierunkowy przepływ danych, testowalność, debugowanie) oraz **_prawdziwe powod_y** (pierw brak API do dependency injection a potem obawy o wydajność Context API, oraz chaos w projektach przytłoczonych wolnością).

Zanim zapoznamy się z Redux Toolkit, które powstało na bazie lekcji wyciągniętych z Reduxa, spróbujmy odpowiedzieć na ważne pytanie:

### Czy mój projekt potrzebuje biblioteki do zarządzania stanem globalnym?

W React bezpieczna odpowiedź brzmi: **to zależy.** Od tego czy Twoja aplikacja faktycznie potrzebuje stanu globalnego, jeżeli tak to: jak często się on zmienia i co jest w niej renderowane.

Jak wspominaliśmy w lekcji , Context API pozwala nam udostępniać stan globalnie, ale musimy liczyć się z mechanizmem re-renderowania konsumentów, stąd z pełnym spokojem nadaje się do obsługi stanu globalnego o charakterze statycznym/rzadko ulegającym zmianom:

- **Ustawienia globalne** aplikacji, takie jak motyw, preferencje językowe czy preferencje dostępności.
    
- **Dane uwierzytelniające użytkownika**, takie jak status zalogowania i uprawnienia, które są potrzebne w różnych częściach aplikacji do zarządzania sesją i uprawnieniami dostępowymi użytkownika.
    
- **UI state**, który musi być dostępny globalnie, ale zmienia się rzadko, na przykład status połączenia internetowego, tryb ciemny/jasny.
    

  
Jednak jeżeli pracujemy nad małą lub średnią aplikacją lub nie potrzebujemy udostępniać danych globalnie, tylko w ramach jednej rozbudowanej funkcji (np. wieloetapowy formularz), to śmiało możemy zdecydować się na dedykowany kontekst połączony z hookami do zarządzania stanem (useState, useReducer). Nie przez przypadek zespół Reacta rekomenduje takie rozwiązanie w ramach [Context API Use Cases](https://react.dev/learn/passing-data-deeply-with-context#use-cases-for-context) oraz [Scaling Up with Reducer and Context](https://react.dev/learn/scaling-up-with-reducer-and-context) - zauważ, że nie ma tam żadnych ostrzeżeń dotyczących zagadnienia rerenderowania. Na dodatek nadchodząca wersja React 19, może przynieść znaczne usprawnienia w zakresie wydajności, o czym więcej [przeczytasz na oficjalnym blogu Reacta](https://react.dev/blog/2024/02/15/react-labs-what-we-have-been-working-on-february-2024).

Pamiętajmy, że wciąganie do projektu biblioteki do zarządzania stanem wnosi następujące trade-offy i ryzyka:

- Trade-off: Ścisłe powiązanie z kluczową zależnością, której **ciężko** pozbyć się w przyszłości
    
- Trade-off: Wyższy próg wejścia do projektu (zależne od biblioteki i kompetencji ludzi na rynku pracy)
    
- Trade-off: Wyższa złożoność projektu (zależne od biblioteki i zespołu)
    
- Ryzyko: Wydłużony czas realizacji projektu i koszta jego utrzymania (czy i jak bardzo, zależy od zespołu, projektu i biblioteki)
    

Jako świadomi developerzy nie dajmy się zastraszyć komentarzom o tym, że Context API pogrąży wydajność dowolnej aplikacji - w większości wypadków to jedynie łańcuszek powtarzany bez zrozumienia, tak samo jak powtarzano, że każda duża/złożona aplikacja powinna korzystać z Reduxa. Pamiętajmy, że programowanie to sztuka trade-offów. Często warto wybrać prostotę i brak dodatkowych zależności kosztem suboptymalnego re-renderowania komponentów. Dlaczego? W wielu widokach różnica pomiędzy optymalnym a subotymalnym rerenderowaniem nie będzie zauważalna dla użytkownika, czyli **nie ma będzie miała znaczenia**. React, podobnie jak konkurencja, naprawdę nieźle radzi sobie z aktualizowaniem DOM - to w końcu jego główne zadanie. Zresztą zobacz sam:

Kiedy biblioteka do zarządania stanem to dobry pomysł bez większych wątpliwości:

- stan globalny ulega bardzo częstym i/lub złożonym zmianom
    
- core naszego interfejsu jest kosztowny w renderowaniu, np. składa się z wykresów, setek/tysięcy elementów lub zawiera liczne animacje
    
- mamy wyśrubowane wymagania co do przewidywalności i testowania stanu, tj. pracujemy w domenie finansów, bezpieczeństwa, zdrowia.
    

Zauważ, że “projekt jest duży” nie znalazł się na tej liście, i nie jest to przypadek.  
  
Oczywiście decyzja o tym czy skorzystać z biblioteki do zarządzania stanem powinna być wypadkową nie tylko analizy wymagań, ale również preferencji zespołu/firmy. Wiele teamów, które podobnie jak ja “nabrały się na Reduxa”, przyzwyczaiło się do korzystania bibliotek, ba, po prostu lubi z nimi pracować, i to jest jak najbardziej okej. Wnoszą one porządek i ukierunkowują na pisanie kodu zgodnie z określonymi patternami. Cały ten wywód to apel, żebyśmy byli świadomi, że podejmujemy decyzje kierując się preferencjami (prawdziwy powód) zamiast szukać dobrych powodów - to może niepotrzebnie zaburzać nasz osąd i dyscyplinę intelektualną w przypadku przyszłych decyzji dotyczących architektury i stacku technologicznego projektu.

---

W przypadku Angulara i Vue sytuacja jest mniej skomplikowana. Frameworki te mają wbudowane API, które pozwalają nam komfortowo zarządzać stanem globalnym bez obaw o wydajność jak w przypadku Reacta (Angular: serwisy, Vue: Composition API). Dzięki temu możemy zrealizować naprawdę wiele projektów i funkcji bez korzystania z zewnętrznej biblioteki.

Osobiście proponujemy trzymać się wbudowanych API zwłaszcza w przypadku Angulara, ponieważ NgRx cierpi na większość tych samych problemów co Redux (i na dodatek ma jeszcze wyższy próg wejścia) - połączenie serwisów i RxJS jest naprawdę potężne, warto korzystać z tego duetu.

W przypadku Vue możemy zdecydować się na bibliotekę [Pinia](https://pinia.vuejs.org/), którą ze względu na swoją prostotę i silną integrację z Composition API można poznać w jeden wieczór. Jedyną istotną ceną jest tutaj ścisłe powiązanie z tą zależnością, resztę trade-offów możemy tutaj pominąć ze względu na niesamowitą intuicyjność i oficjalne wsparcie core team’u VueJS.  
  
Wracając do świata Reacta. Prędzej czy później będziemy musieli zmierzyć się z Reduxem i architekturą Flux, czy to ze względu na wymagania projektu, czy też preferencje zespołów co znajduje odzwierciedlenie w wielu ofertach pracy, stąd zapraszam na spotkanie z RTK.

## Wprowadzenie do Redux-Toolkit

Jak już wspominaliśmy, “czysty” Redux ma swoje problemy. Jego szczegółowość sprawia, że trudno się go nauczyć, a dodatkowy kod potrzebny do codziennej pracy w wielu projektach wprowadza nadmiarową złożoność i ociężałość.

Spośród dostępnych opcji w zakresie bibliotek do zarządzania stanem, obecnie najpopularniejszym graczem jest [Redux Toolkit](https://redux-toolkit.js.org/) (RTK), który cechuje uproszczone i opiniotwórcze podejście do pracy z Reduxem.

Redux Toolkit zapewnia kilka narzędzi i abstrakcji w celu usprawnienia naszej pracy:

- [createSlice](https://redux-toolkit.js.org/api/createSlice): Ta funkcja “magicznie” łączy akcje i reducery w jeden fragment stanu (slice). Automatycznie generuje action creatory i reducery, pozwala pisać “mutowalne” aktualizacje stanu - to wszystko znacznie zmniejsza ilość boilerplate’u.
    
- [configureStore](https://redux-toolkit.js.org/api/configureStore): Ta funkcja konfiguruje store Redux z rozsądnymi wartościami domyślnymi. Zawiera wbudowane middleware’y, takie jak [Redux Thunk](https://redux.js.org/usage/writing-logic-thunks) do obsługi logiki asynchronicznej, i automatycznie konfiguruje rozszerzenie [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd) do debugowania.
    
- [createAsyncThunk](https://redux-toolkit.js.org/api/createAsyncThunk): To narzędzie upraszcza obsługę operacji asynchronicznych w Redux, takich jak wywołania API. Generuje asynchroniczne action creatory, które wysyłają kilka akcji, aby odzwierciedlić różne etapy operacji asynchronicznej (np. ładowanie, sukces, niepowodzenie).
    

Wykorzystując Redux Toolkit, możemy pisać kod Redux w bardziej zwięzły i intuicyjny sposób, zmniejszając ogólną złożoność i boilerplate znane z klasycznego Reduxa. Zresztą zobacz sam:

Redux Toolkit to bardziej przyjazna i zwięzła biblioteka względem pierwowzoru, ale nadal ma istotny wpływ na podniesienie złożoności naszego projektu. Łatwo o tym zapomnieć, kiedy już dobrze ją poznamy, ale wystarczy spojrzeć na objętość [dokumentacji](https://redux-toolkit.js.org/) - jest ona podobna do samego Reacta. W połączeniu z licznymi odnośnikami do [dokumentacji “czystego” Reduxa](https://redux.js.org/), jest tutaj więcej do opanowania niż w samym Reactcie.

W 2024 warto zainwestować czas w naukę RTK, ponieważ jest to najczęściej wykorzystywana biblioteka do zarządzania stanem i spotkasz ją w wielu projektach legacy, co potwierdzają statystyki [npm trends](https://npmtrends.com/@reduxjs/toolkit-vs-jotai-vs-mobx-vs-recoil-vs-valtio-vs-xstate-vs-zustand).

Co istotne, RTK ma rosnącą i co raz silniejszą konkurencję ze strony [Zustand](https://github.com/pmndrs/zustand), biblioteki którą wyróżnia prostota i intuicyjność - jeżeli ten trend się utrzyma a Zustand przegoni RTK i “zostanie z nami na stałe”, to w 2025 możecie się spodziwać aktualizacji rekomendowanej biblioteki oraz samej sekcji “**Czy mój projekt potrzebuje biblioteki do zarządzania stanem globalnym?”**.

---

## Przegląd pozostałych bibliotek do zarządzania stanem

### **React**

1. [**Zustand**](https://github.com/pmndrs/zustand) to minimalistyczna biblioteka do zarządzania stanem, która charakteryzuje się prostotą i łatwością w użyciu. Nie wymaga użycia reducerów ani akcji (w przeciwieństwie do Reduxa), co czyni ją bardziej dostępną dla początkujących. Zustand wykorzystuje hooki do korzystania ze stanu globalnego, które mogą być łatwo wykorzystywane przez komponenty.
    
2. [**Jotai**](https://jotai.org/) **-** biblioteką do zarządzania stanem w React, która oferuje prosty i efektywny sposób na zarządzanie stanem z podejściem atom-based. Pozwala na tworzenie mniejszych, niezależnych jednostek stanu, tzw. atomów, które mogą być wykorzystywane i aktualizowane niezależnie w sposób przypominający sygnały. Istotna wada: stosunkowo niszowe rozwiązanie.
    

### Angular

1. [NgRx](https://ngrx.io/) - NgRx to kompleksowe rozwiązanie do zarządzania stanem dla Angulara, inspirowane przez Redux. Oferuje bogaty zestaw narzędzi do zarządzania stanem aplikacji, efektami ubocznymi, izolacją zależności. Redux + RxJS = sounds like “fun”.
    
2. [NgXs](https://www.npmjs.com/package/@ngxs/store) jest alternatywą dla NgRx, oferującą prostsze i bardziej deklaratywne podejście do zarządzania stanem w Angularze. Umożliwia łatwe zarządzanie stanem poprzez proste dekoratory i mniejszą ilość kodu boilerplate. Istotna wada: stosunkowo niszowe rozwiązanie.
    

### Vue

1. [Pinia](https://pinia.vuejs.org/) - “aktualna” oficjalna biblioteka do zarządzania stanem dla Vue.js Jest nowoczesną, lżejszą alternatywą dla Vuex, oferującą prostsze i bardziej elastyczne podejście do zarządzania stanem w aplikacjach Vue. Charakteryzuje się łatwą konfiguracją i małą ilością boilerplate.
    
2. [Vuex](https://www.npmjs.com/package/vuex) - “emerytowana” oficjalna biblioteka do zarządzania stanem dla Vue.js, zapewniającą scentralizowane przechowywanie dla wszystkich komponentów aplikacji. Wzoruje się na architekturze Flux/Redux, ale jest dostosowane do reaktywności Vue.
    

## **Najlepsze praktyki**

Context API, które pojawia się w powyższych fragmentach jako lekarstwo na zarządzanie stanem globalnym, może czasami prowadzić do nadmiernego odświeżania i renderowania komponentów. Jeśli chcemy sprawić, aby niektóre z komponentów były bardziej stabilne i nie ulegały odświeżeniu przy każdej zmianie kontekstu, na którym polegają, możemy zdecydować się na trzy propozycje od twórcy Reacta.

## Jak radzić sobie z re-renderami w Context API?

To istotna wiedza, więc pozwoliłem sobie przekleić [przetłumaczone rekomendacje Dana Abramova](https://github.com/facebook/react/issues/15156?fbclid=IwAR0mjKkp-m4p4gNrzOuz8zUf37vWeTuagCaF7CQrCMKZu7y45_cmoEYzTaI#issuecomment-474590693).

Kontekst przykładów z poszczególnych opcji: Załóżmy, że pracujesz nad komponentem kontenerowym, który obsługuje rozbudowany formularz wieloetapowy i musi się dostosować do motywu aplikacji, który użytkownik może zmienić w widoku ustawień.

### Opcja 1 (preferowana): Rozdziel konteksty, które nie zmieniają się razem

Jeśli w wielu komponentach potrzebujemy tylko małej części kontekstu, np. _appContextValue.theme_, ale reszta kontekstu zmienia się zbyt często, możemy oddzielić ThemeContext od AppContext.

```
function Button() {
  let theme = useContext(ThemeContext);
  // The rest of your rendering logic
  return <ExpensiveTree className={theme} />;
}
```

Teraz zmiana _AppContext_ nie spowoduje ponownego renderowania konsumentów _ThemeContext_.

Jest to preferowana poprawka. Wtedy nie potrzebujesz żadnego specjalnego ratunku.

## Opcja 2: Podziel swój komponent na dwie części, umieść _memo()_ pomiędzy nimi

Jeśli z jakiegoś powodu nie możesz rozdzielić kontekstów, nadal możesz zoptymalizować renderowanie, dzieląc komponent na dwie części i przekazując bardziej szczegółowe propsy do komponentu zagnieżdżonego, który otoczysz [React.memo()](https://react.dev/reference/react/memo). Nadal będziesz renderować komponent zewnętrzny, ale nie powinno to mieć negatywnego wpływu na wydajność (ten komponent nic nie robi).

```javascript
function Button() {
  let appContextValue = useContext(AppContext);
  let theme = appContextValue.theme; 
  return <ThemedButton theme={theme} />
}

const ThemedButton = memo(({ theme }) => {
  
  return <ExpensiveTree className={theme} />;
});
```

## Opcja 3: Jeden komponent z useMemo wewnątrz

Wreszcie, moglibyśmy uczynić nasz kod nieco bardziej rozwlekłym, ale zachować go w pojedynczym komponencie, wrappując wartość zwracaną w [useMemo](https://react.dev/reference/react/useMemo) i określając konsumowaną wartość kontekstu jako zależności. Nasz komponent zewnętrzny nadal będzie renderował się ponownie, ale React nie będzie renderował ponownie drzewa potomnego, jeśli dane wejściowe useMemo pozostaną takie same.

```javascript
function Button() {
  let appContextValue = useContext(AppContext);
  let theme = appContextValue.theme; 

  return useMemo(() => {
    
    return <ExpensiveTree className={theme} />;
  }, [theme])
}
```

### 👨‍💻 Ćwiczenia praktyczne

1. Redux Toolkit: Dokończ refaktoryzację z Context API na Redux Toolkit. Punkt startowy: **examples/module1/lesson3/shop-rtk-start**.
    
    1. Zainstaluj i zapoznaj się z [Redux DevTools](https://chromewebstore.google.com/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd).
        
    2. Zastąp CartContext uzupełniając cartSlice.
        
        1. Utwórz akcje i reducery dla funkcji: decreaseAmount, removeFromCart - tutaj przydatna będzie [dokumentacja RTK](https://redux-toolkit.js.org/usage/usage-guide), w szczególności [Writing Reducers with Immer](https://redux-toolkit.js.org/usage/immer-reducers).
            
        2. Utwórz selektor dla totalPrice.
            
        3. Podepnij interfejs pod akcje i selektory zamiast CartContext.
            
    3. Utwórz api service dla “Products” i zastąp nim ProductContext. Tutaj szczególnie przyda Ci się dokumentacja [RTK Query: Quick Start](https://redux-toolkit.js.org/tutorials/rtk-query/).
        
2. Context API: Zoptymalizuj nadmiarowe renderowanie wybranego komponentu. Punkt startowy: **examples/module1/lesson3/shop-context.**
    
    1. Wykorzystaj jedną z opcji wymienionych w najlepszych praktykach.
        
    2. Do analizy renderowania komponentów wykorzystaj [React DevTools](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) z włączoną opcją “General → Highlight updates when components render”.
        
3. Dla żądnych wrażeń: Wykonaj refaktoryzację projektu shop-context za pomocą [czystego Reduxa](https://github.com/reduxjs/redux), aby w pełni zrozumieć o czym pisaliśmy w tej lekcji oraz docenić korzyści płynące z RTK. Enjoy the ride! 🙈
    

## **👨‍💻 Materiały dodatkowe**

- [Getting Started with React DevTools in Chrome](https://www.debugbear.com/blog/react-devtools#visualizing-the-cause-of-a-components-render)
    
- [How to use Redux DevTools](https://www.youtube.com/watch?v=BYpuigD01Ew)
    
- [You Might Not Need Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)
    
- [Immutability in React and Redux: The Complete Guide](https://daveceddia.com/react-redux-immutability-guide/)