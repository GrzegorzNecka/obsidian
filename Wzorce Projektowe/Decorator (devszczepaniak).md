## Charakterystyka wzorca projektowego Dekorator

#Dekorator Dekorator jest jednym ze strukturalnych wzorców projektowych. Jego zadaniem jest _„udekorowanie”_ danej klasy, metody właściwości czy parametru. Przez _„dekorowanie”_  rozumiane jest rozszerzenie funkcjonalności dekorowanych komponentów w dynamiczny sposób. Ponadto dekoratory pozwalają na uniknięcie dziedziczenia, przez co fani zasady _composition over inheritance_ (do których się zaliczam) powinni być zadowoleni.

Chcąc znaleźć analogie do życia codziennego, nie trzeba długo szukać:

- dodawanie składników (mleko, cukier) do kawy;
- dodawanie składników na pizzę;
- pakowanie przedmiotu w kilka kartonowych pudełek;
- matrioszki;
- dekorowanie choinki na święta.

Poniżej przedstawiony został prosty diagram obrazujący ideę wzorca projektowego Dekorator.

![[Pasted image 20240521084224.png]]

Wzorzec Dekorator pozwala na wielokrotne dekorowanie tego samego obiektu, przez co możliwe jest dynamiczne konstruowanie złożonych komponentów, z zachowaniem prostoty i spełniając jednocześnie zasadę _Single Responsibility Principle_. Nieistotne z punktu widzenia logiki biznesowej elementy aplikacji mogą zostać wydelegowane do dekoratorów.

Mówiąc o zaletach, warto wspomnieć też o wadach. Fragmenty kodu wykorzystujące kilka dekoratorów mogą zachowywać się inaczej lub nie działać poprawnie w zależności od kolejności dekorowania. Przeanalizuj poniższy przykład. Pierwszym wywołanym dekoratorem jest ten fizycznie najbliższy słowu kluczowemu `function`, a zachowanie udekorowanej funkcji jest podobne do zachowania [złożeń funkcji w matematyce](https://en.wikipedia.org/wiki/Function_composition).

```ts
@make_bold() // Wraps text in <b> tag.
@add_prefix() // Adds [PREFIX] prefix.
function hello() {
    return 'Hello, World!';
}

@add_prefix()
@make_bold()
function hello2() {
    return 'Hello, World!';
}

console.log( hello() ) // '<b>[PREFIX]Hello, World!</b>'
console.log( hello2() ) // '[PREFIX]<b>Hello, World!</b>'
```

Funkcje dekorujące w powyższym przykładzie zaczynają się znakiem `@`. Jest to dość często spotykany _syntactic sugar_. Nie jest to konieczne, choć niewątpliwie zwiększa czytelność.  Inna, równie często spotykana w programowaniu obiektowym implementacja dekoratora, wykorzystuje przekazanie instancji obiektu do udekorowania jako parametr klasy dekorującej.


```ts
const decoratedHandler = new BasicAuthDecorator(
    new HttpGetHandlerDecorator(
        new Handler()
    )
);
```

Dekorowanie może również przysporzyć problemów podczas testowania dekorowanego fragmentu kodu. Tworząc testy dla funkcji `hello` i `hello2` konieczne będzie uwzględnienie działania dekoratorów w testowanym kodzie.

### Przykłady wykorzystania wzorca Dekorator w praktyce

Szukanie przypadków użycia Dekoratora w programowaniu również nie jest szczególnie trudnym wyzwaniem. Przykładem frameworka czerpiącego z zalet wzorca Dekorator pełnymi garściami jest NestJS. Dla niewtajemniczonych w środowisko Node.js NestJS jest jednym z [popularniejszych](https://kinsta.com/knowledgebase/nestjs/) rozwiązań dedykowanych tworzeniu aplikacji backendowych w Node.js. Twórcy NestJS wykorzystują Dekoratory zarówno do dynamicznego rozszerzania tworzonych komponentów, jak i do unikania dziedziczenia. Fajnie to widać na przykładzie kodu przykładowego kontrolera.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}
```

W NestJS Dekoratory rozpoczynają się znakiem `@` i definiowane są nad linią, której dotyczą. Bazowa funkcjonalność kontrolera została ukryta w dekoratorze `@Controller` przyjmującego nazwę zasobu jako parametr. Dzięki temu rejestracja klasy `CatsController` w aplikacji i przypisanie kontrolerowi wymaganych metadanych nie wymaga tworzenia klasy bazowej `Controller` i dziedziczenia po niej.

> Decorators associate classes with required metadata and enable Nest to create a routing map

Z kolei dekorator `@Get` rozszerza metodę `findAll` o informację o wykorzystywanej metodzie HTTP i tworzy handler dla dedykowanego endpointu HTTP.

> The `@Get()` HTTP request method decorator before the `findAll()` method tells Nest to create a handler for a specific endpoint for HTTP requests.

Zachęcam Cię do sprawdzenia strony z [dokumentacją dla kontrolerów w NestJS](https://docs.nestjs.com/controllers), jak również dokumentacji NestJS w ogóle. Nawet jeśli nie interesuje Cię sam framework, to przykłady w dokumentacji idealnie oddają ideę tego wzorca projektowego.

Zachęcam Cię do sprawdzenia strony z [dokumentacją dla kontrolerów w NestJS](https://docs.nestjs.com/controllers), jak również dokumentacji NestJS w ogóle. Nawet jeśli nie interesuje Cię sam framework, to przykłady w dokumentacji idealnie oddają ideę tego wzorca projektowego.

Chcąc skorzystać z dekoratorów w TypeScript, wystarczy włączyć je, korzystając z opcji konfiguracyjnej `experimentalDecorators`. Możesz przekazać ją przy transpilacji lub dodać klucz z wartością `true` w pliku `tsconfig.json`. Po włączeniu dekoratorów można z nich już korzystać, tak jak to opisano [w dokumentacji TypeScript](https://www.typescriptlang.org/docs/handbook/decorators.html). Poniżej znajdziesz praktyczny przykład prostego Handlera, którego metoda handle została udekorowana metodą logującą dane wejściowe.

```typescript

// dekorator
function logParams() {
  return function (
    target: unknown, //to obiekt klasy `Handler`
    propertyKey: string, // nazwa udekorowanej metody
    descriptor: PropertyDescriptor // instancja property descriptora metody `handle`
  ) {
  
    const originalMethod = descriptor.value;

    descriptor.value = function ( ...args: unknown[] ) {
      console.log(
        'Handler called with params:',
        args[ 0 ]
      );

      return originalMethod.apply( this, args );
    };
  };
}

class Handler {
  @logParams()
  handle( params: Record<string, unknown> ) {
    params.bar = 'baz';

    console.log( params );
  }
}

const handler = new Handler();

handler.handle( { foo: 'bar' } );
```

Funkcja zwracana przez funkcję dekorującą ma przekazane parametry, pozwalające na uzyskanie informacji skąd dekorator został wywołany. W przedstawionym przykładzie `target` to obiekt klasy `Handler`, `propertyKey` to nazwa udekorowanej metody a `descriptor` jest instancją [property descriptora](https://devszczepaniak.pl/property-descriptors-w-javascript/) metody `handle`. Zwróć szczególną uwagę, że dekorator zwraca funkcję, która zostanie wywołana w momencie dekorowania. Wszystko powyżej słowa kluczowego return zostanie wywołane przed udekorowaniem metody handle. Przeanalizuj poniższy przykład i zobacz, w jakiej kolejności logowane są poszczególne wiadomości.

```typescript

function decorator1() {
  console.log( 'decorator1 outer' );
 
  return function (
  target: unknown,
  propertyKey: string,
  descriptor: PropertyDescriptor
) {
    console.log( 'decorator1 inner' );
  };
}


 
function decorator2() {
  console.log( 'decorator2 outer' );
  
  return function (
    target: unknown,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    console.log( 'decorator2 inner' );
  };
}



class Handler {
  @decorator1()
  @decorator2()
  handle() {
    console.log( 'handler' );
  }
}

const handler = new Handler();

handler.handle();

// "decorator1 outer" 
// "decorator2 outer" 
// "decorator2 inner" 
// "decorator1 inner" 
// "handler" 
```

Aby udekorować parametry metod i właściwości klas w TypeScript, niezbędne będzie skorzystanie z metadata API, które na moment publikacji tego artykułu również [znajduje się w fazie kandydata](https://github.com/tc39/proposal-decorator-metadata). Aby skorzystać z metadata API konieczna będzie instalacja biblioteki `reflect-metadata`, która jest polyfillem na wspomniane API. By skorzystać z metadata API konieczne będzie włączenie go flagą `emitDecoratorMetadata` w konfiguracji projektu lub przy transpilacji. Po zaimportowaniu polyfilla klauzulą `import "reflect-metadata"` możliwości przy definiowaniu dekoratorów są nieco większe. Dekorowanie parametrów i właściwości pozwala np. na przeniesienie ich walidacji do dekoratora. Innym praktycznym przykładem wykorzystania dekoratorów, z którym spotykam się na co dzień, jest definiowanie struktury wiadomości dla wiadomości serializowanych do formatu zgodnego z [Protocol Buffers](https://protobuf.dev/). Dekoratory wykorzystywane są do zdefiniowania indeksów pól oraz ich typów. Dzięki temu możliwa jest serializacja, przesłanie wiadomości z punktu A do punktu B, a następnie deserializacja wiadomości.

### Materiały dodatkowe i źródła

- [Design Patterns: Elements of Reusable Object-Oriented Software – Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides (1994)](https://helion.pl/view/24853c/ksiazki/wzorce-projektowe-elementy-oprogramowania-obiektowego-wielokrotnego-uzytku-erich-gamma-richard-helm-ralph-johnson-john-vli,wzoevv.htm#format/d)
- [Design Patterns for Web Development](https://dev.to/writescode/design-patterns-for-frontend-developers-2ii3)
- [Decorator Design Pattern](https://sourcemaking.com/design_patterns/decorator)
- [What Is Nest.js? A Look at the Lightweight JavaScript Framework](https://kinsta.com/knowledgebase/nestjs/)
- [Why use @Decorators?](https://www.reddit.com/r/learnpython/comments/60fj9b/why_use_decorators/)
- [NestJS – Controllers](https://docs.nestjs.com/controllers)
- [Composition vs Inheritance](https://www.digitalocean.com/community/tutorials/composition-vs-inheritance)
- [Python Decorators](https://wiki.python.org/moin/PythonDecorators)
- [C# Corner – Decorator Design Pattern](https://www.c-sharpcorner.com/article/decorator-design-pattern2/)
- [JavaScript metaprogramming with the 2022-03 decorators API](https://2ality.com/2022/10/javascript-decorators.html)
- [Design patterns cheat](https://blog.bytebytego.com/p/ep17-design-patterns-cheat-sheet)
- [TypeScript Docs – Decorators](https://www.typescriptlang.org/docs/handbook/decorators.html)
- [Decorators for ES6 classes – TC39 proposal](https://github.com/tc39/proposal-decorators)
- [Decorator metadata – TC39 proposal](https://github.com/tc39/proposal-decorator-metadata)
- [Metadata Reflection API](https://github.com/rbuckton/reflect-metadata)
- [Is Inheritance Dead? A Detailed Look Into the Decorator Pattern](https://dzone.com/articles/is-inheritance-dead)




