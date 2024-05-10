
## **Wprowadzenie**

Poprzednie dwie lekcje pokazały ci, jak szerokim zagadnieniem jest zarządzanie stanem aplikacji. Opanowałeś stan lokalny i globalny, więc zabierasz się do jego inicjalizacji. Tylko skąd go pobrać?

Nowoczesne narzędzia takie jak [Vite](https://vitejs.dev/) czy [Parcel](https://parceljs.org/) umożliwiają ci importy plików, możesz wykorzystać Web Storage API (Local Storage i Session Storage), a nawet pobierać stan z poziomu parametrów URL czy informacji w cookies.

Przede wszystkim możesz jednak zdecydować się na utrzymywanie i aktualizowanie stanu aplikacji po stronie serwera. To właśnie tam najczęściej przechowywane jest źródło prawdy o wszystkim, co dzieje się w ramach aplikacji. Serwer to absolutnie fundamentalna składowa aplikacji webowych, które działając w modelu _“client-server”_ rozdzielają pomiędzy dwie warstwy poszczególne odpowiedzialności.

Serwer to w dużym uproszczeniu niezależnie działający komputer, z którym próbujemy się komunikować przez wystawiony publicznie interfejs (API). Aby robić to skutecznie, w tej lekcji:

- Poznasz terminologię i najważniejsze koncepty komunikacji z API na backendzie
    
- Poznasz popularne narzędzia służące do pobierania i aktualizowania danych
    
- Poznasz dobre praktyki w budowaniu wielowarstwowej aplikacji dostępnej 24/7
    

Zaczynajmy!

## API, ale jakie?

Sam akronim API (Application Programming Interface) nie mówi wprost, z jakiego rodzaju interfejsem pracujemy. Zazwyczaj dotyczy jednak pewnej “bramki” przez którą uzyskujemy dostęp do zestawu określonych zasobów. Czasami tym terminem określa się zbiór publicznie dostępnych funkcji w bibliotece lub frameworku, czasami mówimy o publicznej części jednego z wielu modułów tej samej aplikacji, a czasami o REST / GraphQL API.

Dla uproszczenia ustalmy, że w tej lekcji wymiennie będziemy się posługiwać takimi terminami jak serwer, API lub backend.

W każdym z tych przypadków mamy na myśli pewnego rodzaju **zasób zdalny, działający poza granicami przeglądarki, z którym interakcja odbywa się asynchronicznie**, w modelu klient-serwer. Na początku skupimy się na #model_pull, w którym frontend pobiera na żądanie dane z backendu, ale na końcu omówimy także #model_push w którym to serwer decyduje o momencie publikacji informacji do klientów ( #WebSockets).

## API w aplikacjach webowych

Najbardziej popularne podejścia do budowania webowych API oparte są o REST oraz GraphQL.

### REST API

To styl architektury, który promuje udostępnianie zasobów wykorzystując metody HTTP, takie jak GET, POST, PUT czy DELETE. Metody te stosuje się do następujących operacji:

- **GET** - pobieranie listy zasobów lub jednego zasobu o określonym identyfikatorze, bez modyfikowania jego stanu
    
- **HEAD** - sprawdzenie nagłówków, jakie zostałyby nadane stosując metodę GET (może służyć do wstępnej analizy rozmiaru i dostępności pobieranego zasobu)
    
- **POST** - dodawanie nowego zasobu
    
- **PUT** - aktualizowanie zasobu o określonym identyfikatorze
    
- **DELETE** - usuwanie zasobu o określonym identyfikatorze
    
- **OPTIONS** - sprawdzenie dostępnych metod HTTP dla klienta (w przypadku zapytań #CROSS-ORIGIN[cross-origin](https://auth0.com/blog/cors-tutorial-a-guide-to-cross-origin-resource-sharing/))
    

Każde żądanie HTTP w architekturze REST jest bezstanowe, co oznacza, że serwer nie przechowuje żadnych informacji o stanie klienta (aplikacji webowej, aplikacji mobilnej, etc.). Zasoby mogą być reprezentowane w różnych formatach, takich jak JSON (na dzisiaj to najbardziej popularny format udostępniania danych), XML czy HTML. Klient i serwer negocjują format reprezentacji za pomocą nagłówków HTTP.

Pracując na frontendzie z klasycznym REST API, nasze zapytania mogą wyglądać w ten sposób:

```
GET /users           # pobranie listy użytkowników
GET /users/:id       # pobranie użytkownika o konkretnym id
POST /users          # utworzenie nowego użytkownika
PUT /users/:id       # zaktualizowanie danych użytkownika o konkretnym id
DELETE /users/:id    # usunięcie użytkownika o konkretnym id
```

W praktyce zdarza się, że od tak “książkowo” zaprojektowanego API zdarzają się odstępstwa. Szczególnie w warstwie Backend-For-Frontend (o której w dalszych lekcjach) znajdziemy bardziej złożone API udostępniające wiele zasobów jednocześnie, albo wystawiające dane pod konkretny fragment interfejsu aplikacji.

Więcej na ten temat przeczytasz we wpisie - [Data API vs Application API](https://max.engineer/server-informed-ui)

Pytaniem, które w kontekście REST API często pojawia się na rozmowach kwalifikacyjnych, jest to o różnicę pomiędzy zapytaniami POST i PUT (GET i DELETE są łatwe w odszyfrowaniu). Odpowiedzią za komplet punktów jest #idempotentność.

PUT jest idempotentny, co oznacza, że wielokrotne wysyłanie tego samego żądania jest bezpieczne i powtarzane (np. typowy scenariusz - aktualizacja danych). POST nie jest idempotentny - wysyłając taki sam zestaw parametrów kilka razy, możemy się spodziewać skutków ubocznych (np. błędów pt. “użytkownik z tym adresem email już istnieje”). Przyjęło się, że PUT stosujemy właśnie w przypadku bezpiecznej aktualizacji istniejących zasobów, a POST w przypadku ich tworzenia.

### Publiczne API

W sieci znajdziesz mnóstwo publicznych API, na których możesz ćwiczyć kolejne aspekty budowania aplikacji webowych, korzystających z zewnętrznych zasobów.

Popularna lista znajduje się pod tym adresem - [https://github.com/public-apis/public-apis](https://github.com/public-apis/public-apis)

### Fragmenty zapytania HTTP

W kontekście zapytań HTTP, określenie samej metody zapytania nie wystarczy. Jeśli chcemy przekazywać dane pomiędzy klientem i serwerem, powinniśmy rozumieć czym różnią się **body** i **query string**, a także kiedy potrzebne nam będą **nagłówki (headers)**.

- **Body** (ciało) żądania HTTP to część wiadomości, która zawiera dane wysyłane do serwera. Jest używane głównie w metodach POST, PUT, PATCH, gdzie dane są częścią treści żądania. Może zawierać różne rodzaje danych, takie jak dane formularza, JSON, XML, pliki binarne itp. Jest używane do przesyłania większej ilości danych, które są często wymagane w operacjach takich jak tworzenie lub aktualizacja zasobu (np. tworzenie nowego użytkownika z danymi użytkownika w formacie JSON).
    
- **Query string** to część URL, która zawiera parametry zapytania, które mogą być używane do przekazania dodatkowych informacji do serwera. Rozpoczyna się od znaku zapytania **?** i zawiera pary klucz-wartość oddzielone znakiem **&**. Składa się z prostych par klucz-wartość, gdzie klucz i wartość są ciągami znaków. Jest powszechnie używany w żądaniach GET, aby przekazać krótkie dane do serwera, takie jak parametry wyszukiwania, filtrów, numerowania stron czy kampanii reklamowych.
    

- **Headers**, czyli nagłówki, to dodatkowy sposób na przekazywanie metadanych pomiędzy klientem i serwerem. Nagłówki pomagają określić sposób przetwarzania żądania lub odpowiedzi. Spośród tych najczęściej wykorzystywanych warto znać **Content-Type** (typ przekazywanych danych), **Authorization** (metadane uwierzytelniania zapytania) oraz **Accept** (oczekiwany typ odpowiedzi).
    

### Obietnica lepszego REST API - GraphQL

To technologia opublikowana przez Facebooka w 2015r., która w założeniu miała rozwiązywać problem rozproszonych REST API w dużej skali. Dzięki [GraphQL](https://graphql.org/) autorzy aplikacji client-side (najczęściej aplikacji webowych i mobilnych) nie muszą wykonywać izolowanych zapytań po poszczególne zasoby, a następnie łączyć je pole po polu, ale mogą wysłać jedno zapytanie do rozwiązania przez serwer GraphQL.

Zapytania do API opartego o GraphQL najczęściej wykorzystują dwie metody HTTP - POST i GET, jednak ich zasoby nie są udostępniane przez wiele różnych endpointów, a jeden główny. Co decyduje o kształcie zwracanych danych? Samo zapytanie, którego **body** (lub rzadziej - query string) określa pola których potrzebujemy, lub planujemy modyfikować:

```txt
query UserWithComments {
  user {
    name
    comments {
      body
    }
  }
}
```

Powyższe zapytanie zostaje rozwiązane w oparciu o zasoby **User** i **Comments**, a w odpowiedzi uzyskujemy:

```javascript
{
  "data": {
    "user": {
      "name": "John Doe",
      "comments": [
        {
          "body": "Great job!"
        },
        {
          "body": "Amazing!"
        },
        {
          "body": "I love it!"
        }
      ]
    }
  }
}
```

Główną zaletą GraphQL jest łączenie wielu zapytań do API w jedno, co może być istotną kwestią w przypadku klientów o mniejszych zasobach sprzętowych, oraz zaletą dla programistów frontend, którzy oczekują większej elastyczności w pracy. Istotną wadą, która powoduje że na GraphQL nie decyduje się większość małych i średnich firm, jest narzut związany z utrzymaniem dodatkowej infrastruktury. Wdrażając GraphQL, w stosie technologicznym danego rozwiązania musimy dodać kolejną warstwę, która połączy zapytania od klientów z rozproszonymi, niezależnymi API.

Jeśli chcesz sprawdzić jak pracuje się z tego typu interfejsem, możesz wykorzystać jedno z publicznie dostępnych API, np.:

- Countries API - [https://github.com/trevorblades/countries](https://github.com/trevorblades/countries)
    
- Anime List API - [https://anilist.gitbook.io/anilist-apiv2-docs/](https://anilist.gitbook.io/anilist-apiv2-docs/)
    
- GitHub GraphQL API - [https://docs.github.com/en/graphql](https://docs.github.com/en/graphql)
    

W tym miejscu znajdziesz zestaw starannie redagowanych zasobów na temat GraphQL - [Awesome GraphQL](https://github.com/chentsulin/awesome-graphql).

## Jak wykorzystać statusy odpowiedzi HTTP

Na początku pracy z aplikacjami webowymi może się wydawać, że te niepozorne cyferki pojawiające się obok odpowiedzi z serwera są bardziej ciekawostką, niż narzędziem.

Wystarczy przecież, że nauczymy się czterech prostych reguł:

- 2xx - zapytanie kończy się sukcesem
    
- 3xx - zapytanie kończy się przekierowaniem
    
- 4xx - błąd po stronie klienta
    
- 5xx - błąd po stronie serwera
    

Okazuje się jednak, że w dużej skali, obsługując tysiące zapytań dziennie, musimy na kody błędów zwracać zdecydowanie większą uwagę. W sytuacjach, kiedy włączamy w naszej aplikacji monitoring i chcemy być powiadamiani o nagłym wzroście konkretnego typu błędu (**przedstawimy to w lekcjach modułu trzeciego**), do śledzenia kodów odpowiedzi musimy podejść zdecydowanie bardziej szczegółowo.

Zaprezentujemy to na przykładzie kilku awarii, w których braliśmy udział:

### **🚨 Incydent nr. 1 - Aktualizacja walidacji na serwerze (400 Bad Request)**

**Scenariusz**: Zespół backendowy aktualizuje serwis do walidacji jednego z formularzy na stronie. Zespół frontendowy nie jest świadomy tej zmiany, a monitoring wyłapuje wzrost błędów z kodem 400.

**Rozwiązanie**: Programiści odkrywają, że bez aktualizacji frontendu wielu użytkowników nie wpisuje danych do pola, które od teraz jest wymagane na backendzie. Backend zostaje przywrócony do poprzedniej wersji, aktualizowany jest formularz na frontendzie, a po pewnym czasie nowe reguły wracają na serwer. W tej kolejności wszystko zaczyna działać.

### **🚨 Incydent nr. 2 - Nowa metoda autoryzacji (401 Unauthorized)**

**Scenariusz**: Zespół wprowadza nowy system autoryzacji oparty na tokenach JWT. Po wdrożeniu, monitoring aplikacji zaczyna rejestrować nagły wzrost błędów 401.

**Rozwiązanie**: Programiści szybko identyfikują, że nowy system autoryzacji wymaga odświeżenia tokenów w inny sposób niż poprzedni. Wprowadzają niezbędne zmiany w kodzie klienta, aby poprawnie obsługiwać nowy mechanizm odświeżania tokenów.

### **🚨 Incydent nr. 3 - Usunięcie niepotrzebnej strony (404 Not Found)**

**Scenariusz**: W ramach porządkowania projektu zespół usuwa starą sekcję serwisu, która prawdopodobnie nie jest już używana. Wkrótce po tym, monitoring zgłasza wzrost błędów 404 generowanych przez użytkowników, którzy próbują na tę stronę wejść.

**Rozwiązanie**: Po analizie logów, okazuje się, że inne części serwisu nadal zawierają odnośniki do usuniętej strony. Zespół aktualizuje te linki, aby kierowały na istniejące zasoby, oraz dodaje przekierowania 301 dla starych URLi, aby uniknąć negatywnego wpływu na SEO.

### **🚨 Incydent nr. 4 - Błędy w trakcie wdrożenia (500)**

**Scenariusz**: Bezpośrednio po wdrożeniu nowej wersji aplikacji, system monitorujący zaczyna rejestrować wzrost błędów 500.

**Rozwiązanie**: Zespół przeprowadza analizę logów odkrywając problem z niekompatybilnością nowego kodu z istniejącą bazą danych. Problem rozwiązano poprzez szybką naprawę kodu i ponowne wdrożenie.

### Kontrola nad kodami błędów

Jako uczestnik kursu i frontend developer, możesz nie mieć bezpośredniej kontroli nad kodami błędów generowanymi przez backend, ale twoja rola jest kluczowa w podnoszeniu ich znaczenia.

Współpracując z zespołem backendowym, możesz podkreślać, jak ważne jest dostarczanie szczegółowych i precyzyjnych kodów, które pomagają w debugowaniu, poprawiają doświadczenie użytkownika i ułatwiają obsługę błędów po stronie klienta. W przypadkach, gdy pełnisz rolę full-stack developera, masz bezpośredni wpływ na to, jakie kody błędów są zwracane. Możesz wtedy projektować API w taki sposób, aby zapewnić, że kody błędów są zarówno adekwatne do kontekstu, jak i pomocne w procesie rozwoju aplikacji oraz jej utrzymania.

Twój wpływ na ten aspekt działania kodu server-side może znacząco przyczynić się do zwiększenia jakości i niezawodności aplikacji webowych.

## Komunikacja z API na poziomie aplikacji

### Fetch API

Niezależnie od stosowanego frameworka, najbardziej standardowym podejściem do wykonywania zapytań HTTP w aplikacjach frontendowych jest obecnie Fetch API. To zamiennik dla starszego API XMLHttpRequest (XHR). Metoda `fetch`, czyli główny składnik Fetch API, opiera się o Promise, co znacznie ułatwia obsługę asynchronicznych zapytań a także obsługę rezultatów danego zapytania.

Oto prosty przykład pokazujący, jak używać Fetch API do wykonania żądania GET (bez pełnej obsługi błędów, o czym poniżej):

```javascript
fetch('/api/users.json')
  .then(response => response.json()) // Parsowanie odpowiedzi jako JSON
  .then(data => console.log(data)) // Przetwarzanie otrzymanych danych
  .catch(error => console.error('Fetching error:', error));
```

Wykonanie żądania POST z konkretnymi parametrami wymaga dodatkowego obiektu konfiguracyjnego:

```javascript
// Konfiguracja żądania
const requestOptions = {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(data) // konwersja danych na format JSON
};

// Wykonanie żądania POST
fetch('/api/users.json', requestOptions)
  .then(response => response.json()) // Parsowanie odpowiedzi jako JSON
  .then(data => console.log(data)) // Przetwarzanie otrzymanych danych
  .catch(error => console.error('Fetching error:', error));
```

Fetch API możemy też z powodzeniem łączyć z async/await:

```javascript
async function fetchData(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Fetching error:', error);
  }
}

fetchData('/api/users.json');
```

Strona [CanIUse](https://caniuse.com/fetch) podaje, że to natywne rozwiązanie możemy już stosować w niemal wszystkich nowoczesnych przeglądarkach internetowych:

### Fetch API - Obsługa błędów

W przeciwieństwie do innych popularnych bibliotek HTTP, takich jak omawiany poniżej Axios, Fetch API **nie odrzuca** automatycznie tych zapytań, które kończą się serwerowymi kodami z zakresu 4xx i 5xx. Oznacza to, że odpowiedzi pokroju “Not Found” i “Server Error” są traktowane jako zakończone sukcesem, co może być mylące i prowadzić do problemów.

Koniecznie zapamiętaj, że otrzymanie kodu innego niż 2xx nie jest jednoznaczne z odrzuceniem Promise’a przez Fetch API:

```javascript
fetch('/api/users.json')
  .then(response => {
    return response.json(); // Jeśli otrzymasz kod 4xx lub 5xx, ten fragment i tak się wykona
  })
  .then(data => {
    console.log('Data:', data);
  })
  .catch(error => { // Klasyczny "catch" nie wystarczy do pełnej obsługi błędów
    console.error('Błąd:', error); 
  });
```

Oto przykład, który ilustruje, jak Fetch API radzi sobie z odpowiedziami 4xx i 5xx, oraz jak możesz prawidłowo obsłużyć te przypadki:

```javascript
fetch('/api/users.json')
  .then(response => {
    if (!response.ok) { // Promise rozwiązany z sukcesem, ale pole "ok" jest ustawione na false
      // Jeśli status odpowiedzi nie jest w zakresie 2xx, wyrzuć błąd
      throw new Error(`HTTP Error: ${response.status}`);
    }
    return response.json();
  })
  .then(data => {
    console.log('Data:', data);
  })
  .catch(error => {
    console.error('Błąd:', error);
  });
```

Fetch API to ogromny krok naprzód w porównaniu do zapytań realizowanych przez obiekt XMLHttpRequest, ale być może oczekujesz jeszcze większego komfortu pracy z API. W takim przypadku jedną z najbardziej popularnych opcji jest biblioteka **axios**.

### Axios

[Axios](https://axios-http.com/) jest popularną biblioteką JavaScript do wykonywania zapytań HTTP, używaną zarówno w aplikacjach przeglądarkowych, jak i Node.js. Jest to alternatywa dla natywnej metody **fetch**.

Jej główne zalety to:

- automatyczne przekształcanie danych na format JSON
    
    - w Fetch API musimy to zrobić sami
        
- #interceptory, czyli opakowywanie zapytań i odpowiedzi z serwera
    
    - w Fetch API wymaga to ręcznej implementacji
        
- intuicyjna obsługa błędów (w oparciu o kody niż inne 2xx)
    
    - w Fetch API kody takie jak 4xx i 5xx są uznawane za sukces (otrzymanie odpowiedzi)
        
- rozbudowane wsparcie dla anulowania i limitów czasowych zapytań
    
    - przez dodatkowy parametr (timeout na poziomie oczekiwania na odpowiedź)
        
    - z wykorzystaniem AbortController (timeout na poziomie nawiązywania połączenia)
        
- wsparcie dla starszych przeglądarek
    

Wykonanie podstawowego zapytania GET w bibliotece **axios** wygląda dość podobnie do Fetch API:

```javascript
import axios from 'axios';

axios.get('/api/users.json')
  .then(response => {
    console.log(response.data); // dane są już sparsowane jako JSON
  })
  .catch(error => {
    console.error('Error fetching data:', error);
  });
```

Natomiast w przypadku POST nie musimy ręcznie konwertować obiektu na JSON:

```javascript
import axios from 'axios';

axios.post('/api/users', {
  firstName: 'Fred',
  lastName: 'Flintstone'
})
.then(function (response) {
  console.log(response);
})
.catch(function (error) {
  console.log(error);
});
```

Więcej różnic zauważymy budując obsługę błędów i wsparcie dla przekroczenia czasu oczekiwania na odpowiedź.

### Axios vs Fetch API - Brak odpowiedzi z serwera

Pracując z aplikacjami webowymi na produkcji, musimy się przygotować na nieprzewidziane sytuacje na styku frontendu i backendu. Jedną z takich sytuacji jest przekroczenie czasu odpowiedzi z serwera. Może to być spowodowane wysokim obciążeniem serwera, wykonaniem nieoptymalnego zapytania do bazy, czy niedostępności innego serwisu, z którym nasz backend jest powiązany.

Aby zapewnić optymalne doświadczenia dla użytkownika, nasz frontend powinien mieć zdefiniowany maksymalny czas oczekiwania na odpowiedź i poprawnie obsługiwać taką sytuację.

Porównajmy oba rozwiązania. Najpierw Fetch API i Promise.race:

```javascript
// Rozbudowanie Fetch API o obsługę maksymalnego czasu oczekiwania
const fetchWithTimeout = (url, timeout) => {
  return Promise.race([
    fetch(url),
    new Promise((_, reject) =>
      setTimeout(() => reject(new Error('Timeout')), timeout)
    )
  ]);
};

fetchWithTimeout('/api/users.json', 5000) // timeout 5 sekund
  .then(response => /* obsługa odpowiedzi */)
  .catch(error => /* obsługa błędu lub timeoutu */);
```

W powyższym przykładzie Promise.race oczekuje na pierwszy Promise, który zostanie rozwiązany. Jeśli uzyskamy odpowiedź na zapytanie HTTP poniżej czasu w parametrze _timeout_, to zostanie ona zwrócona. Jeśli nie, to otrzymamy odrzucony Promise z wiadomością ‘Timeout’.

W axios wygląda to zdecydowanie mniej skomplikowanie, a logika timeoutu ukryta jest w bibliotece:

```javascript
import axios from 'axios';

// Natywne wsparcie dla parametru timeout w axios
axios.get('/api/users.json', { timeout: 5000 }) // timeout 5 sekund
  .then(response => /* obsługa odpowiedzi */)
  .catch(error => {
    if (error.code === 'ECONNABORTED') {
      console.log('Timeout');
    } else {
      /* obsługa innych błędów */
    }
  });
```

Biblioteka wspiera również globalną konfigurację, której możemy używać na przekroju całej aplikacji:

```javascript
import axios from 'axios';

export const myProductApi = axios.create({
  baseURL: 'https://myproduct.com',
  timeout: 5000
});

const users = await myProductApi.get('/users') // timeout: 5s
const items = await myProductApi.get('/items') // timeout: 5s
```

### Axios - Anulowanie żądania przez klienta

Poza przekroczeniem czasu na odpowiedź, drugim ze scenariuszy związanych z obsługą błędów jest przekroczenie czasu nawiązywania połączenia z serwerem, lub anulowanie zapytania na skutek konkretnej akcji użytkownika.

Przykładowo, kiedy budujemy dużą aplikację do wyszukiwania danych, użytkownik może zmieniać zakres filtrów zanim jeszcze otrzyma odpowiedź na poprzednie zapytanie. Bez anulowania zapytań interfejs użytkownika może się zmieniać zbyt wiele razy.

📝 Ten przykład znajdziesz w folderze **_examples/module1/lesson4/abort-controller_**.

Aby lepiej zarządzać równoległymi i już trwającymi zapytaniami, możemy wykorzystać wbudowany w przeglądarkę #AbortController (którego wsparcie przewiduje również Fetch API).

```javascript
import axios from 'axios';

const controller = new AbortController(); // AbortController to obiekt wbudowany w przeglądarkę

axios.get('/api/users.json', {
   signal: controller.signal
}).then((response) => {
   //...
}).catch((error) => {
  if (!axios.isCancel(error)) {
    // Obsługa błędu innego niż ręczne anulowanie zapytania
  }
})

controller.abort() // Wywołanie funkcji abort spowoduje anulowanie zapytania
```

To od ciebie zależy kto i kiedy będzie mógł wywołać funkcje “abort”. Może to być głęboki fragment aplikacji, albo rozbudowanie jednej z funkcji wywoływanej przez użytkownika.

Na końcu lekcji znajdziesz ćwiczenie, w którym przetestujesz posługiwanie się AbortControllerem.

### Axios - #interceptory  (Wzorzec Dekorator)

Korzystając z axiosa warto zainteresować się wykorzystaniem tzw. Interceptorów, czyli klasycznego przypadku użycia wzorca projektowego **Dekorator**.

Czym jest Dekorator? #Dekorator to wzorzec, który przydaje się kiedy udostępniamy konsumentowi konkretny, zamknięty zestaw funkcjonalności (np. zestaw funkcji do zapytań HTTP), ale chcemy również umożliwić jej rozszerzanie, np. dodanie logowania do każdego zapytania. Osiągniemy to właśnie dzięki wzorcowi Dekorator, który na konkretnym przykładzie w bibliotece axios wygląda w ten sposób:

```javascript
import axios from 'axios';

const requestLogger = (config) => {
  console.log(
    `Zapytanie ${config.method} pod ${config.url} zarejestrowano o ${new Date().toISOString()}`
  );
  return config;
}

axios.interceptors.request.use(requestLogger);

const { data: { users }} = await axios.get('/api/users.json')
const { data: { items }} = await axios.get('/api/items.json')
```

Dzięki dodaniu interceptora `requestLogger` do wychodzących zapytań, po wykonaniu dwóch żądań GET w konsoli pojawiają się dwa wpisy:

```text
Zapytanie get pod /api/users.json zarejestrowano o 2024-02-01T08:58:26.550Z
Zapytanie get pod /api/items.json zarejestrowano o 2024-02-01T08:58:26.556Z
```

Niezależnie od zapytań możemy też rozszerzać procesowanie odpowiedzi. W obu przypadkach do wykorzystania mamy dwa parametry funkcji “use” - pierwszy to interceptor odpowiedzi z kodem 2xx, czyli sukcesu, a drugi to obsługa błędów:

```javascript
axios.interceptors.response.use(successInterceptor, errorInterceptor);
```

Potencjał interceptorów jest naprawdę szeroki - może to być logowanie zapytań, obsługa i analiza błędów, albo nawet zarządzanie konkretnymi fragmentami interfejsu, prezentującymi stan oczekiwania na odpowiedź z serwera.

W dużej skali interceptory są szczególnie przydatne wtedy, kiedy konwencją w firmie nie jest poleganie na surowej wersji biblioteki. Zamiast tego, zespół platformowy może przygotować “axiosa++” i udostępnić go w wewnętrznym repozytorium rozbudowując go właśnie przez interceptory.

### Modyfikowanie klientów HTTP (Wzorzec Proxy)

Obiekty takie jak **fetch** i **axios** często nazywa się **klientami HTTP**. Zawierają one metody niezbędne do wykonywania zapytań, a także wcześniej przygotowaną konfigurację adresów docelowych serwisów, nagłówków czy obsługi błędów.

Zdarza się, że rozbudowywane konfiguracje klientów HTTP są ukrywane w dedykowanych modułach, a programiści nie pracują z surową wersją biblioteki, a właśnie wersją rozszerzoną. Jak takie rozszerzenie przygotować? Jednym z wcześniej zaprezentowanych rozwiązań są interceptory, ale można do tego celu wykorzystać także wbudowany obiekt **Proxy.**

Jak działa #Proxy? Stwórzmy prostą klasę i jej rozszerzenie przez Proxy:

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

// Funkcja korzystająca z Proxy do rozszerzenia możliwości obiektów klasy User
function createUserProxy(user) {
  return new Proxy(user, {
    get(target, property, receiver) {
      if (property === 'getName') {
        return () => `User Name: ${target.getName()}`;
      }
      return property;
    }
  });
}
```

W tym przykładzie, tworzymy funkcję **createUserProxy**, która tworzy **Proxy** dla instancji **User**. Gdy odwołujemy się do metody **getName**, **Proxy** modyfikuje jej działanie, dodając prefix “User Name:…”.

Wzorzec (i obiekt) Proxy to jedna z wielu możliwości rozszerzania zachowania obiektów, bez ingerowania w ich detale implementacyjne:

```javascript
const user = new User('Marek');
console.log(user.getName()); // Marek

const proxiedUser = createUserProxy(user);
console.log(proxiedUser.getName()); // User Name: Marek
```

To samo Proxy możemy wykorzystać do rozbudowywania naszych klientów, dodając do zapytań nowe nagłówki (wg konwencji - z prefixem “x-”) czy parametry konfiguracji:

```javascript
import { v4 as uuidv4 } from 'uuid';

const fetchProxy = new Proxy(fetch, {
  apply(target, thisArg, argumentsList) {
    let [url, cfg] = argumentsList;
    const newHeader = { 'x-req-id': `kurs-${uuidv4()}` };
    return target(url, {
      ...cfg,
      headers: {
        ...cfg?.headers,
        ...newHeader,
      },
    });
  },
});

fetchProxy('/api/users.json')
  .then((response) => response.json())
  .then((data) => console.log(data));
```

Korzystając z **fetchProxy**, nasze zapytania będą wzbogacone o nowy nagłówek, który możemy czytać na backendzie, a o którym frontend developer nie musi pamiętać:

![[Pasted image 20240430113420.png]]

Co ważne, w takim podejściu nie modyfikujemy wbudowanego w przeglądarkę obiektu **fetch** (bardzo zła praktyka, niestety wciąż spotykana na frontendzie), ale uzyskujemy jego alternatywną wersję.

## Zapytania HTTP w popularnych frameworkach

Zarówno Fetch API jak i bibliotekę axios możesz z powodzeniem wykorzystywać w każdym nowoczesnym frameworku frontendowym. W szczegółach skupimy się na tej tematyce w kolejnej lekcji, natomiast poniżej krótko podsumowujemy jak wygląda obecnie sytuacja z zapytaniami HTTP w danym ekosystemie:

### React / Vue / Svelte

Żaden z tych frameworków nie wymusza, ani nie dostarcza konkretnego klienta HTTP. Jest to zgodne z filozofią tych technologii, skupiających się przede wszystkim na rozwijaniu interaktywnych, reaktywnych widoków.

Zwykle w ich przypadku używa się bezpośrednio metod Fetch API, bibliotek zewnętrznych jak Axios, [TanStack Query](https://tanstack.com/query/latest/) i dodatków takich jak [swr](https://swr.vercel.app/) lub bardziej [rozbudowanych hooków](https://react.dev/learn/synchronizing-with-effects).

Różnice mogą się pojawić na poziomie obsługi stanu, śledzenia zmian i optymalizowania pracy komponentów, ale na tym właśnie skupimy się w kolejnej lekcji.

### Angular

Angular promuje filozofię “batteries included”, dostarczając programistom serwis **HttpClient**, którym zrealizujemy zapytania do API z poziomu naszej aplikacji.

**HttpClient** jest ściśle zintegrowany z biblioteką RxJS, co oznacza, że operacje HTTP zwracają obiekty typu Observable służące do obsługi asynchronicznych strumieni danych. Pozwala to na łatwe stosowanie operatorów RxJS do transformacji, filtrowania i łączenia zapytań HTTP z innymi typami zdarzeń. Wbudowany klient HTTP jest projektowany z myślą o integracji z innymi funkcjami Angulara, takimi jak system Dependency Injection (DI), co ułatwia zarządzanie zależnościami i konfiguracją.

## Inny model komunikacji - #WebSockets 

Wszystko to, co opisaliśmy do tej pory, zakłada jednokierunkową komunikację w #model_pull . Pobieramy z serwera kolejne dane, a użytkownik i warstwa client-side decydują o tym, kiedy to nastąpi.

Kierunek komunikacji można rozszerzyć dzięki WebSocketom, które umożliwiają dwustronną komunikację w #model_push  opartym o publikowanie zdarzeń z serwera do nasłuchujących klientów. W przeciwieństwie do tradycyjnego modelu zapytania i odpowiedzi HTTP, gdzie każda akcja użytkownika wymaga nowego żądania do serwera, WebSockety utrzymują otwarte połączenie pomiędzy warstwami.

Absolutnym liderem w tym obszarze jest biblioteka [Socket.IO](https://socket.io/) (sprawdź także [PartyKit](https://www.partykit.io/) oraz [Liveblocks](https://liveblocks.io/)).

**Gdzie wykorzystywane są WebSockety?**

1. **Aplikacje czatu i komunikatory:** WebSockety są idealne dla aplikacji, które wymagają ciągłej wymiany wiadomości między użytkownikami w czasie rzeczywistym.
    
2. **Gry online:** Umożliwiają szybką wymianę informacji o stanie gry, pozycjach graczy, i innych dynamicznie zmieniających się danych.
    
3. **Aplikacje finansowe i handel:** W przypadku aplikacji śledzących kursy akcji lub walut w czasie rzeczywistym, WebSockety zapewniają natychmiastową aktualizację danych.
    
4. **Notyfikacje w czasie rzeczywistym:** Dla aplikacji wymagających informowania użytkownika o nowych zdarzeniach, wiadomościach czy aktualizacjach bez konieczności odświeżania strony.
    
5. **Dashboardy i monitoring:** Aplikacje do monitorowania danych w czasie rzeczywistym, takie jak dashboardy analityczne, mogą skorzystać na ciągłym strumieniu danych.
    

**Kiedy decydować się na klasyczną komunikację HTTP?**

1. **Aplikacje z małą zmiennością danych:** Jeśli aplikacja nie wymaga aktualizacji w czasie rzeczywistym, utrzymanie otwartego połączenia może być niepotrzebne pod względem złożoności i zasobów.
    
2. **Proste strony internetowe:** Dla statycznych stron internetowych, blogów czy stron informacyjnych, gdzie komunikacja w dwie strony nie jest potrzebna, WebSockety mogą być nadmiarowe.
    
3. **Ograniczenia infrastruktury:** Utrzymanie dużej liczby otwartych połączeń może być wyzwaniem dla serwera, szczególnie w systemach rozproszonych i przy zastosowaniu load balancingu.
    

## Scenariusze z produkcji

**Wymagająca synchronizacja formatu danych**

Rozwijając i utrzymując na produkcji aplikacje webowe, szczególnie te, w których sesja użytkownika trwa więcej niż kilka sekund, warto pamiętać o potencjalnych konfliktach na styku backendu i frontendu. Jeden z takich konfliktów i jego rozwiązanie zobaczysz na poniższym filmie:

📝 Ten przykład znajdziesz w folderze ==**_examples/module1/lesson4/api-contract_**==.

**Kto i kiedy ma obsługiwać błędy na styku frontendu i backendu?**

Na tym etapie wiesz już jak działają popularne natywne (fetch) i zewnętrzne (axios) klienty http, do czego służą kody błędów, a także na jakie scenariusze warto się przygotować pobierając dane z backendu. Nietrudno zauważyć, że kiedy do gry wchodzi więcej niż jedna warstwa aplikacji, sprawy mogą potoczyć się w wielu kierunkach.

Nasza _frontendowa odpowiedzialność_ polega na tym, żeby te najczęściej występujące scenariusze przewidzieć, a potencjalne błędy opanować w ten sposób, żeby użytkownik nie frustrował się w trakcie korzystania z naszej aplikacji.

Pytanie brzmi - gdzie właściwie tę obsługę błędów realizować? Na poziomie klienta http? W funkcji korzystającej z klienta http? A może w obu tych miejscach jednocześnie? Czy powielanie konstrukcji try/catch jest akceptowalne, a może to _code smell_, którego powinniśmy unikać?

W praktyce okazuje się, że obsługa błędów to “ficzer” sam w sobie, a jego implementacja może różnić się w zależności od projektu czy konkretnych wymagań. Błędy będą obsługiwane inaczej w zależności od tego, czy twórca klienta http zna kontekst, w którym jego klient będzie używany, czy może go nie zna, bo tworzy bibliotekę Open Source używaną przez tysiące firm na świecie. Obsługę błędów możemy też realizować na kilku warstwach, a każda warstwa w procesie _error handlingu_ może mieć do zrealizowania inne zadanie.

Dwa równorzędne scenariusze obsługi błędów zobaczysz na poniższym przykładzie:

📝 Ten przykład znajdziesz w folderze **_examples/module1/lesson4/http-error-handling_**.

**Idealny kształt API frontendowego**

Jako frontend developerzy dążymy do tworzenia interfejsów, które komunikują się z backendem w sposób optymalny i przemyślany. Teoretyczne założenia REST API, zakładające bezstanową komunikację i jednolity kształt endpointów, stanowią solidne fundamenty. W rzeczywistym świecie programowania zdarza się jednak, że ścisłe trzymanie się idealnego REST API może nie być najbardziej efektywne.

W takich przypadkach, warto rozważyć dwa alternatywne podejścia do struktury API: **Data API** oraz **Application API**.

- **Data API** koncentruje się na udostępnianiu zasobów jednego typu (zamówienie, produkt, użytkownik, etc.). Jest to podejście zbliżone do klasycznych założeń REST, gdzie każda jednostka danych jest dostępna pod określonym endpointem, a operacje CRUD są łatwo przewidywalne i standardowe. Taka struktura jest idealna, gdy aplikacja potrzebuje dużej elastyczności w dostępie do danych, umożliwiając precyzyjne zarządzanie danymi. Dodatkowo, jeśli wystawiamy nasze API publicznie, to Data API również sprawdzi się tam znakomicie.
    
- **Application API** skupia się na dostarczaniu danych specyficznych dla konkretnego fragmentu UI. Zamiast udostępniania zasobów, endpointy są projektowane tak, aby odpowiadać na konkretne potrzeby interfejsu użytkownika, czyli np. zasilania tabeli, formularza czy listy i jej filtrów. Takie podejście może znacznie zredukować ilość potrzebnych zapytań sieciowych, zwiększając wydajność aplikacji, szczególnie w scenariuszach, gdzie frontend wymaga skomplikowanych zestawień danych. W lekcji poświęconej warstwie **Backend-for-Fronend** przyjrzymy się bliżej właśnie temu stylowi budowania API.
    

Wybór między Data API a Application API powinien być podyktowany specyfiką projektu oraz potrzebami użytkownika końcowego. W niektórych przypadkach, opłaca się odejść od teorii REST, aby dostosować API do wymagań wydajnościowych i użytkowych aplikacji. Ważne jest, aby projektując API, zawsze mieć na uwadze cel, jakim jest zapewnienie najlepszej możliwej interakcji użytkownika z aplikacją.

**Design for failure**

#Design_for_Failure na frontendzie to podejście, które zakłada, że błędy, awarie i nieprzewidziane sytuacje **są nieuniknioną częścią działania aplikacji webowej**. Zamiast próbować stworzyć system, który nigdy nie zawiedzie (co jest praktycznie niemożliwe), powinieneś skupić się na tworzeniu rozwiązań, które potrafią elegancko radzić sobie z problemami, minimalizując ich wpływ na użytkownika końcowego.

Pierwszym krokiem w implementacji Design for Failure jest rozpoznanie **potencjalnych punktów awarii w aplikacji**. Może to być na przykład nieudane zapytanie do API, błąd ładowania zasobu, czy nieprzewidziane zachowanie użytkownika. Dla każdego z tych scenariuszy, warto zaimplementować mechanizmy łagodzenia skutków, takie jak wyświetlanie wiadomości o błędzie, zapewnienie opcji ponownego wczytania zasobu, czy zastosowanie domyślnych wartości, które umożliwią dalsze korzystanie z aplikacji.

Kolejnym elementem jest budowanie **odpornych na błędy interfejsów użytkownika**, które mogą na przykład dynamicznie dostosowywać się do zmieniających się danych. Przykładowo, jeśli aplikacja polega na danych z zewnętrznego API, które może być czasowo niedostępne, interfejs powinien umożliwiać użytkownikowi sensowną interakcję z aplikacją, nawet bez tych danych. Może to oznaczać wykorzystanie tzw. “skeleton screens”, czyli komponentów sugerujących ładowanie treści, zamiast pokazywania pustych ekranów lub błędów. Zapamiętywanie chwilowo niedostępnych danych mogą też zapewniać [Service Workery](https://web.dev/learn/pwa/service-workers?hl=en).

Omawiane w drugim module testowanie to również element podejścia Design for Failure. Obejmuje ono nie tylko testy jednostkowe i integracyjne, ale również testy wydajnościowe, testy obciążeniowe oraz testowanie zachowania aplikacji w nietypowych warunkach. W kontekście komunikacji z API, niektóre firmy decydują się na tzw. “[chaos testing](https://netflix.github.io/chaosmonkey/)”, czyli obserwowanie zachowania aplikacji po umyślnym wyłączeniu z ruchu wybranych serwisów backendowych.

Ostatnim, ale równie ważnym elementem, jest **edukacja użytkowników**. Wskazówki dotyczące rozwiązywania problemów, często zadawane pytania (**FAQ**) czy nawet **proste komunikaty o błędach** mogą znacząco poprawić doświadczenie użytkownika w obliczu awarii. Dzięki temu użytkownik nie tylko rozumie, co się dzieje, ale również wie, co może zrobić, aby kontynuować pracę z aplikacją.

Pamiętaj, że w dużej skali celem nie jest zredukowanie błędów do zera (trudne do osiągnięcia), ale zapewnienie, że gdy coś pójdzie nie tak, aplikacja i jej użytkownicy są na to gotowi.

---

## 🧑‍💻 Ćwiczenia praktyczne

- W folderze **examples/module1/lesson4/abort-feedback** znajdziesz aplikację, która pobiera dane użytkowników. Niestety, API jest aktualnie obciążone i odpowiedź przychodzi dopiero po 10 sekundach. Dodatkowo, komunikaty błędów są wyświetlane niezależnie od rezultatu zapytania. Wprowadź do aplikacji następujące usprawnienia:
    
    - Spraw, aby domyślnie komunikat o problemach z połączeniem nie był widoczny
        
    - Jeśli odpowiedź nie pojawia się przez 5 sekund, wyświetl:
        
        - a) komunikat o problemach z połączeniem
            
        - b) przycisk, który umożliwia ponawianie zapytania.
            
    - Jeśli użytkownik skorzysta z przycisku “Try again”, powtórz zapytanie.
        
    - Nie modyfikuj parametru “timeout” - to dzięki niemu symulujemy opóźnienia z backendu.
        

- W folderze **examples/module1/lesson4/axios-interceptor** znajdziesz aplikację korzystającą z mechanizmu interceptorów axiosa.
    
    - Spraw, aby czas oczekiwania na odpowiedź z backendu był logowany do konsoli
        
    - Interceptory żądań i odpowiedzi mają dostęp do tego samego obiektu konfiguracyjnego - skorzystaj z niego aby zrealizować to zadanie.
        
    - Czy potrafisz zbudować podobne interceptory dla zapytań opartych o Fetch API?
        

## 📚 Materiały dodatkowe

Poniżej znajdziesz materiały poszerzające wiedzę zawartą w tej lekcji:

- Optymalne API - [https://max.engineer/server-informed-ui](https://max.engineer/server-informed-ui)