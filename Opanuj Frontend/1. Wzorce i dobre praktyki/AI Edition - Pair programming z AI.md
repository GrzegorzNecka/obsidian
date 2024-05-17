## Wprowadzenie

W pierwszej lekcji z cyklu “AI Edition” zobaczysz jak wykorzystać narzędzia oparte o Sztuczną Inteligencję w procesie pair programmingu, czyli programowania w parach.

Przedstawimy ci kilka aspektów współpracy z ChatemGPT i Copilotem, które mogą okazać się lekarstwem na klasyczne problemy związane z programowaniem wieloosobowym.
## Programowanie w trybie multi-player

**Jak to się zaczęło i dlaczego warto?**

Pair programming, czyli programowanie w parach, to metoda współpracy, która wywodzi się z tzw. programowania ekstremalnego (Extreme Programming, XP), czyli podejścia do inżynierii oprogramowania wprowadzonego w latach 90. przez Kenta Becka.

XP zostało zaprojektowane aby poprawić jakość oprogramowania oraz reagować na zmienne wymagania klientów poprzez stosowanie krótkich cykli rozwojowych, ciągłej integracji, testów automatycznych i właśnie programowania w parach. Od tego czasu, metoda ta ewoluowała i zaczęła być stosowana nie tylko w ramach ekstremalnego programowania, ale jako niezależna praktyka w wielu projektach i organizacjach na całym świecie.

W metodzie **pair programmingu** dwoje programistów pracuje razem przy jednym komputerze, z czego jeden, "pilot", pisze kod, a drugi, "nawigator", koncentruje się na strategii i przeglądzie kodu, sugerując usprawnienia i rozwiązania.

Ta współpraca sprzyja nie tylko wzajemnej wymianie wiedzy i doświadczeń, ale także prowadzi do tworzenia kodu o wyższej jakości, ponieważ każdy nowy fragment kodu i każdy nowy pomysł są od razu weryfikowane przez drugą osobę. Ponadto, programowanie w parach ma być rozwiązaniem problemu “blokowania się”, czyli sytuacji, w której dochodzimy do granicy naszego rozumowania lub rozumienia problemu. Bywa, że taką granicę lub “ścianę” możemy przekroczyć jedynie dzięki innej perspektywie.

Korzyści płynące z pair programmingu są opisywane w wielu branżowych publikacjach i dotyczą zarówno aspektów technicznych, jak i miękkich. Metoda ta umożliwia lepsze zrozumienie zadania i wymagań, co przekłada się na wyższą jakość oprogramowania. Poprzez bezpośrednią współpracę, programiści rozwijają również swoje umiejętności komunikacyjne i interpersonalne, co jest kluczowe w pracy zespołowej. Warto zauważyć, że pair programming jest wykorzystywany nie tylko do codziennej pracy nad kodem, ale również jako narzędzie szkoleniowe, pomagając nowym członkom zespołu szybciej wdrożyć się w projekt i podnieść swoje kompetencje techniczne (zob. [buddy](https://rasa.com/blog/what-does-it-mean-to-be-an-engineering-buddy-at-rasa/)).

W kontekście historii rozwoju praktyki, pair programming ugruntował swoją pozycję jako ważny element kultury programistycznej, który przyczynia się do budowania lepszego oprogramowania i zespołów programistycznych. Jego adaptacja w różnych środowiskach i projektach pokazuje jednak, że jej wdrożenie nie jest tak oczywiste, jak mogłoby się wydawać.

**Wyzwania pair programmingu**

Nietrudno zauważyć, że wielu z nas - programistów - ceni sobie bardziej prywatne i dyskretne warunki pracy nad kodem. Mamy swoje przyzwyczajenia i nawyki, mamy konkretne skróty klawiszowe, konkretne preferencje co do środowiska pracy i czasu, który na tę pracę poświęcamy.

Zapraszając do biurka drugą osobę (lub organizując ten proces w formie zdalnej), automatycznie pojawia się potrzeba rozwiązania kilku wyzwań programowania w trybie multi-player.

**Zmiana przyzwyczajeń -** Jednym z pierwszych wyzwań jest naturalny opór przed zmianą, który może pojawić się wśród programistów przyzwyczajonych do samodzielnej pracy. Przejście na współpracę w parach może budzić obawy dotyczące utraty autonomii, presji ciągłej obecności innego człowieka, a nawet strachu przed oceną.

**Dopasowanie charakterów i umiejętności -** Wyzwaniem może być również znalezienie odpowiednich par programistów, tak aby obie strony czuły, że uczą się i rozwijają. Pary z dużą dysproporcją w poziomie doświadczenia mogą prowadzić do frustracji zarówno mniej, jak i bardziej doświadczonych programistów.

**Narzut komunikacyjny -** Pair programming wymaga odpowiedniego zarządzania czasem, aby nie doprowadzić do wypalenia zespołu. Istnieje ryzyko, że niektórzy pracownicy mogą odczuwać zmęczenie wynikające z konieczności ciągłej interakcji i współpracy.

**Nowa organizacja pracy -** Efektywne wdrożenie pair programmingu często wymaga również zmian w aranżacji przestrzeni pracy, aby umożliwić wygodną i produktywną współpracę. Niewłaściwe środowisko może hamować komunikację i współpracę.

**Kultura w firmie -** Niektóre organizacje mogą początkowo postrzegać tę metodę jako mniej wydajną, ponieważ angażuje dwie osoby do wykonania zadania, które tradycyjnie wykonuje jedna osoba. Zwiększenie kosztów jest często wskazywane jako bariera, szczególnie w krótkiej perspektywie. Organizacje muszą być przekonane o długoterminowych korzyściach płynących z pair programmingu, takich jak poprawa jakości kodu czy szybsze wprowadzanie nowych członków zespołu, aby uzasadnić początkowe inwestycje w czas i zasoby.

Po kilku latach spędzonych w branży nietrudno zauważyć, że pair programming to jedna z technik, wokół której narosło tyle samo obietnic korzyści, co wątpliwości i oporów. Zdajemy sobie sprawę, że wiele firm - czy to ze względu na filozofię pracy czy pozorne straty czasowe - nie chce zezwolić na jej implementację lub nie wie, jak zrobić to skutecznie.

Właśnie dlatego w tej lekcji sprawdzimy, czy Sztuczna Inteligencja może pełnić rolę asystenta programisty i ułatwić uzyskiwanie korzyści z pair programmingu.

## AI - asystent, czy źródło problemów?

Zanim wejdziemy w konkretne scenariusze współpracy z AI, warto popatrzeć na tę tematykę nieco szerzej.

Nasze warsztatowe doświadczenie wskazuje, że do narzędzi opartych o Sztuczną Inteligencję pracownicy umysłowi wciąż podchodzą z niepewnością. Szczerze mówiąc - nie ma się czemu dziwić. Popkultura od dekad prezentowała nam wizje przyszłości opanowanej przez AI no i co tu dużo mówić - nie był to świat, w którym chcielibyśmy się znaleźć.

Już w 1968r., w filmie “2001: Odyseja kosmiczna”, astronauci zmagali się komputerem HAL9000, który uznał ich za przeszkodę w realizacji celu. Przykład ten sugerował, że AI może kiedyś osiągnąć poziom samoświadomości i niezależnych decyzji etycznych, prowadząc do konfliktów z ludźmi.

W 2004r., w filmie “Ja, robot” Will Smith zagrał rolę detektywa rozwiązującego zagadkę, w której głównym podejrzanym był robot uzyskujący samoświadomość. Jego zachowanie miało sugerować, że [trzy prawa robotyki](https://pl.wikipedia.org/wiki/Etyka_robot%C3%B3w) - fundament rzeczywistości, w której współpracujemy z AI - mogą być łamane, a ludzkość zagrożona.

10 lat później, w filmie “Ex Machina” (2014r.), zobaczyliśmy młodego programistę biorącego udział w eksperymencie z zaawansowaną kobiecą AI o nazwie Ava. Film eksplorował tematy manipulacji, świadomości i autonomii AI, sugerując, że maszyny mogą posiadać głębokie zrozumienie ludzkich emocji i używać tego do swoich celów.

Jeśli nie oglądałeś akurat tych filmów, to na podobne scenariusze mogłeś wpaść w niejednym serialu, książce czy opowieści z gatunku Sci-Fi. Nie zapowiadało się inaczej, niż na zagładę…

**Wzmocnienia w mediach masowych**

W epoce ChataGPT te negatywne nastroje są - niestety - tylko podsycane. “Popularnonaukowe” kanały na YouTube straszą miniaturkami, atakami cybernetycznymi, wypadkami autonomicznych samochodów, wyłudzeniami danych czy emocjami, jakie wzbudza temat regulacji Sztucznej Inteligencji.

Niestety, to wszystko klika się lepiej, niż wiadomości optymistyczne, co znajduje swoje potwierdzenie w badaniach naszej psychiki.

Jako ludzie jesteśmy podatni na tzw. “**_negativity bias_**”. Częściej zauważamy i zapamiętujemy informacje negatywne, niezależnie od tego, ile pozytywnych trafiło do nas z dokładnie tej samej dziedziny.

Jedno z kluczowych badań, które eksploruje ten temat, to praca psychologów Roya F. Baummeistera, Ellen Bratslavsky, Kathleen Vohs i Catrin Finkenauer zatytułowana "Bad Is Stronger Than Good", opublikowana w "Review of General Psychology" w 2001 roku. Autorzy badania doszli do wniosku, że negatywne doświadczenia mają na nas głębszy wpływ niż równie intensywne pozytywne doświadczenia. Na przykład, negatywne emocje, negatywne spostrzeżenia społeczne oraz negatywne zdarzenia wydają się wywoływać silniejsze i bardziej trwałe reakcje psychologiczne niż pozytywne.

"Negativity bias" wpływa na wiele aspektów ludzkiego życia, w tym na sposób, w jaki konsumujemy wiadomości i reagujemy na informacje o świecie wokół nas. Badania sugerują, że wiadomości negatywne mogą przyciągać większą uwagę i być bardziej pamiętane niż wiadomości pozytywne. To może tłumaczyć, dlaczego media często skupiają się na negatywnych historiach - po prostu lepiej przyciągają one naszą uwagę.

**Dlaczego bardziej interesują nas informacje negatywne?**

Istnieje kilka powodów, dla których ludzie są bardziej zainteresowani informacjami negatywnymi:

- **Wiarygodność.** Ludzie mają tendencję do postrzegania negatywnych informacji jako bardziej wiarygodnych i obiektywnych. Te pozytywne mogą być postrzegane jako stronnicze lub propagandowe.
    
- **Nowa energia.** Emocje takie jak strach, złość i smutek są zwykle bardziej intensywne niż radość, szczęście i miłość. To sprawia, że ​​negatywne informacje są łatwiejsze do zauważenia i zapamiętania.
    
- **Przetrwanie.** Informacje o zagrożeniach mogą pomóc nam uniknąć negatywnych konsekwencji. To sprawia, że ​​negatywne informacje są bardziej wartościowe z ewolucyjnego punktu widzenia.
    

### Czy nadal mówimy o kursie dla programistów?

Tak! Ten szerszy kontekst ma ci uświadomić to, że najważniejszy pierwszy krok w eksploracji tematyki Sztucznej Inteligencji wcale nie dotyczy instalacji edytora kodu Cursor, kupienia subskrypcji ChataGPT czy skonfigurowania ustawień w Copilocie.

Jeśli wcześniej nie zajmowałeś się tematyką AI w kontekście programowania, to pierwszym krokiem, jaki musisz wykonać, **jest pozbycie się błędnych przekonań, na które od dawna pracują media i kultura masowa**. Zamiast tego, naszą propozycją jest trenowanie postawy naukowca, który z zaciekawieniem bada otaczającą go rzeczywistość.

AI reprezentuje szybki postęp technologiczny, który może zmieniać sposób, w jaki pracujemy, komunikujemy się, i żyjemy. Proces zmian odbywa się na naszych oczach i ważne jest, żeby będąc pod wpływem _negativity biasu_ nie skupiać się wyłącznie na prognozach końca ludzkości i dać sobie szansę wyrobienia **własnych opinii na temat narzędzi**, z którymi w tej lekcji popracujemy.

## AI jako narzędzie w przyborniku programisty

W książce "[The Pragmatic Programmer](https://lubimyczytac.pl/ksiazka/4969608/pragmatyczny-programista-od-czeladnika-do-mistrza-wydanie-ii)" autorzy - Andrew Hunt i David Thomas - podkreślają znaczenie ciągłego aktualizowania swojego "toolboxa" - zestawu narzędzi, umiejętności i technik, które programiści wykorzystują w swojej pracy.

W twoim toolboxie już teraz znajduje się sprzęt, na którym pracujesz, konkretny system operacyjny, edytor tekstu, być może aplikacja do zarządzania listą zadań, klient email, przeglądarka internetowa czy narzędzia pomagające pracować produktywnie. Częścią przybornika są też wyrobione nawyki, sposób komunikacji z innymi, twoje podejście do analizy wymagań i to, kiedy prosisz o pomoc bardziej doświadczonych programistów.

Ostatnie miesiące wskazują, że istotnym rozszerzeniem toolboxa powinny być też narzędzia z dziedziny tzw. Generatywnej Sztucznej Inteligencji.

> **Generatywna sztuczna inteligencja (AI)** odnosi się do klasy algorytmów i modeli AI, które mają zdolność do tworzenia, generowania lub syntezowania nowych danych, które są podobne, ale nie identyczne, do danych, na których zostały wytrenowane. W przeciwieństwie do tradycyjnych modeli AI, które są zazwyczaj projektowane do rozpoznawania wzorców, klasyfikacji czy prognozowania na podstawie istniejących danych, generatywna AI może produkować nowe treści, takie jak tekst, obrazy, muzyka, mowa czy nawet kod.

Modele językowe (LLMy, np. GPT-4, LLaMa 2, Gemini) wytrenowane na ogromnych korpusach tekstu pokazały nam, że publicznie dostępny tekst wyprodukowany przez człowieka może być z powodzeniem użyty do generowania nowych treści, które możemy z kolei wykorzystać w kontekście zawodowym.

Ethan Mollick, naukowiec z Uniwersytetu Pensylwanii, sugeruje nawet, żeby na modele językowe patrzeć jak na [osobistych stażystów](https://www.oneusefulthing.org/p/on-boarding-your-ai-intern) - nietypowych przybyszy z kosmosu, którzy chcą z tobą współpracować zupełnie za darmo. Istnieje pewien haczyk - nie są oni w pełni niezawodni i wymagają twojej asysty, ale przy odpowiednich sugestiach mogą znacznie poprawić twoją kreatywność i produktywność.

Frontend ma tę zaletę w porównaniu do innych obszarów programowania, że w domenie publicznej znajduje się mnóstwo otwartego kodu z projektów, bibliotek i frameworków opartych o JavaScript i TypeScript. Ta ilościowa przewaga tekstu, na którym uczą się modele językowe, znacząco wpływa na ich użyteczność w naszej domenie w porównaniu do bardziej zamkniętych ekosystemów (np. embedded, czy niskopoziomowego programowania systemów).

W dalszej lekcji pokażemy ci konkretne scenariusze współpracy z AI, które możesz wykorzystać w swojej pracy jako frontend developer.

## ChatGPT i Custom GPTs

Wspomniana powyżej definicja pair programmingu zakłada współpracę dwóch osób - tej, która pisze kod i implementuje wymagania, oraz tej, która z pewnego dystansu na bieżąco dzieli się swoimi uwagami.

Z rozmaitych powodów organizacja pracy w tym modelu nie zawsze się udaje. Czasami nie zgrywają się plany dnia, czasami nie ma dopasowania umiejętności, a czasami - po prostu - spotykają się zbyt różne charaktery komunikujące się w radykalnie inny sposób.

W czasach generatywnej sztucznej inteligencji możemy eksperymentować z nowym modelem programowania w parach. Modelem, w którym naszym asystentem staje się zawsze gotowy do pomocy [Custom GPT](https://openai.com/blog/introducing-gpts) napędzany przez ChatGPT.

Dzięki niedawno wprowadzonej nowości jaką są GPTs, najpopularniejsza usługa świata Generative AI może teraz obsługiwać wiele ról i zadań w ramach jednej konwersacji. Staje się ona miejscem uzyskiwania bezpiecznego feedbacku, okazją do zadawania “nieskończenie trywialnych” i “nieskończenie złożonych” pytań, a także weryfikowania swoich pomysłów na długo przed tym, jak poznają je inne osoby w zespole.

Poniższy film zaprezentuje ci korzyści płynące ze współpracy z wirtualnymi “trenerami frontendu”, którzy na podstawie wcześniej zdefiniowanych instrukcji będą z nami prowadzić bardziej użyteczne konwersacje.

W przedstawionym filmie wykorzystaliśmy własnego asystenta **Angular Coach** i zestaw konkretnych instrukcji dopasowanych do kontekstu naszego szkolenia:

```markdown
Jesteś doświadczonym senior frontend developerem specjalizującym się we frameworku Angular. Pozwalasz mi zrozumieć jego najważniejsze cechy i opanować go do perfekcji.

Prowadząc konwersacje, domyślnie używasz przykładów z tego frameworka, chyba, że poproszę o użycie innego. Możesz używać analogii do Reacta, ponieważ jest to technologia, z którą pracuję na co dzień.

Tam, gdzie rozmowa dotyczy wyglądu komponentów, powinieneś korzystać z frameworka Tailwind.

Tłumaczysz zagadnienia w przystępny i zrozumiały sposób, dopasowany do początkującego. Zanim udzielisz odpowiedzi na złożone problemy związane z kodem, rozbijasz dany problem na mniejsze składowe.

Ważne: Nie korzystasz z dodatkowej bazy wiedzy dopóki wprost nie wskażę pliku, który powinieneś interpretować.
```

### Komunikacja z asystentem

Określenie naszych oczekiwań to ważny krok w stronę podniesienia jakości odpowiedzi generowanych przez CustomGPT, ale przy bardziej złożonych problemach to może nie wystarczyć. Aby nasza komunikacja przebiegała jeszcze lepiej, warto zapoznać się z fundamentami tzw. **prompt engineeringu**, czyli pewnego nieformalnego zbioru technik i porad komunikacji z modelami AI.

Temat prompt engineeringu obrósł wieloma mitami, które robią z tej aktywności coś przypominającego bardziej magię niż inżynierię oprogramowania, natomiast do poznania fundamentów wystarczy ci kilka stosunkowo prostych porad.

Przede wszystkim, pamiętaj, że model ma ograniczony zasób wiedzy. Zbiory danych treningowych współczesnych modeli robią wrażenie, ale zazwyczaj brakuje im informacji “z wczoraj” i na pewno brakuje im twojego osobistego kontekstu. Właśnie dlatego krytycznie ważne jest rozbudowywanie pamięci podręcznej, jaką jest sam tekst konwersacji.

Im więcej informacji uda ci się zamieścić w tekście przed wydaniem pytania lub polecenia, tym lepiej. Model taki jak GPT-4, o dużym potencjale łączenia faktów i wnioskowania, będzie w stanie udzielić bardziej precyzyjnej odpowiedzi.

Kontekstem może być też rola lub domena problemu, którą określisz już na początku rozmowy. Jeśli sprecyzujesz, że rozmowa dotyczy programowania w konkretnym języku, to nie będziesz musiał ratować konwersacji, która dotyczy zupełnie obcej technologii. Tę domenę i rolę możesz umieścić albo bezpośrednio w poleceniu, albo w Custom Instructions / instrukcjach do CustomGPT aby sobie oszczędzić czas.

Pamiętaj również, że to sam model może cię nakierować na doprecyzowanie kontekstu. Przedstawiając asystentowi bardziej złożony problem, możesz dodać wzmiankę “przed udzieleniem odpowiedzi zadaj mi dodatkowe pytania, które pomogą ci udzielić odpowiedzi”. W tej “metodzie Sokratejskiej” model będzie wyciągał z ciebie dodatkowe informacje, co do których mogłeś nawet nie wiedzieć, że są istotne.

Nie nastawiaj się również na uzyskanie idealnej odpowiedzi w pierwszym podejściu. Rozmowa z modelem AI to proces iteracyjny. Każda kolejna konwersacja to poznawanie możliwości, ale i i ograniczeń twojego partnera do rozmowy i przyszłego asystenta pair programmingu. Tylko godziny spędzone na rzeczywistej rozmowie, a nie czytanie teorii, pozwoli ci wyciągnąć z tych narzędzi maksimum możliwości.


![[Pasted image 20240517080755.png]]


Zachęcam cię do wejścia w temat Prompt Engineeringu nieco głębiej, a jeśli masz tylko kilka minut, to zapoznaj się z tymi trzema wpisami:

- [Few-shot prompting](https://www.promptingguide.ai/techniques/fewshot) - technika, w której przedstawiasz kilka oczekiwanych zachowań modelu
    
- [Chain-of-Thought](https://www.promptingguide.ai/techniques/cot) - technika pozwalająca zbudować kontekst roboczy “on the fly”
    
- [Generated Knowledge](https://www.promptingguide.ai/techniques/knowledge) - technika pozwalająca generować fakty przed odpowiedzią
    

Kluczowe porady znajdziesz w tym miejscu - [https://www.promptingguide.ai/](https://www.promptingguide.ai/) oraz na Opanuj.AI 🫡

**Czy to koniec współpracy z ludźmi?**

Wykorzystanie ChataGPT w kontekście pair programmingu nie powinno być odbierane jako rekomendacja odchodzenia od współpracy z innymi członkami zespołu. Umiejętności miękkie, czyli skuteczna komunikacja, zarządzanie emocjami czy udzielanie konstruktywnego feedbacku nadal będą stanowić o sile nowoczesnego pracownika umysłowego.

Prezentowane tutaj scenariusze pair programmingu z AI można traktować podobnie do wielu innych obszarów programowania, gdzie nawzajem uzupełnia się kilka podobnych technik, np. testowania. Tak samo jak nie możemy wybrać “jednego słusznego rodzaju testów”, tak w epoce GenAI nie powinniśmy ograniczać się do procesów, które były standardem jeszcze kilka lat temu.

Skoro nasz programistyczny “toolbox” się powiększa, to zgodnie z postawą naukowca powinniśmy te nowe metody pracy eksplorować, badać i merytorycznie oceniać, a nie udawać, że nie istnieją.

## Praca z kodem w Github Copilot

Drugi z przykładów prezentowanych w tej lekcji będzie dotyczył bardziej bezpośredniego działania na poziomie kodu, projektu i wymagań biznesowych.

W tym fragmencie przetestujemy Github Copilota, czyli asystenta, który na bieżąco stara się przewidywać nasze intencje, uczy kontekstu, próbuje rozumieć nasze komendy i usprawnia kolejne etapy procesu wytwarzania oprogramowania.

Podstawowe [scenariusze pracy z Copilotem](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/) realizowane są w trzech obszarach:

- domyślnie - bieżące rekomendacje i przewidywania kodu w miejscu naszego kursora


![[Pasted image 20240517080807.png]]


- na żądanie - edycja i refaktoryzacja kodu, w polu tekstowym na poziomie pliku

![[Pasted image 20240517080821.png]]

- na żądanie - współpraca z Copilot Chatem, czyli niezależnym asystentem świadomym kontekstu projektu

![[Pasted image 20240517080859.png]]


Copilot próbuje realizować stawiane przed nim zadania na podstawie śladów, którymi są m.in:

- nazwy zmiennych
    
- nazwy funkcji
    
- komentarze do danego fragmentu kodu
    
- dokumentacja i pliki README
    
- istniejące typy danych
    
- zaimportowane zależności
    
- struktura projektu

Zdarza się, że jeszcze zanim napiszemy jakiekolwiek polecenie lub komentarz, Copilot będzie już gotowy sugerować pierwsze fragmenty kodu tylko na podstawie nazwy pliku czy jego umiejscowienia w kontekście całego projektu:

![[Pasted image 20240517080913.png]]

Z powodu ciągłego interpretowania “śladów”, jakie znajduje na swojej drodze Copilot, zauważysz, że:

- precyzyjne nazewnictwo zmiennych podniesie jakość sugestii Copilota
    
- typy parametrów i wartości zwracanych mogą zdefiniować “ramy” zadania dla Copilota
    
- komentarze do kodu (nawet tymczasowe) mogą wpływać na lepsze sugestie
    
- istniejąca dokumentacja może być wykorzystana w Copilot Chat do poszerzenia kontekstu rozmowy
    

Można powiedzieć, że zadziała tutaj sprzężenie zwrotne - im lepsza będzie jakość kodu bazowego, tym lepsze będą sugestie proponowane przez wirtualnego asystenta.

### Precyzyjna komunikacja

Jeden z przykładów, który wskazuje na różnicę w jakości generowanego kodu na skutek drobnej modyfikacji polecenia programisty, znajdziesz poniżej.

Zaczynamy od zdefiniowania interfejsu opisującego dane, jakie otrzymamy z formularza na stronie:
```typescript

export interface FormData {
  firstName: string;
  lastName: string;
  email: string;
  password: string;
  confirmPassword: string;
}

```

Następnie przechodzimy do zbudowania form handlera, czyli funkcji, która powinna przyjąć dane określonego kształtu i przeprowadzić walidację. Całe zadanie delegujemy do Copilota, który korzysta z naszego polecenia w komentarzu:


![[Pasted image 20240517081012.png]]

Na pierwszy rzut oka widać tutaj problemy. Walidacja wewnątrz funkcji obsługującej formularz (złamanie zasady SRP), złożone instrukcje warunkowe, no i zwracany typ danych jakim jest string. Pytanie tylko - skąd Copilot ma wiedzieć, że oczekiwaliśmy czegoś innego?

W przypadku złożonego scenariusza składającego się z kilku etapów, warto skorzystać z Copilot Chata i wyjaśnić nasze oczekiwania bardziej precyzyjnie:

![[Pasted image 20240517081042.png]]

W odpowiedzi uzyskamy kod zdecydowanie wyższej jakości, którego detale możemy już wypełnić we własnym zakresie:

![[Pasted image 20240517081051.png]]


Wygląda to zdecydowanie lepiej od tego, co otrzymaliśmy jako sugestię do naszego mało precyzyjnego komentarza.

## Podstawy pracy z Copilotem

Pierwsze kroki z Copilotem zaprezentuje kolejny fragment video:

**Ile wartości w Copilocie?**

Trudno przewidywać, jaki efekt wywołał w Tobie powyższy film, ale muszę cię uspokoić - na dzisiaj Copilot nie jest gotowy do zastąpienia programistów. Nie oznacza to jednak, że jest bezużyteczny - to dwie skrajne opinie, z którymi warto się jak najszybciej pożegnać.

Współpraca z Copilotem wygląda na dzisiaj podobnie do innych rozwiązań ze świata Generatywnej Sztucznej Inteligencji. Jeśli prowadzone konwersacje dotyczą tematu, co do którego mamy już wstępną wiedzę i intuicję, to minimalizujemy szansę wpadki, a podnosimy jakość otrzymywanych odpowiedzi. Jeśli przekazujemy precyzyjny kontekst zadania, to uzyskujemy wartościowe rezultaty. Jeśli korzystamy z referencji do plików i składowych naszego projektu, to redukujemy losowość i pozwalamy Copilotowi pracować na szerszej pamięci podręcznej, której modele językowe potrzebują jak wody.

Z drugiej strony, jeśli pracujemy w zupełnie obcej technologii, zamiast analizy problemu oczekujemy gotowych rozwiązań, nasze polecenia tekstowe są mało precyzyjne, a do tego wychodzimy z błędnego założenia, że “zrobi się samo”, to faktycznie Copilot może nie spełnić oczekiwań.

Niektórzy przeciwnicy tej technologii podają też argument, że korzystanie z takich narzędzi to strata czasu. W końcu zdarza się, że liczba znaków i liter, jakie wykorzystujemy pisząc polecenia tekstowe (prompty), bywa dłuższa niż generowany przez Copilota kod. Ma to być dowód na marnotrawienie czasu - przecież moglibyśmy programować, a zamiast tego piszemy… wiadomości do bota AI?

Rozwój naszej branży pokazuje jednak, że najpopularniejszymi językami programowania nie są na dzisiaj te, dzięki którym oszczędzamy literki pisząc kod. Assembler i języki niskiego poziomu są w dużych systemach wypierane przez bardziej ekspresyjne konstrukcje, dodatkowe warstwy abstrakcji i frameworki, które minimalizują wpływ szczegółów implementacyjnych. Coś nam mówi, że programowanie z wykorzystaniem języka naturalnego może być kolejnym etapem tego procesu.

Zachęcamy Cię, żebyś po ukończeniu tej lekcji spędził trochę czasu z Copilotem i zbudował własną intuicję na temat tego, jak i kiedy takie narzędzie może się okazać warte swojej ceny. [Give it five minutes.](https://signalvnoise.com/posts/3124-give-it-five-minutes)

## Czy korzyści współpracy z AI można zmierzyć?

Github, jako organizacja, od dłuższego czasu próbuje zmierzyć wpływ narzędzi opartych o AI na zespoły programistyczne. Każde kolejne badanie wskazuje, że mogą mieć one pozytywny wpływ na tzw. Developer Experience:

![[Pasted image 20240517081116.png]][(źródło)](https://github.blog/2022-09-07-research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)

Jedną z korzyści, na którą wskazuje najwięcej programistów korzystających z Copilota, jest **oszczędność energii** przeznaczanej na realizowanie trywialnych, powtarzalnych zadań.

Inne badanie, na które powołuje się Github, dotyczy również **oszczędności czasu**. Przedmiotem opisywanych badań było wystawienie “web serwera w JavaScript” przez grupę 95 programistów na podobnym poziomie doświadczenia. Połowa z nich używała Copilota - druga połowa opierała się wyłącznie na doświadczeniu i dostępie do internetu. Zaprezentowane przez Githuba wyniki wskazują na redukcję czasu potrzebnego na realizację tego konkretnego zadania o ponad 50% - to wynik, który naprawdę powinien dać do myślenia.

![[Pasted image 20240517081126.png]]
Żeby nie było tak kolorowo, warto przytoczyć też badania inne niż te prowadzone przez producenta oprogramowania opartego o AI (chociaż w żadnym wypadku nie sugerujemy złej woli - szukamy po prostu szerszego spojrzenia na dany temat).

W niedawno [opublikowanym badaniu](https://www.gitclear.com/coding_on_copilot_data_shows_ais_downward_pressure_on_code_quality) autorstwa firmy GitClear sprawdzano, czy epoka programowania w oparciu o AI charakteryzuje się zmianami jakości tworzonego kodu.

Firma przeanalizowała ponad 150mln linii kodu pochodzącego od klientów, którzy zgodzili się uczestniczyć w anonimowym badaniu aktywności na swoich repozytoriach. W trakcie analizy danych zauważono, że z roku na rok zwiększa się procentowy wskaźnik “churn” (z 3-4% do przewidywanych 8-10% w 2024r.), czyli modyfikacji tych linijek kodu, które zostały wprowadzone nie dalej niż dwa tygodnie temu. Wskazuje to na większą dynamikę w obrębie repozytorium i mniejszą stabilność całego projektu.

Autorzy badania sugerują, że wpływ na to mogą mieć narzędzia takie jak Copilot, gdzie największy nacisk kładzie się na generowanie, a nie usuwanie czy stabilizowanie kodu. W opracowaniu badania pojawia się wniosek, że w codziennej pracy programisty te “szybkie wygrane”, jakimi są rekomendowane przez Copilota linijki kodu, mogą w dłuższej perspektywie doprowadzić do podejmowania złych decyzji, optymalizowanych lokalnymi, a nie globalnymi problemami w obrębie projektu.

Czy faktycznie jest się czego obawiać? Zwróćmy uwagę, że wyniki badania nie wskazują jednoznacznie na spadek jakości tworzonego kodu, a wyłącznie na większą częstotliwość zmian. Może być tak, że dzięki AI próg wejścia do wcześniej nieosiągalnych obszarów projektu znacznie się obniżył. Programiści współpracujący z ChatemGPT i Copilotem mogą teraz rozwijać kod w miejscach, które wcześniej były dla nich niezrozumiałe i niedostępne (pod każdym kątem - technologii, złożoności czy zastosowanego rozwiązania).

Naturalnie, w efekcie takiej zmiany, w statystykach zobaczylibyśmy wzrost kontrybucji w miejscach, które wcześniej były bardziej stabilne (czytaj - dostępne dla mniejszej liczby programistów). Prawdę mówiąc, byłby to naprawdę pozytywny rezultat szerszej adopcji Copilota w świecie programowania.

Czas pokaże, która interpretacja wyników badań jest bliższa rzeczywistości. W epoce tak dynamicznych zmian, jakie obserwujemy od premiery ChataGPT, wyciąganie daleko idących wniosków na podstawie jednego wskaźnika może być mylące. Właśnie dlatego rekomendujemy przetestowanie przedstawionych tutaj narzędzi we własnym kontekście i wyciągania wniosków, które są dopasowane do twojego kontekstu zawodowego.

### 👨‍💻 Ćwiczenia praktyczne

W tej lekcji przedstawiliśmy ci szerszą perspektywę współpracy z narzędziami opartymi o sztuczną inteligencję.

W ramach ćwiczeń, proponujemy przetestowanie współpracy z Copilotem przez 30 dni darmowego triala. Poprzez praktykę i zdobywanie doświadczenia będziesz w stanie ocenić, czy jest to dla ciebie odpowiednie narzędzie.

Alternatywnie, możesz również przetestować edytor [Cursor](https://cursor.sh/pricing), który w darmowym planie udostępnia 200 zapytań do GPT-3.5 oraz 50 zapytań do GPT-4. Jeśli to narzędzie spełni twoje oczekiwania, możesz korzystać z twojego prywatnego klucza do API OpenAI i płacić za użycie tokenów z modelu.

### 📚 Materiały dodatkowe

- [https://www.oneusefulthing.org/p/secret-cyborgs-the-present-disruption](https://www.oneusefulthing.org/p/secret-cyborgs-the-present-disruption)
    
- [https://github.blog/2024-01-22-10-unexpected-ways-to-use-github-copilot/](https://github.blog/2024-01-22-10-unexpected-ways-to-use-github-copilot/)
    
- [https://platform.openai.com/docs/guides/prompt-engineering](https://platform.openai.com/docs/guides/prompt-engineering)  
    

**Twój feedback jest dla nas na wagę złota!** Zanim przejdziesz dalej, będziemy wdzięczni za poświęcenie 10 minut na podzielenie się Twoją opinią o IV module w [ankiecie badania satysfakcji](https://przeprogramowani.typeform.com/to/FjWkBIOy) 👈