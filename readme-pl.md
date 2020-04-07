<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 Powody dla których ten przewodnik może przenieść twoje umiejętności testowania na wyższy poziom

<br/>

## 📗 45+ najlepszych praktyk: super kompleksowe i wyczerpujące

Jest to przewodnik po niezawodności JavaScript i Node.js od A-Z. Podsumowuje i przygotowuje dla Ciebie dziesiątki najlepszych postów na blogu, książek i narzędzi dostępnych na rynku

## 🚢 Zaawansowane: przekracza 10 000 mil poza zwykłe podstawy

Wskocz w podróż, która wykracza poza podstawy, podróż do zaawansowanych tematów, takich jak testowanie na produkcji, testowanie mutacji, testowanie na podstawie właściwości i wiele innych strategicznych i profesjonalnych narzędzi. Jeśli przeczytasz każde słowo w tym przewodniku, Twoje umiejętności testowania prawdopodobnie przekroczą średnią

## 🌐 Full-stack: front, backend, CI, wszystko

Zacznij od zrozumienia wszechobecnych praktyk testowania, które są podstawą każdej warstwy aplikacji. Następnie zagłęb się w wybrany obszar: frontend/UI, backend, CI, a może wszystkie?

<br/>

### Napisane przez Yoni Goldberg

- Konsultant JavaScript & Node.js
- 📗 [Testowanie Node.js i JavaScript od A do Z](https://www.testjavascript.com) - Mój kompleksowy kurs online z ponad [10 godzinami wideo](https://www.testjavascript.com), 14 typów testów i ponad 40 najlepszych praktyk
- [Obserwuj mnie na Twitter](https://twitter.com/goldbergyoni/)

<br/>

### Tłumaczenia - czytaj w swoim własnym języku

- 🇨🇳[Chinese](readme-zh-CN.md) - dzięki uprzejmości [Yves yao](https://github.com/yvesyao)
- 🇰🇷[Korean](readme.kr.md) - dzięki uprzejmości [Rain Byun](https://github.com/ragubyun)
- 🇵🇱[Polish](readme.pl.md) - dzięki uprzejmości [Michal Biesiada](https://github.com/mbiesiad)
- Chcesz przetłumaczyć na swój język? Proszę skorzystaj z issue 💜

<br/><br/>

## `Spis treści`

#### [`Sekcja 0: Złota zasada`](#sekcja-0️⃣-złota-zasada)

Jedna rada, która inspiruje wszystkich innych (1 specjalny punkt)

#### [`Sekcja 1: Anatomia testu`](#sekcja-1-anatomia-testu)

Podstawa - konstruowanie czystych testów (12 wypunktowań)

#### [`Sekcja 2: Backend`](#sekcja-2️⃣-backend-testing)

Pisanie backendu i wydajne testy Mikroserwisów (8 wypunktowań)

#### [`Sekcja 3: Frontend`](#sekcja-3️⃣-frontend-testing)

Pisanie testów dla webowego interfejsu użytkownika, w tym testy komponentów i testy E2E (11 wypunktowań)

#### [`Sekcja 4: Pomiary skuteczności testów`](#sekcja-4️⃣-pomiary-skuteczności-testów)

Watching the watchman - pomiar jakości testu (4 wypunktowania)

#### [`Sekcja 5: Continuous Integration`](#sekcja-5️⃣-ci-and-other-quality-measures)

Wytyczne dla CI w świecie JS (9 wypunktowań)

<br/><br/>

# Sekcja 0️⃣: Złota zasada

<br/>

## ⚪️ 0 Złota zasada: Projektowanie dla lean testing

:white_check_mark: **Opis:**
Testowany kod nie przypomina kodu produkcyjnego - zaprojektuj go tak, by był prosty, krótki, pozbawiony abstrakcji, płaski, przyjemny w pracy, lean. Trzeba spojrzeć na test i natychmiast uzyskać cel.

Nasz umysł jest przepełniony głównym kodem produkcyjnym, nie mamy 'przestrzeni roboczej' na dodatkową złożoność. Jeśli spróbujemy wcisnąć kolejny trudny kod do naszego słabego mózgu, spowolni to pracę zespołu, co działa wbrew temu, co testujemy. W praktyce wiele zespołów po prostu rezygnuje z testów.

Testy są okazją do czegoś innego - przyjaznego i uśmiechniętego asystenta, z którym przyjemnie się pracuje i zapewnia wielką wartość za tak małą inwestycję. Nauka mówi nam, że mamy dwa systemy mózgowe: system 1 służy do łatwych czynności, takich jak prowadzenie samochodu po pustej drodze, i system 2, który jest przeznaczony do złożonych i świadomych operacji, takich jak rozwiązywanie równania matematycznego. Zaprojektuj swój test dla systemu 1, gdy patrzysz na kod testowy, powinien on czuć się tak łatwo, jak modyfikacja dokumentu HTML, a nie jak rozwiązywanie 2X(17 × 24).

Można to osiągnąć poprzez selektywne wybieranie technik, narzędzi i celów testowych, które są opłacalne i zapewniają duży zwrot z inwestycji. Testuj tylko tyle, ile potrzeba, staraj się, aby był zwinny, czasem warto porzucić niektóre testy i wymienić niezawodność na zwinność i prostotę.

![alt text](/assets/headspace.png "We have no head room for additional complexity")

Większość poniższych porad to pochodne tej zasady.

### Gotów by rozpocząć?

<br/><br/>

# Sekcja 1: Anatomia testu

<br/>

## ⚪ ️ 1.1 Dołącz 3 części do każdej nazwy testu

:white_check_mark: **Opis:** Raport z testu powinien informować, czy bieżąca wersja aplikacji spełnia wymagania osób, które niekoniecznie znają kod: testera, wdrażającego inżyniera DevOps i przyszłego ciebie za dwa lata. Można to najlepiej osiągnąć, jeśli testy są na poziomie wymagań i obejmują 3 części:

(1) Co jest testowane? Na przykład, metoda ProductsService.addNewProduct

(2) W jakich okolicznościach i scenariuszu? Na przykład żadna cena nie jest przekazywana do metody

(3) Jaki jest oczekiwany wynik? Na przykład nowy produkt nie został zatwierdzony

<br/>

❌ **W przeciwnym razie:** Wdrożenie właśnie nie powiodło się, test o nazwie "Dodaj produkt" nie powiódł się. Czy to mówi ci, co dokładnie działa nieprawidłowo?

<br/>

**👇 Uwaga:** Każdy pocisk ma przykłady kodu, a czasem także ilustrację. Kliknij aby rozszerzyć

<details><summary>✏ <b>Przykłady kodu</b></summary>
  
<br/>
  
### :clap: Przykład robienia tego dobrze: nazwa testu, która składa się z 3 części

![](https://img.shields.io/badge/🔨%20Example%20using%20Mocha-blue.svg "Using Mocha to illustrate the idea")

```javascript
//1. unit under test
describe('Products Service', function() {
  describe('Add new product', function() {
    //2. scenario and 3. expectation
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});

```

<br/>

### :clap: Przykład robienia tego dobrze: nazwa testu, która składa się z 3 części

![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️ 1.2 Struktura testów według wzorca AAA

:white_check_mark: **Opis:** Ustrukturyzuj swoje testy za pomocą 3 dobrze oddzielonych sekcji: Arrange, Act & Assert (AAA). Przestrzeganie tej struktury gwarantuje, że czytelnik nie poświęci procesora mózgu na zrozumienie planu testu:

1st A - Arrange: Cały kod instalacyjny, aby wprowadzić system do scenariusza, którego test ma na celu symulację. Może to obejmować tworzenie instancji testowanego konstruktora, dodawanie rekordów DB, mockowanie/usuwanie obiektów i każdy inny kod przygotowawczy

2nd A - Act: Wykonaj unit pod test. Zwykle 1 linia kodu

3rd A - Assert: Upewnij się, że otrzymana wartość spełnia oczekiwania. Zwykle 1 linia kodu

<br/>

❌ **W przeciwnym razie:** Nie tylko spędzasz godziny na zrozumieniu głównego kodu, ale to, co powinno być najprostszą częścią dnia (testowanie) obciąża Twój mózg

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: test oparty na wzorcu AAA

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest") ![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
describe("Customer classifier", () => {
  test("When customer spent more than 500$, should be classified as premium", () => {
    //Arrange
    const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
    const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });

    //Act
    const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);

    //Assert
    expect(receivedClassification).toMatch("premium");
  });
});
```

<br/>

### :thumbsdown: Przykład antywzorca: brak separacji, jedna masa, trudniejsza do interpretacji

```javascript
test("Should be classified as premium", () => {
  const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
  const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });
  const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);
  expect(receivedClassification).toMatch("premium");
});
```

</details>

<br/><br/>

## ⚪ ️1.3 Opisz oczekiwania w języku produktu: stosuj asercje w stylu BDD

:white_check_mark: **Opis:** Kodowanie testów w stylu deklaratywnym pozwala czytelnikowi na natychmiastowe złapanie go bez wydawania nawet jednego cyklu mózg-procesor. Kiedy piszesz kod imperatywny wypełniony logiką warunkową, czytelnik jest zmuszony wywierać więcej cykli mózg-procesor. W takim przypadku zakoduj oczekiwanie w języku przypominającym język człowieka, deklaratywnym stylu BDD, używając `expect` lub `should` i nie używając niestandardowego kodu. Jeśli Chai & Jest nie zawiera żądanej asercji i jest wysoce powtarzalne, rozważ [rozszerzenie Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) lub napisanie [wtyczki niestandardowej Chai](https://www.chaijs.com/guide/plugins/)
<br/>

❌ **W przeciwnym razie:** Zespół napisze mniej testów i ozdobi części irytujące z .skip()

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

### :thumbsdown: Przykład antywzorca: Czytelnik musi przejrzeć niezbyt krótki i imperatywny kod, aby uzyskać historię testową

```javascript
test("When asking for an admin, ensure only ordered admins in results", () => {
  //assuming we've added here two admins "admin1", "admin2" and "user1"
  const allAdmins = getUsers({ adminOnly: true });

  let admin1Found,
    adming2Found = false;

  allAdmins.forEach(aSingleUser => {
    if (aSingleUser === "user1") {
      assert.notEqual(aSingleUser, "user1", "A user was found and not admin");
    }
    if (aSingleUser === "admin1") {
      admin1Found = true;
    }
    if (aSingleUser === "admin2") {
      admin2Found = true;
    }
  });

  if (!admin1Found || !admin2Found) {
    throw new Error("Not all admins were returned");
  }
});
```

<br/>

### :clap: Przykład robienia tego dobrze: Przejrzenie poniższego testu deklaratywnego to pestka

```javascript
it("When asking for an admin, ensure only ordered admins in results", () => {
  //assuming we've added here two admins
  const allAdmins = getUsers({ adminOnly: true });

  expect(allAdmins)
    .to.include.ordered.members(["admin1", "admin2"])
    .but.not.include.ordered.members(["user1"]);
});
```

</details>

<br/><br/>

## ⚪ ️ 1.4 Trzymaj się testów czarnej skrzynki: testuj tylko metody publiczne

:white_check_mark: **Opis:** Testowanie elementów wewnętrznych przynosi ogromne koszty prawie za nic. Jeśli Twój kod / interfejs API zapewnia prawidłowe wyniki, czy naprawdę warto zainwestować następne 3 godziny w testowanie JAK działało ono wewnętrznie, a następnie utrzymać te delikatne testy? Za każdym razem, gdy sprawdzane jest zachowanie publiczne, implementacja prywatna jest również domyślnie testowana, a testy zostaną przerwane tylko w przypadku wystąpienia określonego problemu (np. nieprawidłowego wyniku). Takie podejście jest również określane jako `behavioral testing`. Z drugiej strony, jeśli przetestujesz wewnętrzne elementy (podejście z białą ramką) - skupiasz się na planowaniu wyniku komponentu na drobiazgowe szczegóły, a twój test może się zepsuć z powodu drobnych refaktorów kodu, chociaż wyniki są w porządku - to dramatycznie zwiększa konserwację, obciąża
<br/>

❌ **W przeciwnym razie:** Twoje testy zachowują się jak [chłopiec, który wołał wilka](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf): krzycząc false-positive (np. test kończy się niepowodzeniem, ponieważ zmieniono nazwę zmiennej prywatnej). Nic dziwnego, że ludzie wkrótce zaczną ignorować powiadomienia CI, aż pewnego dnia prawdziwy błąd zostanie zignorowany…

<br/>
<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: Przypadek testowy testuje elementy wewnętrzne bez uzasadnionego powodu

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai")

```javascript
class ProductService {
  //this method is only used internally
  //Change this name will make the tests fail
  calculateVATAdd(priceWithoutVAT) {
    return { finalPrice: priceWithoutVAT * 1.2 };
    //Change the result format or key name above will make the tests fail
  }
  //public method
  getPrice(productId) {
    const desiredProduct = DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
    return finalPrice;
  }
}

it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
  //There's no requirement to allow users to calculate the VAT, only show the final price. Nevertheless we falsely insist here to test the class internals
  expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});
```

</details>

<br/><br/>

## ⚪ ️ ️1.5 Wybierz odpowiedni test doubles: Unikaj mockowania na rzecz stubs i spies

:white_check_mark: **Opis:** Test doubles są złem koniecznym, ponieważ są sprzężone z wewnętrznymi elementami aplikacji, ale niektóre zapewniają ogromną wartość (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Przeczytaj tutaj przypomnienie o test doubles: mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Przed użyciem test doubles zadaj bardzo proste pytanie: czy używam go do testowania funkcjonalności, która pojawia się lub może pojawić się w dokumencie wymagań? Jeśli nie, jest to white-box testing smell.

  Na przykład jeśli chcesz przetestować, czy aplikacja zachowuje się rozsądnie, gdy usługa płatnicza jest wyłączona, możesz zlikwidować usługę płatniczą i uruchomić niektóre zwracając ‘Brak odpowiedzi’, aby upewnić się, że testowana jednostka zwraca prawidłową wartość. To sprawdza zachowanie / odpowiedź / wynik naszej aplikacji w określonych scenariuszach. Możesz także użyć spies, aby potwierdzić, że wiadomość e-mail została wysłana, gdy ta usługa nie działa - jest to ponownie kontrola behawioralna, która prawdopodobnie pojawi się w dokumencie wymagań („Wyślij wiadomość e-mail, jeśli nie można zapisać płatności”). Z drugiej strony, jeśli mockujesz usługę płatności i upewniasz się, że została ona wywołana za pomocą odpowiednich typów JavaScript - wtedy twój test koncentruje się na wewnętrznych rzeczach, które nie mają nic z funkcjonalnością aplikacji i prawdopodobnie często się zmieniają
<br/>

❌ **W przeciwnym razie:** Wszelka refaktoryzacja kodu nakazuje wyszukiwanie wszystkich próbnych elementów w kodzie i odpowiednią aktualizację. Testy stają się ciężarem, a nie pomocnym przyjacielem

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: Mocks skupiające się na elementach wewnętrznych

![](https://img.shields.io/badge/🔧%20Example%20using%20Sinon-blue.svg "Examples with Sinon")

```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
  //Assume we already added a product
  const dataAccessMock = sinon.mock(DAL);
  //hmmm BAD: testing the internals is actually our main goal here, not just a side-effect
  dataAccessMock
    .expects("deleteProduct")
    .once()
    .withArgs(DBConfig, theProductWeJustAdded, true, false);
  new ProductService().deletePrice(theProductWeJustAdded);
  dataAccessMock.verify();
});
```

<br/>

### :clap:Przykład robienia tego dobrze: spies koncentrują się na testowaniu wymagań, ale jako efekt uboczny nieuchronnie dotykają elementów wewnętrznych

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
  //Assume we already added here a product
  const spy = sinon.spy(Emailer.prototype, "sendEmail");
  new ProductService().deletePrice(theProductWeJustAdded);
  //hmmm OK: we deal with internals? Yes, but as a side effect of testing the requirements (sending an email)
  expect(spy.calledOnce).to.be.true;
});
```

</details>

<br/><br/>

## 📗 Chcesz poznać wszystkie te praktyki z wideo na żywo?

### Odwiedź mój kurs online [Testowanie Node.js i JavaScript od A do Z](https://www.testjavascript.com)

<br/><br/>

## ⚪ ️1.6 Nie "foo", używaj realistycznych danych wejściowych

:white_check_mark: **Opis:** Często błędy produkcyjne są ujawniane pod bardzo konkretnymi i zaskakującymi danymi wejściowymi - im bardziej realistyczny jest wkład testowy, tym większe są szanse na wczesne wykrycie błędów. Użyj dedykowanych bibliotek takich jak [Faker](https://www.npmjs.com/package/faker) do generowania pseudo-rzeczywistych danych, które przypominają różnorodność i formę danych produkcyjnych. Na przykład takie biblioteki mogą generować realistyczne numery telefonów, nazwy użytkowników, karty kredytowe, nazwy firm, a nawet tekst „lorem ipsum”. Możesz także utworzyć niektóre testy (oprócz testów jednostkowych, a nie zamienników), które losowo dodają fałszywych danych, aby rozciągnąć testowaną jednostkę lub nawet zaimportować prawdziwe dane ze środowiska produkcyjnego. Chcesz przenieść go na wyższy poziom? Zobacz następny punkt (testy oparte na właściwościach).
<br/>

❌ **W przeciwnym razie:** Wszystkie testy programistyczne będą fałszywie pokazywać kolor zielony, gdy użyjesz syntetycznych danych wejściowych, takich jak „Foo”, ale wtedy produkcja może zmienić kolor na czerwony, gdy haker przejdzie tak nieprzyjemny ciąg znaków, jak “@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA”

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: Zestaw testowy, który przechodzi z powodu nierealistycznych danych

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
const addProduct = (name, price) => {
  const productNameRegexNoSpace = /^\S*$/; //no white-space allowed

  if (!productNameRegexNoSpace.test(name)) return false; //this path never reached due to dull input

  //some logic here
  return true;
};

test("Wrong: When adding new product with valid properties, get successful confirmation", async () => {
  //The string "Foo" which is used in all tests never triggers a false result
  const addProductResult = addProduct("Foo", 5);
  expect(addProductResult).toBe(true);
  //Positive-false: the operation succeeded because we never tried with long
  //product name including spaces
});
```

<br/>

### :clap:Przykład robienia tego dobrze: Randomizing realistic input

```javascript
it("Better: When adding new valid product, get successful confirmation", async () => {
  const addProductResult = addProduct(faker.commerce.productName(), faker.random.number());
  //Generated random input: {'Sleek Cotton Computer',  85481}
  expect(addProductResult).to.be.true;
  //Test failed, the random input triggered some path we never planned for.
  //We discovered a bug early!
});
```

</details>

<br/><br/>

## ⚪ ️ 1.7 Testowanie wielu kombinacji danych wejściowych za pomocą testów opartych na właściwościach

  :white_check_mark: **Opis:** Zazwyczaj wybieramy kilka próbek wejściowych dla każdego testu. Nawet jeśli format wejściowy przypomina dane rzeczywiste (zobacz punkt ‘Nie foo’), obejmujemy tylko kilka kombinacji danych wejściowych (method(‘’, true, 1), method(“string” , false” , 0)). Jednak w produkcji interfejs API, który jest wywoływany z 5 parametrami, może być wywoływany z tysiącami różnych kombinacji, jeden z nich może spowolnić nasz proces ([zobacz Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)). Co jeśli mógłbyś napisać pojedynczy test, który automatycznie wysyła 1000 permutacji różnych danych wejściowych i wyłapuje, dla których danych wejściowych nasz kod nie zwraca poprawnej odpowiedzi? Testowanie oparte na właściwościach jest techniką, która robi dokładnie to: wysyłając wszystkie możliwe kombinacje danych wejściowych do testowanego urządzenia, zwiększa to prawdopodobieństwo znalezienia błędu. Na przykład, biorąc pod uwagę metodę - addNewProduct (identyfikator, nazwa, isDiscount) - biblioteki obsługujące będą wywoływać tę metodę z wieloma kombinacjami (liczba, łańcuch, wartość logiczna), takich jak (1, „iPhone”, false), (2, „Galaxy ", prawdziwe). Możesz uruchomić testy oparte na właściwościach, używając swojego ulubionego test runnera (Mocha, Jest, etc) za pomocą bibliotek takich jak [js-verify](https://github.com/jsverify/jsverify) lub [testcheck](https://github.com/leebyron/testcheck-js) (znacznie lepsza dokumentacja). Aktualizacja: Nicolas Dubien sugeruje w komentarzach poniżej [sprawdzenie fast-check](https://github.com/dubzzz/fast-check#readme) który wydaje się oferować dodatkowe funkcje, a także jest aktywnie utrzymywany
<br/>

❌ **W przeciwnym razie:** Nieświadomie wybierasz wejścia testowe, które obejmują tylko dobrze działające ścieżki kodu. Niestety obniża to efektywność testowania jako pojazdu do wykrywania błędów

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Testing many input permutations with “fast-check”

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
import fc from "fast-check";

describe("Product service", () => {
  describe("Adding new", () => {
    //this will run 100 times with different random properties
    it("Add new product with random yet valid properties, always successful", () =>
      fc.assert(
        fc.property(fc.integer(), fc.string(), (id, name) => {
          expect(addNewProduct(id, name).status).toEqual("approved");
        })
      ));
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.8 Jeśli potrzeba, użyj tylko short & inline snapshots

:white_check_mark: **Opis:** Gdzie jest potrzeba na [testy snapshot](https://jestjs.io/docs/en/snapshot-testing), używaj tylko krótkich i skoncentrowanych snapshotów (np. 3-7 linie), które są uwzględnione w ramach testu ([Inline Snapshot](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)) i nie w plikach zewnętrznych. Przestrzeganie tych wytycznych sprawi, że testy będą zrozumiałe i mniej kruche.

Z drugiej strony, poradniki ‘klasycznych snapshotów’ i narzędzia zachęcają do przechowywania dużych plików (np. znaczników renderowania komponentu, wyniku API JSON) na jakimś zewnętrznym nośniku i zapewniają za każdym razem, gdy uruchamiany jest test w celu porównania otrzymanego wyniku z zapisaną wersją. To, na przykład, może pośrednio powiązać nasz test z 1000 liniami z 3000 wartościami danych, o których twórca testów nigdy nie czytał i nie uzasadniał. Dlaczego to źle? W ten sposób istnieje 1000 powodów niepowodzenia testu - wystarczy zmienić jedną linię, aby migawka stała się nieważna, i prawdopodobnie zdarzy się to często. Jak często? Dla każdej przestrzeni, komentarza lub drobnej zmiany CSS / HTML. Nie tylko to, nazwa testu nie dałaby informacji o niepowodzeniu, ponieważ po prostu sprawdza, czy 1000 wierszy się nie zmieniło, zachęca także twórcy testu do zaakceptowania jako pożądanego prawdziwego długiego dokumentu, którego nie mógł sprawdzić i zweryfikować. Wszystko to są objawy niejasnego i niecierpliwego testu, który nie jest skoncentrowany i ma na celu osiągnięcie zbyt wiele

Warto zauważyć, że istnieje kilka przypadków, w których dopuszczalne są długie i zewnętrzne migawki - podczas potwierdzania schematu, a nie danych (wyodrębnianie wartości i skupianie się na polach) lub gdy otrzymany dokument rzadko się zmienia
<br/>

❌ **W przeciwnym razie:** Test interfejsu użytkownika kończy się niepowodzeniem. Kod wydaje się prawidłowy, ekran wyświetla idealne piksele, co się stało? Twoje testowanie migawek właśnie znalazło różnicę między dokumentem źródłowym, a aktualnie otrzymanym - do znacznika została dodana pojedyncza spacja...

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: Łączymy nasz test z niewidzialnymi 2000 liniami kodu

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
it("TestJavaScript.com is renderd correctly", () => {
  //Arrange

  //Act
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  //Assert
  expect(receivedPage).toMatchSnapshot();
  //We now implicitly maintain a 2000 lines long document
  //every additional line break or comment - will break this test
});
```

<br/>

### :clap: Przykład robienia tego dobrze: Oczekiwania są widoczne i skoncentrowane

```javascript
it("When visiting TestJavaScript.com home page, a menu is displayed", () => {
  //Arrange

  //Act
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  //Assert

  const menu = receivedPage.content.menu;
  expect(menu).toMatchInlineSnapshot(`
<ul>
<li>Home</li>
<li> About </li>
<li> Contact </li>
</ul>
`);
});
```

</details>

<br/><br/>

## ⚪ ️1.9 Unikaj globalnych test fixture i seeds, dodawaj dane na test

:white_check_mark: **Opis:** Kierując się złotą zasadą (punkt 0), każdy test powinien dodawać i działać na swoim własnym zestawie wierszy BD, aby zapobiec sprzężeniu i łatwo uzasadnić przebieg testu. W rzeczywistości jest to często naruszane przez testerów, którzy zapełniają bazę danych danymi przed uruchomieniem testów ([znany również jako ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) w celu poprawy wydajności. Chociaż wydajność jest istotnym problemem - można ją złagodzić (patrz punkt „Testowanie komponentów”), jednak złożoność testów jest bardzo bolesnym smutkiem, który powinien rządzić innymi względami przez większość czasu. Praktycznie spraw, aby każdy przypadek testowy wyraźnie dodał potrzebne rekordy BD i działał tylko na tych rekordach. Jeśli wydajność stanie się kluczowym problemem - zrównoważony kompromis może przyjść w postaci inicjowania jedynego zestawu testów, które nie powodują mutacji danych (np. zapytania)
<br/>

❌ **W przeciwnym razie:** Niewiele testów kończy się niepowodzeniem, wdrożenie zostało przerwane, nasz zespół spędza teraz cenny czas, czy mamy błąd? Zbadajmy, och nie - wydaje się, że dwa testy mutowały te same dane seed

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: testy nie są niezależne i polegają na pewnym globalnym hook do zasilania globalnych danych BD

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
before(() => {
  //adding sites and admins data to our DB. Where is the data? outside. At some external json or migration framework
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Failure! The previous test change the name :[
});

```

<br/>

### :clap: Przykład robienia tego dobrze: Możemy pozostać w teście, każdy test działa na własny zestaw danych

```javascript
it("When updating site name, get successful confirmation", async () => {
  //test is adding a fresh new records and acting on the records only
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });

  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");

  expect(updateNameResult).to.be(true);
});
```

</details>

<br/>

## ⚪ ️ 1.10 Nie wychwytuj błędów, oczekuj ich

:white_check_mark: **Opis:** Podczas próby stwierdzenia, że niektóre dane wejściowe powodują błąd, może być właściwe użycie try-catch-finally i zapewnienie, że wprowadzono klauzulę catch. Wynikiem jest niezręczny i pełny przypadek testowy (przykład poniżej), który ukrywa prosty cel testu i oczekiwania na wynik

Bardziej elegancką alternatywą jest użycie dedykowanego asercji Chai w jednym wierszu: expect (method).to.throw (lub w Jest: expect(method).toThrow()). Absolutnie obowiązkowe jest również upewnienie się, że wyjątek zawiera właściwość określającą typ błędu, w przeciwnym razie biorąc pod uwagę tylko ogólny błąd, aplikacja nie będzie w stanie zrobić wiele, zamiast wyświetlać rozczarowujący komunikat użytkownikowi
<br/>

❌ **W przeciwnym razie:** Trudno będzie wnioskować z raportów testów (np. raportów CI), co poszło nie tak

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: Długi przypadek testowy, który próbuje potwierdzić istnienie błędu z try-catch

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
it("When no product name, it throws error 400", async () => {
  let errorWeExceptFor = null;
  try {
    const result = await addNewProduct({});
  } catch (error) {
    expect(error.code).to.equal("InvalidInput");
    errorWeExceptFor = error;
  }
  expect(errorWeExceptFor).not.to.be.null;
  //if this assertion fails, the tests results/reports will only show
  //that some value is null, there won't be a word about a missing Exception
});
```

<br/>

### :clap: Przykład robienia tego dobrze: Oczekiwanie czytelne dla człowieka, które może być łatwo zrozumiane, może nawet przez QA lub technicznego PM

```javascript
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

</details>

<br/><br/>

## ⚪ ️ 1.11 Taguj twoje testy

:white_check_mark: **Opis:** Różne testy muszą być uruchamiane w różnych scenariuszach: quick smoke, IO-less, testy powinny być uruchamiane, gdy programista zapisuje lub commituje plik, pełne kompleksowe testy zwykle uruchamiane są po przesłaniu nowego pull requesta itp. Można to osiągnąć poprzez oznaczenie testów słowami kluczowymi takimi jak #cold #api #sanity, aby można było grepować za pomocą uprzęży testującej i wywołać pożądany podzbiór. Na przykład w ten sposób można wywołać tylko grupę sanity test z Mocha: mocha — grep ‘sanity’
<br/>

❌ **W przeciwnym razie:** Uruchamianie wszystkich testów, w tym testów, które wykonują dziesiątki zapytań BD, za każdym razem, gdy programista wprowadzi małą zmianę, może być bardzo powolny i powstrzymuje programistów przed uruchomieniem testów

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Tagowanie testów jako ‘#cold-test’ umożliwia test runnerowi wykonywanie tylko szybkich testów (testy cold===quick które nie wykonują operacji wejścia/wyjścia i mogą być wykonywane często, nawet gdy programista pisze)

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
//this test is fast (no DB) and we're tagging it correspondigly
//now the user/CI can run it frequently
describe("Order service", function() {
  describe("Add new order #cold-test #sanity", function() {
    test("Scenario - no currency was supplied. Expectation - Use the default currency #sanity", function() {
      //code logic here
    });
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.12 Kategoryzuj testy na co najmniej 2 poziomach

:white_check_mark: **Opis:** Zastosuj pewną strukturę do swojego zestawu testów, aby od czasu do czasu odwiedzający mógł łatwo zrozumieć wymagania (testy to najlepsza dokumentacja) i różne testowane scenariusze. Powszechną metodą jest umieszczanie co najmniej 2 bloków 'opisz' nad testami: pierwszy to nazwa testowanej jednostki, a drugi to dodatkowy poziom kategoryzacji, taki jak scenariusz lub kategorie niestandardowe (patrz przykłady kodu i prtscn poniżej). Takie postępowanie znacznie poprawi również raporty z testów: Czytelnik łatwo wywnioskuje kategorie testów, zagłębi się w żądaną sekcję i skoreluje testy zakończone niepowodzeniem. Ponadto programistom łatwiej będzie poruszać się po kodzie pakietu z wieloma testami. Istnieje wiele alternatywnych struktur dla zestawu testów, które możesz rozważyć, jak [given-when-then](https://github.com/searls/jasmine-given) oraz [RITE](https://github.com/ericelliott/riteway)

<br/>

❌ **W przeciwnym razie:** Patrząc na raport z płaską i długą listą testów, czytelnik musi przejrzeć długie teksty, aby zakończyć główne scenariusze i skorelować powszechność nieudanych testów. Rozważ następujący przypadek: gdy testy 7/100 zakończą się niepowodzeniem, przeglądanie płaskiej listy będzie wymagało przeczytania tekstu testów zakończonych niepowodzeniem, aby zobaczyć, jak się ze sobą wiążą. Jednak w hierarchicznym raporcie wszystkie z nich mogą podlegać temu samemu przepływowi lub kategorii, a czytelnik szybko zorientuje się, co lub gdzie jest źródło przyczyny awarii

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Strukturyzacja pakietu z nazwą jednostki pod test i scenariuszy doprowadzi do wygodnego raportu pokazanego poniżej

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
// Unit under test
describe("Transfer service", () => {
  //Scenario
  describe("When no credit", () => {
    //Expectation
    test("Then the response status should decline", () => {});

    //Expectation
    test("Then it should send email to admin", () => {});
  });
});
```

![alt text](assets/hierarchical-report.png)

<br/>

### :thumbsdown: Przykład antywzorca: Płaska lista testów utrudni czytelnikowi identyfikację historii użytkowników i skorelowanie testów zakończonych niepowodzeniem

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Mocha")

```javascript
test("Then the response status should decline", () => {});

test("Then it should send email", () => {});

test("Then there should not be a new transfer record", () => {});
```

![alt text](assets/flat-report.png)

<br/>

</details>

<br/><br/>

## ⚪ ️1.13 Inne ogólne dobre zasady higieny testowania

:white_check_mark: **Opis:** Ten post skupia się na poradach dotyczących testowania, które są związane lub przynajmniej mogą być zilustrowane przykładem Node JS. Ten punkt zawiera jednak kilka dobrze znanych wskazówek niezwiązanych z Node


Uczyć się i ćwiczyć [zasady TDD](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) — dla wielu są niezwykle cenne, ale nie przestrasz się, jeśli nie pasują do Twojego stylu, nie tylko tobie. Rozważ napisanie testów przed kodem w [style red-green-refactor](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), upewnij się, że każdy test sprawdza dokładnie jedną rzecz, gdy znajdziesz błąd - przed naprawą napisz test, który wykryje ten błąd w przyszłości, pozwól każdemu testowi zawieść co najmniej raz, zanim zmieni kolor na zielony, uruchom moduł, pisząc szybki i uproszczony kod, który satysfakcjonuje test - następnie stopniowo refaktoryzuj i przenieś go do poziomu klasy produkcyjnej, unikaj jakiejkolwiek zależności od środowiska (ścieżki, systemu operacyjnego itp.)
<br/>

❌ **W przeciwnym razie:** Będziesz tęsknić za perłami mądrości zbieranymi przez dziesięciolecia

<br/><br/>

# Sekcja 2️⃣: Backend Testing

## ⚪ ️2.1 Wzbogać swoje portfolio testowe: wyjdź poza testy jednostkowe i piramidę

:white_check_mark: **Opis:** [Piramida testowania](https://martinfowler.com/bliki/TestPyramid.html), pomimo że 10> lat starsza, to świetny i odpowiedni model, który sugeruje trzy typy testowania i wpływa na strategię testowania większości programistów. Jednocześnie pojawiła się ponad garstka nowych, błyszczących technik testowania, które ukrywają się w cieniu piramidy testowania. Biorąc pod uwagę wszystkie dramatyczne zmiany, które widzieliśmy w ciągu ostatnich 10 lat (Microservices, cloud, serverless), czy jest możliwe, że jeden dość stary model będzie odpowiedni _wszystkim_ typom aplikacji? Czy świat testowania nie powinien rozważyć przyjęcia nowych technik testowania?

Nie zrozumcie mnie źle, w 2019 roku piramida testowania, TDD i testy jednostkowe są nadal potężną techniką i prawdopodobnie najlepiej pasują do wielu aplikacji. Tylko jak każdy inny model, pomimo swojej przydatności, [czasem musi się mylić](https://en.wikipedia.org/wiki/All_models_are_wrong). Rozważmy na przykład aplikację IOT, która pobiera wiele zdarzeń do magistrali komunikatów, takiej jak Kafka/RabbitMQ, która następnie przepływa do jakiejś hurtowni danych i jest w końcu odpytywana przez interfejs analityczny. Czy naprawdę powinniśmy wydać 50% naszego budżetu z testów na pisanie testów jednostkowych dla aplikacji, która jest zorientowana na integrację i prawie nie ma logiki? Wraz ze wzrostem różnorodności typów aplikacji (boty, krypto, Alexa-skills) rośnie szansa na znalezienie scenariuszy, w których piramida testowania nie jest najlepszym rozwiązaniem.

Nadszedł czas, aby wzbogacić swoje portfolio testowania i zapoznać się z większą liczbą typów testów (następne punkty sugerują kilka pomysłów), modelami umysłu, takimi jak piramida testowania, ale także dopasować typy testowania do rzeczywistych problemów, z którymi się borykasz (‘Hej, nasz interfejs API jest zepsuty, napiszmy testowanie umów konsumenckich!’), zdywersyfikuj swoje testy jak inwestor, który buduje portfel na podstawie analizy ryzyka - oceń, gdzie mogą pojawić się problemy i dopasuj niektóre środki zapobiegawcze, aby zmniejszyć potencjalne ryzyko

Słowo ostrzeżenia: argument TDD w świecie oprogramowania ma typową fałszywą dychotomię, niektórzy głoszą, że można go używać wszędzie, inni uważają, że to diabeł. Każdy, kto mówi w absolutach, jest w błędzie :]

<br/>

❌ **W przeciwnym razie:** Będziesz tęsknić za niektórymi narzędziami z niesamowitym ROI, takimi jak Fuzz, lint, i mutacją która może zapewnić wartość w 10 minut

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Cindy Sridharan sugeruje wzbogacić portfolio testowania w swoim niesamowitym poście 'Testowanie mikrousług - w ten sam sposób'

![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Przykład: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️2.2 Testowanie komponentów może być Twoją najlepszą kwestią

:white_check_mark: **Opis:** Każdy test jednostkowy obejmuje niewielką część aplikacji i jest to kosztowne, aby pokryć całość, podczas gdy kompleksowe testy z łatwością obejmują dużo gruntu, ale są niestabilne i wolniejsze, dlaczego nie zastosować zrównoważonego podejścia i napisać testy, które są większe niż testy jednostkowe, ale mniejsze niż testy kompleksowe? Testowanie komponentów to nieoceniona piosenka świata testowego - zapewniają to, co najlepsze z obu światów: rozsądną wydajność i możliwość zastosowania wzorców TDD + realistyczne i doskonałe pokrycie.

Testy komponentów koncentrują się na mikroserwisowej ‘jednostce’, działają przeciwko interfejsowi API, nie mockują niczego, co należy do samego mikroserwisu (np. prawdziwa baza danych lub przynajmniej wersja tej bazy danych w pamięci), ale usuwają wszystko, co jest zewnętrzne, jak wywołania innych mikrousług. W ten sposób testujemy to, co wdrażamy, podchodzimy do aplikacji od zewnątrz do wewnątrz i zyskujemy dużą pewność w rozsądnym czasie.
<br/>

❌ **W przeciwnym razie:** Możesz spędzać długie dni na pisaniu testów jednostkowych, aby dowiedzieć się, że masz tylko 20% zasięgu systemu

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Supertest pozwala zbliżyć się do Express API w trakcie procesu (szybki i obejmuje wiele warstw)

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 Upewnij się, że nowe wersje nie psują interfejsu API

:white_check_mark: **Opis:** Tak więc twój mikroserwis ma wielu klientów i uruchamiasz wiele wersji usługi ze względu na kompatybilność (aby wszyscy byli zadowoleni). Potem zmieniasz jakieś pole i 'buum!'. Jakiś ważny klient, który działa na tym, jest zły. Oto Catch-22 w świecie integracji: po stronie serwera bardzo trudne jest uwzględnienie wszystkich oczekiwań wielu klientów - z drugiej strony klienci nie mogą przeprowadzać żadnych testów, ponieważ serwer kontroluje daty wydania. [Umowy konsumenckie i framework PACT](https://docs.pact.io/) stworzone zostały, aby sformalizować ten proces z bardzo destrukcyjnym podejściem - nie serwer sam określa plan testów, a klient określa testy… serwera! PACT może rejestrować oczekiwania klienta i umieszczać je we wspólnej lokalizacji, „brokerze”, dzięki czemu serwer może wyciągać oczekiwania i uruchamiać każdą kompilację za pomocą biblioteki PACT, aby wykrywać zerwane umowy - oczekiwanie klienta, które nie jest spełnione. W ten sposób wszystkie niedopasowania API serwer-klient zostaną wykryte wcześnie podczas kompilacji / CI i mogą zaoszczędzić sporo frustracji.
<br/>

❌ **W przeciwnym razie:** Alternatywami są wyczerpujące testy ręczne lub strach przed wdrożeniem

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "Examples with PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪ ️ 2.4 Przetestuj swoje middleware w izolacji

:white_check_mark: **Opis:** Wiele osób unika testowania oprogramowania pośredniego, ponieważ stanowią one niewielką część systemu i wymagają aktywnego serwera Express. Oba powody są błędne - oprogramowanie pośrednie jest małe, ale wpływa na wszystkie lub większość żądań i można je łatwo przetestować jako dostępne funkcje {req,res} obiekty JS. Aby przetestować funkcję oprogramowania pośredniego, należy ją po prostu wywołać i szpiegować ([używając na przykład Sinon](https://www.npmjs.com/package/sinon)) w połączeniu z obiektami {req,res} aby upewnić się, że funkcja wykonała właściwą akcję.
Biblioteka [node-mock-http](https://www.npmjs.com/package/node-mocks-http) posuwa się jeszcze dalej i uwzględnia obiekty {req, res} wraz ze szpiegowaniem ich zachowania. Na przykład można sprawdzić, czy status HTTP ustawiony w obiekcie res jest zgodny z oczekiwaniami (patrz przykład poniżej)
<br/>

❌ **W przeciwnym razie:** Błąd w middleware Express === błąd we wszystkich lub większości żądań

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap:Przykład robienia tego dobrze: Tesowanie middleware w izolacji, bez wykonywania połączeń sieciowych i budzenia całej maszyny Express

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
//the middleware we want to test
const unitUnderTest = require("./middleware");
const httpMocks = require("node-mocks-http");
//Jest syntax, equivelant to describe() & it() in Mocha
test("A request without authentication header, should return http status 403", () => {
  const request = httpMocks.createRequest({
    method: "GET",
    url: "/user/42",
    headers: {
      authentication: ""
    }
  });
  const response = httpMocks.createResponse();
  unitUnderTest(request, response);
  expect(response.statusCode).toBe(403);
});
```

</details>

<br/><br/>

## ⚪ ️2.5 Pomiar i refaktoryzacja za pomocą narzędzi do analizy statycznej

:white_check_mark: **Opis:** Korzystanie z narzędzi do analizy statycznej pomaga, zapewniając obiektywne sposoby poprawy jakości kodu i utrzymania kodu w stanie możliwym do utrzymania. Możesz dodać narzędzia analizy statycznej do kompilacji CI, aby przerwać, gdy wykryje code smells. Jego głównymi zaletami w stosunku do zwykłego lintowania jest możliwość kontroli jakości w kontekście wielu plików (np. wykrywanie duplikacji), przeprowadzania zaawansowanej analizy (np. złożoności kodu) oraz śledzenia historii i postępu problemów z kodem. Są dwa przykłady narzędzi, których możesz użyć [Sonarqube](https://www.sonarqube.org/) (2,600+ [gwiazdek](https://github.com/SonarSource/sonarqube)) oraz [Code Climate](https://codeclimate.com/) (1,500+ [gwiazdek](https://github.com/codeclimate/codeclimate))

Źródło: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **W przeciwnym razie:** Przy złej jakości kodu błędy i wydajność zawsze będą stanowić problem, którego nie będzie w stanie naprawić żadna nowa błyszcząca biblioteka ani najnowocześniejsze funkcje

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: CodeClimate, komercyjne narzędzie, które potrafi zidentyfikować złożone metody:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimat, a commercial tool that can identify complex methods:")

</details>

<br/><br/>

## ⚪ ️ 2.6 Sprawdź swoją gotowość na chaos związany z Node

:white_check_mark: **Opis:** Co dziwne, większość testów oprogramowania dotyczy wyłącznie logiki i danych, ale jednymi z najgorszych rzeczy, które się zdarzają (i naprawdę trudno je złagodzić) są problemy infrastrukturalne. Na przykład, czy kiedykolwiek testowałeś, co dzieje się, gdy pamięć procesowa jest przeciążona lub kiedy serwer/proces umiera, czy też twój system monitorowania zdaje sobie sprawę, kiedy API staje się o 50% wolniejsze? Aby przetestować i złagodzić tego rodzaju złe rzeczy — [Chaos engineering](https://principlesofchaos.org/) został stworzony przez Netflix. Ma na celu zapewnienie świadomości, frameworków i narzędzi do testowania odporności naszej aplikacji na chaotyczne problemy. Na przykład jedno z jego słynnych narzędzi, [the chaos monkey](https://github.com/Netflix/chaosmonkey), losowo zabija serwery, aby mieć pewność, że nasza usługa może nadal obsługiwać użytkowników i nie polegać na jednym serwerze (istnieje również wersja Kubernetes, [kube-monkey](https://github.com/asobti/kube-monkey), która zabija pods). Wszystkie te narzędzia działają na poziomie hosta / platformy, ale co zrobić, jeśli chcesz przetestować i wygenerować czysty chaos w Node, na przykład sprawdzić, jak proces Node'a radzi sobie z nieprzechwyconymi błędami, nieobsługiwanym odrzuceniem obietnicy (promise), pamięci v8 przeciążonej maksymalną dozwoloną wartością 1,7 GB lub czy Twój UX pozostaje zadowalający, gdy pętla zdarzeń jest często blokowana? Aby rozwiązać ten problem, napisałem, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) który zapewnia wszelkiego rodzaju chaotyczne akty związane z Node'm.
<br/>

❌ **W przeciwnym razie:** Nie ma ucieczki, prawo Murphy'ego uderzy w twoją produkcję bez litości

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: : Node-chaos może generować różnego rodzaju pranki z Node.js, dzięki czemu możesz przetestować odporność aplikacji na chaos

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 Unikaj global test fixtures oraz seeds, dodawaj dane na test

:white_check_mark: **Opis:** Przestrzeganie złotej zasady (punkt 0), każdy test powinien dodawać i działać na swoim własnym zestawie wierszy BD, aby zapobiec sprzężeniu i łatwo uzasadnić przebieg testu. W rzeczywistości jest to często naruszane przez testerów, którzy zapełniają bazę danych danymi przed uruchomieniem testów (znany również jako ‘test fixture’) w celu poprawy wydajności. Chociaż wydajność jest istotnym problemem - można ją złagodzić (patrz punkt “Component testing”), jednak złożoność testu jest bardzo bolesnym smutkiem, który przez większość czasu powinien rządzić innymi rozważaniami. Spraw praktycznie, aby każdy przypadek testowy wyraźnie dodał potrzebne rekordy BD i działał tylko na tych rekordach. Jeśli wydajność stanie się kluczowym problemem - zrównoważony kompromis może przyjść w postaci inicjowania jedynego zestawu testów, które nie powodują mutacji danych (np. zapytania)
<br/>

❌ **W przeciwnym razie:** Niewiele testów kończy się niepowodzeniem, wdrożenie zostało przerwane, nasz zespół spędza teraz cenny czas, czy mamy błąd? Zbadajmy, och nie - wydaje się, że dwa testy mutowały te same dane seed

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: testy nie są niezależne i polegają na pewnym globalnym hook do zasilania globalnych danych BD

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
before(() => {
  //adding sites and admins data to our DB. Where is the data? outside. At some external json or migration framework
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Failure! The previous test change the name :[
});

```

<br/>

### :clap: Przykład robienia tego dobrze: Możemy pozostać w teście, każdy test działa na własny zestaw danych

```javascript
it("When updating site name, get successful confirmation", async () => {
  //test is adding a fresh new records and acting on the records only
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });
  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");
  expect(updateNameResult).to.be(true);
});
```

</details>

<br/><br/>

# Sekcja 3️⃣: Frontend Testing

## ⚪ ️ 3.1 Oddziel interfejs użytkownika od funkcjonalności

:white_check_mark: **Opis:** Podczas koncentrowania się na testowaniu logiki komponentu szczegóły interfejsu użytkownika stają się szumem, który należy wyodrębnić, aby testy mogły koncentrować się na czystych danych. Praktycznie wyodrębnij pożądane dane ze znaczników w abstrakcyjny sposób, który nie jest zbyt sprzężony z implementacją graficzną, potwierdzaj tylko na czystych danych (vs szczegóły graficzne HTML / CSS) i wyłącz spowalniające animacje. Możesz ulec pokusie unikania renderowania i testowania tylko tylnej części interfejsu użytkownika (np. usług, akcji, store), ale spowoduje to testy fikcyjne, które nie przypominają rzeczywistości i nie ujawnią przypadków, w których właściwe dane nie są nawet przybyć do interfejsu użytkownika

<br/>

❌ **W przeciwnym razie:** Czysto obliczone dane z testu mogą być gotowe za 10 ms, ale wtedy cały test potrwa 500 ms (100 testów = 1 minuta) z powodu jakiejś wymyślnej i nieistotnej animacji

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Oddzielanie szczegółów interfejsu użytkownika

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
test("When users-list is flagged to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Extract the data from the UI first
  const allRenderedUsers = getAllByTestId("user").map(uiElement => uiElement.textContent);
  const allRealVIPUsers = allUsers.filter(user => user.vip).map(user => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //compare data with data, no UI here
});
```

<br/>

### :thumbsdown: Przykład antywzorca: asercja miesza szczegóły interfejsu użytkownika i dane

```javascript
test("When flagging to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Mix UI & data in assertion
  expect(getAllByTestId("user")).toEqual('[<li data-testid="user">John Doe</li>]');
});
```

</details>

<br/><br/>

## ⚪ ️ 3.2 Zapytaj elementy HTML na podstawie atrybutów, których zmiana jest mało prawdopodobna

:white_check_mark: **Opis:** Zapytaj elementy HTML na podstawie atrybutów, które prawdopodobnie przetrwają zmiany graficzne, w przeciwieństwie do selektorów CSS i podobnych etykiet formularzy. Jeśli wyznaczony element nie ma takich atrybutów, utwórz dedykowany atrybut testowy, taki jak 'test-id-submit-button'. Podążanie tą drogą nie tylko gwarantuje, że testy funkcjonalne / logiczne nigdy nie psują się z powodu zmian wyglądu i odczuć, ale także staje się jasne dla całego zespołu, że ten element i atrybut są wykorzystywane przez testy i nie należy ich usuwać

<br/>

❌ **W przeciwnym razie:** Chcesz przetestować funkcjonalność logowania obejmującą wiele komponentów, logikę i usługi, wszystko jest skonfigurowane idealnie - stubs, spies, połączenia Ajax są izolowane. Wszystko wydaje się idealne. Następnie test kończy się niepowodzeniem, ponieważ projektant zmienił klasę CSS div 'thick-border' do 'thin-border'

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Zapytanie o element przy użyciu dedykowanego atrybutu do testowania

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React")

```html
// the markup code (part of React component)
<h3>
  <Badge pill className="fixed_badge" variant="dark">
    <span data-testid="errorsLabel">{value}</span>
    <!-- note the attribute data-testid -->
  </Badge>
</h3>
```

```javascript
// this example is using react-testing-library
test("Whenever no data is passed to metric, show 0 as default", () => {
  // Arrange
  const metricValue = undefined;

  // Act
  const { getByTestId } = render(<dashboardMetric value={undefined} />);

  expect(getByTestId("errorsLabel").text()).toBe("0");
});
```

<br/>

### :thumbsdown: Przykład antywzorca: Poleganie na atrybutach CSS

```html
<!-- the markup code (part of React component) -->
<span id="metric" className="d-flex-column">{value}</span>
<!-- what if the designer changes the classs? -->
```

```javascript
// this exammple is using enzyme
test("Whenever no data is passed, error metric shows zero", () => {
  // ...

  expect(wrapper.find("[className='d-flex-column']").text()).toBe("0");
});
```

</details>

<br/>

## ⚪ ️ 3.3 O ile to możliwe, testuj z realistycznym i w pełni renderowanym komponentem

:white_check_mark: **Opis:** Kiedy tylko rozsądny rozmiar, przetestuj komponent z zewnątrz, tak jak robią to użytkownicy, w pełni renderuj interfejs użytkownika, działaj na nim i upewnij się, że renderowany interfejs zachowuje się zgodnie z oczekiwaniami. Unikaj wszelkiego rodzaju mockowania, częściowego i płytkiego renderowania - takie podejście może skutkować niezakłóconymi błędami z powodu braku szczegółów i utrudniać konserwację, gdy testy brudzą się z elementów wewnętrznych (patrz punkt 'Preferuj testowanie czarnej skrzynki'). Jeśli jeden z elementów potomnych znacznie spowalnia (np. animacja) lub komplikuje konfigurację - zastanów się nad wyraźnym zastąpieniem go fake'm

Biorąc to wszystko pod uwagę, należy zachować ostrożność: ta technika działa w przypadku małych / średnich komponentów, które pakują rozsądne rozmiary komponentów potomnych. Pełne renderowanie komponentu ze zbyt dużą liczbą potomnych utrudni rozumowanie na temat błędów testów (analiza przyczyn) i może być zbyt wolne. W takich przypadkach napisz tylko kilka testów z tym głównym składnikiem macierzystym i więcej testów z jego potomnymi.

<br/>

❌ **W przeciwnym razie:** Podczas wbijania się w wewnętrzne komponenty przez wywoływanie ich prywatnych metod i sprawdzania stanu wewnętrznego - podczas refaktoryzacji implementacji komponentów musiałbyś przefakturować wszystkie testy. Czy naprawdę masz możliwości takiego poziomu konserwacji?

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Praca w trybie rzeczywistym z całkowicie renderowanym komponentem

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Enzyme-blue.svg "Examples with Enzyme")

```javascript
class Calendar extends React.Component {
  static defaultProps = { showFilters: false };

  render() {
    return (
      <div>
        A filters panel with a button to hide/show filters
        <FiltersPanel showFilter={showFilters} title="Choose Filters" />
      </div>
    );
  }
}

//Examples use React & Enzyme
test("Realistic approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = mount(<Calendar showFilters={false} />);

  // Act
  wrapper.find("button").simulate("click");

  // Assert
  expect(wrapper.text().includes("Choose Filter"));
  // This is how the user will approach this element: by text
});
```

### :thumbsdown: Przykład antywzorca: Mockowanie rzeczywistości z płytkim renderowaniem

```javascript
test("Shallow/mocked approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = shallow(<Calendar showFilters={false} title="Choose Filter" />);

  // Act
  wrapper
    .find("filtersPanel")
    .instance()
    .showFilters();
  // Tap into the internals, bypass the UI and invoke a method. White-box approach

  // Assert
  expect(wrapper.find("Filter").props()).toEqual({ title: "Choose Filter" });
  // what if we change the prop name or don't pass anything relevant?
});
```

</details>

<br/>

## ⚪ ️ 3.4 Nie śpij, użyj wbudowanej obsługi frameworków dla zdarzeń asynchronicznych. Spróbuj także przyspieszyć

:white_check_mark: **Opis:** W wielu przypadkach czas zakończenia testu jest po prostu nieznany (np. animacja wstrzymuje wygląd elementu) - w takim przypadku unikaj spania (np. SetTimeOut) i preferuj bardziej deterministyczne metody, które zapewnia większość platform. Niektóre biblioteki pozwalają na oczekiwanie na operacje (np. [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), inne zapewniają API do czekania jak [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance). Czasami bardziej eleganckim sposobem jest zlikwidowanie wolnego zasobu, na przykład API, a następnie, gdy moment odpowiedzi staje się deterministyczny, komponent można jawnie ponownie renderować. Gdy zależy od jakiegoś zewnętrznego komponentu, który śpi, może się przydać [hurry-up the clock](https://jestjs.io/docs/en/timer-mocks). Spanie to schemat, którego należy unikać, ponieważ wymusza powolny lub ryzykowny test (podczas oczekiwania na zbyt krótki okres). Ilekroć spanie i odpytywanie jest nieuniknione i nie ma wsparcia ze strony środowiska testowego, niektóre biblioteki npm jak [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) mogą pomóc w rozwiązaniu pół-deterministycznym
<br/>

❌ **W przeciwnym razie:** Podczas snu przez długi czas testy będą o rząd wielkości wolniejsze. Podczas próby spania dla małych liczb test nie powiedzie się, gdy testowana jednostka nie zareagowała w odpowiednim czasie. Sprowadza się to zatem do kompromisu między flakiness, a złą wydajnością

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: E2E API rozwiązuje to dopiero po zakończeniu operacji asynchronicznych (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: Przykład robienia tego dobrze: Biblioteka testująca, która czeka na elementy DOM


```javascript
// @testing-library/dom
test("movie title appears", async () => {
  // element is initially not present...

  // wait for appearance
  await wait(() => {
    expect(getByText("the lion king")).toBeInTheDocument();
  });

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

### :thumbsdown: Przykład antywzorca: niestandardowy sleep code

```javascript
test("movie title appears", async () => {
  // element is initially not present...

  // custom wait logic (caution: simplistic, no timeout)
  const interval = setInterval(() => {
    const found = getByText("the lion king");
    if (found) {
      clearInterval(interval);
      expect(getByText("the lion king")).toBeInTheDocument();
    }
  }, 100);

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

</details>

<br/>

## ⚪ ️ 3.5 Zobacz, jak treść jest udostępniana przez sieć

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Examples with Lighthouse")

✅ **Opis:** Zastosuj aktywny monitor, który zapewnia optymalizację ładowania strony w rzeczywistej sieci - obejmuje to wszelkie problemy związane z UX, takie jak powolne ładowanie strony lub niezminimalizowany pakiet. Rynek narzędzi inspekcyjnych nie jest krótki: podstawowe narzędzia, takie jak [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) można łatwo skonfigurować, aby sprawdzał, czy serwer żyje i reagował na podstawie rozsądnej SLA. To tylko rysuje powierzchnię tego, co może się nie udać, dlatego lepiej wybrać narzędzia specjalizujące się we frontendzie (np. [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) i wykonać bogatszą analizę. Należy skoncentrować się na objawach, wskaźnikach, które bezpośrednio wpływają na UX, takich jak czas ładowania strony, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [czas, aż strona stanie się interaktywna (TTI)](https://calibreapp.com/blog/time-to-interactive/). Ponadto można również zwrócić uwagę na przyczyny techniczne, takie jak zapewnienie kompresji zawartości, czas do pierwszego bajtu, optymalizacja obrazów, zapewnienie rozsądnego rozmiaru DOM, SSL i wiele innych. Wskazane jest, aby mieć te bogate monitory zarówno podczas projektowania, jako część CI, a co najważniejsze - 24x7 przez serwery produkcji / CDN

<br/>

❌ **W przeciwnym razie:** Musi być rozczarowujące, gdy zda się sobie sprawę, że po tak wielkiej dbałości o interfejs użytkownika, 100% testy funkcjonalne zdały i wyrafinowane pakowanie - UX jest straszny i powolny z powodu błędnej konfiguracji CDN

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

### :clap: Przykład robienia tego dobrze: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

</details>

<br/>

## ⚪ ️ 3.6 Stub niestabilne i wolne zasoby, takie jak interfejsy API zaplecza

:white_check_mark: **Opis:** When coding your mainstream tests (not E2E tests), avoid involving any resource that is beyond your responsibility and control like backend API and use stubs instead (i.e. test double). Practically, instead of real network calls to APIs, use some test double library (like [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) for stubbing the API response. The main benefit is preventing flakiness - testing or staging APIs by definition are not highly stable and from time to time will fail your tests although YOUR component behaves just fine (production env was not meant for testing and it usually throttles requests). Doing this will allow simulating various API behavior that should drive your component behavior as when no data was found or the case when API throws an error. Last but not least, network calls will greatly slow down the tests

<br/>

❌ **W przeciwnym razie:** The average test runs no longer than few ms, a typical API call last 100ms>, this makes each test ~20x slower

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Stubbing or intercepting API calls

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// unit under test
export default function ProductsList() {
  const [products, setProducts] = useState(false);

  const fetchProducts = async () => {
    const products = await axios.get("api/products");
    setProducts(products);
  };

  useEffect(() => {
    fetchProducts();
  }, []);

  return products ? <div>{products}</div> : <div data-testid="no-products-message">No products</div>;
}

// test
test("When no products exist, show the appropriate message", () => {
  // Arrange
  nock("api")
    .get(`/products`)
    .reply(404);

  // Act
  const { getByTestId } = render(<ProductsList />);

  // Assert
  expect(getByTestId("no-products-message")).toBeTruthy();
});
```

</details>

<br/>

## ⚪ ️ 3.7 Have very few end-to-end tests that spans the whole system

:white_check_mark: **Do:** Although E2E (end-to-end) usually means UI-only testing with a real browser (See bullet 3.6), for other they mean tests that stretch the entire system including the real backend. The latter type of tests is highly valuable as they cover integration bugs between frontend and backend that might happen due to a wrong understanding of the exchange schema. They are also an efficient method to discover backend-to-backend integration issues (e.g. Microservice A sends the wrong message to Microservice B) and even to detect deployment failures - there are no backend frameworks for E2E testing that are as friendly and mature as UI frameworks like [Cypress](https://www.cypress.io/) and [Pupeteer](https://github.com/GoogleChrome/puppeteer). The downside of such tests is the high cost of configuring an environment with so many components, and mostly their brittleness - given 50 microservices, even if one fails then the entire E2E just failed. For that reason, we should use this technique sparingly and probably have 1-10 of those and no more. That said, even a small number of E2E tests are likely to catch the type of issues they are targeted for - deployment & integration faults. It's advisable to run those over a production-like staging environment

<br/>

❌ **Otherwise:** UI might invest much in testing its functionality only to realizes very late that the backend returned payload (the data schema the UI has to work with) is very different than expected

<br/>

## ⚪ ️ 3.8 Speed-up E2E tests by reusing login credentials

:white_check_mark: **Opis:** In E2E tests that involve a real backend and rely on a valid user token for API calls, it doesn't payoff to isolate the test to a level where a user is created and logged-in in every request. Instead, login only once before the tests execution start (i.e. before-all hook), save the token in some local storage and reuse it across requests. This seem to violate one of the core testing principle - keep the test autonomous without resources coupling. While this is a valid worry, in E2E tests performance is a key concern and creating 1-3 API requests before starting each individial tests might lead to horrible execution time. Reusing credentials doesn't mean the tests have to act on the same user records - if relying on user records (e.g. test user payments history) than make sure to generate those records as part of the test and avoid sharing their existence with other tests. Also remember that the backend can be faked - if your tests are focused on the frontend it might be better to isolate it and stub the backend API (see bullet 3.6).

<br/>

❌ **W przeciwnym razie:** Given 200 test cases and assuming login=100ms = 20 seconds only for logging-in again and again

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Logging-in before-all and not before-each

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
let authenticationToken;

// happens before ALL tests run
before(() => {
  cy.request('POST', 'http://localhost:3000/login', {
    username: Cypress.env('username'),
    password: Cypress.env('password'),
  })
  .its('body')
  .then((responseFromLogin) => {
    authenticationToken = responseFromLogin.token;
  })
})

// happens before EACH test
beforeEach(setUser => () {
  cy.visit('/home', {
    onBeforeLoad (win) {
      win.localStorage.setItem('token', JSON.stringify(authenticationToken))
    },
  })
})

```

</details>

<br/>

## ⚪ ️ 3.9 Have one E2E smoke test that just travels across the site map

:white_check_mark: **Opis:** For production monitoring and development-time sanity check, run a single E2E test that visits all/most of the site pages and ensures no one breaks. This type of test brings a great return on investment as it's very easy to write and maintain, but it can detect any kind of failure including functional, network and deployment issues. Other styles of smoke and sanity checking are not as reliable and exhaustive - some ops teams just ping the home page (production) or developers who run many integration tests which don't discover packaging and browser issues. Goes without saying that the smoke test doesn't replace functional tests rather just aim to serve as a quick smoke detector

<br/>

❌ **W przeciwnym razie:** Everything might seem perfect, all tests pass, production health-check is also positive but the Payment component had some packaging issue and only the /Payment route is not rendering

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Smoke travelling across all pages

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
it("When doing smoke testing over all page, should load them all successfully", () => {
  // exemplified using Cypress but can be implemented easily
  // using any E2E suite
  cy.visit("https://mysite.com/home");
  cy.contains("Home");
  cy.contains("https://mysite.com/Login");
  cy.contains("Login");
  cy.contains("https://mysite.com/About");
  cy.contains("About");
});
```

</details>

<br/>

## ⚪ ️ 3.10 Expose the tests as a live collaborative document

:white_check_mark: **Opis:** Besides increasing app reliability, tests bring another attractive opportunity to the table - serve as live app documentation. Since tests inherently speak at a less-technical and product/UX language, using the right tools they can serve as a communication artifact that greatly aligns all the peers - developers and their customers. For example, some frameworks allow expressing the flow and expectations (i.e. tests plan) using a human-readable language so any stakeholder, including product managers, can read, approve and collaborate on the tests which just became the live requirements document. This technique is also being referred to as 'acceptance test' as it allows the customer to define his acceptance criteria in plain language. This is [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) at its purest form. One of the popular frameworks that enable this is [Cucumber which has a JavaScript flavor](https://github.com/cucumber/cucumber-js), see example below. Another similar yet different opportunity, [StoryBook](https://storybook.js.org/), allows exposing UI components as a graphic catalog where one can walk through the various states of each component (e.g. render a grid w/o filters, render that grid with multiple rows or with none, etc), see how it looks like, and how to trigger that state - this can appeal also to product folks but mostly serves as live doc for developers who consume those components.

❌ **W przeciwnym razie:** After investing top resources on testing, it's just a pity not to leverage this investment and win great value

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Describing tests in human-language using cucumber-js

![](https://img.shields.io/badge/🔨%20Example%20using%20Cucumber-blue.svg "Examples using Cucumber")

```javascript
// this is how one can describe tests using cucumber: plain language that allows anyone to understand and collaborate

Feature: Twitter new tweet

  I want to tweet something in Twitter

  @focus
  Scenario: Tweeting from the home page
    Given I open Twitter home
    Given I click on "New tweet" button
    Given I type "Hello followers!" in the textbox
    Given I click on "Submit" button
    Then I see message "Tweet saved"

```

### :clap: Przykład robienia tego dobrze: Visualizing our components, their various states and inputs using Storybook

![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Detect visual issues with automated tools

:white_check_mark: **Opis:** Setup automated tools to capture UI screenshots when changes are presented and detect visual issues like content overlapping or breaking. This ensures that not only the right data is prepared but also the user can conveniently see it. This technique is not widely adopted, our testing mindset leans toward functional tests but it's the visuals what the user experience and with so many device types it's very easy to overlook some nasty UI bug. Some free tools can provide the basics - generate and save screenshots for the inspection of human eyes. While this approach might be sufficient for small apps, it's flawed as any other manual testing that demands human labor anytime something changes. On the other hand, it's quite challenging to detect UI issues automatically due to the lack of clear definition - this is where the field of 'Visual Regression' chime in and solve this puzzle by comparing old UI with the latest changes and detect differences. Some OSS/free tools can provide some of this functionality (e.g. [wraith](https://github.com/BBC-News/wraith), [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>) but might charge signficant setup time. The commercial line of tools (e.g. [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) takes is a step further by smoothing the installation and packing advanced features like management UI, alerting, smart capturing by elemeinating 'visual noise' (e.g. ads, animations) and even root cause analysis of the DOM/css changes that led to the issue

<br/>

❌ **W przeciwnym razie:** How good is a content page that display great content (100% tests passed), loads instantly but half of the content area is hidden?

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: A typical visual regression - right content that is served badly

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Przykład robienia tego dobrze: Configuring wraith to capture and compare UI snapshots

![](https://img.shields.io/badge/🔨%20Example%20using%20Wraith-blue.svg "Using Wraith")

```
​# Add as many domains as necessary. Key will act as a label​

domains:
  english: "http://www.mysite.com"​

​# Type screen widths below, here are a couple of examples​

screen_widths:

  - 600​
  - 768​
  - 1024​
  - 1280​

​# Type page URL paths below, here are a couple of examples​
paths:
  about:
    path: /about
    selector: '.about'​
  subscribe:
      selector: '.subscribe'​
    path: /subscribe
```

### :clap: Przykład robienia tego dobrze: Using Applitools to get snapshot comaprison and other advanced features

![](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg "Using AppliTools") ![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
import * as todoPage from "../page-objects/todo-page";

describe("visual validation", () => {
  before(() => todoPage.navigate());
  beforeEach(() => cy.eyesOpen({ appName: "TAU TodoMVC" }));
  afterEach(() => cy.eyesClose());

  it("should look good", () => {
    cy.eyesCheckWindow("empty todo list");
    todoPage.addTodo("Clean room");
    todoPage.addTodo("Learn javascript");
    cy.eyesCheckWindow("two todos");
    todoPage.toggleTodo(0);
    cy.eyesCheckWindow("mark as completed");
  });
});
```

</details>

<br/><br/>

# Sekcja 4️⃣: Measuring Test Effectiveness

<br/><br/>

## ⚪ ️ 4.1 Get enough coverage for being confident, ~80% seems to be the lucky number

:white_check_mark: **Opis:** The purpose of testing is to get enough confidence for moving fast, obviously the more code is tested the more confident the team can be. Coverage is a measure of how many code lines (and branches, statements, etc) are being reached by the tests. So how much is enough? 10–30% is obviously too low to get any sense about the build correctness, on the other side 100% is very expensive and might shift your focus from the critical paths to the exotic corners of the code. The long answer is that it depends on many factors like the type of application — if you’re building the next generation of Airbus A380 than 100% is a must, for a cartoon pictures website 50% might be too much. Although most of the testing enthusiasts claim that the right coverage threshold is contextual, most of them also mention the number 80% as a thumb of a rule ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) that presumably should satisfy most of the applications.

Implementation tips: You may want to configure your continuous integration (CI) to have a coverage threshold ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) and stop a build that doesn’t stand to this standard (it’s also possible to configure threshold per component, see code example below). On top of this, consider detecting build coverage decrease (when a newly committed code has less coverage) — this will push developers raising or at least preserving the amount of tested code. All that said, coverage is only one measure, a quantitative based one, that is not enough to tell the robustness of your testing. And it can also be fooled as illustrated in the next bullets

<br/>

❌ **W przeciwnym razie:** Confidence and numbers go hand in hand, without really knowing that you tested most of the system — there will also be some fear. and fear will slow you down

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Example: A typical coverage report

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Przykład robienia tego dobrze: Setting up coverage per component (using Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Using Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Inspect coverage reports to detect untested areas and other oddities

:white_check_mark: **Opis:** Some issues sneak just under the radar and are really hard to find using traditional tools. These are not really bugs but more of surprising application behavior that might have a severe impact. For example, often some code areas are never or rarely being invoked — you thought that the ‘PricingCalculator’ class is always setting the product price but it turns out it is actually never invoked although we have 10000 products in DB and many sales… Code coverage reports help you realize whether the application behaves the way you believe it does. Other than that, it can also highlight which types of code is not tested — being informed that 80% of the code is tested doesn’t tell whether the critical parts are covered. Generating reports is easy — just run your app in production or during testing with coverage tracking and then see colorful reports that highlight how frequent each code area is invoked. If you take your time to glimpse into this data — you might find some gotchas
<br/>

❌ **W przeciwnym razie:** If you don’t know which parts of your code are left un-tested, you don’t know where the issues might come from

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Przykład antywzorca: What’s wrong with this coverage report?

Based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Measure logical coverage using mutation testing

:white_check_mark: **Opis:** The Traditional Coverage metric often lies: It may show you 100% code coverage, but none of your functions, even not one, return the right response. How come? it simply measures over which lines of code the test visited, but it doesn’t check if the tests actually tested anything — asserted for the right response. Like someone who’s traveling for business and showing his passport stamps — this doesn’t prove any work done, only that he visited few airports and hotels.

Mutation-based testing is here to help by measuring the amount of code that was actually TESTED not just VISITED. [Stryker](https://stryker-mutator.io/) is a JavaScript library for mutation testing and the implementation is really neat:

(1) it intentionally changes the code and “plants bugs”. For example the code newOrder.price===0 becomes newOrder.price!=0. This “bugs” are called mutations

(2) it runs the tests, if all succeed then we have a problem — the tests didn’t serve their purpose of discovering bugs, the mutations are so-called survived. If the tests failed, then great, the mutations were killed.

Knowing that all or most of the mutations were killed gives much higher confidence than traditional coverage and the setup time is similar
<br/>

❌ **W przeciwnym razie:** You’ll be fooled to believe that 85% coverage means your test will detect bugs in 85% of your code

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: 100% coverage, 0% testing

![](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg "Using Stryker")

```javascript
function addNewOrder(newOrder) {
  logger.log(`Adding new order ${newOrder}`);
  DB.save(newOrder);
  Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

  return { approved: true };
}

it("Test addNewOrder, don't use such test names", () => {
  addNewOrder({ asignee: "John@mailer.com", price: 120 });
}); //Triggers 100% code coverage, but it doesn't check anything
```

<br/>

### :clap: Przykład robienia tego dobrze: Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>

<br/><br/>

## ⚪ ️4.4 Preventing test code issues with Test linters

:white_check_mark: **Opis:** A set of ESLint plugins were built specifically for inspecting the tests code patterns and discover issues. For example, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) will warn when a test is written at the global level (not a son of a describe() statement) or when tests are [skipped](https://mochajs.org/#inclusive-tests) which might lead to a false belief that all tests are passing. Similarly, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) can, for example, warn when a test has no assertions at all (not checking anything)

<br/>

❌ **W przeciwnym razie:** Seeing 90% code coverage and 100% green tests will make your face wear a big smile only until you realize that many tests aren’t asserting for anything and many test suites were just skipped. Hopefully, you didn’t deploy anything based on this false observation

<br/>
<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: A test case full of errors, luckily all are caught by Linters

```javascript
describe("Too short description", () => {
  const userToken = userService.getDefaultToken() // *error:no-setup-in-describe, use hooks (sparingly) instead
  it("Some description", () => {});//* error: valid-test-description. Must include the word "Should" + at least 5 words
});

it.skip("Test name", () => {// *error:no-skipped-tests, error:error:no-global-tests. Put tests only under describe or suite
  expect("somevalue"); // error:no-assert
});

it("Test name", () => {*//error:no-identical-title. Assign unique titles to tests
});
```

</details>

<br/><br/>

# Sekcja 5️⃣: CI and Other Quality Measures

<br/><br/>

## ⚪ ️ 5.1 Enrich your linters and abort builds that have linting issues

:white_check_mark: **Opis:** Linters are a free lunch, with 5 min setup you get for free an auto-pilot guarding your code and catching significant issue as you type. Gone are the days where linting was about cosmetics (no semi-colons!). Nowadays, Linters can catch severe issues like errors that are not thrown correctly and losing information. On top of your basic set of rules (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), consider including some specializing Linters like [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) that can discover tests without assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) can discover promises with no resolve (your code will never continue), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) which can discover eager regex expressions that might get used for DOS attacks, and [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) is capable of alarming when the code uses utility library methods that are part of the V8 core methods like Lodash.\_map(…)
<br/>

❌ **W przeciwnym razie:** Consider a rainy day where your production keeps crashing but the logs don’t display the error stack trace. What happened? Your code mistakenly threw a non-error object and the stack trace was lost, a good reason for banging your head against a brick wall. A 5min linter setup could detect this TYPO and save your day

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>

<br/><br/>

## ⚪ ️ 5.2 Shorten the feedback loop with local developer-CI

:white_check_mark: **Opis:** Using a CI with shiny quality inspections like testing, linting, vulnerabilities check, etc? Help developers run this pipeline also locally to solicit instant feedback and shorten the [feedback loop](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Why? an efficient testing process constitutes many and iterative loops: (1) try-outs -> (2) feedback -> (3) refactor. The faster the feedback is, the more improvement iterations a developer can perform per-module and perfect the results. On the flip, when the feedback is late to come fewer improvement iterations could be packed into a single day, the team might already move forward to another topic/task/module and might not be up for refining that module.

Practically, some CI vendors (Example: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/)) allow running the pipeline locally. Some commercial tools like [wallaby provide highly-valuable & testing insights](https://wallabyjs.com/) as a developer prototype (no affiliation). Alternatively, you may just add npm script to package.json that runs all the quality commands (e.g. test, lint, vulnerabilities) — use tools like [concurrently](https://www.npmjs.com/package/concurrently) for parallelization and non-zero exit code if one of the tools failed. Now the developer should just invoke one command — e.g. ‘npm run quality’ — to get instant feedback. Consider also aborting a commit if the quality check failed using a githook ([husky can help](https://github.com/typicode/husky))
<br/>

❌ **W przeciwnym razie:** When the quality results arrive the day after the code, testing doesn’t become a fluent part of development rather an after the fact formal artifact

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: npm scripts that perform code quality inspection, all are run in parallel on demand or when a developer is trying to push new code

```javascript
"scripts": {
    "inspect:sanity-testing": "mocha **/**--test.js --grep \"sanity\"",
    "inspect:lint": "eslint .",
    "inspect:vulnerabilities": "npm audit",
    "inspect:license": "license-checker --failOn GPLv2",
    "inspect:complexity": "plato .",

    "inspect:all": "concurrently -c \"bgBlue.bold,bgMagenta.bold,yellow\" \"npm:inspect:quick-testing\" \"npm:inspect:lint\" \"npm:inspect:vulnerabilities\" \"npm:inspect:license\""
  },
  "husky": {
    "hooks": {
      "precommit": "npm run inspect:all",
      "prepush": "npm run inspect:all"
    }
}

```

</details>

<br/><br/>

## ⚪ ️5.3 Perform e2e testing over a true production-mirror

:white_check_mark: **Opis:** End to end (e2e) testing are the main challenge of every CI pipeline — creating an identical ephemeral production mirror on the fly with all the related cloud services can be tedious and expensive. Finding the best compromise is your game: [Docker-compose](https://serverless.com/) allows crafting isolated dockerized environment with identical containers using a single plain text file but the backing technology (e.g. networking, deployment model) is different from real-world productions. You may combine it with [‘AWS Local’](https://github.com/localstack/localstack) to work with a stub of the real AWS services. If you went [serverless](https://serverless.com/) multiple frameworks like serverless and [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) allows the local invocation of Faas code.

The huge Kubernetes eco-system is yet to formalize a standard convenient tool for local and CI-mirroring though many new tools are launched frequently. One approach is running a ‘minimized-Kubernetes’ using tools like [Minikube](https://kubernetes.io/docs/setup/minikube/) and [MicroK8s](https://microk8s.io/) which resemble the real thing only come with less overhead. Another approach is testing over a remote ‘real-Kubernetes’, some CI providers (e.g. [Codefresh](https://codefresh.io/)) has native integration with Kubernetes environment and make it easy to run the CI pipeline over the real thing, others allow custom scripting against a remote Kubernetes.
<br/>

❌ **W przeciwnym razie:** Using different technologies for production and testing demands maintaining two deployment models and keeps the developers and the ops team separated

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Example: a CI pipeline that generates Kubernetes cluster on the fly <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Parallelize test execution

:white_check_mark: **Opis:** When done right, testing is your 24/7 friend providing almost instant feedback. In practice, executing 500 CPU-bounded unit test on a single thread can take too long. Luckily, modern test runners and CI platforms (like [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) and [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) can parallelize the test into multiple processes and achieve significant improvement in feedback time. Some CI vendors do also parallelize tests across containers (!) which shortens the feedback loop even further. Whether locally over multiple processes, or over some cloud CLI using multiple machines — parallelizing demand keeping the tests autonomous as each might run on different processes

❌ **W przeciwnym razie:** Getting test results 1 hour long after pushing new code, as you already code the next features, is a great recipe for making testing less relevant

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze: Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Stay away from legal issues using license and plagiarism check

:white_check_mark: **Opis:** Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like [license check](https://www.npmjs.com/package/license-checker) and [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stackoverflow and apparently violates some copyrights

❌ **W przeciwnym razie:** Unintentionally, developers might use packages with inappropriate licenses or copy paste commercial code and run into legal issues

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Przykład robienia tego dobrze:

```javascript
//install license-checker in your CI environment or also locally
npm install -g license-checker

//ask it to scan all licenses and fail with exit code other than 0 if it found unauthorized license. The CI system should catch this failure and stop the build
license-checker --summary --failOn BSD

```

<br/>

![alt text](assets/bp-25-nodejs-licsense.png)

</details>

<br/><br/>

## ⚪ ️5.6 Constantly inspect for vulnerable dependencies

:white_check_mark: **Opis:** Even the most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community tools such as [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), or commercial tools like [snyk](https://snyk.io/) (offer also a free community version). Both can be invoked from your CI on every build

❌ **Otherwise:** Keeping your code clean from vulnerabilities without dedicated tools will require to constantly follow online publications about new threats. Quite tedious

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Example: NPM Audit result

![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>

<br/><br/>

## ⚪ ️5.7 Automate dependency updates

:white_check_mark: **Opis:** Yarn and npm latest introduction of package-lock.json introduced a serious challenge (the road to hell is paved with good intentions) — by default now, packages are no longer getting updates. Even a team running many fresh deployments with ‘npm install’ & ‘npm update’ won’t get any new updates. This leads to subpar dependent packages versions at best or to vulnerable code at worst. Teams now rely on developers goodwill and memory to manually update the package.json or use tools [like ncu](https://www.npmjs.com/package/npm-check-updates) manually. A more reliable way could be to automate the process of getting the most reliable dependency versions, though there are no silver bullet solutions yet there are two possible automation roads:

(1) CI can fail builds that have obsolete dependencies — using tools like [‘npm outdated’](https://docs.npmjs.com/cli/outdated) or ‘npm-check-updates (ncu)’ . Doing so will enforce developers to update dependencies.

(2) Use commercial tools that scan the code and automatically send pull requests with updated dependencies. One interesting question remaining is what should be the dependency update policy — updating on every patch generates too many overhead, updating right when a major is released might point to an unstable version (many packages found vulnerable on the very first days after being released, [see the](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope incident).

An efficient update policy may allow some ‘vesting period’ — let the code lag behind the @latest for some time and versions before considering the local copy as obsolete (e.g. local version is 1.3.1 and repository version is 1.3.8)
<br/>

❌ **W przeciwnym razie:** Your production will run packages that have been explicitly tagged by their author as risky

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Example: [ncu](https://www.npmjs.com/package/npm-check-updates) can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")

</details>

<br/><br/>

## ⚪ ️ 5.8 Other, non-Node related, CI tips

:white_check_mark: **Opis:** This post is focused on testing advice that is related to, or at least can be exemplified with Node JS. This bullet, however, groups few non-Node related tips that are well-known

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use a declarative syntax. This is the only option for most vendors but older versions of Jenkins allows using code or UI</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opt for a vendor that has native Docker support</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Fail early, run your fastest tests first. Create a ‘Smoke testing’ step/milestone that groups multiple fast inspections (e.g. linting, unit tests) and provide snappy feedback to the code committer</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Make it easy to skim-through all build artifacts including test reports, coverage reports, mutation reports, logs, etc</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Create multiple pipelines/jobs for each event, reuse steps between them. For example, configure a job for feature branch commits and a different one for master PR. Let each reuse logic using shared steps (most vendors provide some mechanism for code reuse)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Never embed secrets in a job declaration, grab them from a secret store or from the job’s configuration</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Explicitly bump version in a release build or at least ensure the developer did so</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Build only once and perform all the inspections over the single build artifact (e.g. Docker image)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Test in an ephemeral environment that doesn’t drift state between builds. Caching node_modules might be the only exception</li></ol>
<br/>

❌ **W przeciwnym razie:** You‘ll miss years of wisdom

<br/><br/>

## ⚪ ️ 5.9 Build matrix: Run the same CI steps using multiple Node versions

:white_check_mark: **Opis:** Quality checking is about serendipity, the more ground you cover the luckier you get in detecting issues early. When developing reusable packages or running a multi-customer production with various configuration and Node versions, the CI must run the pipeline of tests over all the permutations of configurations. For example, assuming we use MySQL for some customers and Postgres for others — some CI vendors support a feature called ‘Matrix’ which allow running the suit of testing against all permutations of MySQL, Postgres and multiple Node version like 8, 9 and 10. This is done using configuration only without any additional effort (assuming you have testing or any other quality checks). Other CIs who doesn’t support Matrix might have extensions or tweaks to allow that
<br/>

❌ **W przeciwnym razie:** So after doing all that hard work of writing testing are we going to let bugs sneak in only because of configuration issues?

<br/>

<details><summary>✏ <b>Przykłady kodu</b></summary>

<br/>

### :clap: Example: Using Travis (CI vendor) build definition to run the same test over multiple Node versions

<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# Zespół

## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Rola:** Writer

**Opis:** Jestem niezależnym konsultantem, który współpracuje z firmami Fortune 500 i garażowymi startupami przy dopracowywaniu aplikacji JS i Node.js. Bardziej niż jakikolwiek inny temat fascynuje mnie, i mam na celu, opanowanie sztuki testowania. Jestem także autorem [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

**📗 Kurs online:** Podobał Ci się ten przewodnik i chcesz maksymalnie wykorzystać swoje umiejętności testowania? Rozważ skorzystanie z mojego kompleksowego kursu [Testowanie Node.js i JavaScript od A do Z](https://www.testjavascript.com)

<br/>

**Obserwuj:**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 Kontakt](https://testjavascript.com/contact-2/)
- [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**Rola:** Recenzent i doradca techniczny

Zadbał o poprawienie, ulepszenie, usunięcie i dopracowanie wszystkich tekstów

**Opis:** full-stack web engineer, entuzjasta Node.js & GraphQL

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Rola:** Koncepcja, projekt i świetna rada

**Opis:** Wytrawny frontend developer, ekspert CSS i emojis freak

## [Kyle Martin](https://github.com/js-kyle)

**Rola:** Pomaga utrzymać ten projekt w ruchu i weryfikuje praktyki związane z bezpieczeństwem

**Opis:** Uwielbia pracę nad projektami Node.js i bezpieczeństwem aplikacji internetowych.

## Współtwórcy ✨

Podziękowania dla tych wspaniałych ludzi, którzy przyczynili się do tego repozytorium!

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://geospatialscott.blogspot.com/"><img src="https://avatars3.githubusercontent.com/u/1326248?v=4" width="100px;" alt=""/><br /><sub><b>Scott Davis</b></sub></a><br /><a href="#content-stdavis" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AdrienRedon"><img src="https://avatars2.githubusercontent.com/u/5978436?v=4" width="100px;" alt=""/><br /><sub><b>Adrien REDON</b></sub></a><br /><a href="#content-AdrienRedon" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/NoriSte"><img src="https://avatars0.githubusercontent.com/u/173663?v=4" width="100px;" alt=""/><br /><sub><b>Stefano Magni</b></sub></a><br /><a href="#content-NoriSte" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.joer.im"><img src="https://avatars2.githubusercontent.com/u/47742486?v=4" width="100px;" alt=""/><br /><sub><b>Yeoh Joer</b></sub></a><br /><a href="#content-yjoer" title="Content">🖋</a></td>
    <td align="center"><a href="http://jhonnymoreira.dev"><img src="https://avatars0.githubusercontent.com/u/2177742?v=4" width="100px;" alt=""/><br /><sub><b>Jhonny Moreira</b></sub></a><br /><a href="#content-jhonnymoreira" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Germanika"><img src="https://avatars2.githubusercontent.com/u/8846678?v=4" width="100px;" alt=""/><br /><sub><b>Ian Germann</b></sub></a><br /><a href="#content-Germanika" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AbdelrahmanHafez"><img src="https://avatars3.githubusercontent.com/u/19984935?v=4" width="100px;" alt=""/><br /><sub><b>Hafez</b></sub></a><br /><a href="#content-AbdelrahmanHafez" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.ruxandrafediuc.com"><img src="https://avatars1.githubusercontent.com/u/11021586?v=4" width="100px;" alt=""/><br /><sub><b>Ruxandra Fediuc</b></sub></a><br /><a href="#content-ruxandrafed" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jacklee814"><img src="https://avatars0.githubusercontent.com/u/9951291?v=4" width="100px;" alt=""/><br /><sub><b>Jack</b></sub></a><br /><a href="#content-jacklee814" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.petercarrero.com"><img src="https://avatars0.githubusercontent.com/u/231727?v=4" width="100px;" alt=""/><br /><sub><b>Peter Carrero</b></sub></a><br /><a href="#content-aloyr" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/huhgawz"><img src="https://avatars3.githubusercontent.com/u/369338?v=4" width="100px;" alt=""/><br /><sub><b>Huhgawz</b></sub></a><br /><a href="#content-huhgawz" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/haakonmb"><img src="https://avatars1.githubusercontent.com/u/7099302?v=4" width="100px;" alt=""/><br /><sub><b>Haakon Borch</b></sub></a><br /><a href="#content-haakonmb" title="Content">🖋</a></td>
    <td align="center"><a href="https://jaimemendoza.com/"><img src="https://avatars3.githubusercontent.com/u/5395811?v=4" width="100px;" alt=""/><br /><sub><b>Jaime Mendoza</b></sub></a><br /><a href="#content-jaimemendozadev" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/camerondunford"><img src="https://avatars0.githubusercontent.com/u/840612?v=4" width="100px;" alt=""/><br /><sub><b>Cameron Dunford</b></sub></a><br /><a href="#content-camerondunford" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/shadowspawn"><img src="https://avatars1.githubusercontent.com/u/15719847?v=4" width="100px;" alt=""/><br /><sub><b>John Gee</b></sub></a><br /><a href="#content-shadowspawn" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/aurelijusrozenas"><img src="https://avatars0.githubusercontent.com/u/3273544?v=4" width="100px;" alt=""/><br /><sub><b>Aurelijus Rožėnas</b></sub></a><br /><a href="#content-aurelijusrozenas" title="Content">🖋</a></td>
    <td align="center"><a href="http://aaronshivers.com"><img src="https://avatars2.githubusercontent.com/u/42848750?v=4" width="100px;" alt=""/><br /><sub><b>Aaron</b></sub></a><br /><a href="#content-aaronshivers" title="Content">🖋</a></td>
    <td align="center"><a href="https://tomdoes.tech/"><img src="https://avatars1.githubusercontent.com/u/8683577?v=4" width="100px;" alt=""/><br /><sub><b>Tom Nagle</b></sub></a><br /><a href="#content-tomanagle" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/yvesyao"><img src="https://avatars0.githubusercontent.com/u/7723729?v=4" width="100px;" alt=""/><br /><sub><b>Yves yao</b></sub></a><br /><a href="#content-yvesyao" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Userbit"><img src="https://avatars1.githubusercontent.com/u/34487074?v=4" width="100px;" alt=""/><br /><sub><b>Userbit</b></sub></a><br /><a href="#content-Userbit" title="Content">🖋</a></td>
    <td align="center"><a href="https://glaucialemos.netlify.com/"><img src="https://avatars0.githubusercontent.com/u/1631477?v=4" width="100px;" alt=""/><br /><sub><b>Glaucia Lemos</b></sub></a><br /><a href="#maintenance-glaucia86" title="Maintenance">🚧</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://twitter.com/koooge"><img src="https://avatars2.githubusercontent.com/u/7419215?v=4" width="100px;" alt=""/><br /><sub><b>koooge</b></sub></a><br /><a href="#content-koooge" title="Content">🖋</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->
