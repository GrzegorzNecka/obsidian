
**MySQL**

Wykład ten przedstawia podstawowe pojęcia związane z projektowaniem relacyjnych baz danych oraz językiem SQL - Structure Query Language.

1. [**MySQL** - relacyjna baza danych](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
2. [Zapytanie CREATE](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
3. [Zapytanie SELECT](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
4. [Zapytanie INSERT, UPDATE](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
5. [Zapytanie DROP, DELETE](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
6. [Instrukcja ALTER](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
7. [Złączenia JOIN](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
8. [Transakcje](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
9. [Administracja bazą danych](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)
10. [Normalizacja bazy danych](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#)

# **MySQL** - relacyjna baza danych

|Rodzaje baz danych|   |
|---|---|
|Bazy kartotekowe|W bazach kartotekowych każda tablica danych jest samodzielnym dokumentem i nie może współpracować z innymi tablicami. Z baz tego typu korzystają liczne programy typu: książka telefoniczna, książka kucharska, spisy książek, kaset i inne. Wspólną cechą tych baz jest ich zastosowanie w jednym wybranym celu.|
|Bazy hierarchiczne|W modelu hierarchicznym dane są przechowywane na zasadzie rekordów nadrzędnych-podrzędnych, tzn. rekordy przypominają strukturę drzewa. Każdy rekord (z wyjątkiem głównego) jest związany z dokładnie jednym rekordem nadrzędnym.|
|Bazy relacyjne|W bazach relacyjnych wiele tablic danych może współpracować ze sobą (są między sobą powiązane). Bazy relacyjne posiadają wewnętrzne języki programowania, wykorzystujące zwykle SQL do operowania na danych, za pomocą których tworzone są zaawansowane funkcje obsługi danych.|
|Bazy obiektowe|W bazach obiektowych dane przechowywane są w strukturach obiektowych (zdefiniowanych jako klasy). Koncepcje akademickie dotyczące baz obiektowych były najbardziej popularne w latach 90. Współcześnie popularność tego tematu zmalała, choć prace badawcze nad nimi nadal trwają, a na rynku pojawiły się obiektowe SZBD (np. Versant, db4o, LoXiM).|
|Bazy relacyjno-obiektowe|Bazy relacyjno-obiektowe pozwalają na manipulowanie danymi jako zestawem obiektów, posiadają jednak bazę relacyjną jako wewnętrzny mechanizm przechowywania danych.|
|Bazy strumieniowe|Strumieniowa baza danych to baza danych, w której dane są przedstawione w postaci zbioru strumieni danych. System zarządzania taką bazą nazywany jest strumieniowym systemem zarządzania danymi (DSMS - ang. Data Stream Management System).|
|Bazy temporalne|Jest odmianą bazy relacyjnej, w której każdy rekord posiada stempel czasowy, określający czas w jakim wartość jest prawdziwa. Posiada także operatory algebry relacyjnej, które pozwalają operować na danych temporalnych (wyciągać historię).|
|Bazy nierelacyjne|Pod pojęciem bazy nierelacyjnej (NoSQL database) najczęściej rozumie się przechowywanie danych w formie listy par obiektów klucz-wartość, w których nie występują powiązania relacyjne między przechowywanymi obiektami. W bazie NoSQL najczęściej nie ma wymagania aby obiekty były jednorodne pod względem struktury.|

### Instalacja relacyjnej bazy danych **MySQL**

W pierwszej kolejności musimy pobrać wersję instalacyjną [MySQL](http://home.agh.edu.pl/~pamalino/programowanie/mysql/download/mysql-installer-web-community-8.0.15.0.msi "MySQL").

Możemy również wykorzystać gotowy pakiet serwerów apache, mysql, interpretera php, np. [XAMPP](http://home.agh.edu.pl/~pamalino/programowanie/mysql/download/xampp-windows-x64-7.3.3-0-VC15-installer.exe) (zalecane rozwiązanie na potrzeby kursu).

Po zainstalowaniu bazy danych MySQL otwieramy konsolę cmd i przechodzimy do katalogu instalacji pakietu do ścieżki (pakietu XAMPP) za pomocą polecenia:  

```bash
cd c:/xampp/mysql/bin/
```

Uruchamiamy polecenie:  

```bash
mysql -u root
```

  
i jesteśmy w konsoli bazy danych MySQL.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/konsola_MySQL.png "Konsola MySQL")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/konsola_MySQL.png)

Do tworzenia, usuwania, modyfikowania baz danych, tabel, widoków w MySQL stosujemy język **SQL - Structured Query Language**. Jest to strukturalny język zapytań służący do pracy z bazą danych.

Utworzymy bazę danych test - wpisując polecenie:  
  

```mysql
CREATE DATABASE test;
```

  

```mysql
USE test;
```

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql1.png "Konsola MySQL")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql1.png)

Jeżeli nie ma błędu baza danych test została utworzona. Po wykonaniu polecenia USE test wybraliśmy do dalszej pracy bazę danych test. Co można zauważyć w kwadratowych nawiasach [test].

Teraz utworzymy tabelę o nazwie samochody wydając następujące polecenie:  

```mysql
CREATE TABLE samochody  
  (  
     id             _INT_ auto_increment,  
     marka          _VARCHAR_(30),  
     model          _VARCHAR_(30),  
     rocznik        _INT_,  
     pojemnosc      _FLOAT_,  
     przyspieszenie _FLOAT_,  
     PRIMARY KEY(id)  
  );
```

Za pomocą polecenia:  

```mysql
INSERT INTO samochody  
VALUES     (NULL,  
            "bugatti",  
            "veyron",  
            2018,  
            7993.0,  
            2.5);
```

  
wprowadzimy wiersz do tabeli samochody.  

```mysql
INSERT INTO samochody  
VALUES     (NULL,  
            "lamborghini",  
            "aventador",  
            2018,  
            6498.0,  
            2.9);
```

Wydając polecenie:  

```mysql
SELECT *  
FROM   samochody;
```

  
uzyskamy podgląd wyników.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql2.png "Konsola MySQL")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql2.png)

W kursie tym będziemy również używać narzędzia phpMyAdmin z pakietu XAMPP.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin.png "phpMyAdmin")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin.png)  

Aby uzyskać dostęp do phpMyAdmin należy uruchomić panel sterowania XAMPP i uruchomić serwer Apache i MySQL.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/xampp.png "Panel sterowania XAMPP")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/xampp.png)

Następnie w oknie przeglądarki wpisujemy  

```
http://localhost/phpMyAdmin
```

Wykorzystując narzędzie phpMyAdmin założymy nową bazę danych studia. Klikamy na zakładkę Bazy danych.W polu tekstowym nazwa bazy danych wpisujemy studia, a kodowanie znaków wybieramy utf8_polish_ci i klikamy Utwórz.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin1.png "phpMyAdmin")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin1.png)  

Widzimy po lewej stronie że baza danych studia została utworzona. Następnie wprowadzimy do niej tabelę student z 11 kolumnami i naciskamy Wykonaj.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin2.png "phpMyAdmin")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin2.png)

Poniżej znajduje się instrukcja wygenerowana przez phpMyAdmin:  

```sql
CREATE TABLE `studia`.`student`  
  (  
     `id_student`    _INT_ NOT NULL auto_increment,  
     `imie`          _VARCHAR_(20) CHARACTER SET utf8 COLLATE utf8_polish_ci NOT  
     NULL,  
     `nazwisko`      _VARCHAR_(30) CHARACTER SET utf8 COLLATE utf8_polish_ci NOT  
     NULL,  
     `id_wydzial`    _INT_ NOT NULL,  
     `id_kierunek`   _INT_ NOT NULL,  
     `nr_albumu`     _INT_ NOT NULL,  
     `rok_studiow`  _INT_ NOT NULL,  
     `miejscowosc`   _VARCHAR_(30) CHARACTER SET utf8 COLLATE utf8_polish_ci NOT  
     NULL,  
     `wojewodztwo`   _VARCHAR_(30) CHARACTER SET utf8 COLLATE utf8_polish_ci NOT  
     NULL,  
     `rok_urodzenia` _INT_ NOT NULL,  
     `status`        _ENUM_('student', 'urlop', 'skreslony', 'absolwent')  
     CHARACTER SET utf8  
     COLLATE utf8_polish_ci NOT NULL,  
     PRIMARY KEY (`id_student`)  
  )  
engine = innodb  
charset=utf8  
COLLATE utf8_polish_ci;
```

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin3.png "phpMyAdmin")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin3.png)  

**Co to jest baza danych?**  
Baza danych jest to zbiór informacji odzwierciedlający pewien wycinek rzeczywistości, uporządkowany w tabelach.  
**Co to jest tabela?**  
Tabela zbudowana jest z wierszy i kolumn. Każda kolumna składa się z nazwy i typu danych, który reprezentuje. Przykład tabeli.

|text imie|text nazwisko|text nr_albumu|int rok_studiow|text miejscowosc|text wojewodztwo|int rok_urodzenia|
|---|---|---|---|---|---|---|
|Jan|Kowalski|15344-345|3|Kraków|małopolskie|1996|
|Adam|Nowak|15344-346|2|Kielce|świętokrzyskie|1998|
|Jan|Kowalski|15344-313|1|Warszawa|mazowieckie|1999|

|        |
| ------ |
| Rekord |
| Pole   |

W kolumnach przechowujemy cechy obiektu np. imię, nazwisko, numer albumu, datę urodzenia, itp.  
Wiersz - inaczej **rekord** to zestaw cech jednego studenta.  
**Pole** to część tabeli przechowujące wybrane dane studenta, np. imię, nazwisko.

Więcej o typach danych znajduje się w rozdziale

By uniknąć sytuacji, gdy w bazie danych znajduje się dwóch studentów o tych samych danych osobowych, tzn. imię, nazwisko, do tabeli dodajemy kolumnę z unikatowymi wartościami nazwaną kluczem podstawowym.

|int id_student|text imie|text nazwisko|text nr_albumu|int rok_studiow|text miejscowosc|text wojewodztwo|int rok_urodzenia|
|---|---|---|---|---|---|---|---|
|1|Jan|Kowalski|15344-345|3|Kraków|małopolskie|1996|
|2|Adam|Nowak|15344-346|2|Kielce|świętokrzyskie|1998|
|3|Jan|Kowalski|15344-313|1|Warszawa|mazowieckie|1999|

|   |
|---|
|Klucz podstawowy|

Wtedy studenci pomimo, że mają takie same imię i nazwisko mają różną wartość w kolumnie id_student (klucz podstawowy). Dzięki temu każdy rekord w tabeli jest unikatowy.

**Klucz podstawowy** - to kolumna, w której każda wartość jest unikatowa i jednoznacznie identyfikuje każdy rekord w tabeli. Gdyby w tabeli nie było klucza podstawowego, mogłoby dojść do utraty spójności danych.

**Klucz obcy** - to kolumna, która wskazuje na klucz podstawowy innej tabeli. Dzięki zastosowaniu klucza obcego w jednej tabeli, tworzymy relację z drugą tabelą, w której ten klucz jest kluczem podstawowym.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/relacje.png "Relacje")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/relacje.png)  

Na powyższym schemacie widzimy trzy tabele znajdujące się w bazie danych studia. Pierwsza z nich opisuje studenta, druga wydział, a trzecia kierunki studiów.

**Relacja** - jest to połączenie dwóch tabel za pomocą klucza podstawowego jednej tabeli z kluczem obcym innej tabeli.

Kolorem czerwonym została pokazana relacja pomiędzy tabelami Student i Wydzial. Klucz podstawowy tabeli Wydzial o nazwie id_wydzial połączony jest z kluczem obcym o tej samej nazwie w tabeli Student.

Kolorem zielonym została pokazana relacja pomiędzy tabelami Student i Kierunek. Klucz podstawowy tabeli Kierunek o nazwie id_kierunek połączony jest z kluczem obcym o tej samej nazwie w tabeli Student.

Kolorem niebieskim została pokazana relacja pomiędzy tabelami Wydzial i Kierunek. Klucz podstawowy tabeli Wydzial o nazwie id_wydzial połączony jest z kluczem obcym o tej samej nazwie w tabeli Kierunek.

Poniżej zestawiono w tabelach najważniejsze typy danych obsługiwanie przez MySQL.

|Typ|Ile bajtów|Min (ze znakiem)|Max (ze znakiem)|Min (bez znaku)|Max (bez znaku)|
|---|---|---|---|---|---|
|TINYINT|1|-128|127|0|255|
|SMALLINT|2|-32768|32767|0|65535|
|MEDIUMINT|3|-8388608|8388607|0|16777215|
|INT|4|-2147483648|2147483647|0|4294967295|
|BIGINT|8|-263|263 - 1|0|264 - 1|

|Typ|Rozmiar|Opis|
|---|---|---|
|CHAR[Length]|Length bajtów|Pole o stałej długości, przechowuje od 0 do 255 znaków|
|VARCHAR[Length]|Długość łańcucha + 1 bajt|Pole tekstowe o zmiennej długości|
|TINYTEXT|Długość łańcucha + 1 bajt|Łańcuch o maksymalnej długości 255 znaków|
|TEXT|Długość łańcucha + 2 bajty|Łańcuch o maksymalnej długości 65535 znaków|
|MEDIUMTEXT|Długość łańcucha + 3 bajty|Łańcuch o maksymalnej długości 16777215 znaków|
|LONGTEXT|Długość łańcucha + 4 bajty|Łańcuch o maksymalnej długości 4294967295 znaków|
|FLOAT|4|Mała liczba zmiennoprzecinkowa|
|DOUBLE[Length, Decimals]|8|Duża liczba zmiennoprzecinkowa|
|DECIMAL[Length, Decimals]|Length +1 lub Length + 2|Liczba typu DOUBLE przechowywana w postaci łańcucha, co pozwala na zastosowanie stałej liczby miejsc po przecinku|
|DATE|3|Data w formacie YYYY-MM-DD|
|DATETIME|8|Data w formacie YYYY-MM-DD HH:MM:SS|
|TIMESTAMP|4|Data w formacie YYYYMMDDHHMMSS; dopuszczalny zakres kończy się na rok 2037|
|TIME|3|Czas w formacie HH:MM:SS|
|ENUM|1 lub 2|Typ wyliczeniowy. W kolumnie może się znaleźć jedna z podanych wartości.|
|SET|1, 2, 3, 4 lub 8|Tak samo jak ENUM z tym że w kolumnie może się znaleźć kilka wartości jednocześnie|

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#collapseExample1) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#collapseExample2)

# Zapytanie CREATE

  
### Zapytanie CREATE DATABASE
  
Składnia instrukcji CREATE DATABASE:  
CREATE DATABASE nazwa_bazy_danych;  
  
**Przykład 1:**  

```
CREATE DATABASE magazyn;
```

  

### Zapytanie CREATE TABLE

  

Składnia instrukcji CREATE TABLE:  
CREATE TABLE nazwa_tabeli (nazwa_kolumny typ [atrybuty], ...);  

**Przykład 1:** Zapytanie CREATE TABLE wygenerowane przez phpMyAdmin  
  

```mysql
CREATE TABLE `oferta`
             (
                          `id_oferta`    int(11) NOT NULL,
                          `id_firma`     int(11) NOT NULL,
                          `id_wydzial`   int(11) NOT NULL,
                          `id_kategoria` int(11) NOT NULL,
                          `tytul`        varchar(255) COLLATE utf8_polish_ci NOT NULL,
                          `opis` text COLLATE utf8_polish_ci NOT NULL,
                          `slowa` text COLLATE utf8_polish_ci NOT NULL,
                          `obszary` text COLLATE utf8_polish_ci NOT NULL,
                          `innowacyjnosc` text COLLATE utf8_polish_ci NOT NULL,
                          `id_gotowosc` int(11) NOT NULL,
                          `id_status`   int(11) NOT NULL,
                          `materialy` text COLLATE utf8_polish_ci NOT NULL,
                          `informacje` text COLLATE utf8_polish_ci NOT NULL,
                          `inne` text COLLATE utf8_polish_ci NOT NULL
```

  
**Przykład 2:**  

```mysql
CREATE TABLE dvd  
  (  
     id_dvd  _INT_ NOT NULL PRIMARY KEY auto_increment,  
     tytul   _VARCHAR_(100),  
     gatunek _ENUM_("Horror", "Thriller", "Komedia", "Sensacyjny", "Obyczajowy"),  
     rok     _INT_  
  );
```

Ogólna zasada tworzenia tabel jest taka, że po CREATE TABLE podajemy nazwę tabeli i następnie w nawiasach (,) wprowadzamy nazwę kolumny, jej typ danych ewentualnie argumenty takie jak np: NOT NULL, PRIMARY KEY, DEFAULT wartość, AUTO_INCREMENT. Kolumny oddzielamy przecinkiem. Po nawiasach możemy określić tzw. storage engine - silnik przechowywania informacji. Najważniejsze z nich to: InnoDB, MyISAM, MEMORY, CSV. Pełna składnia zapytania select znajduje się w dokumentacji systemu.

### Tworzenie tabel za pomocą zapytania **SELECT**

  
Składnia instrukcji jest następująca:  
CREATE TABLE nazwa_tabeli SELECT lista_kolumn FROM istniejąca_tabela WHERE warunek  
  
**Przykład 3:**  

```sql
CREATE TABLE modele  
  SELECT marka,  
         model  
  FROM   samochody;
```

**Przykład 4:**  

```sql
CRETAE TABLE tytul_ksiazkiSELECT tytul  
FROM   ksiazki;
```

  

### Zapytanie CREATE VIEW

  
**VIEW** - widok jest to dostęp do wybranej części tabeli wcześniej zdefiniowanej za pomocą zapytania CREATE VIEW. Składnia zapytania CREATE VIEW wygląda następująco:  
CREATE VIEW nazwa_widoku (kolumny) AS SELECT kolumny FROM tabela;  
  
**Przykład 1:**  

```sql
CREATE VIEW miasta (miejscowosc, wojewodzwto)  
AS  
  SELECT miejscowosc,  
         wojewodztwo  
  FROM   student;
```

**Przykład 2:**  


```sql
CREATE VIEW data_wypozyczenia (id_wypozyczono, data_wyp, data_zwrotu)  
AS  
  SELECT id_wypozyczono,  
         data_wyp,  
         data_zwrotu  
  FROM   wypozyczono;
```

Dzięki wykorzystaniu widoków mamy dostęp tylko do wybranej części tabeli.

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#create_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#create_pytania)

# Zapytanie SELECT

  

Aby rozpocząć pracę z językiem SQL - Structured Query Language w pierwszej kolejności zaimportujemy bazę danych [studia](https://home.agh.edu.pl/~pamalino/programowanie/mysql/studia.sql). Mając zapisany plik studia.sql zaimportujemy go do phpMyAdmin za pomocą polecenia import.  

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin4.png "phpMyAdmin")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/phpMyAdmin4.png)  

Można to również wykonać za pomocą konsoli wydając polecenie source ścieżka_do_pliku_sql  
Jeżeli przekopiujemy plik studia.sql do katalogu bin, to nie musimy podawać całej ścieżki tylko nazwę pliku.  

```sql
source studia.sql;
```

  

### Proste zapytania SELECT

  
Przechodzimy do konsoli MySQL i wpisujemy następujące polecenia:  

```mysql
USE studia;
```

```mysql
SHOW tables;
```

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql3.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql3.png)  

Składnia polecenia SELECT  
SELECT kolumna/y  
FROM tabela/e  
WHERE warunek/nki  
GROUP BY kolumna/y  
HAVING  
ORDER BY kolumna/y  
LIMIT  
**SELECT** - oznacza wybierz poszczególne kolumny  
**FROM** - z tabeli  
**WHERE** - gdzie warunki  
  
Przy warunkach korzystamy z operatorów =, >, <, >=, <=, <>, LIKE.  
Operator LIKE wymaga krótkiego wyjaśnienia.  
Operator **LIKE** służy do wyszukiwania odpowiednich wzorców w rekordach tabeli zawężając wyświetlane wyniki.  
  
**Przykład** wykorzystania operatora LIKE:  

```mysql
SELECT *  
FROM   ksiazki  
WHERE  tytul LIKE "%c#%";
```

  

Efektem wykonania się tego zapytania będą wszystkie rekordy tabeli książki, gdzie w tytule znajduje się "C#" czy na początku, w środku lub na końcu tytułu. Wykorzystano tu znak (%), który oznacza nieokreślony ciąg znaków. Istnieje jeszcze jeden znak (_), który oznacza pojedynczy znak.

  
  
**Przykład: Wypisz wszystkie rekordy, gdzie autor ma w nazwisku drugą literę a.**  

```mysql
SELECT *  
FROM   ksiazki  
WHERE  autor LIKE "_a%";
```

  
Klauzula **DISTINCT** powoduje usunięcie powtarzających się wierszy.  
Proszę wyświetlić z jakich województw są studenci.  

```mysql
SELECT wojewodztwo  
FROM   student;
```

  
  
W wyniku wykonania się instrukcji otrzymamy następujące wyniki:  

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/wojewodztwo1.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/wojewodztwo1.png)  

**Przykład zastosowania klauzuli DISTINCT**. Gdy zastosujemy klauzulę DISTINCT wynik będzie inny:  

```mysql
SELECT DISTINCT wojewodztwo  
FROM   student;
```

  

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/wojewodztwo2.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/wojewodztwo2.png)  
  

Widzimy, że po zastosowaniu klauzuli DISTINCT wszystkie wiersze wyświetlone są bez powtórzeń.

  

### Funkcje agregujące

|Lp.|Nazwa|Opis|
|---|---|---|
|1|avg(kolumna)|Wylicza wartość średnią w kolumnie|
|2|count(kolumna)|Zlicza ilość rekordów w tabeli|
|3|min(kolumna)|Podaje minimalną wartość w kolumnie|
|4|max(kolumna)|Podaje maksymalną wartość w kolumnie|
|5|std(kolumna)|Wylicza odchylenie standardowe|
|6|sum(kolumna)|Oblicza sumę wartości w kolumnie|

  

**COUNT()** - to funkcja agregująca posiadająca dwie odmiany - COUNT(*) oraz COUNT(kolumna). Pierwsza z nich zwraca ilość wierszy w tabeli. Druga werjsa zlicza tylko te wystąpienia, gdzie wartość kolummy jest różna od NULL. Funkcja agregująca COUNT może posiadać dwie opcjonalne klauzule GROUP BY oraz HAVING.  
  
Klauzula **GROUP BY** stanowi dodatkowy warunek, który muszą spełniać wiersze. GROUP BY wykorzystaywana jest tylko z funkcjami agregującymi i działa na kolumnach zagregowanych.  
  
Opcjonalna klauzula **HAVING** pozwala wybrać wiersze, w których wynik działania COUNT(*) spełnia podany warunek.  

**Przykład:**  

```mysql
SELECT count(id_student) AS "Liczba studentów", nazwa FROM student, wydzial WHERE student.id_wydzial = wydzial.id_wydzial GROUP By wydzial.nazwa;
```

  
Wykorzystanie klauzuli HAVING:  

```mysql
SELECT _Count_(id_student) AS "Liczba studentów",  
       nazwa  
FROM   student,  
       wydzial  
WHERE  student.id_wydzial = wydzial.id_wydzial  
GROUP  BY wydzial.nazwa;
```

Klauzula **ORDER BY** służy do sortowania wyników według zadanej kolumny rosnąco (ASC) lub malejąco (DESC).  
**Przykład:**  

```mysql
SELECT nazwisko  
FROM   student  
ORDER  BY rok_urodzenia ASC;
```

  
  
Klauzula **LIMIT** służy do ograniczenia ilości wyświetlanych wyników.  
**Przykład:**  

```mysql
SELECT nazwisko  
FROM   student  
ORDER  BY rok_urodzenia ASC  
LIMIT  1;
```

  

### Funkcje numeryczne

  

|Funkcja|Opis|
|---|---|
|ABS()|Wartość bezwzględna.|
|CEILING(x)|Zwraca najmniejszą liczbę całkowitą nie mniejszą niż x.|
|COS(x)|Zwraca cosinus z x, gdzie x jest wartością wyrażoną w radianach|
|DEGREES(r)|Konwertuje kąt z radianów na stopnie.|
|RADIANS(d)|Konwertuje kąt ze stopni na radiany.|
|EXP(x)|Podnosi liczbę e do potęgi x.|
|FLOOR(x)|Zwraca największą liczbę całkowitą nie większą niż x.|
|LOG(x)|Logarytm naturalny|
|LOG10(x)|Logarytm o podstawie 10|
|MOD(x,y)|Reszta z dzielenia x przez y|
|PI()|Zwraca liczbę pi|
|POW(x,y)|Podnosi x do potęgi y|
|RAND()|Zwraca liczbę losową z zakresu 0.0 do 1.0|
|ROUND(x)|Zaokrągla do najbliższej liczby całkowitej|
|SIN(x)|Zwraca sinus liczby x, podanej w radianach|
|SQRT(x)|Zwraca pierwiastek liczby x|
|TAN(x)|Zwraca tangens liczby x, podanej w radianach|
|TRUNCATE(x,d)|Obcina liczbę x do określonej przez d liczby miejsc po przecinku|

  

### Funkcje obsługujące ciągi znaków

  

| Funkcja             | Opis                                                                                                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **ASCII(x)**        | Zwraca kod ASCII pierwszego znaku ciągu x lub 0, gdy ciąg ma zerową długość lub gdy ma wartość NULL.                                                                                             |
| **CHAR(x,y,...)**   | Zwraca ciąg będący złączeniem sekwencji wartości numerycznych traktowanych jako kody ASCII poszczególnych znaków.                                                                                |
| **CONCAT(x,y,...)** | Zwraca ciąg będący złączeniem ciągów podanych jako argumenty lub NULL, jeżeli choć jeden z argumentów ma wartość NULL.                                                                           |
| **FORMAT(x,y)**     | Formatuje liczbę x jako ciąg; formatowana liczba zawiera y miejsc dziesiętnych.                                                                                                                  |
| **INSTR(x,y)**      | Zwraca pozycję podciągu y w ciągu x.                                                                                                                                                             |
| **LEFT(x,y)**       | Zwraca y znaków z lewej strony ciągu x.                                                                                                                                                          |
| **LENGTH(x)**       | Zwraca długość ciągu x.                                                                                                                                                                          |
| **LOWER(x)**        | Zwraca ciąg x skonwertowany do zapisu małymi literami.                                                                                                                                           |
| **MID(x,p,l)**      | Z ciągu x zwraca l znaków rozpoczynając od pozycji p; pierwszy znak ciągu znajduje się na pozycji 1.                                                                                             |
| **RIGHT(x,y)**      | Zwraca y znaków z prawej strony ciągu x.                                                                                                                                                         |
| **RTRIM(x)**        | Usuwa nadmiarowe spacje z końca ciągu x.                                                                                                                                                         |
| **SUBSTR(x,p,l)**   | Zwraca ciąg rozpoczynający się na pozycji p w ciągu x, którego długość jest mniejsza lub równa l; jeżeli nie zostanie podana wartość l, zwracane są wszystkie znaki od pozycji p do końca ciągu. |
| **TRIM(x)**         | Usuwa nadmiarowe spacje na początku i końcu ciągu x.                                                                                                                                             |
| **UPPER(s)**        | Konwertuje ciąg na zapisany wielkimi literami                                                                                                                                                    |

  

### Funkcje do obsługi daty i czasu

  

| Funkcja                                | Opis                                                                                              |
| -------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **DAYOFWEEK(data)**                        | Zwraca dzień tygodnia, przyjmując niedzielę jako 1.                                               |
| **DAYOFMONTH(data)**                       | Zwraca dzień miesiąca, rozpoczynając od 1.                                                        |
| **DAYOFYEAR(data)**                        | Zwraca kolejny dzień roku, rozpoczynając od 1.                                                    |
| **MONTH(data)**                            | Zwraca miesiąc rozpoczynając od 1.                                                                |
| **DAYNAME(data)**                          | Zwraca nazwę dnia tygodnia jako ciąg znaków.                                                      |
| **MONTHNAME(data)**                        | Zwraca nazwę miesiąca jako ciąg znaków.                                                           |
| **YEAR(data)**                             | Zwraca rok.                                                                                       |
| **HOUR(czas)**                             | Zwraca godzinę.                                                                                   |
| **MINUTE(czas)**                           | Zwraca minuty.                                                                                    |
| **SECOND(czas)**                           | Zwraca sekundy.                                                                                   |
| **DATE_ADD(data, INTERVAL wyrażenie typ)** | Dodaje do daty okres zadawany poprzez wyrażenie INTERVAL, np.: DATE_ADD(NOW(), INTERVAL 1 MONTH). |
| **DATE_SUB(data, INTERVAL wyrażenie typ)** | Odejmuje od daty jakiś okres.                                                                     |
| **TO_DAYS(data)**                          | Przelicza datę na liczbę dni od roku 0.                                                           |
| **FROM_DAYS(data)**                        | Przelicza ilość dni na datę.                                                                      |
| **SEC_TO_TIME(sekundy)**                   | Przelicza ilość sekund na wartość typu czas.                                                      |
| **TIME_TO_SEC(czas)**                      | Przelicza wartość typu czas na ilość sekund.                                                      |
| **DATE_FORMAT(data, format)**              | Formatuje datę                                                                                    |
| **CURDATE()**                              | Zwraca bieżącą datę.                                                                              |
| **CURTIME()**                              | Zwraca bieżący czas.                                                                              |
| **NOW()**                                  | Zwraca informację typu TIMESTAMP, zawierającą bieżącą datę i czas.                                |

  

### Formatowanie daty i czasu

  


### Aliasy

  
Alias to inaczej inna nazwa tabeli, kolumny. Przykład:  

```sql
SELECT s.imie     AS "Imię",  
       s.nazwisko AS "Nazwisko",  
       w.nazwa    AS "Wydział"  
FROM   student AS s,  
       wydzial AS w  
WHERE  s.id_student = 1  
       AND s.id_wydzial = w.id_wydzial;
```

  

W przykładzie tym wykorzystaliśmy aliasy w dwóch miejscach - przy nazwie kolumn oraz przy nazwie tabel. Widzimy, że zastosowanie aliasów ułatwia pracę oraz ładnie można zapisać wyniki wyszukiwania.

|Lp.|Pytanie|Rozwiązanie|Wynik|
|---|---|---|---|
|1|Pokaż imię i nazwisko studenta o id = 8.|```<br>SELECT imie, nazwisko FROM student<br>WHERE id_student = 8;<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql4.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql4.png)|
|2|Pokaż imię i nazwisko wszystkich studentów z województwa małopolskiego.|```<br>SELECT imie, nazwisko FROM student<br>WHERE wojewodztwo = "małopolskie";<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql5.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql5.png)|
|3|Pokaż wszystkie dane studentów z pierwszego roku.|```<br>SELECT * FROM student<br>WHERE rok_studiow = 1;<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql6.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql6.png)|
|4|Pokaż wszystkie dane studentów i posortuj je rosnąco po kolumnie nazwisko.|```<br>SELECT * FROM student<br>ORDER BY nazwisko ASC;<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql7.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql7.png)|
|5|Wyświetl imię i nazwisko oraz miasto urodzenia wszystkich studentów z województwa małopolskiego.|```<br>SELECT imie, nazwisko, miejscowosc FROM student<br>WHERE wojewodztwo = "małopolskie";<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql8.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql8.png)|
|6|Wyświetl id_student, imię, nazwisko studentów urodzonych w latach 1997 - 1999.|```<br>SELECT id_student, imie, nazwisko FROM student<br>WHERE rok_urodzenia BETWEEN 1997 AND 1999;<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql9.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql9.png)|
|7|Wyświetl nazwisko najstarszego studenta|```<br>SELECT nazwisko FROM student<br>ORDER BY rok_urodzenia ASC LIMIT 1;<br>```|[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql10.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/mysql10.png)|

  

### Złożone zapytania SELECT

  

Złożone zapytanie ponieważ operuje na co najmniej dwóch tabelach. W poniższym przykładzie wykorzystamy tą samą bazę danych o nazwie studia, ale będziemy korzystać z trzech tabel w celu uzyskania potrzebnych informacji.

| Lp. | Pytanie                                                                                                 | Rozwiązanie                                                                                                                                                                                                                                                                  | Wynik                                                                                                                                                         |
| --- | ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Pokaż imię, nazwisko wszystkich studentów z Wydziału Zarządzania.                                       | SELECT imie, nazwisko, miejscowosc FROM student, kierunek<br>WHERE student.id_kierunek = kierunek.id_kierunek<br>AND kierunek.id_kierunek = 4;                                                                                                                               | [![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select1.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select1.png) |
| 2   | Pokaż imię, nazwisko i miejscowość wszystkich studentów, którzy wybrali kierunek Informatyka Stosowana. | SELECT imie,  <br>       nazwisko,  <br>       miejscowosc  <br>FROM   student,  <br>       kierunek  <br>WHERE  student.id_kierunek = kierunek.id_kierunek  <br>AND    kierunek.id_kierunek =                                                                               | [![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select2.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select2.png) |
| 3   | Pokaż wszystkie kierunki z Wydziału Informatyki.                                                        | SELECT kierunek.nazwa  <br>FROM   kierunek,  <br>       wydzial  <br>WHERE  kierunek.id_wydzial = wydzial.id_wydzial  <br>       AND wydzial.id_wydzial = 1;                                                                                                                 | [![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select3.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select3.png) |
| 4   | Pokaż po ilu studentow jest na każdym wydziale.                                                         | SELECT _Count_(id_student) AS "Liczba studentów",  <br>       nazwa  <br>FROM   student,  <br>       wydzial  <br>WHERE  student.id_wydzial = wydzial.id_wydzial  <br>GROUP  BY wydzial.nazwa;                                                                               | [![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select4.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select4.png) |
| 5   | Pokaż wszystkie wydziały, gdzie jest więcej niż 2 studentow posortowane malejąco po nazwie wydziału.    | SELECT _Count_(id_student) AS "Liczba studentów",  <br>       wydzial.nazwa  <br>FROM   student,  <br>       wydzial  <br>WHERE  student.id_wydzial = wydzial.id_wydzial  <br>GROUP  BY wydzial.nazwa  <br>HAVING _Count_(id_student) > 2  <br>ORDER  BY wydzial.nazwa DESC; | [![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select5.png "konsola")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/Select5.png) |

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#collapseExample3) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#collapseExample4)

# Zapytanie INSERT, UPDATE

### Zapytanie INSERT

  
Zapytanie **INSERT** służy do wprowadzania wierszy do tabeli.  
Składnia zapytania INSERT wygląda następująco:  
INSERT INTO nazwa_tabeli (kolumna1, kolumna2, ... , kolumnaN) VALUES (wartość1, wartość2, ... , warośćN);  
**Przykład 1:**  

```mysql
INSERT INTO kierunek  
            (id_kierunek,  
             nazwa,  
             id_wydzial)  
VALUES      (NULL,  
             "komputerowe wspomaganie procesow inzynierskich",  
             5);
```

**Przykład 2:**  
Równoważna instrukcja wpisująca dane do wszystkich kolumn tabeli kierunek wygląda następująco:  

```mysql
INSERT INTO kierunek  
VALUES      (NULL,  
             "komputerowe wspomaganie proces�w in�ynierskich",  
             5);
```

  
W tej wersji musimy pamiętać by wartości umieszczać zgodnie z kolejnością kolumn. Jeżeli chcemy uzupełnić cały wiersz danej tabeli, to nie musimy specyfikować, które kolumny będziemy uzupełniać po nazwie tabeli, ale musimy pamiętać o odpowiedniej kolejności.  
Kolejność wpisywania kolumn jest dowolna, ale muszą one korespondować z wpisywanymi wartościami.
  
**Przykład 3:**  
Do tabeli możemy wprowadzić dane wybrane przez nas. Przykład:  

```mysql
INSERT INTO student  
            (id_student,  
             imie,  
             nazwisko,  
             rok_urodzenia)  
VALUES      (NULL,  
             "rafał",  
             "cichowski",  
             1995);
```

  
**Przykład 4:**  
Za pomocą jednego zapytania INSERT możemy wprowadzić do tabeli więcej niż jeden wiersz.  

```mysql
INSERT INTO wydzial  
VALUES      (NULL,  
             "wydzia� odlewnictwa"),  
            (NULL,  
             "wydzia� in�ynierii mechanicznej i robotyki"),  
            (NULL,  
             "wydzia� informatyki, elektroniki i telekomunikacji");
```

  
**Przykład 5:**  
Istnieje jeszcze alternatywna instrukcja INSERT bez słowa VALUES.  

```mysql
INSERT INTO wydzial  
SET id_wydzial = NULL,  
    nazwa =  
"wydzia� elektrotechniki, automatyki, informatyki i in�ynierii biomedycznej";
```

  
  

### Zapytanie UPDATE

  

Zapytanie **UPDATE** służy do aktualizacji pola lub całego wiersza.  
Składnia zapytania UPDATE wygląda następująco:  
UPDATE tabela SET kolumna = wartość WHERE warunek;  

**Przykład 1:**  
Adam Nowak studiował na Wydziale Fizyki i Informatyki Stosowanej. Był bardzo dobrym studentem. Postanowił się przenieść na Wydział Informatyki. Zapytanie, które musimy wykonać wygląda następująco:  

```mysql
UPDATE student  
SET    id_wydzial = 1  
WHERE  id_student = 2;
```

  
Gdybyśmy nie umieścili klauzli WHERE nastąpiłaby podmiana wartości id_wydzial = 1 dla wszystkich studentów.  
  
**Przykład 2:**  
Skończył się rok akademicki, skończyła się sesja. Wszyscy studenci uzyskali oceny pozytywne. W bazie danych należy dla każdego studenta zwiększyć wartość kolumny rok_studiow. Zapytanie wygląda następująco:  

```mysql
UPDATE student  
SET    rok_studiow = rok_studiow + 1;
```

  
W typ przypadku każdy student awansował i nie potrzebujemy specyfikować warunku dla klauzuli WHERE.  
  
**Przykład 3:**  
Pani Agnieszka Borówka z Wydziału Zarządzania skończyła urlop dziekański i powróciła na studia. Należy zaktualizować w kolumnie status z wartości urlop wartość na student. Zapytanie wygląda następująco:  
```mysql
UPDATE student  
SET    status = "student"  
WHERE  id_student = 5;
```

  
**Przykład 4:**  
Pani Magdalena Jędraszek wyszła za mąż, zmieniła nazwisko na Kowalczyk i przeprowadziła się do Krakowa. Zapytanie wygląda następująco:  

```mysql
UPDATE student  
SET    nazwisko = "kowalczyk",  
       miejscowosc = "krak�w",  
       wojewodztwo = "ma�opolskie"  
WHERE  id_student = 9;
```

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#collapseExample5) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#collapseExample6)

# Zapytanie DROP, DELETE

  

### Zapytanie DROP

  

Instrukcja DROP usuwa jednocześnie dane i strukturę.  
Składnia instrukcji DROP:  
DROP DATABASE/TABLE/VIEW

**Przykład 1:**  
Proszę usunąć całą bazę danych magazyn.  

```mysql
DROP DATABASE magazyn;
```

**Przykład 2:**  
Proszę usunąć tabelę student.  

```mysql
DROP TABLE student;
```

**Przykład 3:**  
Proszę usunąć widok miasta.  

```mysql
DROP VIEW miasta;
```

  

### Zapytanie DELETE

  

Instrukcja DELETE usuwa dane(wiersze) z tabeli.  
Składnia instrukcji DELETE:  
DELETE FROM tabela WHERE warunek;  

**Przykład 1:**  
Proszę usunąć z tabeli książki, pozycję o id = 88;  

```mysql
DELETE FROM ksiazki  
WHERE  id = 88;
```

  
  
**Przykład 2:**  
Proszę usunąć wszystkie wiersze z tabeli samochody  

```mysql
DELETE FROM samochody;
```

  
  
Alternatywnym zapytaniem wykonującym to samo, czyli usunięcie wierszy z tabeli samochody jest instrukcja TRUNCATE.  
Składnia zapytania TRUNCATE wygląda następująco:  
TRUNCATE TABLE nazwa_tabeli;  
  
**Przykład 3:**  

```mysql
TRUNCATE TABLE samochody;
```

  
  
**Przykład 4:**  
Proszę usunąć z tabeli studenci najstarszego studenta.  

```mysql
DELETE FROM student  
ORDER BY rok_urodzenia  
LIMIT 1;
```

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#drop_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#drop_pytania)

# Instrukcja ALTER

  

Instrukcja **ALTER** służy do modyfikowania struktury tabeli. Możemy dodawać kolumny, usuwać je, zmieniać ich nazwy, typ danych, zmieniać nazwę tabeli, dodawać i usuwać klucz podstawowy.

  
**Dodawanie kolumny**  
  

```mysql
ALTER TABLE ksiazki  
  ADD COLUMN rok_wydania _INT_ after wydawnictwo;
```

  

Instrukcja ta dodaje kolumnę rok_wydania typu całkowitego do tabeli ksiazki zaraz za kolumną wydawnictwo. Jeżeli chcemy dodać kolumnę na początku tabeli jako pierwszą, to zamiast słowa AFTER nazwa kolumny wpisujemy FIRST.

  
**Usuwanie kolumny**  
  

```mysql
ALTER TABLE ksiazki DROP COLUMN rok_wydania;
```

  

Instrukcja ta usuwa kolumnę rok_wydania z tabeli ksiazki.

  
**Zmiana kolumny**  
  

```mysql
ALTER TABLE ksiazki  
  CHANGE COLUMN tytul tytul_ksiazki _VARCHAR_(200);
```

  

Instrukcja ta zmienia kolumnę tytul na kolumnę tytul_ksiazki.

  
**Zmiana nazwy tabeli**  
  

```mysql
ALTER TABLE ksiazki  
  RENAME AS ksiegozbior;
```

  

Instrukcja ta zmienia nazwę tabeli z ksiazki na ksiegozbior.

  
**Dodanie klucza podstawowego**  
  

```mysql
ALTER TABLE ksiazki ADD PRIMARY KEY (autor);
```

  

Instrukcja ta dodaje klucz podstawowy (kolumna autor) do tabeli ksiazki.

  
**Usuwanie klucza podstawowego**  
  

```mysql
ALTER TABLE ksiazki  
  DROP PRIMARY KEY;
```

  

Instrukcja ta usuwa klucz podstawowy z tabeli ksiazki.

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#alter_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#alter_pytania)

# Złączenia JOIN

  

Wyróżniamy kilka typów złączeń:

- Złączenia wewnętrzne - INNER **JOIN**
- Złączenia zewnętrzne - OUTER JOIN
    - Złączenie zewnętrzne lewostronne - **LEFT** OUTER **JOIN**
    - Złączenie zewnętrzne prawostronne - **RIGHT** OUTER **JOIN**
    - Złączenia pełne - **FULL** OUTER **JOIN**
- Iloczyn kartezjański - **CROSS JOIN**
- Samozłączenia - SELF JOIN

Złączenie wewnętrzne dwóch tabel jako wynik podaje część wspólną tych tabel

Złączenie zewnętrzne lewostronne w wyniku daje część wspólną (INNER JOIN) oraz wszystkie rekordy z lewej tabeli

Złączenie zewnętrzne prawostronne jako wynik daje część wspólną dwóch tabel (INNER JOIN) oraz wszystkie rekordy z tabeli po prawej stronie joina

Złączenie pełne w wyniku daje połączenie dwóch tabel

  
[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#join_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#join_pytania)

# Transakcje

  

**Transakcja** stanowi sekwencję powiązanych ze sobą instrukcji, które muszą być traktowane jako całość. Oznacza to, że albo wszystkie instrukcje zawarte w transakcji zostaną wykonane, albo żadna z nich. Każda transakcja posiada pewne charakterystyczne cechy zwane właściwościami **ACID - Atomicity Consistency Isolation Durability**. ACID to inaczej - niepodzielność, spójność, izolacja, trwałość.

- **Atomicity - niepodzielność**. Transakcja musi być wykonana w całości (wszystkie instrukcje), albo wcale (żadna instrukcja).  
    Niepodzielność jak sama nazwa wskazuje, oznacza, że transakcji nie można podzielić. Albo wszystkie zmiany dokonane przez transakcję zostaną zachowane w bazie danych, albo żadna z nich. W razie pojawienia się błędu zewnętrznego byłoby idealnie, gdyby proces odzyskiwania potrafił dokończyć każdą transakcję, która była wykonywana. Jednak akceptowane byłoby również cofnięcie wszystkich zmian, które wchodziły w skład niedokończonych transakcji.
- **Consistency - spójność, integralność danych**. Własność danych wykluczająca zmianę danych w niedozwolony sposób.  
    Spójność oznacza, że operacje przekształcają bazę danych z jednego stanu prawidłowego w inny. Nie mogą wystąpić etapy, w których dane są niespójne. Baza danych powinna również nie zezwalać na operacje, które mogą naruszyć ograniczenia spójności. Jeżeli przechowujemy dane o kontach klientów banku, nie powinno być możliwe utworzenie klienta, który nie istnieje, czy usunięcie klienta z tabeli klientów, jeżeli istnieją jeszcze związane z nim konta.
- **Isolation - izolacja**. Transakcja wykonuje się niezależnie od innych instrukcji, transakcji. Oznacza to, że jeśli dwie transakcje wykonują się równocześnie, to nie widzą wprowadzonych przez siebie zmian.  
    Izolacja oznacza, że transakcje nie kolidują ze sobą, gdy są wykonywane. Każda transakcja powinna być przeprowadzana tak, jakby w danej chwili tylko ona mogła wykonywać operacje odczytu i aktualizacji. W praktyce zwykle tak nie jest, ale blokady używane są do utrzymania takiej iluzji. w zależności od bazy danych i ustawionych opcji, dostępne są różne poziomy izolacji.
- **Durability - trwałość danych**. Oznacza sytuację, w której system zarządzania bazą danych SZBD po awarii potrafi odtworzyć spójne i aktualne dane przed transakcją.  
    Trwałość oznacza, że po wykonaniu transakcji w bazie danych, efekty transakcji są stałe. To wymaganie łatwo byłoby spełnić w prostym programie, ale w rozbudowanym systemie SZBD, w którym można stosować blokowanie i dozwolone są jednoczesny dostęp dla wielu użytkowników oraz buforowanie podręczne - spełnienie tego wymaganie nie jest proste. Poza tym z zapewnienia trwałości wynika, że powinniśmy móc wrócić do obecnego stanu bazy danych w przypadku awarii. Jeżeli wystąpi jakaś katastrofa (awaria zasilania, czy dysku twardego) między wysyłaniem transakcji przez klienta do bazy danych a zapisaniem transakcji na dysk, wtedy powinniśmy móc wykorzystać kopię zapasową oraz dziennik, aby przywrócić bazę danych do jej stanu sprzed katastrofy, a także byłoby dobrze, gdybyśmy jeszcze mogli wykonać transakcje, które zostały wpisane do dziennika, a nie zostały jeszcze wykonane.

  

Baza danych MySQL działa w tak zwanym trybie autocommit (automatyczne zatwierdzanie transakcji). Każda instrukcja w MySQL traktowana jest jako pojedyncza transakcja. Aby można zbudować transakcję z kilku instrukcji musimy wyłączyć tryb autocommit za pomocą instrukcji:  
**SET autocommit = 0;**  
Od tej pory możemy budować transakcje złożone z większej ilości inrukcji.  
Aby powrócić do poprzedniego trybu wpisujemy komendę:  
**SET autocommit = 1;**

Transakcje obsługiwane są przez silnik InnoDB. Aby rozpocząć transakcję należy wydać polecenie:  
**START TRANSACTION**  
lub  
**BEGIN WORK**  
lub po prostu  
**BEGIN**  
Nadstępnie wpisujemy zestaw instrukcji, które wchodzą w skład transakcji. Aby transakcja się wykonała wpisujemy polecenie:  
**COMMIT;**  

W tym momencie wszystkie instrukcje wchodzące w skład transakcji zostaną wykonane. W przypadku gdy chcemy przywrócić stan bazy danych do momentu przed transakcją, to nie wpisujemy instrukcji COMMIT zatwierdzającej transakcję tylko instrukcję:  
**ROLLBACK;**  
Instrukcja ROLLBACK cofa wszystkie wykonane instrukcje zawarte w danej transakcji.

  
**Przykład 1:**  

```
MariaDB [test]> CREATE TABLE test(liczba int);
Query OK, 0 rows affected (0.02 sec)
MariaDB [test]> BEGIN;
Query OK, 0 rows affected (0.00 sec)
MariaDB [test]> INSERT INTO test VALUES(23);
Query OK, 1 row affected (0.00 sec)
MariaDB [test]> SELECT liczba FROM test;
+--------+
| liczba |
+--------+
|     23 |
+--------+
1 row in set (0.00 sec)
MariaDB [test]> ROLLBACK;
Query OK, 0 rows affected (0.01 sec)
MariaDB [test]> SELECT liczba FROM test;
Empty set (0.00 sec)
```

  

Instrukcja BEGIN rozpoczyna transakcję. Wykonujemy instrukcję INSERT, następnie SELECT i widzimy zapisane wyniki w tabeli. Instrukcja ROLLBACK odwołuje to, co dotąd wykonaliśmy w ramach transakcji - czyli wycofuje wprowadzone do tabeli dane. Pokazuje to ostatnia instrukcja SELECT, która nie zwróciła żadnych wyników.

  
**Przykład 2:**  
**Sesja 1:**  

```
MariaDB [test]> BEGIN;
Query OK, 0 rows affected (0.00 sec)
MariaDB [test]> INSERT INTO test VALUES(33);
Query OK, 1 row affected (0.00 sec)
MariaDB [test]> SELECT liczba FROM test;
+--------+
| liczba |
+--------+
|     33 |
+--------+
1 row in set (0.00 sec)
```

  
**Sesja 2:**  

```
MariaDB [test]> SELECT liczba FROM test;
Empty set (0.00 sec)
```

  
**Sesja 1:**  

```
MariaDB [test]> COMMIT;
Query OK, 0 row affected (0.00 sec)
```

  
**Sesja 2:**  

```
MariaDB [test]> SELECT liczba FROM test;
+--------+
| liczba |
+--------+
|     33 |
+--------+
1 row in set (0.00 sec)
```

  
Poziomy izolacji transakcji (wymienione w kolejności rosnącej szczelności izolacji:

- READ UNCOMMITED
- READ COMMITED
- REPEATABLE READ
- SERIALIZABLE

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#transakcje_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#transakcje_pytania)

# Administracja bazą danych

  

### Tworzenie konta użytkownika

  

Utwórz konto użytkownika student pracującego lokalnie z hasłem: haslo.

```mysql
CREATE USER student@localhost IDENTIFIED BY 'haslo';
```

student@localhost - oznacza użytkownik@host

  

### Usuwanie konta użytkownika

  

Usuń konto użytkownika student na localhost

```mysql
DROP USER student@localhost;
```

  

### Nadawanie uprawnień

  

Nadaj wszystkie uprawnienia dla wszystkich baz danych i dla wszystkich tabel dla użytkownika student pracującego na localhost

```mysql
GRANT ALL  ON *.* TO student@localhost
```

*.* - oznacza wszystkie bazy danych.wszystkie tabele

  

### Odbieranie uprawnień

  

Odbierz wszystkie uprawnienia dla wszystkich baz danych i dla wszystkich tabel użytkownikowi student pracującemu na localhost

```mysql
REVOKE ALL ON *.* from student@localhost;
```

  

### Uprawnienia

  

|Słowo kluczowe|Znaczenie|
|---|---|
|ALL|Nadaje użytkownikowi wszystkie wymienione dalej uprawnienia|
|ALL PRIVILEGES|Takie samo jak ALL|
|ALTER|Pozwala na wykonywanie polecenia ALTER tabela|
|CREATE|Pozwala na tworzenie baz danych i tabel|
|DELETE|Pozwala na usuwanie danych z tabel|
|DROP|Pozwala na usuwanie baz danych i tabel|
|FILE|Pozwala na dostęp do plików zapisanych na serwerze|
|INDEX|Pozwala na zarządzanie indeksami|
|INSERT|Pozwala na wstawianie danych do tabel|
|PROCESS|Pozwala na przeglądanie informacji o procesie serwera|
|RELOAD|Pozwala na powtórne załadowanie informacji z tabel uprawnień do serwera|
|SELECT|Pozwala na pobieranie danych z tabel|
|SHUTDOWN|Pozwala na zatrzymanie bazy danych|
|UPDATE|Pozwala na zmianę informacji w tabelach|
|USAGE|Pozwala na utworzenie konta użytkownika bez żadnych uprawnień|

To samo możemy również wykonać przy pomocy phpMyAdmin.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/dodaj_konto.png "Dodawanie użytkownika")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/dodaj_konto.png)

  

### Kopia zapasowa

  

**Kopia zapasowa** - dane, które mają służyć do odtworzenia oryginalnych danych w przypadku ich utraty lub uszkodzenia.  
Wykonanie kopii zapasowej jest działaniem koniecznym jeśli pracujemy modyfikujemy, kasujemy dane.

  

**mysqldump** - narzędzie do tworzenia kopii zapasowej systemu MySQL.  
Składnia polecenia mysqldump  
**kopia zapasowa:** mysqldump -u user -p[haslo] [nazwa_bazy] > plik.sql  
**odzyskiwanie kopii zapasowej:** mysql -u user -p[haslo] [nazwa_bazy] < plik.sql

  
**Przykład:** - Proszę utworzyć kopię zapasową bazy danych biblioteka.  
  

```bash
mysqldump -u root biblioteka > biblioteka.sql
```

  
  

```bash
-- MySQL dump 10.16  Distrib 10.1.34-MariaDB, for Win32 (AMD64)
--
-- Host: localhost    Database: biblioteka
-- ------------------------------------------------------
-- Server version	10.1.34-MariaDB

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Temporary table structure for view `data_wypozyczenia`
--

DROP TABLE IF EXISTS `data_wypozyczenia`;
/*!50001 DROP VIEW IF EXISTS `data_wypozyczenia`*/;
SET @saved_cs_client     = @@character_set_client;
SET character_set_client = utf8;
/*!50001 CREATE TABLE `data_wypozyczenia` (
  `id_wypozyczono` tinyint NOT NULL,
  `data_wyp` tinyint NOT NULL,
  `data_zwrotu` tinyint NOT NULL
) ENGINE=MyISAM */;
SET character_set_client = @saved_cs_client;

--
-- Table structure for table `ksiazki`
--

DROP TABLE IF EXISTS `ksiazki`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `ksiazki` (
  `id_ksiazki` int(11) NOT NULL AUTO_INCREMENT,
  `tytul` varchar(200) COLLATE utf8_polish_ci DEFAULT NULL,
  `autor` varchar(50) COLLATE utf8_polish_ci DEFAULT NULL,
  `wydawnictwo` varchar(30) COLLATE utf8_polish_ci DEFAULT NULL,
  PRIMARY KEY (`id_ksiazki`)
) ENGINE=InnoDB AUTO_INCREMENT=225 DEFAULT CHARSET=utf8 COLLATE=utf8_polish_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `ksiazki`
--

LOCK TABLES `ksiazki` WRITE;
/*!40000 ALTER TABLE `ksiazki` DISABLE KEYS */;
INSERT INTO `ksiazki` VALUES (65,'Sprzedaj swój software','Hasted Edward','Wiley'),(66,'Visual Basic .NET - Księga przykładów','Macdonald Matthew','Microsoft Press'),(67,'Core C# i .NET','Perry Stephen C.','Prentice Hall PTR'),(68,'Wprowadzenie do systemów baz danych','Elmasri Ramez, Navathe Shamkant B.','Addison-Wesley'),(69,'HTML i CSS. Zaprojektuj i zbuduj witrynę WWW','Duckett Jon','John Wiley & Sons'),(70,'Adobe Flash CS3 Professional. Oficjalny podręcznik','Galvan Richard','Adobe Press'),(71,'Flash. Filmy i dźwięk. Techniki zaawansowane','Aleo Tania','FoED Press'),(72,'Flash MX 2004. Skuteczne rozwiązania','Elliott Shane','New Riders'),(73,'Flash MX 2004. Sztuka projektowania','Rebenschied Shane, Weinman Lynda','Peachpit Press'),(74,'Tworzenie stron WWW we Flashu CS3 Professional','Morris David','Peachpit Press'),(75,'Flash MX 2004. Same konkrety','Bhangal Sham, deHaan Jen','Sybex'),(76,'Macromedia Flash MX 2004','deHaan Jen','Macromedia Press'),(77,'Macromedia Flash MX 2004. Biblia','Reinhardt Robert, Dowd Snow','John Wiley & Sons'),(78,'Macromedia Flash 8. Oficjalny podręcznik','English James','Pearson Education'),(79,'Visual C# 2005 Express Edition. Od podstaw','Matulewski Jacek','Helion'),(80,'Przejście do VB.NET','Appleman Dan','Apress'),(81,'Tworzenie aplikacji graficznych w .NET 3.0','Rychlicki-Kicior Krzysztof','Helion'),(82,'Visual Basic .NET. Praktyczny kurs','Czogalik Bogdan','Helion'),(83,'Wprowadzenie do .NET','Conard James','Wrox Press'),(84,'Programowanie C#','Liberty Jesse','O\'Reilly'),(85,'Visual Basic .NET oraz Visual C# .NET w programowaniu obiektowym','Reynolds-Haertle Robin A.','Microsoft Press'),(86,'Visual C# 2005. Zapiski programisty','Liberty Jesse','O\'Reilly'),(87,'ASP.NET. Programowanie','Liberty Jesse, Hurwitz Dan','O\'Reilly'),(88,'SQL Server 2005 Express. Skuteczne rozwiązania','Mendrala Danuta, Szeliga Marcin','Helion'),(89,'Sztuka programowania SQL.','Faroult Stephane, Robson Peter','O\'Reilly'),(90,'MySQL Podstawy','Welling Luke, Thomson Laura','Pearson Education'),(91,'MySQL. Ćwiczenia','Nowakowski Marek','Helion'),(92,'Bazy danych. Europejski Certyfikat Umiejętności Komputerowych','Kopertowska Mirosława','Mikom'),(93,'Bazy danych i PostrgeSQL','Stones Richard, Matthew Neil','Wrox Press'),(94,'Bazy danych dla zwykłych śmiertelników','Hernandez Michael J.','Addison-Wesley'),(95,'PostgreSQL','Momjian Bruce','Addison-Wesley'),(96,'HTML5 nieoficjalny podręcznik','Macdonald Matthew','O\'Reilly'),(97,'Projektowanie stron internetowych','Robbins Jennifer Niederst','O\'Reilly'),(98,'HTML5. Przewodnik profesjonalisty','Stevens Luke, Owen RJ','Apress'),(99,'HTML5. Strony mobilne','Weyl Estelle','O\'Reilly'),(100,'Aplikacje 3D. Przewodnik po HTML5, WebGL i CSS3','Parisi Tony','O\'Reilly'),(101,'HTML5. Programowanie aplikacji','Kessin Zachary','O\'Reilly'),(102,'HTML5 i CSS3. Praktyczne projekty','Gajda Włodzimierz','Helion'),(103,'HTML5. Tworzenie gier z wykorzystaniem CSS i Javascript','Bunyan Karl','Helion'),(104,'Single Page Web Applications. Programowanie aplikacji internetowych z JavaScript','Mikowski Michael, Powell Josh','Helion'),(105,'Web development. Receptury nowej generacji','Hogan Brian P.','Helion'),(106,'Podręcznik projektantów WWW','Friedman Vitaly, Lennartz Sven','Smashing Media'),(107,'HTML5. Tworzenie gier','Seidelin Jacob','Helion'),(108,'CSS. Witryny internetowe szyte na miarę','Wyke-Smith Charles','New Riders'),(109,'Bootstrap. Tworzenie interfejsów stron WWW.','Rahman Syed Fazle','SitePoint'),(110,'Responsive Web Design. Nowoczesne strony WWW na przykładach','Firdaus Thoriq','Packt Publishing'),(111,'Responsive Web Design. Projektowanie elastycznych witryn w HTML5 i CSS3','Frain Ben','Packt Publishing'),(112,'Solidworks 2006 w praktyce','Babiuch Mirosław','Helion'),(113,'Jak zarabiać w Internecie. Poradnik dla przedsiębiorczych webmasterów.','Grzesiak Paweł','Helion'),(114,'Spam. Profilaktyka i obrona','Danowski Bartosz, Kozicki Łukasz','Helion'),(115,'MS Office 2000 i 2002/XP. Tworzenie własnych aplikacji w VBA.','Łoś Maciej','Helion'),(116,'Podstawy ochrony komputerów.','Lehtinen Rick, Russel Deborah','O\'Reilly'),(117,'Poczta elektroniczna','Fabicki Dariusz','Mikom'),(118,'Joomla! System zarządzania treścią','Graf Hagen','Packt Publishing'),(119,'Windows Small Business Server 2003. Administracja systemem.','Snedaker Susan, Bendell Daniel H.','Syngress Publishing'),(120,'Slackware Linux','Sokół Radosław','Helion'),(121,'Blender. Kompendium.','Kuklo Kamil, Kolmaga Jarosław','Helion'),(122,'Więcej niż architektura oprogramowania','Hohmann Luke','Addison-Wesley'),(123,'75 sposobów na statystykę. Jak zmierzyć świat i wygrać z prawdopodobieństwem.','Frey Bruce','O\'Reilly'),(124,'Piękny kod. Tajemnice mistrzów programowania.','Oram Andy, Wilson Greg','Helion'),(125,'Hacking. Sztuka penetracji.','Erickson Jon','Helion'),(126,'PGP. Szyfrowanie informacji. Ćwiczenia praktyczne','Czarny Piotr','Helion'),(127,'Karta elektroniczna - bezpieczny nośnik informacji.','Kubas Monika, Molski Marian','Mikom'),(128,'Apache. Agresja i ochrona.','Anonim','Sams'),(129,'Język C++','Stroustrup Bjarne','Wydawnictwo Naukowo-Techniczne'),(130,'Biblia TCP/IP tom 1. Protokoły','Stevens W. Richard','Addison-Wesley'),(131,'OpenGL. Księga eksperta','Wright Richard S., Lipchak Benjamin','Sams'),(132,'Excel w biznesie. Praktyczne zastosowania','Abdulezer Loren','Wiley'),(133,'Thinking in C++','Eckel Bruce','Pearson Education'),(134,'Photoshop CS3 PL.','Owczarz-Dadan Anna','Helion'),(135,'SCSI i IDE - protokoły, zastosowania i programowanie','Schmidt Fridhelm','Addison-Wesley'),(136,'Sieci komputerowe. Kompendium.','Krysiak Karol','Helion'),(137,'Cisza w sieci','Zalewski Michał','Helion'),(138,'Google App Engine. Tworzenie wydajnych aplikacji w Javie.','de Jonge Adriaan','Addison-Wesley'),(139,'Cuda w przykładach','Sanders Jason, Kandrot Edward','Addison-Wesley'),(140,'BIOS przewodnik','Pyrchla Andrzej, Danowski Bartosz','Helion'),(141,'Netykieta czyli kodeks dla internautów.','Van der Leun Gerard, Mandel Thomas','Mikom'),(142,'Podpis elektroniczny','Dąbrowski Włodzimierz, Kowalczuk Przemysław','Mikom'),(143,'Sieci miejscowe PROFIBUS','Sacha Krzysztof','Mikom'),(144,'Thinking in Java','Eckel Bruce','Prentice Hall PTR'),(145,'Dane w sieci WWW od relacji do modelu semistrukturalnego i XML.','Abiteboul Serge, Buneman Peter,Suciu Dan','Mikom'),(146,'Excel w nauce i technice. Receptury.','Bourg David M.','O\'Reilly'),(147,'Asembler w koprocesorze','Kruk Stanisław','Mikom'),(148,'Zarządzanie projektami. Sztuka przetrwania.','Jones Richard','MT Biznes'),(151,'Programowanie funkcyjne z JavaScriptem. Sposoby na lepszy kod','Atencio Luis','Helion'),(152,'Bazy danych i MySQL. Od podstaw','Stones Richard, Matthew Neil','Wrox Press'),(153,'Internetowi milionerzy czyli jak zdobyć fortunę online.','Fox Scott','Helion'),(154,'Mała książeczka która podbija rynek','Greenblatt Joel','MT Biznes'),(155,'Sztuka motywacji','McGinnis Alan Loy','Vocatio'),(156,'Jak napisać biznesplan','Finch Brian','One Press'),(157,'Psychologia inwestowania','Nofsinger John R.','One Press'),(158,'Sztuka bycia towarzyskim czyli jak odnaleźć się w każdej sytuacji','Martinet Jeanne','Sensus'),(159,'Zapanować nad czasem. Jak efektywnie pracować, by mieć czas na wszystko','Prentice Steve','Wiley'),(160,'Więcej przebojowości! Jak pewnie kroczyć przez życie.','Ryan M.J.','Sensus'),(161,'Sztuka bycia atrakcyjnym. Sekrety osobistego magnetyzmu.','Hogan Kevin, Labay Mary Lee','Sensus'),(162,'Alchemia sprzedaży czyli jak skutecznie sprzedawać produkty, usługi, pomysły i wizerunek samego siebie','Pankiewicz Konrad','One Press'),(163,'Struktura magii. Kształtowanie ludzkiej psychiki, czyli więcej niż NLP.','Bandler Richard, Grinder John','One Press'),(164,'Siła motywacji - jak dopingować siebie i ludzi, z którymi pracujesz','Kordziński Jarosław','One Press'),(165,'Sztuka obserwacji czyli skuteczne studiowanie drugiego człowieka','Dimitrius Jo-Ellan, Mazarella Mark C.','Sensus'),(166,'Sekretny język biznesu. Rozszyfruj każdego w 3 sekundy.','Hogan Kevin','One Press'),(167,'Getting Things Done','Allen David','One Press'),(168,'Nowa era komunikacji','Green John O.','PrÃ³szyÅ„ski i S-ka'),(169,'Sztuka negocjacji w stylu Donalda Trumpa','Ross George H.','One Press'),(170,'Mroczna wiedza. Podręcznik manipulacji umysłami.','Lung Haha, Prowant Christopher B.','Sensus'),(171,'JavaScript. Leksykon kieszonkowy','Flanagan David','O\'Reilly'),(172,'PHP4. Leksykon kieszonkowy','Lerdorf Rasmus','O\'Reilly'),(173,'HTML. Leksykon kieszonkowy','Niederst Jennifer','O\'Reilly'),(174,'E-marketing w akcji, czyli jak skutecznie wzbudzać pożądanie klientów i zazdrość konkurencji','Pankiewicz Konrad','One Press'),(175,'Prowadź BLOG. Przewodnik dla małych firm.','Wibbels Andy','One Press'),(176,'Sztuka perswazji czyli język wpływu i manipulacji','Batko Andrzej','One Press'),(177,'Marketing partyzancki. Jak za darmo wypromować swój biznes.','Levinson Jay Conrad','One Press'),(178,'12 sposobów na supermózg. Jak przetrwać w pracy, domu i szkole.','Medina John','PrÃ³szyÅ„ski i S-ka'),(179,'Pozyskiwanie nowych klientów. 151 błyskotliwych rozwiązań.','Wilson Jerry R.','One Press'),(180,'Zarządzanie wzrostem firmy','Mohr Angie','One Press'),(181,'Biznesowy savoir-vivre','Pachter Barbara, Magee Susan','One Press'),(182,'Podręcznik manipulacji. Zakazana retoryka.','Beck Gloria','Sensus'),(183,'Generator charyzmy. Kreowanie osobowości menedżera.','Smółka Paweł','Sensus'),(184,'PHP5, Apache i MySQL. Od podstaw.','Naramore Elizabeth, Gerner Jason, ...','Wrox Press'),(185,'Funkcjonalność stron internetowych','Pearrow Mark','Helion'),(186,'CSS. Kaskadowe arkusze stylów. Przewodnik encyklopedyczny.','Meyer Eric A.','O\'Reilly'),(187,'PHP. 101 praktycznych skryptów.','Lis Marcin','Helion'),(188,'XHTML w przykładach.','Navarro Ann','Mikom'),(189,'Zostań webmasterem','Wimmer Paweł','Helion'),(190,'HTML i XHTML. Przewodnik encyklopedyczny.','Musciano Chuck, Kennedy Bill','O\'Reilly'),(191,'HTML 4. Ćwiczenia praktyczne.','Danowski Bartosz','Helion'),(192,'Projektowanie stron www. Jak to zrobić?','Williams Robin, Tollet John','Helion'),(193,'ABC kaskadowych arkuszy stylów.','Danowski Bartosz','Helion'),(194,'Projektowanie serwisów WWW. Standardy sieciowe.','Zeldman Jeffrey','New Riders'),(195,'HTML i XHTML dla każdego.','Lemay Laura','Sams'),(196,'MySQL.','DuBois Paul','Mikom'),(197,'CSS według Erica Meyera. Sztuka projektowania stron WWW.','Meyer Eric A.','New Riders'),(198,'505 praktycznych skryptów dla webmastera.','Lis Marcin','Helion'),(199,'PHP i MySQL. Dynamiczne strony WWW.','Ullman Larry','Helion'),(200,'PHP i MySQL. Tworzenie sklepów internetowych.','Bargieł Daniel, Marek Sebastian','Helion'),(201,'PHP i MySQL. Tworzenie stron WWW. Vademecum profesjonalisty.','Welling Luke, Thomson Laura','Helion'),(202,'Po prostu DHTML. Dynamic HTML.','Teague Jason Cranford','Helion'),(203,'Techniki programowania. Visual Basic .NET','Connel John','Microsoft Press'),(204,'PHP4. Od podstaw.','Choi Wankyu, Kent Allan, Lea Chris','Wrox Press'),(205,'Serwisy WWW. Projektowanie, tworzenie i zarządzanie.','Cohen June','New Riders'),(206,'Po prostu HTML4.','Castro Elizabeth','Helion'),(207,'Podstawy Microsoft .NET','Platt David S.','Wydawnictwo RM'),(208,'Sieci VPN. Zdalna praca i bezpieczeństwo danych.','Serafin Marek','Helion'),(209,'Programowanie baz danych w Visual Basic .NET.','Thomsen Carsten','Apress'),(210,'Microsoft Visual Basic .NET','Halvorson Michael','Wydawnictwo RM'),(211,'Visual Basic 2005. Zapiski programisty.','Macdonald Matthew','O\'Reilly'),(212,'PHP, MySQL i Apache dla każdego.','Meloni Julie C.','Sams'),(213,'Zarządzanie projektami IT. Poznaj najskuteczniejsze metody zarządzania przedsięwzięciami informatycznymi','Phillips Joseph','One Press'),(214,'Jak zwiększyć poczucie własnej wartości. Trening.','Schiraldi Glenn R.','Sensus'),(215,'Zarządzanie dla bystrzaków.','Nelson Bob','Helion'),(216,'Niech klienci tłoczą się u Twoich drzwi.','Edwards Paul, Edwards Sarah, Douglas Laura Clampit','One Press'),(217,'Zarządzanie projektami.','Mingus Nancy','One Press'),(218,'Zarządzanie czasem. Strategie dla administratorów systemów.','Limoncelii Thomas A.','O\'Reilly'),(219,'Giełda. Podstawy inwestowania.','Zaremba Adam','One Press'),(220,'Sztuka pisania oprogramowania.','Spolsky Joel','Helion'),(221,'Sekrety skutecznych prezentacji multimedialnych.','Lenar Paweł','One Press'),(222,'Superpamięć. Trening z Kevinem Trudeau','Trudeau Kevin','Sensus'),(223,'Jak być asertywnym? Trening.','Paterson Randy J.','Sensus'),(224,'Efektywne zarządzanie projektami.','Wysocki Robert K., McGary Rudd','One Press');
/*!40000 ALTER TABLE `ksiazki` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `student`
--

DROP TABLE IF EXISTS `student`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `student` (
  `id_student` int(11) NOT NULL AUTO_INCREMENT,
  `imie` varchar(20) COLLATE utf8_polish_ci NOT NULL,
  `nazwisko` varchar(30) COLLATE utf8_polish_ci NOT NULL,
  `id_wydzial` int(11) NOT NULL,
  `id_kierunek` int(11) NOT NULL,
  `nr_albumu` int(11) NOT NULL,
  `rok_studiow` int(11) NOT NULL,
  `miejscowosc` varchar(30) COLLATE utf8_polish_ci NOT NULL,
  `wojewodztwo` varchar(30) COLLATE utf8_polish_ci NOT NULL,
  `rok_urodzenia` int(11) NOT NULL,
  `status` enum('student','urlop','skreslony','absolwent') COLLATE utf8_polish_ci NOT NULL,
  PRIMARY KEY (`id_student`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8 COLLATE=utf8_polish_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `student`
--

LOCK TABLES `student` WRITE;
/*!40000 ALTER TABLE `student` DISABLE KEYS */;
INSERT INTO `student` VALUES (1,'Jan','Kowalski',1,1,34772,3,'Kielce','świętokrzyskie',1999,'student'),(2,'Adam','Nowak',2,4,34553,1,'Kalisz','wielkopolskie',2000,'student'),(3,'Michał','Szczęsny',2,5,34557,2,'Opole','opolskie',1997,'skreslony'),(4,'Jakub','Przygoński',3,8,34554,4,'Kraków','małopolskie',1998,'urlop'),(5,'Agnieszka','Borówka',3,7,34775,2,'Tarnów','małopolskie',1996,'urlop'),(6,'Izabela','Skała',3,6,34211,5,'Krosno','podkarpackie',1995,'absolwent'),(7,'Bożena','Kralisz',1,2,34675,1,'Częstochowa','śląskie',1999,'student'),(8,'Damian','Izdebski',2,4,34212,3,'Katowice','śląskie',1997,'skreslony'),(9,'Magdalena','Jędraszek',4,9,34222,4,'Iława','warmińsko-mazurskie',1997,'student'),(10,'Justyna','Kędzior',3,7,34556,1,'Wrocław','dolnośląskie',2000,'student');
/*!40000 ALTER TABLE `student` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `wypozyczono`
--

DROP TABLE IF EXISTS `wypozyczono`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `wypozyczono` (
  `id_wypozyczono` int(11) NOT NULL AUTO_INCREMENT,
  `id_student` int(11) NOT NULL,
  `id_ksiazki` int(11) NOT NULL,
  `data_wyp` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  `data_zwrotu` datetime NOT NULL,
  PRIMARY KEY (`id_wypozyczono`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8 COLLATE=utf8_polish_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `wypozyczono`
--

LOCK TABLES `wypozyczono` WRITE;
/*!40000 ALTER TABLE `wypozyczono` DISABLE KEYS */;
INSERT INTO `wypozyczono` VALUES (1,9,131,'2018-10-05 10:23:55','2018-10-22 00:00:00'),(2,7,101,'2018-10-05 10:23:59','2018-10-25 00:00:00'),(3,4,125,'2018-10-05 10:24:04','2018-10-13 00:00:00'),(4,2,75,'2018-10-02 08:24:35','2018-10-23 00:00:00'),(5,6,90,'2018-08-07 08:25:02','2018-10-19 00:00:00'),(6,6,112,'2018-10-05 10:23:25','2018-10-17 00:00:00'),(7,9,93,'2018-10-05 10:23:25','2018-10-27 00:00:00'),(8,1,66,'2018-10-05 10:23:25','2018-10-30 00:00:00'),(9,5,111,'2018-10-05 10:23:25','2018-10-29 00:00:00'),(10,4,123,'2018-10-05 10:23:25','2018-11-15 00:00:00'),(11,8,143,'2018-10-05 10:23:25','2018-10-15 00:00:00'),(12,6,111,'2018-10-05 10:23:25','2018-10-22 00:00:00');
/*!40000 ALTER TABLE `wypozyczono` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Final view structure for view `data_wypozyczenia`
--

/*!50001 DROP TABLE IF EXISTS `data_wypozyczenia`*/;
/*!50001 DROP VIEW IF EXISTS `data_wypozyczenia`*/;
/*!50001 SET @saved_cs_client          = @@character_set_client */;
/*!50001 SET @saved_cs_results         = @@character_set_results */;
/*!50001 SET @saved_col_connection     = @@collation_connection */;
/*!50001 SET character_set_client      = cp852 */;
/*!50001 SET character_set_results     = cp852 */;
/*!50001 SET collation_connection      = cp852_general_ci */;
/*!50001 CREATE ALGORITHM=UNDEFINED */
/*!50013 DEFINER=`root`@`localhost` SQL SECURITY DEFINER */
/*!50001 VIEW `data_wypozyczenia` AS select `wypozyczono`.`id_wypozyczono` AS `id_wypozyczono`,`wypozyczono`.`data_wyp` AS `data_wyp`,`wypozyczono`.`data_zwrotu` AS `data_zwrotu` from `wypozyczono` */;
/*!50001 SET character_set_client      = @saved_cs_client */;
/*!50001 SET character_set_results     = @saved_cs_results */;
/*!50001 SET collation_connection      = @saved_col_connection */;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2018-10-25 12:45:28
```

  

Kopię zapasową możemy również wykonać przy pomocy phpMyAdmin.

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/backup.png "Backup")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/backup.png)

  

### Odtwarzanie kopii zapasowej

  

**Przykład:** - Proszę odtworzyć kopię zapasową bazy danych biblioteka.

```bash
mysql -u root biblioteka_test < biblioteka.sql
```

  

Kopię zapasową można odtworzyć również za pomocą narzędzia phpMyAdmin.

  

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/tworzenie_bazy.png "Backup")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/tworzenie_bazy.png)

  

[![](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/wczytywanie_pliku.png "Backup")](https://home.agh.edu.pl/~pamalino/programowanie/mysql/img/wczytywanie_pliku.png)

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#administracja_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#administracja_pytania)

# Normalizacja bazy danych

  

**Normalizacja** to bezstratny proces organizowania danych w tabelach mający na celu zmniejszenie ilości danych składowanych w bazie oraz wyeliminowanie potencjalnych anomalii związanych z przechowywaniem danych.

### Postacie normalne

**Pierwsza postać normalna (1NF)**  

Pierwsza postać normalna (1NF) - mówi o atomowości danych. Czyli każde pole przechowuje tylko jedną informację. Wartość każdego pola jest niepodzielna.

  

```
+------+------+----------+--------------------------------+
| id   | imie | nazwisko | jezyki                         |
+------+------+----------+--------------------------------+
|    1 | Jan  | Kowalski | angielski, niemiecki, rosyjski |
+------+------+----------+--------------------------------+
```

  
Jest to przykład nieznormalizowanej bazy, ponieważ widać, że kolumna języki zawiera więcej niż jedną wartość. W celu normalizacji bazy danych i dostosowania do pierwszej postaci normalnej (1NF) należy zamienić wartości w kolumnie jezyki na wartości niepodzielne.  

```
+------+------+----------+-----------+
| id   | imie | nazwisko | jezyki    |
+------+------+----------+-----------+
|    1 | Jan  | Kowalski | angielski |
|    2 | Jan  | Kowalski | niemiecki |
|    3 | Jan  | Kowalski | rosyjski  |
+------+------+----------+-----------+
```

  
**Druga postać normalna (2NF)**  

Druga postać normalna (2NF) - oznacza, że każda tabela powinna przechowywać informacje dotyczące tylko jednego typu obiektu.

  

```
+------+------+----------+
| id   | imie | nazwisko |
+------+------+----------+
|    1 | Jan  | Kowalski |
+------+------+----------+
```

  

```
+------+-----------+
| id   | jezyki    |
+------+-----------+
|    1 | angielski |
|    1 | niemiecki |
|    1 | rosyjski  |
+------+-----------+
```

  
**Trzecia postać normalna (3NF)**  

Trzecia postać normalna (3NF) - oznacza, że kolumna, która nie należy do klucza głównego nie zależy od innej kolumny.

  

Baza danych przed normalizacją.

  

```
+------------+------+----------+------------+-----------------------+
| id_student | imie | nazwisko | id_wydzial | nazwa_wydzialu        |
+------------+------+----------+------------+-----------------------+
|          1 | Jan  | Kowalski |          1 | Automatyka i Robotyka |
+------------+------+----------+------------+-----------------------+
```

  

Kolumna nazwa_wydzialu zależy nie tylko od klucza głównego czyli id_student, ale również od kolumny id_wydział. W związku z tym należy wydzielić kolumnę nazwa_wydziału do nowej tabeli i połączyć ją z id_wydziału. Natomiast w poprzedniej tabeli pozostawić id_wydział.

  

```
+------------+------+----------+------------+
| id_student | imie | nazwisko | id_wydzial |
+------------+------+----------+------------+
|          1 | Jan  | Kowalski |          1 |
+------------+------+----------+------------+
```

  

```
+------------+-----------------------+
| id_wydzial | nazwa_wydzialu        |
+------------+-----------------------+
|          1 | Automatyka i Robotyka |
+------------+-----------------------+
```

  
**Zalety normalizacji bazy danych:**

- zmniejszamy ogólną liczbę danych przechowywanych w bazach,
- rozwiązujemy problemy anomalii dodawania, modyfikacji i usuwania informacji (rekordów) z bazy,
- czasem spowalniamy wykonywanie zapytań – cena jaką płacimy za konieczność łączenia tabel,
- ale też przyspieszamy wykonywanie określonych zapytań – tworzymy osobne tabele więc możemy utworzyć więcej indeksów klastrowych, lepsza efektywność przechowywania danych w tabelach,
- wąskie tabele to bardziej efektywne przetwarzanie i składowanie ich na dysku, mniej operacji I/O,
- lepsze zarządzanie transakcjami – szybsze wykonywanie update’ów, mniej blokad.

[Zadania do wykonania](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#normalizacja_zadania) [Pytania sprawdzające](https://home.agh.edu.pl/~pamalino/programowanie/mysql/#normalizacja_pytania)

© Wszelkie prawa zastrzeżone. Paweł Malinowski - 2018. [_pamalino@agh.edu.pl_](mailto: pamalino@agh.edu.pl), współpraca [Smart Foundry](https://smart-foundry.ai/)