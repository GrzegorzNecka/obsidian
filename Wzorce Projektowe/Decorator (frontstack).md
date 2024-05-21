
#Dekorator najczęściej będzie nową klasą (obiektem), implementującą ten sam interfejs co klasa bazowa. Dzięki temu zachowamy kompatybilność z istniejącym już kodem klienckim, a także będziemy w stanie korzystać w ten sam sposób zarówno z klasy bez, jak i z dekoratorem. Oczywiście nic nie stoi na przeszkodzie, aby klasa bazowa została „opakowana” w kilka dekoratorów. Dzięki takiemu podejściu możemy utrzymać porządek w kodzie, delegując każdej klasie tylko jedno zadanie i dynamicznie aplikować różne dekoratory w zależności od naszych potrzeb.

Nakładka może wpłynąć na wynik wywołania dekorowanej klasy (klasy głównej), wykonując coś przed, albo po przekazaniu do niej żądania. Wzorzec ten może być już znany osobom, które jeszcze w czasach pre-hookowych korzystały z biblioteki [react-redux](https://react-redux.js.org/) oraz metody [`connect()`](https://react-redux.js.org/api/connect). Metoda ta jest funkcją wyższego rzędu, która przyjmuje komponent jako argument, zawija na niego pewne właściwości (propsy) i zwraca inny komponent, który posiada pierwotne oraz dodatkowe właściwości. W tym przypadku `connect()` dekoruje nam komponent Reacta.

## Cienki, kurczak, mieszany"

Wyobraźmy sobie teraz, iż tworzymy prosty system zamówień i rozliczeń dla lokalnej budki z kebabami (mam nadzieję, że macie naprawdę bujną wyobraźnię 😉). Tak długo, jak właściciel będzie serwował najpopularniejszy w Polsce zestaw „na cienkim z kurczakiem, sos mieszany”, wszystko damy radę załatwić jedną klasą – `Kebab`. Jeżeli jednak do serwowanej kanapki będziemy mogli dokupić dodatkowe rzeczy, wtedy możemy dodawać kolejny metody do głównej klasy (np. `makeKebabWithCokeAndFries()`, `makeKebabButFalafel()`) bądź tworzyć nowe podklasy klasy `Kebab`. Nie jest to jednak najbardziej skalowalne rozwiązanie – dużo lepiej skorzystać tutaj z kilku dekoratorów. Dzięki temu naszą główną klasę (tworzącą kebaba) będziemy mogli rozszerzać o wybrane przez klienta dodatki.

![](https://www.frontstack.pl/blog/decorator-design-pattern/kebs.gif)

Na poniższym przykładzie mamy pokazany mały wycinek z aplikacji, która mogłaby być wdrożona do systemu zarządzania zamówieniami w restauracji. Bazowa klasa jest odpowiedzialna za wygenerowanie elementów potrzebnych do przygotowania głównego dania i obliczenia jego ceny. Poza klasą główną posiadamy również dekoratory, które to rozszerzają nam listę potrzebnych składników i do ceny dania głównego dodają cenę dodatków.


```ts
/**
 * Klasa bazowa. Może ona istnieć samodzielnie bądź być dekorowana
 * przez inne klasy.
 */

class KebabSet {
  constructor() {
    this.ingridients = ["kebab"];
    this.price = 15;
  }

  /**

   * Metody "getSetItems" oraz "getPrice" występują zarówno
   * na klasie bazowej jak i na dekoratorach, aby zachować
   * spójność interfejsów.

   */

  getSetItems() {
    return this.ingridients;
  }

  getPrice() {
    return this.price;
  }

}

/**
 * Pomocnicza klasa z której to będziemy tworzyć przyszłe
 * dekoratory. Nie musimy dzięki temu ciągle powtarzać
 * pisania metod "getSetItems" oraz "getPrice".

 */

class SetAddOn {
  constructor(kebabSet) {
    this.ingridients = [];
    this.price = 0;
    this.kebabSet = kebabSet;
  }

  getSetItems() {
    return [...this.kebabSet.getSetItems(), ...this.ingridients];
  }

  getPrice() {
    return this.kebabSet.getPrice() + this.price;
  }
}

/**
 * Dekorator "Fries" dodaje do zestawu frytki.
 */

class Fries extends SetAddOn {
  constructor(kebabSet) {
    super();
    this.ingridients = ["fries"];
    this.price = 5;
    this.kebabSet = kebabSet;
  }
}

/**
 * Dekorator "Coke" dodaje do zestawu napój.
 */

class Coke extends SetAddOn {
  constructor(kebabSet) {
    super();
    this.ingridients = ["coke"];
    this.price = 7;
    this.kebabSet = kebabSet;
  }
}

/**
 * Kod kliencki.
 * Komponujemy zestaw na bieżąco "dekorując"
 * bazową część zestawu wybranymi dodatkami.
 */

console.log("1. Kebab only:");

const kebabSet = new KebabSet();
console.log(kebabSet.getSetItems())
console.log("Price:", kebabSet.getPrice());
console.log("2. Kebab set with fries");

const withFries = new Fries(kebabSet);
// albo const withFries = new Fries(new KebabSet());
console.log(withFries.getSetItems());
console.log("Price:", withFries.getPrice());
console.log("3. Kebab set with fries and coke");

const withFriesAndCoke = new Coke(new Fries(kebabSet));
console.log(withFriesAndCoke.getSetItems());
console.log("Price:", withFriesAndCoke.getPrice());
console.log("4. Kebab set with coke");

const withCoke = new Coke(kebabSet);
console.log(withCoke.getSetItems());
console.log("Price:", withCoke.getPrice());
```

W wyniku wywołania powyższego kodu otrzymamy następujący wynik:

![[Pasted image 20240521102808.png]]


## Wady i ograniczenia

Mimo że Decorator Design Pattern jest potężnym narzędziem, które może znacząco poprawić skalowalność i modularność kodu, nie jest pozbawione wad i ograniczeń. Oto kilka z nich:

- **Złożoność:** Dekoratory mogą zwiększać złożoność kodu, szczególnie w przypadku dużych ilości zagnieżdżonych dekoratorów. Mogą również sprawiać trudności przy debugowaniu, ponieważ zachowanie może być rozproszone między wieloma dekoratorami.
- **Zachowanie interfejsu:** Dekoratory muszą implementować ten sam interfejs co dekorowane obiekty. Oznacza to, że jeśli dekorowany obiekt zmieni swój interfejs, wszystkie jego dekoratory muszą również zostać zaktualizowane.
- **Kontrola nad procesem:** Dekorator nie ma kontroli nad tym, kiedy metoda dekorowanego obiektu zostanie wywołana. Jeżeli ta kontrola jest potrzebna, warto rozważyć inne wzorce, takie jak Mediator czy Observer.
- **Problem identyfikacji obiektu:** Kiedy obiekt jest opakowany w dekorator, jego oryginalna tożsamość może zostać ukryta. W praktyce, może to prowadzić do problemów, gdy potrzebujemy porównać obiekty lub sprawdzić ich typy.


