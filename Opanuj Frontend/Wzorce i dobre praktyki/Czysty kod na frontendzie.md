## Wprowadzenie

Witaj w pierwszej lekcji pierwszego modułu Opanuj Frontend! W pierwszym module skupimy się na tematyce wzorców i praktyk podnoszących jakość budowanego przez ciebie frontendu. Przejdziemy przez wzorce ułatwiające zarządzanie stanem aplikacji, wzorce usprawniające przepływ danych i komunikację pomiędzy komponentami, wzorce profesjonalnej komunikacji z API oraz techniki, które poprawią wydajność twoich aplikacji.

Zanim rozpędzimy się na dobre, w tej lekcji zastanowimy się dlaczego kod i projekty tworzone przez frontend developera mogą być podatne na spadek jakości, trudności w utrzymaniu i dalszej rozbudowie. Przejdziemy też przez kilka pierwszych przykładów i ćwiczeń, które pokażą Ci jak tę jakość podnieść stosunkowo niskim kosztem.

## Jakość w programowaniu

Duża część komunikacji wokół naszego kursu dotyczy tematyki jakości i budowania profesjonalnych (w domyśle - stabilnych, skalowalnych, zrozumiałych) aplikacji frontendowych. Struktura naszego kursu wygląda tak, a nie inaczej, ponieważ jakość w programowaniu wpływa w dużym stopniu na ostateczny sukces projektu, w którym bierzesz udział.

- Po pierwsze, **jakość, przejrzystość i niska złożoność kodu w bezpośredni sposób wpływają na tempo rozwoju projektu**. Jeśli architektura jest otwarta na rozszerzenia, a na etapie planowania zapewniono możliwość rozbudowy projektu o nowe możliwości, to zespół nie będzie tracił czasu rozmyślając gdzie dodać nowy komponent, jak zintegrować go z istniejącym interfejsem, jak zdebugować nową funkcję, albo co stanie się, kiedy usuniemy pozornie zbędne linijki kodu.
    
- Po drugie, **wiele realizowanych przez nas projektów rozpoczynało się i kończyło w zupełnie innym stanie zespołów** programistycznych. Pojawiały się nowe osoby, niektóre odchodziły, a projekt ciągle pozostawał na firmowej roadmapie. Kierunek rozwoju projektu często pozostawał na barkach najbardziej doświadczonych programistów, ale osiąganie kolejnych milestonów decydowało się w momentach, kiedy ich zabrakło bo np. przeszli do innego zespołu, dostali inne zadania lub po prostu wypadli z przyczyn losowych. Wyjście z trudnej sytuacji ułatwiało nic innego jak łatwy do zrozumienia, udokumentowany kod.
    
- Po trzecie, **korzyści płynące z utrzymywania kodu wysokiej jakości widać szczególnie mocno wtedy, kiedy tej jakości zaczyna brakować**. Objawia się to nie tylko regularnymi bugami, o których informują nas klienci, ale również spadkiem morale w zespole, cyklicznie pojawiającymi się przerwami w dostępie do aplikacji i negatywnymi komentarzami, które mogą pojawiać się na portalach recenzujących nasze rozwiązania. Finalnie mówimy tutaj o utracie pieniędzy (czy, jak to się ładnie określa - wartości biznesowej), a od tego już krótka droga do odczucia spadku jakości w dniu wypłaty lub podczas rozmów z szefem.
    

### Wpływ świata rzeczywistego

Mówiąc o jakości, nie można zapominać o realnych warunkach, w jakich często realizujemy nasze projekty.

Pierwszy często pojawiający się warunek dotyczy **presji czasu**. Za rogiem nowy release, obietnice dla klienta już dawno złożone, kontrakt podpisany, a strona nadal nie działa tak, jak powinna. Mało który developer zdecyduje się w tym momencie na szczerą rozmowę z managerem - zmieni się prawdopodobnie akceptowalna jakość kolejnych Pull Requestów, przymykanie oka na code review czy pomarańczowe testy.

Dodatkowo, różne projekty cechują się różnym poziomem trudności. Tzw. **greenfield**, czyli projekt budowany od zera, to szansa na wdrożenie wszystkich ostatnio poznanych metod i technik zapewniania wysokiej jakości (np. tych poznanych w Opanuj Frontend). Poza greenfieldami zdarzy się też **brownfield**, czyli projekt zastany, przez którego przeszło kilka pokoleń developerów i który mógł być przerzucany z jednego końca organizacji na drugi. Jakość w obu przypadkach będzie radykalnie inna, ale i tu i tu musimy umieć się odnaleźć jako programiści.

Mówiąc o programistach, nie możemy też zignorować naszych własnych ograniczeń wiedzy i doświadczenia. Tak jak media społecznościowe zbudowały wokół nas bańki opinii, tak nasza własna przygoda z programowaniem również może się odbywać w tego rodzaju bańce jednego frameworka lub biblioteki. Nawet wtedy, kiedy na rynku będą już dostępne lepsze i łatwiejsze rozwiązania danego problemu, niektórzy z nas będą nieświadomie wybierać ścieżkę trudniejszą, bo innej po prostu nie znają (albo co gorsza - czasami nie chcą jej poznać).

Jeśli temat jakości nie wydaje ci się jeszcze wystarczająco skomplikowany, to na dokładkę porozmawiajmy o tym, jak sam frontend całą tę dyskusję utrudnia.

## 🤔 Zanim przejdziesz dalej

Zastanów się co sprawia, że tworzenie frontendowych aplikacji wysokiej jakości jest trudnym zadaniem. Co może być powodem nie zawsze pozytywnych opinii na temat programowania na frontendzie - zarówno na poziomie technologii jak i praktyk programowania?

Porównaj swoje spostrzeżenia z dalszą częścią tej lekcji ⬇️

## Prosty język do złożonych aplikacji

JavaScript został stworzony przez Brendana Eicha w 1995 roku z zamiarem umożliwienia dodawania prostych interakcji do statycznych stron internetowych. Jak przyznaje sam autor, cały [proces tworzenia pierwszej wersji tego języka zajął mu zaledwie… 10 dni](https://youtu.be/S0ZWtsYyX8E)!

Początkowo był to język o bardzo ograniczonych możliwościach, pasujących jednak do prostych stron i możliwości sprzętu, na którym te strony wczytywano. Z biegiem czasu rola tego języka zaczęła stopniowo rosnąć. Na dzisiaj to fundament tworzenia złożonych, wielowarstwowych, interaktywnych aplikacji internetowych, który zajmuje najwyższe miejsca w rankingach popularności.

O ile popularność języka i jego elastyczność wpłynęły pozytywnie na szybki rozwój frontendowego ekosystemu, to wspomniany rozjazd oryginalnych założeń i rosnących oczekiwań stał się wyzwaniem dla wszystkich, którzy do JavaScriptu podchodzili bez odpowiedniego przygotowania.

Jedną z głównych trudności w pracy z JavaScriptem jest jego stosunkowo uboga biblioteka standardowa, zwłaszcza w porównaniu do języków takich jak Python czy Java. Różnice widać w takich obszarach jak obsługa bardziej złożonych typów danych, zarządzanie datą i czasem, praca na systemie plików czy debugowanie i profilowanie kodu. Ta ograniczona funkcjonalność oznacza, że programiści muszą polegać na zewnętrznych środowiskach uruchomieniowych takich jak Node, a także mnożących się zależnościach na biblioteki i narzędzia, które nie zawsze rozwijane są w profesjonalny sposób.

Dodatkową komplikację stanowią też zróżnicowane środowiska uruchomieniowe (przeglądarki, serwery, systemy wbudowane, etc.) oraz warstwy aplikacji, w których ten sam JavaScript próbujemy uruchomić. Wielokrotnie zdarzało nam się brać udział w dyskusjach, gdzie tłumaczyliśmy komuś innemu dlaczego ta sama funkcja języka działa w Chrome, a nie działa w Safari (nie mówiąc o Internet Explorerze, ale ten temat przemilczymy).

Mało? Dodajmy do tego fragmentu sam charakter aplikacji, jakie tworzymy z wykorzystaniem JavaScriptu. Frontend jest warstwą, gdzie odbywa się interakcja użytkownika z aplikacją, co wiąże się z obsługą zdarzeń, animacji, aktualizacji stanu, asynchronicznych zapytań po dane i obsługi renderowania. Zarządzanie tymi aspektami w sposób, który jest zarówno wydajny, jak i łatwo utrzymywalny, jest niebanalnym zadaniem.

Wszystko to sprawia, że na frontendzie stosunkowo łatwo spotkać tzw. “code smells”, czyli fragmenty kodu niskiej jakości i praktyki, które komplikują złożoność budowanych rozwiązań.

Z przykładów można wymienić chociażby:

- nadmierne poleganie na zewnętrznych zależnościach
    
- brak separacji pomiędzy warstwami widoku i logiki aplikacji
    
- nadużywanie globalnych zmiennych i obiektów konfiguracyjnych
    
- niedostateczna modularyzacja kodu w obrębie domen biznesowych
    
- trudny w debugowaniu stan aplikacji i przepływ danych
    
- brak kontroli nad obsługą błędów i zapytań do serwera
    
- nadmierne i niekontrolowane aktualizowanie widoków aplikacji
    

Coś nam podpowiada, że kilka z tych problemów miałeś już okazję poznać we własnym zakresie.

Całej społeczności projektującej standard ECMA Script (więcej na ten temat w materiałach dodatkowych) trzeba jednak oddać, że wysiłki ostatnich lat znacznie zwiększyły możliwości najważniejszego z języków nowoczesnego frontendu. JavaScript, mający swoje korzenie w programowaniu przeglądarkowym, ewoluował w kierunku obsługi dużych aplikacji internetowych, z naciskiem na asynchroniczność i interaktywność interfejsów użytkownika.

Z biegiem czasu w języku zaczęły się pojawiać nowe rodzaje obiektów wbudowanych (Set, Map), metody pracy z kolekcjami (some, every, includes), łatwiejsza obsługa asynchroniczności (Promise, async/await) czy natywne wsparcie dla modułów (ES Modules).

Dzięki tym zmianom programiści zaczęli stopniowo otrzymywać kolejne narzędzia podnoszące jakość tworzonych projektów. **W kolejnych lekcjach zobaczysz to w praktyce.**

Zanim wskoczymy w konkretne obszary aplikacji frontendowych, pozostańmy jeszcze przez chwilę na poziomie fundamentów i upewnijmy się, że mamy je opanowane do perfekcji.

## Fundamenty kodu wysokiej jakości

### Zadbaj o czytelność

Pierwszym z fundamentów, który przychodzi na myśl mówiąc o dobrych praktykach w programowaniu, jest **czytelność.** Szczególnie mocno zwracaliśmy na to uwagę przeprowadzając setki Code Review w kursie Opanuj JavaScript. Kiedy uczestnicy dzielili się z nami rozwiązaniami kursowych ćwiczeń, często problemem okazywało się niestaranne formatowanie kodu, mało intuicyjne nazewnictwo zmiennych i funkcji, a także nieoptymalna organizacja poszczególnych wyrażeń.

Wystarczy tylko porównać dwa fragmenty kodu. Co robi funkcja poniżej?

```javascript
var successMessage = "musisz mieć więcej niż 18 lat";

function f(entry) {
    var n = entry.firstName, s = entry.lastName, a = entry.age;
    
    if (a < 18) {
        return successMessage;
    }

    var result = '';
    var map = { firstName: 'Imię: ', lastName: 'Nazwisko: ', age: 'Wiek: ' };
    for (const key in map) {
        result += map[key] + entry[key] + ', ';
    }

    return result.slice(0, -2);
}
```

A co robi ta funkcja?

```ts
// User.ts
interface User {
  firstName: string;
  lastName: string;
  age: number;
}

// index.ts
function formatUserInfo(user: User): string {
    const { firstName, lastName, age } = user;
    const AGE_LIMIT = 18;
    const WARNING_MESSAGE = "Musisz mieć więcej niż 18 lat";

    if (age < AGE_LIMIT) {
        return WARNING_MESSAGE;
    }

    return `Imię: ${firstName}, Nazwisko: ${lastName}, Wiek: ${age}`;
}
```

Jak pewnie zauważyłeś - obie funkcje realizują dokładnie to samo zadanie. Przyjmują obiekt z danymi użytkownika, pobierają niezbędne informacje, wykonują dodatkowe sprawdzenie wieku i - w przypadku obejścia limitu - zwracają poprawną wiadomość.

Różnica w trudności zrozumienia każdej z nich jest radykalnie inna, oczywiście na korzyść tej drugiej, gdzie czytelność stoi na wyższym poziomie. Co o tym decyduje?

- nazwa funkcji mówi, jakie zadanie możesz dzięki niej zrealizować (_formatUserInfo_)
    
- nazwa parametru wskazuje na domenę i rodzaj obiektu, z którym pracujesz (_user_)
    
- wartości stałe są łatwe do zidentyfikowania dzięki konwencji o wykorzystaniu wielkich liter (_AGE_LIMIT_)
    
- funkcja ma stosunkowo niską złożoność i nie korzysta ze zbędnych pętli i obiektów
    
- parametr i wartość zwracana z funkcji mają jasno zdefiniowane typy danych
    

**Czytelność** kodu można porównać do czytania dobrze napisanej książki. Kiedy każde zdanie płynnie przechodzi w następne, a rozdziały są logicznie uporządkowane, lektura staje się przyjemna i zrozumiała. Podobnie, czysty i dobrze zorganizowany kod pozwala szybko zrozumieć jego intencje i strukturę, co sprawia, że praca z nim jest efektywna i satysfakcjonująca. Przekłada się to również na nawigację w projekcie, kiedy zamiast jednego modułu, pracujemy z dziesiątkami lub setkami na raz.

### Ustal zasady

Pisząc o czytelności trudno nie wspomnieć o standardach, regułach i narzędziach do formatowania kodu, które pozwalają nam kontrolować kształt projektu, i - co równie ważne - wprowadzać bardziej obiektywne standardy formatowania i organizacji kodu na poziomie całego zespołu (np. gdzie dawać spacje, czym robić wcięcia, jak powinna wyglądać destrukturyzacja).

Narzędzia, które pozwolą ci dbać o czytelny, dobrze sformatowany kod to m.in.:

- [eslint](https://eslint.org/) - najpopularniejsze obecnie narzędzie do statycznej analizy kodu z szeroką bazą reguł publikowanych w formie Open Source, np.:
    
    - [eslint-config-google](https://www.npmjs.com/package/eslint-config-google) - konfiguracja używana przez Google
        
    - [eslint-config-airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb) - konfiguracja używana przez AirBnb
        
    - [@shopify/eslint-plugin](https://www.npmjs.com/package/@shopify/eslint-plugin) - konfiguracja używana przez Shopify
        
- [Prettier](https://prettier.io/) - równie popularny formatter kodu z wbudowanymi regułami dla najważniejszych języków frontendu, w tym dla JavaScriptu, TypeScriptu, HTML i CSS
    
- [Biome](https://biomejs.dev/) - zestaw narzędzi do utrzymywania spójności kodu oparty o język Rust (kiedyś _Rome_)
    

W kolejnych lekcjach naszego kursu zobaczysz jak automatyzować wykorzystanie tych narzędzi na poziomie dużych projektów i całego zespołu.

### Wykorzystuj możliwości języka

Na czytelność wpływa nie tylko **nazewnictwo**, ale sprawne posługiwanie się **nowoczesnymi konstrukcjami**, na które pozwala twój ulubiony język.

- Zamiast używania zbyt ogólnego słowa kluczowego **var**, możemy korzystać z bardziej precyzyjnych **let** i **const**_,_ określających przy okazji, czy zmienna może się… zmieniać ;)
    

- Zamiast niepotrzebnego wyłuskiwania i przepisywania zmiennych, w powyższym przykładzie do pobierania danych wykorzystujemy **destrukturyzację.**
    
- Zamiast ręcznego budowania finalnej wiadomości, lub składania jej w przesadnie skomplikowany sposób, wykorzystujemy **literały i szablony stringów**.
    

Dzięki refaktoryzacji w kierunku nowego standardu języka, możemy przejść z kodu takiego jak ten poniżej…

```javascript
var msg = "Musisz mieć więcej niż 18 lat";
var fName = entry.firstName, lName = entry.lastName, a = entry.age;
return "Imię: " + fName + ", Nazwisko: " + lName + ", Wiek: " + a;
```

…do kodu zdecydowanie bardziej czytelnego:

```ts
const message = "Musisz mieć więcej niż 18 lat";
const { firstName, lastName, age } = user;
return `Imię: ${firstName}, Nazwisko: ${lastName}, Wiek: ${age}`;
```

Zdecydowanie rekomendujemy trzymanie ręki na pulsie zmian wokół JavaScriptu. Cały proces dokumentowany jest przez grupę roboczą [TC39](https://tc39.es/#proposals), która prowadzi regularne dyskusje na temat kolejnych usprawnień i tempa ich prowadzania.

Jeśli natomiast nie jesteś pewien, czy nowoczesne konstrukcje można wykorzystywać na produkcji, skorzystaj ze strony [CanIUse.com](https://caniuse.com/), która pokaże ci wsparcie przeglądarek w wybranym przez ciebie obszarze.

### Nie wprowadzaj niepotrzebnej złożoności

Czy kod może wykorzystywać poprawne nazewnictwo, nowoczesne konstrukcje języka, a pomimo tego nadal być nieczytelnym? Oczywiście!

Kiedy do rozwiązywania określonych problemów stosujemy nieproporcjonalnie skomplikowane struktury danych, wyrażenia czy algorytmy, to złożoność kodu rośnie. To coś, co **przekłada się negatywnie** na długoterminowe utrzymanie projektu, efektywność współpracy zespołowej i skuteczne rozwiązywanie bugów na produkcji.


W przypadku wcześniej zaprezentowanej funkcji, złożoność wzrasta tam, gdzie zamiast _string templates_ decydujemy się na obiekty, pętle i dodatkowe, zupełnie zbędne operacje na danych:

```ts
const map = { firstName: 'Imię: ', lastName: 'Nazwisko: ', age: 'Wiek: ' };
for (const key in map) {
    result += map[key] + entry[key] + ', ';
}

return result.slice(0, -2);
```

Pierwszy rzut oka na ten fragment sugeruje, że służy on do czegoś znacznie bardziej skomplikowano, niż w rzeczywistości jest. Kod o niskiej złożoności, który służy do tego samego celu (formatowanie stringa), wygląda następująco:

```ts
return `Imię: ${firstName}, Nazwisko: ${lastName}, Wiek: ${age}`;
```

Programista czytający ten kod nie musi utrzymywać w głowie kształtu dodatkowych obiektów, nie musi iterować po kolejnych wykonaniach pętli, no i (co istotne w kontekście bugów) nie musi zarządzać nieprzewidzianymi sytuacjami, takimi jak dodanie przecinka na końcu tekstu.

Wychodząc poza ten przykład, złożoność może również wzrosnąć na skutek:

- wprowadzania do kodu niestandardowych struktur danych
    
- budowania złożonych algorytmów
    
- nadużywania lub ignorowania wzorców projektowych
    

- niewystarczającego lub przesadnego polegania na zewnętrznych bibliotekach
    
- zmian wprowadzonych w ramach tzw. przedwczesnej optymalizacji
    

> “If you make an optimization and don’t measure to confirm the performance increase, all you know for certain is that **you’ve made your code harder to read**.” - Martin Fowler [(źródło)](https://www.martinfowler.com/ieeeSoftware/yetOptimization.pdf)

Zarządzanie złożonością jest **o wiele bardziej wymagającym aspektem pracy programisty niż poprawne nazewnictwo czy wykorzystywanie nowych konstrukcji języka**. To umiejętność, którą rozwijamy przez całą karierę, pracując w różnorodnych projektach i ucząc się nieznanych wcześniej podejść do pisania kodu.

Zauważ, że świadomie używamy też zwrotu “zarządzanie złożonością” a nie jej redukowanie, bo w przypadku szczególnie trudnych problemów, tej złożoności nie do końca można uniknąć. Wtedy warto natomiast zadbać o odpowiednią izolację szczególnie złożonych fragmentów kodu od reszty, aby w razie potrzeby łatwo je wymienić lub aktualizować.

Jeśli natomiast z takimi problemami szczególnej wagi nie pracujemy, to bezpiecznie jest korzystać z praktycznej zasady KISS, czyli “Keep It Simple, Stupid”.

### Organizacja większych fragmentów kodu

Jeśli opanowaliśmy sztukę pisania kodu czytelnego, wykorzystującego nowoczesne konstrukcje języka oraz takiego, gdzie złożoność utrzymujemy pod kontrolą, to możemy wejść na poziom modułów i większych fragmentów projektu. O czym warto pamiętać w tym kontekście?

> “The primary feature for easy maintenance is **locality**: Locality is that characteristic of source code that enables a programmer to understand that source by looking at only a small portion of it.” - [Richard Gabriel](https://www.dreamsongs.com/Files/PatternsOfSoftware.pdf)

Dwie bliskie sobie reguły, które warto stosować, to #Locality_of_Behavior oraz 
#Proximity_Principle
”. Chociaż moglibyśmy je rozpatrywać osobno, to w uproszczeniu sprowadzają się one do dwóch punktów:

- utrzymuj **możliwie blisko siebie** te fragmenty projektu, które są ze sobą ściśle powiązane i zmieniają się w tym samym tempie
    
- **redukuj do minimum** akcje i działania potrzebne do zrozumienia danego fragmentu projektu

Wyobraźmy sobie, że rozwijamy formularz do obsługi zamówień w sklepie internetowym. Kod utrzymywany w zgodzie z regułą bliskości powinien nam umożliwiać wprowadzanie zmian na maksymalnie małym obszarze projektu, często nawet w obrębie jednego folderu. W nim moglibyśmy znaleźć:

- komponent definiujący działanie formularza
    
- style wpływające na wygląd formularza
    
- testy weryfikujące najważniejsze aspekty działania formularza
    
- interfejsy i typy danych, jakimi posługujemy się w formularzu
    
- komunikację z backendem
    
- logikę walidacji danych
    
- obsługę błędów
    

Taka organizacja projektu pozwala w łatwy sposób zrozumieć granice odpowiedzialności pomiędzy modułami, pozwala na łatwiejsze budowanie alternatywnych rozwiązań niemal obok siebie, no i pozwala na łatwiejsze usuwanie kodu, co w kontekście utrzymania niskiej złożoności bywa bardziej istotne, niż jego dodawanie.

### Klasyczne praktyki czystego kodu - DRY, SOLID, CUPID



**#DRY**, czyli Dont Repeat Yourself to jedna z najbardziej popularnych rekomendacji w świecie programowania.

W założeniu jej przesłanie jest jak najbardziej rozsądne - unikaj powtórzeń, buduj możliwe do ponownego użycia funkcje, moduły i biblioteki, oszczędzaj czas wprowadzając zmiany tylko w jednym miejscu. W przypadku prostych projektów to powinno zdecydowanie wystarczyć.

W praktyce okazuje się jednak, że do DRY powinniśmy podchodzić pragmatycznie. Okazjonalne powielenie fragmentu kodu nie jest natychmiastowym przepisem na porażkę, a sposobem na unikanie niepotrzebnych powiązań i tzw. “couplingu”. Zdarza się, że powtórzony w dwóch miejscach fragment kodu tylko przez chwilę pozostaje identyczny, a po chwili jeden z wariantów zaczyna ewoluować w nowym kierunku. Budowanie abstrakcji i gotowych na wszystkie przyszłe rozszerzenia modułów nie zawsze jest rozwiązaniem optymalnym.

DRY można też wprowadzać stopniowo. Nie zawsze trzeba zaczynać od budowania prawdziwie reużywalnej, możliwej do pobrania biblioteki, którą umieścimy na zewnątrz projektu. Jeśli algorytm w projekcie powtarza się dwa razy, to można zacząć od przesunięcia go do dedykowanego modułu, który następnie dwukrotnie zaimportujemy. Oszczędzimy czas, unikniemy duplikacji i zyskamy moment na lepszą ocenę sytuacji.

**#SOLID** to z kolei zestaw pięciu zasad projektowania oprogramowania, które mówią o tym, że:

- Funkcja lub moduł powinny realizować jedno zadanie (Single Responsibility Principle)
    
- Kod powinien być otwarty na rozszerzenia i zamknięty na zmiany (Open-Closed Principle)
    
- Wymiana mniejszych fragmentów aplikacji nie powinna wymuszać aktualizacji całej architektury (Liskov Substitution Principle)
    
- Zamiast jednego ogólnego interfejsu stosuj kilka niezależnych od siebie (Interface Segregation Principle)
    
- Zewnętrzne zależności powinny być luźno powiązane z konsumentami i gotowe na wymianę (Dependency Inversion Principle)
    

O regułach SOLID napisano już dziesiątki artykułów i zakładamy, że prawdopodobnie nie spotykasz się z nimi po raz pierwszy w naszym kursie. Aby jednak sprawdzić, czy na pewno rozumiesz ich działanie, ćwiczenia na końcu tej lekcji pozwolą ci przetestować frontendowy SOLID w praktyce.

Jeśli reguły **SOLID** uważasz za mało przekonujące lub nie do końca odpowiadające twoim codziennym zadaniom, przyjrzyj się bliżej podejściu [**CUPID**](https://dannorth.net/cupid-for-joyful-coding/), które stawia na pierwszym miejscu przyjemność z kodowania.

W przeciwieństwie do mocno określonych zasad SOLIDnej piątki, CUPID to przede wszystkim “doświadczenia” i kierunek, w którym możesz stopniowo podążać refaktoryzując twój kod.

Autor podejścia #CUPID, Dan North, wyjaśnia to w ten sposób:

> “Properties define a goal or centre to move towards. Your code is only closer to or further from the centre, and there is always a clear direction of travel. You can use properties as a lens or filter to assess your code and you can decide which ones to address next.” - Dan North

Zobacz czym charakteryzuje się kod zgodny z CUPID:

- Composable - Kod łatwy do wykorzystania ponownie, z określonym przeznaczeniem
    
- [Unix Philosophy](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html) - Kod opierający się o małe, precyzyjne, łączące się ze sobą moduły
    
- Predictable - Kod robiący to, co na pierwszy rzut oka sugeruje jego architektura
    
- Idiomatic - Kod zgodny z ekosystemem i tradycją, w której powstał
    
- Domain-based - Kod korzystający z terminologii problemu, który rozwiązuje
    

W przeciwieństwie do reguł SOLID, CUPID nie skupia się na czarno-białym określeniu jakości kodu względem konkretnych praktyk. Jest to raczej pragmatyczny zestaw rekomendacji i celów, które powinniśmy sobie stawiać budując możliwe do utrzymania oprogramowanie, który zrozumie inny programista na podobnym do nas stanowisku.

Podobnie jak w przypadku reguł SOLID, zalecenia CUPID przetestujemy w sekcji ćwiczeń do tej lekcji.

### Zastosowanie na frontendzie

Wobec praktyk takich jak SOLID czy CUPID czasami pojawia się zarzut, że ich obiektowe (?) pochodzenie nie do końca łączy się z mocno funkcyjnym frontendem. Ile w tym prawdy?

**Komponenty wysokiej jakości**

Zacznijmy od komponentów, czyli podstawowej składowej współczesnych interfejsów użytkownika. W ich przypadku zdecydowanie powinniśmy stosować regułę “realizacji jednego zadania” oraz kompozycji w większą całość. Trudno wyobrazić sobie profesjonalną aplikację z jednym komponentem, który odpowiada za synchronizację całego interfejsu użytkownika. Nasz UI zwykle rozbijamy na mniejsze, możliwe do wymiany elementy. Zazwyczaj staramy się też odwzorować nazewnictwo domeny, w której te komponenty działają.

To nic innego jak trzy rekomendacje w jednym:

- Single Responsibility Principle (SOLID)
    
- Composability (CUPID)
    
- Domain-based naming (CUPID)
    
![[Pasted image 20240307145836.png]]
Planowanie nawet najprostszej struktury aplikacji to ćwiczenie, na które warto zdecydować się na początkowych etapach projektu. Pozwoli nam to określić konsekwencje takiego, a nie innego układu komponentów. Odkryjemy również wymagania związane ze stanem i przepływem danych, a cały zespół uzyska wspólne zrozumienie decyzji wpływających na skuteczne realizowanie projektu. Tę tematykę pogłębimy w ostatnim module poświęconym architekturze na frontendzie, a już w kolejnych lekcjach zobaczysz różne podejścia do zarządzania stanem, wynikające wprost z układu komponentów względem siebie.

A jeśli budujemy komunikację z API? Czy naprawdę biblioteki takie jak _axios_ lub _superagent_ powinny na nas wymuszać związanie się z nimi już na zawsze? Co w przypadku natywnego API _fetch_, które w pewnym momencie zaczęło być obowiązującym standardem? To właśnie czysty kod i wspomniane wyżej wzorce decydują o łatwości migracji do nowych standardów.

Jeśli nasze komponenty będą mocno powiązane z zewnętrznymi zależnościami, takimi jak konkretna biblioteka http, to przy jej ewentualnej aktualizacji będziemy mieć do wykonania mnóstwo pracy. Reguła odwrócenia zależności mówi, że tego typu zależności powinny być luźno powiązane z corem aplikacji i dostarczane z zewnątrz.

W przypadku Angulara, złamaniem tej zasady byłoby tworzenie instancji klienta http wewnątrz komponentu:

```typescript
class MyComponent {

  private http: HttpService = new AxiosService(); // złamanie Dependency Inversion

}
```

Zamiast tego, możemy polegać na wbudowanym systemie Dependency Injection, który umożliwia rozłączenie deklarowania zależności i korzystania z nich wewnątrz komponentów.

```typescript
class MyComponent {

  constructor(private http: HttpService) { ... } // zależność wstrzykiwana przez konstruktor

}

// --- Tworzenie nowej instancji wraz z zastosowaniem Dependency Injection:

const cmp = new MyComponent(new AxiosService()); // zazwyczaj realizowane przez framework
```

W przeciwieństwie do Angulara, React nie dostarcza natywnego systemu Dependency Injection, ale podobną separację komponentów i zależności możemy osiągnąć przez własne hooki.

W poniższym przykładzie komponent _ArticlesList_ korzysta z hooka _useArticlesClient_ który enkapsuluje (ukrywa) szczegóły implementacyjne pobierania danych. Dzięki temu zarówno sam hook można wykorzystać ponownie w innym komponencie, jak i sam komponent można w razie potrzeby łatwo przepiąć na inną bibliotekę http.

```typescript
import { ArticlePreview } from './ArticlePreview';
import { useArticlesClient } from './useArticlesClient';

export function ArticlesList() {
  const { articles, loading, error } = useArticlesClient();

  return (
    <>
      <h1 className="font-bold text-xl mb-4 text-gray-800">Articles</h1>
      {loading && <div>Loading...</div>}
      {error && <div>{error}</div>}
      <div className="flex flex-col space-y-2">
        {articles.map((article) => (
          <ArticlePreview key={article.id} {...article} />
        ))}
      </div>
    </>
  );
}
```

Wspomniany hook zobaczysz na przykładzie poniżej:

```typescript
import { useEffect, useState } from 'react';
import axios from 'axios';
import { Article, ArticleResponse } from './types';

export function useArticlesClient() {
  const [articles, setArticles] = useState<Article[]>([]);
  const [loading, setLoading] = useState<boolean>(false);
  const [error, setError] = useState<string>();

  useEffect(() => {
    setLoading(true);
    axios
      .get<ArticleResponse>(
        'http://localhost:3000/api/data/articles?timeout=2000'
      )
      .then(({ data: { articles } }) => {
        setArticles(articles);
      })
      .catch((error) => {
        setError('Cannot fetch articles!');
        console.error(error);
      })
      .finally(() => {
        setLoading(false);
      });
  }, []);

  return { articles, loading, error };
}
```

Dodatkową zaletą rozdzielania logiki biznesowej (hook) od warstwy widoku (komponent) jest refaktoryzacja kodu w kierunku jego testowalności. W ten wątek wejdziemy głębiej w drugim module, natomiast już teraz możesz zauważyć korzyści budowania funkcji, które nie są ściśle związane z konkretnym komponentem. W przypadku testowania pozwoli ci to unikać złożonej konfiguracji i inicjalizacji komponentów w testach, skupiając się na tym, co istotne z punktu widzenia wymagań biznesowych.

📝 Ten przykład znajdziesz w folderze **_examples/module1/lesson1/react-hooks_**.

**Komponent otwarty i zamknięty (jednocześnie)**

W teoretycznej części praktyk SOLID czytamy, że zgodność z Open-Closed Principle to tworzenie kodu:

- otwartego na rozszerzenia
    
- zamkniętego na zmiany
    

W jaki sposób jeden komponent może realizować oba te założenia jednocześnie? Czy nowe wymagania biznesowe nie powinny każdorazowo zmuszać programisty do modyfikacji wcześniej napisanych linijek kodu?

Okazuje się, że istnieją techniki łączące te pozornie sprzeczne wymagania. Zobacz, jak technika _render props_ pozwala zaimplementować rekomendację Open-Closed Principle:

Render props to jedna z wielu technik implementacji Open-Closed Principle w praktyce. Najważniejszy element tej rekomendacji dotyczy określenia tego, jakie fragmenty funkcji, modułu lub komponentu powinny być ukryte przed światem zewnętrznym, a jakie można konfigurować w dowolny sposób. Pisząc nasz kod w ten sposób minimalizujemy ryzyko wprowadzania błędów przy jednoczesnym zachowaniu oczekiwanej elastyczności. Win-win!

**Inspiracje systemami Unix**

CUPID wspomina o rozwijaniu kodu zgodnie z tzw. filozofią Unixa (Unix Philosophy). W systemach UNIXowych promowane są małe programy (awk, grep, tr, itd.), które przy pomocy operatora _pipe_ mogą przekazywać sobie nawzajem dane i łączyć się w realizacji większego zadania:

```bash
echo "1 4 6 8 10" | 
  tr ' ' '\n' |                  # Podział na wiele wierszy
  awk '{print $1*2}' |           # Mnożenie przez 2
  awk '$1<=10' |                 # Filtrowanie
  awk '{sum+=$1} END {print sum}' # Sumowanie
```

Naprawdę warto zastanowić się przez chwilę jak eleganckie jest to rozwiązanie. Narzędzia mają ściśle określoną rolę, muszą być odpowiednio elastyczne i otwarte na różne konteksty użycia, a wymiana lub ulepszenie jednego z nich nie zmusza nas do modyfikacji reszty (im mniej kodu musimy zmieniać, tym mniejsza szansa na wprowadzenie potencjalnych błędów).

Jak możemy się inspirować Unix Philosophy na frontendzie? Zamiast imperatywnych poleceń opisywanych krok po kroku (wyrażenia warunkowe, pętle for, etc.), na frontendzie przyjętą konwencją jest korzystanie z mikro-narzędzi i funkcji wyższego rzędu (_map, filter, reduce_), które możemy ze sobą łączyć.

Dzięki temu z kodu o takim kształcie…

```javascript
const numbers = [1, 4, 6, 8, 10];
let sum = 0;

for (let i = 0; i < numbers.length; i++) {
    const doubled = numbers[i] * 2;
    if (doubled <= 10) {
        sum += doubled;
    }
}

console.log(sum);
```

…możemy przejść na elegancki, deklaratywny łańcuch możliwych do łączenia funkcji:

```javascript
const numbers = [1, 4, 6, 8, 10];

const result = numbers
  .map(num => num * 2)
  .filter(num => num <= 10)
  .reduce((sum, num) => sum + num, 0);

console.log(result);
```

Pisząc kod w ten sposób, detale takie jak indeksy, warunki zatrzymania funkcji czy zmienne pomocnicze nie są nam potrzebne. Znowu - im mniejsza złożoność kodu, tym mniej okazji do popełniania błędów.

Nie zawsze uzyskamy w ten sposób kod bardziej wydajny (liczba wykonań pętli się zwiększa), ale często zdecydowanie łatwiejszy w utrzymaniu.

Korzyści wynikające ze stosowania praktyk takich jak SOLID czy CUPID docenia z biegiem czasu niemal każdy programista. Chociaż nie są to zasady wymuszane przez środowisko programistyczne, a ich złamanie nie grozi odebraniem licencji na programowanie, przyjmuje się je za wskaźnik oprogramowania wysokiej jakości.

## Wzorce projektowe na frontendzie

Podobie sprawa wygląda z wzorcami projektowymi. Nie jest to ostateczny cel rozwijania kodu frontendowego, ale raczej zestaw narzędzi, z których możesz - ale nie musisz - korzystać.

Tak się składa, że unikalne wyzwania i cechy charakterystyczne dla tej warstwy aplikacji rozwiązano już w przeszłości wielokrotnie, więc możesz na tych pomysłach polegać, lub (na własną odpowiedzialność) ignorować, ponosząc wszystkie koszty takiej decyzji.

Chociaż szczegółowo w temat wzorców wejdziemy w kolejnych lekcjach, to na wstępnie chcielibyśmy krótko uzasadnić potrzebę ich stosowania w codziennej pracy:

- **Zarządzanie stanem** - Frontend często musi radzić sobie z dynamicznie zmieniającym się stanem aplikacji, który jest reakcją na interakcje użytkownika oraz dane przychodzące z backendu. Wzorce takie jak Flux lub Redux pomagają w organizacji i przewidywaniu zmian w stanie, zapewniając jednokierunkowy przepływ danych. To z kolei ułatwia śledzenie, debugowanie i testowanie stanu aplikacji.
    
- **Reakcja na zdarzenia** - Frontend wymaga obsługi zdarzeń generowanych przez użytkownika (np. kliknięcia, przewijanie) oraz na skutek śledzenia zewnętrznych źródeł danych. Wzorce takie jak Obserwator lub Pub/Sub umożliwiają zarządzanie tymi zdarzeniami w sposób zdecentralizowany, bez konieczności tworzenia skomplikowanych łańcuchów zależności między komponentami.
    
- **Asynchroniczność -** Środowisko przeglądarki jest z natury asynchroniczne i zdarzeniowe. Przeglądarka musi równocześnie obsługiwać wiele zadań, takich jak renderowanie interfejsu użytkownika, przetwarzanie zdarzeń od użytkownika oraz wykonywanie kodu JavaScript. Asynchroniczny kod staje się niezbędny w sytuacjach, gdy działania, takie jak zapytania sieciowe, odczytywanie plików lub inne operacje I/O, mogą trwać dłużej. Wzorce pracy z asynchronicznym kodem pozwalają zachować nad nim kontrolę.
    
- **Złożoność projektów** - Współczesne aplikacje frontendowe składają się z wielu modułów i komponentów. Nikogo nie dziwi już realizowanie pełnoprawnych, rozbudowanych aplikacji z logiką biznesową w warstwie przeglądarki. Wzorce projektowe takie jak Kompozycja, Moduł, czy Fabryka pozwalają na projektowanie kodu w sposób modularny, co ułatwia jego ponowne wykorzystanie i utrzymanie. Dzięki temu, możesz tworzyć bardziej zorganizowane, skalowalne i łatwiejsze w utrzymaniu aplikacje, co jest kluczowe przy pracy nad dużymi projektami.
    
- **Wybór stacku technologicznego** - Zrozumienie wzorców projektowych w praktyce frontendowej może znacznie ułatwić dobór odpowiedniego narzędzia do problemu, który próbujesz rozwiązać. Widać to chociażby na przykładzie reaktywności i śledzenia zmian, gdzie konkurują ze sobą podejścia oparte o Virtual DOM, RxJS albo Signals. Możesz decydować się na frameworki wprost korzystające z systemu wstrzykiwania zależności, albo takie, które tego rozwiązania nie stosują. Optymalne rozwiązanie możesz wybrać samemu, zamiast polegania na argumentach pokroju “zaufaj mi”.
    

### Refaktoryzacja kodu zastanego

Wraz ze wzrostem doświadczenia będziesz poznawał kolejne wzorce i dobre praktyki, które pozytywnie wpływają na całościową jakość projektu. W pewnym momencie może pojawić się dylemat - czy wprowadzać je stopniowo, zaczynając od najmniejszych możliwych części projektu, czy może postawić na duży refaktoring (czyli proces podnoszenia jakości kodu w aplikacji), który zacznie się już na samej górze drzewa komponentów?

Oba podejścia mają swoje plusy i minusy, a szczegóły poznasz poniżej:

### **Podejście “Top-down”**

Na całościowe przepisanie aplikacji decydujemy się zazwyczaj wtedy, kiedy sytuacja jest naprawdę poważna, lub kiedy chcemy wprowadzić radykalne usprawnienia np. na poziomie stacku technologicznego (wymiana frameworka). W tym podejściu nowa, ulepszona wersja aplikacji powstaje niezależnie od tej wdrożonej na produkcji. W momencie, kiedy funkcjonalności są odwzorowane 1:1 można zadecydować o zastąpieniu poprzedniej wersji aplikacji tą nową, z lepszą architekturą lub nowoczesnymi fundamentami.

**Plusy tego podejścia:**

- przestrzeń na wdrożenie istotnej zmiany architektury i stosu technologicznego
    
- kontynuacja pracy nad aktualną wersją aplikacji przebiega bez zakłóceń
    
- część zespołu może skupić się na nowym, niezależnym projekcie
    

**Minusy tego podejścia:**

- długi czas trwania całego projektu, od jego rozpoczęcia do wdrożenia na produkcję
    
- wymagane utrzymywanie dwóch spójnych wersji aplikacji - starej i nowej
    
- ryzyko zmiany planów i porzucenia projektu przed wdrożeniem na produkcję
    

### **Podejście “Bottom-up”**

W tym podejściu core naszej aplikacji pozostaje stabilny, a my skupiamy się na ulepszaniu najmniejszych możliwych elementów aplikacji. W przypadku frontendu i interfejsów użytkownika, dobrze rozumianą granicą zmian jest poziom pojedynczego komponentu. Oczywiście nie musimy pozostać na jednym komponencie, ale możemy tutaj zmieniać zestaw kilku współpracujących ze sobą elementów.

**Plusy tego podejścia:**

- możliwość ciągłego i regularnego wdrażania usprawnień aplikacji na produkcję
    
- mniejsze ryzyko “rozjazdu” dwóch alternatywnych wersji aplikacji (por. podejście top-down)
    
- łatwiejszy model pracy dla mniejszych zespołów o ograniczonych zasobach
    

**Minusy tego podejścia:**

- duże błędy na poziomie architektury mogą być niemożliwe do usunięcia
    
- skupiając się na lokalnych usprawnieniach możemy stracić z oczu całościowy obraz projektu
    
- czas przeznaczany na zmiany lokalne może nie dawać odczuwalnych korzyści dla użytkownika
    

### **Które podejście wybrać?**

Chociaż oba podejścia mają swoje plusy i minusy, to zgodnie ze zwinnymi praktykami rozwoju oprogramowania zdecydowanie łatwiej realizować refaktoryzację w podejściu bottom-up. Pozwala ona na bardziej elastyczny model wdrażania zmian, nie wymaga tak dużego narzutu komunikacyjnego jak podejście top-down i zmniejsza wymagany próg wejścia dla tych programistów, którzy chcą w projekcie dodać coś od siebie. Model komponentowy, który jest obecnym standardem budowania frontendu, ułatwia wdrażanie zmian właśnie w tym modelu, a komponenty wyznaczają granicę refaktoryzacji, nad którą pracujemy.

Radykalne zmiany architektury, wymiana frameworka lub całych fundamentów aplikacji (tak jak w top-down) to zdecydowanie większe ryzyko, trudniejsze dyskusje z przełożonymi i potencjalnie oddalająca się linia mety, której czasami nigdy nie uda się przekroczyć. Właśnie dlatego przepisywanie i wymiana całych aplikacji to najbardziej radykalny krok, którego wielu doświadczonych programistów stara się zupełnie unikać.

## Podsumowanie

W naszym kursie podkreślamy, że wzorce projektowe i opisywane tutaj praktyki to tylko i wyłącznie narzędzia, a nie cele twojej przygody z programowaniem. Można je traktować jak obszerne notatki i podsumowania eksperymentów, które pozostawili po sobie bardziej doświadczeni programiści z przeszłości.

Poznając i stosując te najbardziej użyteczne wzorce, oszczędzasz cenny czas i energię. Zamiast odkrywać koło na nowo, możesz w swoich projektach stosować gotowe przepisy na rozwiązania problemów z którymi spotykano się już wielokrotnie.

Zanim zdecydujesz się z nich zrezygnować, ważne jest abyś rozumiał, dlaczego zostały one opracowane i jaka była oryginalna intencja autora. Ta wiedza pozwoli Ci dokonać przemyślanych wyborów na poziomie stacku technologicznego, projektowania architektury czy implementowania nowych wymagań biznesowych.

W kolejnych dwóch lekcjach poznasz najbardziej użyteczne wzorce i praktyki, które umożliwią ci efektywne zarządzanie stanem lokalnym i globalnym twojej aplikacji.

Na koniec zachęcamy również do przesłuchania [rozmowy z Wiktorem Jamro](https://www.youtube.com/live/KaDMmOzH98U), jednym z ekspertów kursu Opanuj Frontend, który niedawno przekazywał nam najważniejsze doświadczenia i lekcje z niemal dwóch dekad pracy pracy w warstwie frontendu.

👉 [https://www.youtube.com/live/KaDMmOzH98U](https://www.youtube.com/live/KaDMmOzH98U) 👈

---

## 🧑‍💻 Ćwiczenia praktyczne

- Przeprowadź refaktoryzację kodu w przykładzie **examples/module1/lesson1/validate-it**
    
    - Aplikacja nie działa poprawnie - co jest tego powodem i jak to naprawić?
        
    - Aplikacja robi się co raz trudniejsza w utrzymaniu - spróbuj ułatwić zrozumienie tego kodu innym programistom w zespole poprzez lepszą organizację kodu.
        
    - Jak sprawić, żeby dodawanie i usuwanie kolejnych reguł walidacji nie wpływało na każdorazową edycję funkcji do walidacji?
        
- Przeprowadź refaktoryzację kodu w przykładzie **examples/module1/lesson1/solver**
    
    - Jeśli nie pracowałeś do tej pory z Reactem, skup się na tych fragmentach projektu, które nie są ściśle powiązane z samym frameworkiem (np. style i logika biznesowa).
        
    - Jakie trzy usprawnienia wprowadzisz, aby ułatwić dalszy rozwój projektu?
        
    - Czy uda ci się znaleźć więcej okazji do refaktoryzacji tej aplikacji?
        
    - Jak wprowadzić obsługę błędów na wypadek niepoprawnych danych wejściowych?
        

## 📚 Materiały dodatkowe

Poniżej znajdziesz materiały poszerzające wiedzę zawartą w tej lekcji:

- Czym jest ECMA Script? - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/JavaScript_technologies_overview](https://developer.mozilla.org/en-US/docs/Web/JavaScript/JavaScript_technologies_overview)
    
- Dependency Inversion - [https://blog.logrocket.com/dependency-inversion-principle-typescript/](https://blog.logrocket.com/dependency-inversion-principle-typescript/)
    
- Zdroworozsądkowe zasady programowania - [https://grugbrain.dev/](https://grugbrain.dev/)
    
- Zrozumieć filozofię oprogramowania - [https://lubimyczytac.pl/ksiazka/4902573/a-philosophy-of-software-design](https://lubimyczytac.pl/ksiazka/4902573/a-philosophy-of-software-design)
    
- Struktura komponentów kontra złożoność - [https://epicreact.dev/one-react-mistake-thats-slowing-you-down/](https://epicreact.dev/one-react-mistake-thats-slowing-you-down/)
    

## 🛟 Pomoc

Jeśli potrzebujesz pomocy, skorzystaj z sekcji komentarzy do tej lekcji lub napisz wiadomość na ogólnym czacie dla uczestników kursu - .

Pomożemy tak szybko, jak to możliwe - powodzenia!