
## Wyzwania związane z testami e2e

Testy end-to-end (e2e) są potężnym narzędziem w arsenale jakości oprogramowania, ale niosą ze sobą wyzwania, które mogą podważyć ich skuteczność.

### **Kluczowe wyzwania przy zarządzaniu testami e2e**

1. **Niestabilność (flakiness)**: Testy e2e mogą być ==niestabilne z powodu zmienności środowiska testowego==, zależności od zewnętrznych usług, czy zmian w UI.
2. **Złożoność**: Duża ilość scenariuszy i interakcji między komponentami może sprawić, że testy staną się skomplikowane do utrzymania.
3. **Czas wykonania**: Testy e2e często wymagają więcej czasu na wykonanie niż testy jednostkowe czy integracyjne, co może spowolnić tempo wychodzenia z nową wersją aplikacji na produkcję (zwłaszcza w połączeniu z flakiness).
    
### **Strategie minimalizacji problemów**

1. **Selekcja Testów**: Nie każdy test musi być testem e2e. ==Wybieraj te scenariusze, które najlepiej oddają kluczowe ścieżki użytkownika i mają największy wpływ na doświadczenie klienta==.
2. **Projektowanie dla ponownego użycia**: Twórz modułowe i łatwe do ponownego użycia skrypty testowe, aby zmniejszyć ich złożoność i ułatwić utrzymanie. Zadbaj o to, żeby każdy test można było uruchomić samodzielnie, bez opierania się na wynikach poprzednich testów.
3. **Izolacja zależności**: Użyj narzędzi takich jak Playwright Mock API lub msw.js do mockowania zewnętrznych zależności i API, co pozwoli na bardziej stabilne i szybkie testy.
    
Powyższe strategie minimalizacji problemów omówimy w kolejnej sekcji.

## Wzorce i dobre praktyki

Aby podnieść skuteczność testów e2e i minimalizować związane z nimi problemy, pamiętaj o następujących dobrych praktykach i wzorcach:

## **1. Selekcja scenariuszy testowych**

Istnieje kilka podejść do strukturyzacji i organizacji testów e2e, a każde z nich ma swoje zalety w zależności od kontekstu projektu i celów testowania. Poniżej omówimy trzy główne podejścia: skupione na scenariuszach użytkownika, skupione na funkcjonalnościach oraz skupione na stronach.

**1. Podejście skupione na scenariuszach użytkownika**

To podejście koncentruje się na symulacji rzeczywistych ścieżek i interakcji, jakich użytkownicy mogą doświadczyć podczas korzystania z aplikacji. ==Testy te są organizowane wokół typowych przypadków użycia, odzwierciedlając dokładne kroki, które użytkownik może podjąć, aby osiągnąć określone cele.== Na przykład, scenariusz dla sklepu internetowego może obejmować wyszukanie produktu, dodanie go do koszyka i zrealizowanie zakupu.

**2. Podejście skupione na funkcjach**

To podejście skupia się na indywidualnych funkcjach lub możliwościach aplikacji. Ten rodzaj testowania jest bardziej modułowy niż testowanie oparte na scenariuszach użytkownika. ==Przykłady mogą obejmować testowanie formularza rejestracji, procesu logowania lub funkcji wyszukiwania==. Chociaż to podejście zapewnia, że poszczególne funkcje działają poprawnie, może nie w pełni oddawać rzeczywiste ścieżki użytkownika oraz interakcje między funkcjami.

**3. Podejście skupione na stronach**

To podejście koncentruje się na testowaniu indywidualnych stron lub ekranów aplikacji. Testy te mogą koncentrować się na sprawdzeniu, ==czy wszystkie elementy są poprawnie wyświetlane, czy interakcje z elementami interfejsu użytkownika prowadzą do oczekiwanych rezultatów i czy nawigacja między stronami działa poprawnie==. Jest to podejście bardziej zorientowane na UI niż na faktyczne zachowanie użytkowników.

### **Dlaczego skupienie się na scenariuszach użytkownika ma najwięcej sensu?**

Skupienie się na scenariuszach użytkownika ma najwięcej sensu z kilku powodów:

- **Wierność rzeczywistemu użyciu**: Scenariusze użytkownika odwzorowują rzeczywiste ścieżki, którymi użytkownicy mogą podążać, co oznacza, że testy są bardziej reprezentatywne dla realnych warunków użycia aplikacji.
- **Zrozumienie zachowań użytkownika**: Testowanie scenariuszy pozwala zespołom deweloperskim i testerom zrozumieć, jak użytkownicy wchodzą w interakcje z aplikacją, co może prowadzić do lepszych decyzji projektowych.
- **Odkrywanie złożonych błędów**: Testy oparte na scenariuszach mogą ujawnić problemy, które mogą nie być widoczne podczas testowania jednostkowego lub izolowanego testowania funkcji, szczególnie te, które pojawiają się podczas interakcji między różnymi częściami aplikacji.
- **Optymalizacja doświadczenia użytkownika**: Koncentrując się na scenariuszach, można lepiej zidentyfikować i wyeliminować przeszkody w doświadczeniu użytkownika, co bezpośrednio przekłada się na poprawę satysfakcji użytkownika.
    

Sama selekcja scenariuszy testowych jest procesem indywidualnym dla każdej aplikacji. Warto skupić się na scenariuszach, które są krytyczne dla poprawnego działania aplikacji z punktu widzenia użytkownika i biznesu. W testach Booking.com takim scenariuszem byłoby przejście przez proces zakupowy:

1. Zalogowanie się na konto
2. Wyszukanie dostępnych hoteli
3. Wybranie jednej z opcji i złożenie rezerwacji
4. Finalizacja zakupu
    
Najlepiej przeprowadzić proces selekcji scenariuszy we współpracy z product managerem, który najlepiej rozumie potrzeby oraz zachowania użytkowników. W tym przydają się również dane analityczne (eventy) informujące o tym jak użytkownicy korzystają z aplikacji (temat analityki omawiamy w module trzecim).

## **2. Jakie selektory wybrać?**

Jednym z fundamentalnych wyzwań w projektowaniu skutecznych testów e2e jest wybór odpowiednich selektorów, które umożliwią niezawodne i precyzyjne identyfikowanie elementów interfejsu użytkownika. Ta decyzja ma dalekosiężne konsekwencje, wpływając zarówno na trwałość i niezawodność testów, jak i na ich zdolność do odzwierciedlenia rzeczywistych scenariuszy użytkowania.

### **Dostępne opcje selektorów**

Podczas projektowania testów e2e, mamy do dyspozycji wiele rodzajów selektorów, w tym identyfikatory ID, klasy CSS, specjalnie przygotowane selektory, takie jak **data-testid** i selektory związane z dostępnością (a11y). Wybór między nimi zależy od wielu czynników, w tym od stabilności selektorów w czasie, łatwości ich użycia, oraz wpływu na dostępność i doświadczenie użytkownika.

1. Użycie selektorów CSS

```javascript
test('go through order process', async ({ page }) => {
  await page.goto('https://example-shop.com');
  await page.click('#add-to-cart'); 
  await page.click('.checkout-btn'); 
  await page.fill('#checkout-form > input.address', '123 Testowa Ulica'); 
  // Kontynuacja procesu zakupu
  await expect(page).toHaveURL('https://example-shop.com/confirmation');
});
```

2. Użycie _data-testid_
    

```javascript
test('go through order process', async ({ page }) => {
  await page.goto('https://example-shop.com');
  await page.getByTestId('add-to-cart').click(); 
  await page.getByTestId('checkout'); 
  await page.getByTestId('adress').fill('123 Testowa Ulica'); 
  // Kontynuacja procesu zakupu
  await expect(page).toHaveURL('https://example-shop.com/confirmation');
});
```

3. Użycie selektorów a11y
    
```javascript
test('go through order process', async ({ page }) => {
  await page.goto("https://example-shop.com");
  await page.getByRole("button", { name: "Add to cart" }).click();
  await page.getByRole("button", { name: "Checkout" }).click();
  await page.getByLabel("Adress").fill("123 Testowa Ulica");
  // Kontynuacja procesu zakupu
  await expect(page).toHaveURL('https://example-shop.com/confirmation');
});
```

**Dlaczego to istotna decyzja?**

Wybór odpowiednich selektorów jest istotny z kilku powodów:

1. **Stabilność testów**: Testy e2e powinny być odporne na mniejsze zmiany w kodzie aplikacji, takie jak aktualizacje stylów czy zmiany w strukturze DOM. Selektory, które są mniej podatne na takie zmiany, zwiększają stabilność testów.
2. **Precyzja identyfikacji**: Testy muszą precyzyjnie zidentyfikować elementy interfejsu, aby móc wchodzić z nimi w interakcję w sposób przewidywalny i powtarzalny.
3. **Dostępność i user experience (UX)**: Wybierając selektory, które odzwierciedlają sposób, w jaki użytkownicy faktycznie korzystają z aplikacji (np. selektory a11y), testy mogą lepiej symulować rzeczywiste interakcje i przyczyniać się do poprawy dostępności oraz ogólnego doświadczenia użytkownika.

W związku z tym, decyzja o wyborze selektorów w testach e2e wymaga rozważenia zarówno technicznych aspektów realizacji testów, jak i szerszej perspektywy użytkowania aplikacji. Odpowiedni balans między stabilnością a reprezentatywnością testów, a także promowanie dostępności, są kluczowe dla budowania niezawodnych, efektywnych i skoncentrowanych na użytkowniku scenariuszy testowych.

### **Dlaczego selektory CSS nie są dobrym wyborem?**

W kontekście projektowania niezawodnych testów end-to-end (e2e), istnieją ważne powody, dla których należy unikać polegania na strukturze DOM, klasach CSS oraz, w miarę możliwości, atrybutach ID. Choć ta metoda może wydawać się intuicyjna i prosta w użyciu, jej nadmierne wykorzystanie może prowadzić do szeregu problemów:

- **Łatwość zmian**: Klasy CSS ==są często modyfikowane== w procesie rozwijania i utrzymania aplikacji webowej, zwłaszcza gdy dokonuje się zmian w wyglądzie lub layoucie strony. Takie zmiany w stylach lub strukturze DOM mogą łatwo popsuć testy e2e, które polegają na takich selektorach, czyniąc je kruchymi i mniej niezawodnymi.
- **Oddalenie od rzeczywistej interakcji**: Klasy CSS ==nie odzwierciedlają sposobu, w jaki użytkownicy wchodzą w interakcje z aplikacją==. Testy oparte na tych selektorach mogą więc pomijać aspekty dostępności i użyteczności, które są kluczowe dla zapewnienia jakości doświadczeń użytkownika.
- **Brak semantyki**: Klasy CSS często nie niosą znaczenia semantycznego związanego z funkcją elementu na stronie, to tak naprawdę detale implementacyjne interfejsu. To utrudnia rozumienie i utrzymanie testów w dłuższym okresie.
- **Zarządzanie konfliktami**: W dużych projektach, gdzie wiele osób pracuje nad tym samym kodem, łatwo o konflikty nazw klas, co może prowadzić do błędów i nieścisłości w selektorach.

Stąd warto zastąpić selektory CSS za pomocą alternatyw: selektorów a11y oraz datatest-id, których zalety i wady omawiamy poniżej.

## **Analiza zalet i wad selektorów a11y**

Zalety korzystania z selektorów a11y (Accessibility) w porównaniu do _data-testid_ do celów testowych dotyczą przede wszystkim promowania dostępności i odzwierciedlania interakcji użytkownika. Oto szczegółowe spojrzenie na te zalety:

- **Promowanie dostępności:** selektory A11Y zostały zaprojektowane w celu kierowania elementów na podstawie ich semantycznych ról lub atrybutów, które są ważne dla użytkowników korzystających z technologii wspomagających. Korzystanie z selektorów A11Y może pomóc zapewnić, że aplikacja jest dostępna dla wszystkich użytkowników. Na przykład wyszukiwanie elementów według ich roli może bardziej odzwierciedlać sposób interakcji użytkowników z aplikacją. Może to prowadzić do bardziej niezawodnych testów, które nie tylko sprawdzają obecność elementów, ale także weryfikują ich dostępność.
- **Odzwierciedlanie interakcji użytkownika:** selektory A11Y zachęcają do testowania praktyk, które są zgodne z tym, jak użytkownicy faktycznie poruszają się po aplikacji i wchodzą z nią w interakcje. Lokatory a11y z API Playwright to: [_page.getByRole()_](https://playwright.dev/docs/locators#locate-by-role), [_page.getByText()_](https://playwright.dev/docs/locators#locate-by-text), [page.getByLabel()](https://playwright.dev/docs/locators#locate-by-label) oraz [page.getByAltText()](https://playwright.dev/docs/locators#locate-by-alt-text). Ich wykorzystanie może prowadzić do łatwiejszych w utrzymaniu testów, które są mniej podatne na awarie w przypadku zmian w interfejsie użytkownika, które nie mają wpływu na doświadczenie użytkownika.
  
**Ograniczenia i uwagi**  
W niektórych przypadkach elementom może brakować charakterystycznych dostępnych atrybutów lub wiele elementów może mieć tę samą dostępną nazwę lub rolę. W takich sytuacjach atrybuty _data-testid_ mogą zapewnić niezawodny sposób wybierania elementów.

## **Analiza zalet i wad selektorów _data-testid_**

Zalety korzystania z atrybutów _data-testid_ w porównaniu z selektorami A11Y (accessibility) do celów testowych ==dotyczą przede wszystkim stabilności, specyficzności i kontroli w identyfikowaniu elementów w środowisku testowym==. Oto szczegółowe spojrzenie na te zalety:

- **Stabilność**: Atrybuty _data-testid_ zapewniają stabilny sposób wybierania elementów, co jest szczególnie przydatne w dynamicznej aplikacji, w której nazwy klas i struktury elementów mogą się często zmieniać. Ta stabilność jest ==kluczowa dla utrzymania niezawodności testów w czasie==.
- **Specyficzność**: Przypisując unikalny _data-testid_ do elementu, możemy bezpośrednio wybrać ten element, bez polegania na jego zawartości tekstowej, roli lub pozycji w DOM. Ta specyficzność jest korzystna, gdy elementom brakuje charakterystycznych dostępnych atrybutów lub gdy wiele elementów ma tę samą dostępną nazwę lub rolę.
- **Izolacja od zmian interfejsu użytkownika**: Ponieważ atrybuty _data-testid_ są przeznaczone wyłącznie do celów testowych, pozwalają one na identyfikację elementów niezależnie od ich wizualnej prezentacji lub atrybutów dostępności. Oznacza to, że ==testy mogą pozostać nienaruszone przez zmiany stylu elementu lub zawartości tekstowej==, które w przeciwnym razie mogłyby wymagać dostosowania testów.
- **Obsługa dynamicznej zawartości**: W przypadkach, gdy zawartość tekstowa elementu jest dynamiczna lub generowana w czasie wykonywania, _data-testid_ zapewnia niezawodny ==sposób wybierania tych elementów bez zależności od ich zawartości, która może nie być przewidywalna==.
- **Integracja z narzędziami do testowania**: Wiele nowoczesnych frameworków i bibliotek testowych oferuje pierwszorzędne wsparcie dla wybierania elementów za pomocą _data-testid_, dzięki czemu można je łatwo zintegrować z istniejącymi zestawami testów. W Playwright jest to metoda [_page.getByTestId()_](https://playwright.dev/docs/locators#locate-by-test-id)_._
  
**Ograniczenia i uwagi**  
Nadmierne poleganie na _data-testid_ może prowadzić do testów, które są mniej reprezentatywne dla sposobu interakcji użytkowników z aplikacją, potencjalnie pomijając kwestie dostępności.

### **Rekomendacja: domyślnie wybieraj selektory _a11y_**

==Podsumowując, selektory A11Y są potężnym narzędziem do osiągania dostępnego i skoncentrowanego na użytkowniku wyboru elementów w testach. Warto z nich korzystać “by default”, pamiętając o możliwości ich uzupełnienia atrybutami _data-testid_. Dzięki temu testy pozostaną zarówno solidne, jak i reprezentatywne dla interakcji użytkownika==.

## **3. Pisanie testów zgodnie z dobrymi praktykami**

Przy prezentowaniu wzorców projektowania skutecznych testów wykorzystamy aplikację [Wikipedia.org](http://en.wikipedia.org/). To aplikacja ze stabilnym UI, która służy milionom użytkowników na całym świecie. Na dodatek Wiki jest typową aplikacją legacy, gdzie znajdziemy rozwiązania, które odbiegają od najnowszych trendów - to dobrze, ponieważ często właśnie takie aplikacje przyjdzie nam testować na produkcji.

Jeżeli chodzi o najlepsze praktyki związane z projektowaniem do ponownego użycia, to są one następujące:

**3.1 Współdzielenie stanu zalogowania (basic)**

Testy w Playwright mogą ładować istniejący stan sesji. Eliminuje to potrzebę uwierzytelniania w każdym teście, co znacznie przyspiesza wykonanie całości test suite.

**Ważne**: [jak wskazuje dokumentacja](https://playwright.dev/docs/auth#basic-shared-account-in-all-tests), przedstawiona konfiguracja nie jest optymalna dla testów modyfikujących stan serwera. Postawiłem na prostotę, aby nie komplikować lekcji dla osób zaczynających z Playwrightem. Pisząc testy modyfikujące stan serwera, skorzystaj ze sposobu: “[One account per parallel worker](https://playwright.dev/docs/auth#moderate-one-account-per-parallel-worker)” - jest on opisany w dalszej części lekcji.

**3.2 Stosowanie wzorca ==Page Object Model==**

Wzorzec Page Object model pozwala ustrukturyzować nasze testy, ułatwiając pisanie i utrzymanie scenariuszy testowych. Zobacz jak możemy zastosować Page Object Models do reprezentacji strony głównej oraz strony logowania na Wikipedii:

**Przykładowy scenariusz testowy z Page Object Model**

Uzbrojeni w znajomość wzorca POM możemy przejść do pisania pierwszego scenariusza testowego, który sprawdzi możliwość dodania “Today’s featured article” do watchlisty.

Metoda wykorzystana do poradzenia sobie z problemem dot. zbyt wolnego ładowania skryptów pomocniczych to [page.waitForUrl().](https://playwright.dev/docs/api/class-page#page-wait-for-url)

## 4. Mockowanie API i izolacja testów od zależności

Mockowanie API w testach end-to-end (e2e) ==pełni istotną rolę w kontekście izolacji testów od zewnętrznych zależności oraz zapewnienia stabilności i przewidywalności wyników==. Pozwala to na symulowanie zachowań API bez konieczności wykonywania rzeczywistych zapytań do serwera backendowego.

**Kiedy warto mockować API, a kiedy zachować pełne testy e2e?**

Mockowanie ma sens, jeżeli chcemy przetestować UI, który jest silnie zależny od danych przychodzących z API, ale nie zależy nam na sprawdzaniu samej integracji z backendem. Do tej grupy zaliczam testy skoncentrowane na stronach. Dzięki kontrolowaniu API ==możemy łatwo sprawdzić obsługę różnych stanów testowanej strony (np. pusta lista, lista elementów, obsługa błędów). ==Taki rodzaj testów interfejsu, gdzie odcinamy się od API przez mocki, jest zwykle nazywany== ==**UI tests**.

Pamiętajmy, że celem testów ==e2e jest sprawdzenie integracji całego systemu, włącznie z rzeczywistym backendem i bazą danych==. Te testy są ważne do weryfikacji, czy wszystkie części systemu współpracują ze sobą poprawnie - nie traktujmy UI testów jako alternatywy dla testów e2e, w naszej piramidzie testowania znajdują się na granicy testów integracyjnych i testów e2e.

Tak jak pisałem wcześniej, w pierwszej kolejności warto skupić się na poprawnym wyborze kluczowych scenariuszy testów e2e a pozostałe zasoby możemy przeznaczyć na pisanie UI testów poszczególnych stron.

**Jakich narzędzi używać do mockowania API?**

Korzystając z Playwrighta mamy do dyspozycji kilka opcji, z czego dwie najpopularniejsze to: Playwright Mock APIs oraz biblioteka msw.js.

[Playwright Mock APIs](https://playwright.dev/docs/mock) oferuje proste i intuicyjne API do przechwytywania calli do backendu wykonywanych w przeglądarce:

```ts
test("mocks a fruit and doesn't call api", async ({ page }) => {
  await page.route('*/**/api/v1/fruits', async route => {
    const json = [{ name: 'Strawberry', id: 21 }];
    await route.fulfill({ json });
  });
  await page.goto('https://demo.playwright.dev/api-mocking');

  await expect(page.getByText('Strawberry')).toBeVisible();
});
```

Jeżeli nasze testy wymagają wyłącznie mockowania zapytań wykonywanych w przeglądarce, to Playwright Mock APIs jest świetnym wyborem. Taka decyzja pozwoli nam uniknąć dodatkowej złożoności oraz zarządzania zależnościami.

[msw.js](https://mswjs.io/) (Mock Service Worker) to biblioteka umożliwiające tworzenie mocków API bezpośrednio w przeglądarce lub w Node.js. Jego przewaga nad Playwright Mock APIs to możliwość mockowania zapytań w warstwie Node.js oraz pełnoprawne wsparcie dla GraphQL. To świetne rozwiązanie, jeżeli nasza aplikacja korzysta z architektury Backend For Frontend (BFF), dzięki czemu możemy korzystać z jednego narzędzia w przeglądarce i Node.js. Więcej o BFF dowiesz się z modułu 5.

W tym video przedstawiam jak mockować zapytania do API właśnie za pomocą msw.js, aby wprowadzić Cię w to narzędzie. Przypadek testowy z filmu moglibyśmy spokojnie obsłużyć za pomocą Playwright Mock APIs.


Więcej informacji o msw i playwright-msw znajdziesz w dokumentacjach narzędzi podlikowanych w materiałach dodatkowych.

### **5. Współdzielenie stanu zalogowania: advanced**

Testy e2e skoncentrowane na scenariuszach użytkownika mają to do siebie, że zazwyczaj modyfikują stan serwera. Playwright umożliwia i promuje współbieżne wykonywanie przypadków testowych w oparciu o kilka workerów uruchamianych w tym samym czasie. Współbieżność i ilość workerów definiujemy na poziomie konfiguracji playwright.config ([opis dostępnych opcji](https://playwright.dev/docs/test-configuration)). Wszystko fajnie, tylko takie podejście nie pozwala nam na bezpieczne wykorzystywanie jednego konta, ponieważ może dojść do konfliktów pomiędzy workerami - jeden z nich zmodyfikuje stan, który jest w tym samym czasie weryfikowany przez inny. Aby uniknąć takich konfliktów należy przydzielić osobne konto każdemu z workerów, co jest opisane w dokumentacji [One account per parallel worker](https://playwright.dev/docs/auth#moderate-one-account-per-parallel-worker).

Poniżej znajdziesz implementację tej metody dostosowaną do przykładów z lekcji:

```javascript
// examples/module2/lesson2/extended/fixtures.ts
import { test as baseTest, expect } from '@playwright/test';
import fs from 'fs';
import path from 'path';
import { LoginPage } from './pages/login.page';
import { MainPage } from './pages/main.page';
import { acquireAccount } from './utils/acquire-account';
import { URLs } from './utils/constants';

export * from '@playwright/test';
export const test = baseTest.extend<object, { workerStorageState: string }>({
  // Współdziel stan sesji pomiędzy wszystkimi testami w ramach jednego workera.
  storageState: ({ workerStorageState }, use) => use(workerStorageState),

  // Wykonaj uwierzytelnianie dla każdego z workerów.
  workerStorageState: [
    async ({ browser }, use) => {
      // parallelIndex służy unikalnego identyfikatora dla każdego pracownika.
      const id = test.info().parallelIndex;

      if (id >= 2) {
        // Ograniczamy liczbę obsługiwanych workerów do dwóch
        // To przykładowy projekt, nie mamy możliwości tworzenia nowych kont przez API.
        throw new Error('This example project only supports two workers');
      }

      const fileName = path.resolve(
        test.info().project.outputDir,
        `.auth/${id}.json`
      );

      if (fs.existsSync(fileName)) {
        // Ponowne wykorzystanie istniejącego stanu uwierzytelniania, jeśli taki istnieje.
        await use(fileName);
        return;
      }

      // Ważne: Upewnij się, że korzystamy z czystego środowiska, resetując stan storage.
      const page = await browser.newPage({ storageState: undefined });

      // Uzyskaj dostęp do konta w oparciu o ID workera.
      // W przykładzie korzystamy z dwóch kont zdefiniowanych na poziomie .env.
      // Na produkcji zwykle korzystamy z API do tworzenia dedykowanych kont testowych.
      const account = await acquireAccount(id);

      // Przejdź przez proces logowania.
      const loginPage = new LoginPage(page);
      await loginPage.navigate();
      await loginPage.fillLoginForm(account.username, account.password);

      // Czekamy aż strona otrzyma cookiesy z uwierzytelnieniem.
      // Czasami proces logowania może składać się z kilku redirectów,
      // stąd warto zaczekać na finalny URL, aby mieć pewność że mamy wszystkie cookiesy.
      const mainPage = new MainPage(page);
      await expect(page).toHaveURL(URLs.MAIN_PAGE);
      await expect(mainPage.getNavigation()).toContainText(account.username, {
        ignoreCase: true,
      });

      // Koniec uwierzytelniania.
      await page.context().storageState({ path: fileName });
      await page.close();
      await use(fileName);
    },
    { scope: 'worker' },
  ],
});
```

_test_ i _expect wyeksportowane_ z tego modułu wykorzystujemy następnie w testach, które wymagają zalogowania.

Powyższy kod wraz z dodatkowymi testami znajdziesz w _examples/module2/lesson2/extended_. Aby go uruchomić, zmień _PROJECT_DIR_ z base na extended w _playwright.config.ts_.

### Ćwiczeni

### 📚 Materiały dodatkowe

1. [Dokumentacja Playwright](https://playwright.dev/docs/intro), najważniejsze fragmenty:
    
    1. [Actions](https://playwright.dev/docs/input)
        
    2. [Authentication](https://playwright.dev/docs/auth)
        
    3. [Assertions](https://playwright.dev/docs/test-assertions)
        
    4. [Best Practices](https://playwright.dev/docs/best-practices)
        
    5. [Browsers](https://playwright.dev/docs/browsers)
        
    6. [Locators](https://playwright.dev/docs/locators)
        
    7. [Page object models](https://playwright.dev/docs/pom)
        
    8. [Mock APIs](https://playwright.dev/docs/mock) + [Advanced Networking](https://playwright.dev/docs/network)
        
    9. [Navigations](https://playwright.dev/docs/navigations)
        
2. [Dokumentacja msw.js](https://mswjs.io/)
    
3. [Porównanie msw.js z dostępnymi alternatywami](https://mswjs.io/docs/comparison)
    
4. [Dokumentacja playwright-msw](https://github.com/valendres/playwright-msw/blob/main/packages/playwright-msw/README.md)
    
5. [Cheatsheet API Playwright](https://proxiesapi.com/articles/the-complete-playwright-cheatsheet?utm_source=pocket_reader)