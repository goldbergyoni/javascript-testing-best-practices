<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 Por que este guia pode levar suas habilidades de teste para o próximo nível

<br/>

## 📗 45+ boas práticas: Super abrangente e exaustivo
Este é um guia para a confiabilidade JavaScript & Node.js da A-Z. Ele resume e organiza para você dezenas das melhores publicações, livros, ferramentas e postagens de blogs que o mercado tem a oferecer


## 🚢 Avançado: vai 10.000 milhas além do básico
Entre em uma jornada que vai muito além do básico, para tópicos avançados como testes em produção, testes de mutação, testes baseados em propriedades e muitas outras ferramentas estratégicas e profissionais. Se você ler todas as palavras deste guia, é provável que suas habilidades de teste superem a média


## 🌐 Full-stack: front, backend, CI(Integração Contínua), qualquer coisa
Comece entendendo as práticas de teste onipresentes que são a base para qualquer camada de aplicativo. Em seguida, mergulhe na sua área de escolha: front-end/UI, back-end, CI(Integração Contínua) ou talvez todos eles?

<br/>

### Escrito por Yoni Goldberg
* Um consultor JavaScript & Node.js
* 👨‍🏫 [Minha oficina de testes](https://www.testjavascript.com) -  aprenda sobre [meus workshops](https://www.testjavascript.com) na Europe & Estados Unidos
* [Me siga no twitter ](https://twitter.com/goldbergyoni/)
* Venha me ouvir falar em [LA](https://js.la/), [Verona](https://2019.nodejsday.it/), [Kharkiv](https://kharkivjs.org/), [free webinar](https://zoom.us/webinar/register/1015657064375/WN_Lzvnuv4oQJOYey2jXNqX6A). Eventos futuros TBD
* [Newsletter informativo de qualidade sobre JavaScript](https://testjavascript.com/newsletter/) - insights e conteúdo apenas em assuntos estratégicos


<br/><br/>

## `Índice`

#### [`Seção 0: A Regra de ouro`](#section-0️⃣-the-golden-rule)

Um único conselho que inspira todos os outros (1 marcador especial)

#### [`Seção 1: A Anatomia do Teste`](#section-1-the-test-anatomy-1)

A fundação - estruturando testes limpos (12 marcadores)

#### [`Seção 2: Backend`](#section-2️⃣-backend-testing)

Escrevendo testes de back-end e microsserviços com eficiência (8 marcadores)

#### [`Seção 3: Frontend`](#section-3️⃣-frontend-testing)

Escrevendo testes para interface do usuário da web, incluindo testes de componentes e E2E (11 marcadores)

#### [`Seção 4: Metrificando Testes Efetivamente`](#section-4️⃣-measuring-test-effectiveness)

Observando o vigia - medindo a qualidade do teste (4 marcadores)

#### [`Seção 5: Integração Contínua`](#section-5️⃣-ci-and-other-quality-measures)

Diretrizes para CI no mundo JS (9 marcadores)


<br/><br/>


# Seção 0️⃣: A Regra de Ouro

<br/>

## ⚪️ 0. A Regra de Ouro: Design para testes enxutos

:white_check_mark: **Faça:**
O código de teste não é como o código de produção - projete-o para ser simples, curto, sem abstrações, plano, agradável de se trabalhar, enxuto. Deve-se olhar para um teste e obter a intenção instantaneamente.

Nossas mentes estão cheias com o código principal de produção, não temos 'espaço de sobra' para complexidade adicional. Se tentarmos espremer outro código desafiador em nosso cérebro fraco, a equipe ficará mais lenta, o que vai de encontro com a razão pela qual fazemos os testes. Praticamente é aqui que muitas equipes abandonam os testes.

Os testes são uma oportunidade para outra coisa - um assistente amigável e sorridente, que é agradável de trabalhar e oferece grande valor para um investimento tão pequeno. A ciência diz que temos dois sistemas cerebrais: o sistema 1, usado para atividades sem esforço, como dirigir um carro em uma estrada vazia, e o sistema 2, destinado a operações complexas e conscientes, como resolver uma equação matemática. Projete seu teste para o sistema 1, ao analisar o código de teste, ele deve parecer tão fácil quanto modificar um documento HTML e não como resolver um equação 2X (17 × 24).

Isso pode ser alcançado através de técnicas, ferramentas e alvos de teste selecionados de forma econômica, que são econômicos e proporcionam um ótimo ROI. Teste apenas o necessário, esforce-se para mantê-lo ágil, às vezes vale a pena abandonar alguns testes e trocar a confiabilidade por agilidade e simplicidade.

![alt text](/assets/headspace.png "We have no head room for additional complexity")
 
A maioria dos conselhos abaixo são derivados desse princípio.

### Pronto para começar?


<br/><br/>

# Seção 1: A Anatomia do Teste

<br/>

## ⚪ ️ 1.1 Inclua 3 partes em cada nome de teste

:white_check_mark: **Faça:** Um relatório de teste deve informar se a revisão atual do aplicativo atende aos requisitos para as pessoas que não estão necessariamente familiarizadas com o código: o testador, o engenheiro DevOps que está implantando e você daqui a dois anos. Isso pode ser melhor alcançado se os testes falarem no nível de requisitos e incluirem 3 partes:

(1) O que está sendo testado? Por exemplo, o método ProductsService.addNewProduct

(2) Sob que circunstâncias e cenário? Por exemplo, nenhum preço é passado para o método

(3) Qual é o resultado esperado? Por exemplo, o novo produto não é aprovado

<br/>


❌ **Caso contrário:** Uma implantação acabou de falhar, um teste chamado "Adicionar produto" falhou. Isso diz o que exatamente está com defeito?

<br/>

**👇 Nota:** Cada marcador possui exemplos de código e alguns tem ilustrações. Clique para expandir
<details><summary>✏ <b>Códigos de Exemplo</b></summary>
  
<br/>
  
### :clap: Exemplo: um nome de teste que constitui 3 partes

![](https://img.shields.io/badge/🔨%20Example%20using%20Mocha-blue.svg
 "Using Mocha to illustrate the idea")

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

### :clap: Exemplo: um nome de teste que constitui 3 partes
![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️ 1.2 Testes de estrutura pelo padrão em inglês AAA

:white_check_mark: **Faça:** Estruture seus testes com 3 seções bem separadas: Organizar, Atuar e Afirmar (OAA). Seguir essa estrutura garante que o leitor não gaste CPU do cérebro na compreensão do plano de teste:

1st O - Organizar: todo o código de configuração para levar o sistema ao cenário que o teste pretende simular. Isso pode incluir instanciar a unidade sob o construtor de teste, adicionar registros de banco de dados, mockar/stubbing de objetos e qualquer outro código de preparação

2nd A - Ato: Execute teste em unidade. Geralmente 1 linha de código

3rd A - Afirmar: Garanta que o valor recebido satisfaça a expectativa. Geralmente 1 linha de código


<br/>


❌ **Caso contrário:** Você não gata apenas longas horas diárias para entender o código principal, agora também o que deveria ter sido a parte simples do dia (teste) estica seu cérebro

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Doing It Right Example: A test structured with the AAA pattern

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest") ![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Jest")
  
```javascript
describe('Customer classifier', () => {
    test('When customer spent more than 500$, should be classified as premium', () => {
        //Arrange
        const customerToClassify = {spent:505, joined: new Date(), id:1}
        const DBStub = sinon.stub(dataAccess, "getCustomer")
            .reply({id:1, classification: 'regular'});

        //Act
        const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);

        //Assert
        expect(receivedClassification).toMatch('premium');
    });
});
```

<br/>

### :thumbsdown: Anti Pattern Example: No separation, one bulk, harder to interpret

```javascript
test('Should be classified as premium', () => {
        const customerToClassify = {spent:505, joined: new Date(), id:1}
        const DBStub = sinon.stub(dataAccess, "getCustomer")
            .reply({id:1, classification: 'regular'});
        const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);
        expect(receivedClassification).toMatch('premium');
    });
```


</details>



<br/><br/>




## ⚪ ️1.3 Describe expectations in a product language: use BDD-style assertions

:white_check_mark: **Do:** Coding your tests in a declarative-style allows the reader to get the grab instantly without spending even a single brain-CPU cycle. When you write an imperative code that is packed with conditional logic the reader is thrown away to an effortful mental mood. In that sense, code the expectation in a human-like language, declarative BDD style using expect or should and not using custom code. If Chai & Jest don’t include the desired assertion and it’s highly repeatable, consider [extending Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) or writing a [custom Chai plugin](https://www.chaijs.com/guide/plugins/)
<br/>


❌ **Otherwise:** The team will write less test and decorate the annoying ones with .skip()

<br/>

<details><summary>✏ <b>Code Examples</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")
  
  ### :thumbsdown: Anti Pattern Example: The reader must skim through not so short, and imperative code just to get the test story

```javascript
test("When asking for an admin, ensure only ordered admins in results" , () => {
    //assuming we've added here two admins "admin1", "admin2" and "user1"
    const allAdmins = getUsers({adminOnly:true});

    const admin1Found, adming2Found = false;

    allAdmins.forEach(aSingleUser => {
        if(aSingleUser === "user1"){
            assert.notEqual(aSingleUser, "user1", "A user was found and not admin");
        }
        if(aSingleUser==="admin1"){
            admin1Found = true;
        }
        if(aSingleUser==="admin2"){
            admin2Found = true;
        }
    });

    if(!admin1Found || !admin2Found ){
        throw new Error("Not all admins were returned");
    }
});

```
<br/>

### :clap: Doing It Right Example: Skimming through the following declarative test is a breeze


```javascript
it("When asking for an admin, ensure only ordered admins in results" , () => {
    //assuming we've added here two admins
    const allAdmins = getUsers({adminOnly:true});

    expect(allAdmins).to.include.ordered.members(["admin1" , "admin2"])
  .but.not.include.ordered.members(["user1"]);
});

```

</details>


<br/><br/>


## ⚪ ️  1.4 Stick to black-box testing: Test only public methods

:white_check_mark: **Do:** Testing the internals brings huge overhead for almost nothing. If your code/API deliver the right results, should you really invest your next 3 hours in testing HOW it worked internally and then maintain these fragile tests? Whenever a public behavior is checked, the private implementation is also implicitly tested and your tests will break only if there is a certain problem (e.g. wrong output). This approach is also referred to as behavioral testing. On the other side, should you test the internals (white box approach) — your focus shifts from planning the component outcome to nitty-gritty details and your test might break because of minor code refactors although the results are fine- this dramatically increases the maintenance burden
<br/>


❌ **Otherwise:** Your test behaves like the [child who cries wolf](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf): shoot out loud false-positive cries (e.g., A test fails because a private variable name was changed). Unsurprisingly, people will soon start to ignore the CI notifications until someday a real bug will get ignored…

<br/>
<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: A test case is testing the internals for no good reason
![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Mocha & Chai")
```javascript
class ProductService{
  //this method is only used internally
  //Change this name will make the tests fail
  calculateVAT(priceWithoutVAT){
    return {finalPrice: priceWithoutVAT * 1.2};
    //Change the result format or key name above will make the tests fail
  }
  //public method
  getPrice(productId){
    const desiredProduct= DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
  }
}


it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
    //There's no requirement to allow users to calculate the VAT, only show the final price. Nevertheless we falsely insist here to test the class internals
    expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});

```

</details>




<br/><br/>

## ⚪ ️ ️1.5 Choose the right test doubles: Avoid mocks in favor of stubs and spies

:white_check_mark: **Do:**  Test doubles are a necessary evil because they are coupled to the application internals, yet some provide an immense value (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Read here a reminder about test doubles: mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Before using test doubles, ask a very simple question: Do I use it to test functionality that appears, or could appear, in the requirements document? If no, it’s a smell of white-box testing.

For example, if you want to test what your app behaves reasonably when the payment service is down, you might stub the payment service and trigger some ‘No Response’ return to ensure that the unit under test returns the right value. This checks our application behavior/response/outcome under certain scenarios. You might also use a spy to assert that an email was sent when that service is down — this is again a behavioral check which is likely to appear in a requirements doc (“Send an email if payment couldn’t be saved”). On the flip side, if you mock the Payment service and ensure that it was called with the right JavaScript types — then your test is focused on internal things that got nothing with the application functionality and are likely to change frequently
<br/>


❌ **Otherwise:** Any refactoring of code mandates searching for all the mocks in the code and updating accordingly. Tests become a burden rather than a helpful friend

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-pattern example: Mocks focus on the internals
![](https://img.shields.io/badge/🔧%20Example%20using%20Sinon-blue.svg
 "Examples with Mocha & Chai")
```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
    //Assume we already added a product
    const dataAccessMock = sinon.mock(DAL);
    //hmmm BAD: testing the internals is actually our main goal here, not just a side-effect
    dataAccessMock.expects("deleteProduct").once().withArgs(DBConfig, theProductWeJustAdded, true, false);
    new ProductService().deletePrice(theProductWeJustAdded);
    dataAccessMock.verify();
});
```
<br/>

### :clap:Doing It Right Example: spies are focused on testing the requirements but as a side-effect are unavoidably touching to the internals

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
    //Assume we already added here a product
    const spy = sinon.spy(Emailer.prototype, "sendEmail");
    new ProductService().deletePrice(theProductWeJustAdded);
    //hmmm OK: we deal with internals? Yes, but as a side effect of testing the requirements (sending an email)
});
```

</details>



<br/><br/>

## ⚪ ️1.6 Don’t “foo”, use realistic input data

:white_check_mark: **Do:**  Often production bugs are revealed under some very specific and surprising input — the more realistic the test input is, the greater the chances are to catch bugs early. Use dedicated libraries like [Faker](https://www.npmjs.com/package/faker) to generate pseudo-real data that resembles the variety and form of production data. For example, such libraries can generate realistic phone numbers, usernames, credit card, company names, and even ‘lorem ipsum’ text. You may also create some tests (on top of unit tests, not instead) that randomize fakers data to stretch your unit under test or even import real data from your production environment. Want to take it to the next level? see next bullet (property-based testing).
<br/>


❌ **Otherwise:** All your development testing will falsely seem green when you use synthetic inputs like “Foo” but then production might turn red when a hacker passes-in a nasty string like “@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA”


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: A test suite that passes due to non-realistic data

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")
 
 
```javascript
const addProduct = (name, price) =>{
  const productNameRegexNoSpace = /^\S*$/;//no white-space allowd

  if(!productNameRegexNoSpace.test(name))
    return false;//this path never reached due to dull input

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

### :clap:Doing It Right Example: Randomizing realistic input
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

## ⚪ ️ 1.7 Test many input combinations using Property-based testing

:white_check_mark: **Do:** Typically we choose a few input samples for each test. Even when the input format resembles real-world data (see bullet ‘Don’t foo’), we cover only a few input combinations (method(‘’, true, 1), method(“string” , false” , 0)), However, in production, an API that is called with 5 parameters can be invoked with thousands of different permutations, one of them might render our process down ([see Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)). What if you could write a single test that sends 1000 permutations of different inputs automatically and catches for which input our code fails to return the right response? Property-based testing is a technique that does exactly that: by sending all the possible input combinations to your unit under test it increases the serendipity of finding a bug. For example, given a method — addNewProduct(id, name, isDiscount) — the supporting libraries will call this method with many combinations of (number, string, boolean) like (1, “iPhone”, false), (2, “Galaxy”, true). You can run property-based testing using your favorite test runner (Mocha, Jest, etc) using libraries like [js-verify](https://github.com/jsverify/jsverify) or [testcheck](https://github.com/leebyron/testcheck-js) (much better documentation). Update: Nicolas Dubien suggests in the comments below to [checkout fast-check](https://github.com/dubzzz/fast-check#readme) which seems to offer some additional features and also to be actively maintained
<br/>


❌ **Otherwise:** Unconsciously, you choose the test inputs that cover only code paths that work well. Unfortunately, this decreases the efficiency of testing as a vehicle to expose bugs


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap:  Doing It Right Example: Testing many input permutations with “mocha-testcheck”

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Jest")

```javascript
require('mocha-testcheck').install();
const {expect} = require('chai');

describe('Product service', () => {
  describe('Adding new', () => {
    //this will run 100 times with different random properties
    check.it('Add new product with random yet valid properties, always successful',
      gen.int, gen.string, (id, name) => {
        expect(addNewProduct(id, name).status).to.equal('approved');
      });
  })
});

```

</details>




<br/><br/>

## ⚪ ️ 1.8 If needed, use only short & inline snapshots

:white_check_mark: **Do:** When there is a need for [snapshot testing](https://jestjs.io/docs/en/snapshot-testing), use only short and focused snapshots (i.e. 3-7 lines) that are included as part of the test ([Inline Snapshot](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)) and not within external files. Keeping this guideline will ensure your tests remain self-explanatory and less fragile.

On the other hand, ‘classic snapshots’ tutorials and tools encourage to store big files (e.g. component rendering markup, API JSON result) over some external medium and ensure each time when the test run to compare the received result with the saved version. This, for example, can implicitly couple our test to 1000 lines with 3000 data values that the test writer never read and reasoned about. Why is this wrong? By doing so, there are 1000 reasons for your test to fail - it’s enough for a single line to change for the snapshot to get invalid and this is likely to happen a lot. How frequently? for every space, comment or minor CSS/HTML change. Not only this, the test name wouldn’t give a clue about the failure as it just checks that 1000 lines didn’t change, also it encourages to the test writer to accept as the desired true a long document he couldn’t inspect and verify. All of these are symptoms of obscure and eager test that is not focused and aims to achieve too much

It’s worth noting that there are few cases where long & external snapshots are acceptable - when asserting on schema and not data (extracting out values and focusing on fields) or when the received document rarely changes
<br/>

❌ **Otherwise:** A UI test fails. The code seems right, the screen renders perfect pixels, what happened? your snapshot testing just found a difference from the origin document to current received one - a single space character was added to the markdown... 

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: Coupling our test to unseen 2000 lines of code

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")
 
```javascript
it('TestJavaScript.com is renderd correctly', ()  => {

//Arrange

//Act
const receivedPage = renderer
.create(  <DisplayPage page  =  "http://www.testjavascript.com"  > Test JavaScript < /DisplayPage>)
.toJSON();

//Assert
expect(receivedPage).toMatchSnapshot();
//We now implicitly maintain a 2000 lines long document
//every additional line break or comment - will break this test

});
```
<br/>

### :clap: Doing It Right Example: Expectations are visible and focused
```javascript
it('When visiting TestJavaScript.com home page, a menu is displayed', () => {
//Arrange

//Act
receivedPage tree = renderer
.create(  <DisplayPage page  =  "http://www.testjavascript.com"  > Test JavaScript < /DisplayPage>)
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

## ⚪ ️1.9 Avoid global test fixtures and seeds, add data per-test

:white_check_mark: **Do:** Going by the golden rule (bullet 0), each test should add and act on its own set of DB rows to prevent coupling and easily reason about the test flow. In reality, this is often violated by testers who seed the DB with data before running the tests ([also known as ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) for the sake of performance improvement. While performance is indeed a valid concern — it can be mitigated (see “Component testing” bullet), however, test complexity is a much painful sorrow that should govern other considerations most of the time. Practically, make each test case explicitly add the DB records it needs and act only on those records. If performance becomes a critical concern — a balanced compromise might come in the form of seeding the only suite of tests that are not mutating data (e.g. queries)
<br/>


❌ **Otherwise:** Few tests fail, a deployment is aborted, our team is going to spend precious time now, do we have a bug? let’s investigate, oh no — it seems that two tests were mutating the same seed data


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: tests are not independent and rely on some global hook to feed global DB data

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Jest")
 
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

### :clap: Doing It Right Example: We can stay within the test, each test acts on its own set of data

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

## ⚪ ️ 1.10 Don’t catch errors, expect them
:white_check_mark: **Do:**   When trying to assert that some input triggers an error, it might look right to use try-catch-finally and asserts that the catch clause was entered. The result is an awkward and verbose test case (example below) that hides the simple test intent and the result expectations

A more elegant alternative is the using the one-line dedicated Chai assertion: expect(method).to.throw (or in Jest: expect(method).toThrow()). It’s absolutely mandatory to also ensure the exception contains a property that tells the error type, otherwise given just a generic error the application won’t be able to do much rather than show a disappointing message to the user
<br/>


❌ **Otherwise:** It will be challenging to infer from the test reports (e.g. CI reports) what went wrong


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-pattern Example: A long test case that tries to assert the existence of error with try-catch

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Jest")
 
```javascript
it("When no product name, it throws error 400", async() => {
let errorWeExceptFor = null;
try {
  const result = await addNewProduct({name:'nest'});}
catch (error) {
  expect(error.code).to.equal('InvalidInput');
  errorWeExceptFor = error;
}
expect(errorWeExceptFor).not.to.be.null;
//if this assertion fails, the tests results/reports will only show
//that some value is null, there won't be a word about a missing Exception
});

```
<br/>

### :clap: Doing It Right Example: A human-readable expectation that could be understood easily, maybe even by QA or technical PM

```javascript
it.only("When no product name, it throws error 400", async() => {
  expect(addNewProduct)).to.eventually.throw(AppError).with.property('code', "InvalidInput");
});

```

</details>




<br/><br/>

## ⚪ ️ 1.11 Tag your tests

:white_check_mark: **Do:**  Different tests must run on different scenarios: quick smoke, IO-less, tests should run when a developer saves or commits a file, full end-to-end tests usually run when a new pull request is submitted, etc. This can be achieved by tagging tests with keywords like #cold #api #sanity so you can grep with your testing harness and invoke the desired subset. For example, this is how you would invoke only the sanity test group with Mocha: mocha — grep ‘sanity’
<br/>


❌ **Otherwise:** Running all the tests, including tests that perform dozens of DB queries, any time a developer makes a small change can be extremely slow and keeps developers away from running tests


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Tagging tests as ‘#cold-test’ allows the test runner to execute only fast tests (Cold===quick tests that are doing no IO and can be executed frequently even as the developer is typing)

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")
```javascript
//this test is fast (no DB) and we're tagging it correspondigly
//now the user/CI can run it frequently
describe('Order service', function() {
  describe('Add new order #cold-test #sanity', function() {
    test('Scenario - no currency was supplied. Expectation - Use the default currency #sanity', function() {
      //code logic here
    });
  });
});


```

</details>




<br/><br/>

## ⚪ ️1.12 Other generic good testing hygiene
:white_check_mark: **Do:**  This post is focused on testing advice that is related to, or at least can be exemplified with Node JS. This bullet, however, groups few non-Node related tips that are well-known

Learn and practice [TDD principles](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) — they are extremely valuable for many but don’t get intimidated if they don’t fit your style, you’re not the only one. Consider writing the tests before the code in a [red-green-refactor style](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), ensure each test checks exactly one thing, when you find a bug — before fixing write a test that will detect this bug in the future, let each test fail at least once before turning green, start a module by writing a quick and simplistic code that satsifies the test - then refactor gradually and take it to a production grade level, avoid any dependency on the environment (paths, OS, etc)
<br/>


❌ **Otherwise:** You‘ll miss pearls of wisdom that were collected for decades

<br/><br/>


# Section 2️⃣: Backend Testing

## ⚪ ️2.1 Enrich your testing portfolio: Look beyond unit tests and the pyramid

:white_check_mark: **Do:**  The [testing pyramid](https://martinfowler.com/bliki/TestPyramid.html), though 10> years old, is a great and relevant model that suggests three testing types and influences most developers’ testing strategy. At the same time, more than a handful of shiny new testing techniques emerged and are hiding in the shadows of the testing pyramid. Given all the dramatic changes that we’ve seen in the recent 10 years (Microservices, cloud, serverless), is it even possible that one quite-old model will suit *all* types of applications? shouldn’t the testing world consider welcoming new testing techniques?

Don’t get me wrong, in 2019 the testing pyramid, TDD and unit tests are still a powerful technique and are probably the best match for many applications. Only like any other model, despite its usefulness, [it must be wrong sometimes](https://en.wikipedia.org/wiki/All_models_are_wrong). For example, consider an IOT application that ingests many events into a message-bus like Kafka/RabbitMQ, which then flow into some data-warehouse and are eventually queried by some analytics UI. Should we really spend 50% of our testing budget on writing unit tests for an application that is integration-centric and has almost no logic? As the diversity of application types increase (bots, crypto, Alexa-skills) greater are the chances to find scenarios where the testing pyramid is not the best match.

It’s time to enrich your testing portfolio and become familiar with more testing types (the next bullets suggest few ideas), mind models like the testing pyramid but also match testing types to real-world problems that you’re facing (‘Hey, our API is broken, let’s write consumer-driven contract testing!’), diversify your tests like an investor that build a portfolio based on risk analysis — assess where problems might arise and match some prevention measures to mitigate those potential risks

A word of caution: the TDD argument in the software world takes a typical false-dichotomy face, some preach to use it everywhere, others think it’s the devil. Everyone who speaks in absolutes is wrong :]

<br/>


❌ **Otherwise:** You’re going to miss some tools with amazing ROI, some like Fuzz, lint, and mutation can provide value in 10 minutes


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’
![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Example: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")


</details>




<br/><br/>

## ⚪ ️2.2 Component testing might be your best affair

:white_check_mark: **Do:** Each unit test covers a tiny portion of the application and it’s expensive to cover the whole, whereas end-to-end testing easily covers a lot of ground but is flaky and slower, why not apply a balanced approach and write tests that are bigger than unit tests but smaller than end-to-end testing? Component testing is the unsung song of the testing world — they provide the best from both worlds: reasonable performance and a possibility to apply TDD patterns + realistic and great coverage.

Component tests focus on the Microservice ‘unit’, they work against the API, don’t mock anything which belongs to the Microservice itself (e.g. real DB, or at least the in-memory version of that DB) but stub anything that is external like calls to other Microservices. By doing so, we test what we deploy, approach the app from outwards to inwards and gain great confidence in a reasonable amount of time.
<br/>


❌ **Otherwise:** You may spend long days on writing unit tests to find out that you got only 20% system coverage


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Supertest allows approaching Express API in-process (fast and cover many layers)

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Jest")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 Ensure new releases don’t break the API using

:white_check_mark: **Do:**  So your Microservice has multiple clients, and you run multiple versions of the service for compatibility reasons (keeping everyone happy). Then you change some field and ‘boom!’, some important client who relies on this field is angry. This is the Catch-22 of the integration world: It’s very challenging for the server side to consider all the multiple client expectations — On the other hand, the clients can’t perform any testing because the server controls the release dates. [Consumer-driven contracts and the framework PACT](https://docs.pact.io/) were born to formalize this process with a very disruptive approach — not the server defines the test plan of itself rather the client defines the tests of the… server! PACT can record the client expectation and put in a shared location, “broker”, so the server can pull the expectations and run on every build using PACT library to detect broken contracts — a client expectation that is not met. By doing so, all the server-client API mismatches are caught early during build/CI and might save you a great deal of frustration
<br/>


❌ **Otherwise:** The alternatives are exhausting manual testing or deployment fear


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg
 "Examples with PACT")
 
![alt text](assets/bp-14-testing-best-practices-contract-flow.png )


</details>



<br/><br/>


## ⚪ ️ 2.4 Test your middlewares in isolation

:white_check_mark: **Do:** Many avoid Middleware testing because they represent a small portion of the system and require a live Express server. Both reasons are wrong — Middlewares are small but affect all or most of the requests and can be tested easily as pure functions that get {req,res} JS objects. To test a middleware function one should just invoke it and spy ([using Sinon for example](https://www.npmjs.com/package/sinon)) on the interaction with the {req,res} objects to ensure the function performed the right action. The library [node-mock-http](https://www.npmjs.com/package/node-mocks-http) takes it even further and factors the {req,res} objects along with spying on their behavior. For example, it can assert whether the http status that was set on the res object matches the expectation (See example below)
<br/>


❌ **Otherwise:** A bug in Express middleware === a bug in all or most requests


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap:Doing It Right Example: Testing middleware in isolation without issuing network calls and waking-up the entire Express machine

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")

```javascript
//the middleware we want to test
const unitUnderTest = require('./middleware')
const httpMocks = require('node-mocks-http');
//Jest syntax, equivelant to describe() & it() in Mocha
test('A request without authentication header, should return http status 403', () => {
  const request = httpMocks.createRequest({
    method: 'GET',
    url: '/user/42',
    headers: {
      authentication: ''
    }
  });
  const response = httpMocks.createResponse();
  unitUnderTest(request, response);
  expect(response.statusCode).toBe(403);
});

```

</details>




<br/><br/>

## ⚪ ️2.5 Measure and refactor using static analysis tools
:white_check_mark: **Do:** Using static analysis tools helps by giving objective ways to improve code quality and keep your code maintainable. You can add static analysis tools to your CI build to abort when it finds code smells. Its main selling points over plain linting are the ability to inspect quality in the context of multiple files (e.g. detect duplications), perform advanced analysis (e.g. code complexity) and follow the history and progress of code issues. Two examples of tools you can use are [Sonarqube](https://www.sonarqube.org/) (2,600+ [stars](https://github.com/SonarSource/sonarqube)) and [Code Climate](https://codeclimate.com/) (1,500+ [stars](https://github.com/codeclimate/codeclimate))

Credit:: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>


❌ **Otherwise:** With poor code quality, bugs and performance will always be an issue that no shiny new library or state of the art features can fix


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example:  CodeClimate, a commercial tool that can identify complex methods:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg
 "Examples with CodeClimate")
 
![alt text](assets/bp-16-yoni-goldberg-quality.png " CodeClimat, a commercial tool that can identify complex methods:")

</details>




<br/><br/>

## ⚪ ️ 2.6 Check your readiness for Node-related chaos
:white_check_mark: **Do:** Weirdly, most software testings are about logic & data only, but some of the worst things that happen (and are really hard to mitigate ) are infrastructural issues. For example, did you ever test what happens when your process memory is overloaded, or when the server/process dies, or does your monitoring system realizes when the API becomes 50% slower?. To test and mitigate these type of bad things — [Chaos engineering](https://principlesofchaos.org/) was born by Netflix. It aims to provide awareness, frameworks and tools for testing our app resiliency for chaotic issues. For example, one of its famous tools, [the chaos monkey](https://github.com/Netflix/chaosmonkey), randomly kills servers to ensure that our service can still serve users and not relying on a single server (there is also a Kubernetes version, [kube-monkey](https://github.com/asobti/kube-monkey), that kills pods). All these tools work on the hosting/platform level, but what if you wish to test and generate pure Node chaos like check how your Node process copes with uncaught errors, unhandled promise rejection, v8 memory overloaded with the max allowed of 1.7GB or whether your UX stays satisfactory when the event loop gets blocked often? to address this I’ve written, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) which provides all sort of Node-related chaotic acts
<br/>


❌ **Otherwise:**  No escape here, Murphy’s law will hit your production without mercy


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: : Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos
![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 Avoid global test fixtures and seeds, add data per-test

:white_check_mark: **Do:** Going by the golden rule (bullet 0), each test should add and act on its own set of DB rows to prevent coupling and easily reason about the test flow. In reality, this is often violated by testers who seed the DB with data before running the tests (also known as ‘test fixture’) for the sake of performance improvement. While performance is indeed a valid concern — it can be mitigated (see “Component testing” bullet), however, test complexity is a much painful sorrow that should govern other considerations most of the time. Practically, make each test case explicitly add the DB records it needs and act only on those records. If performance becomes a critical concern — a balanced compromise might come in the form of seeding the only suite of tests that are not mutating data (e.g. queries)
<br/>


❌ **Otherwise:** Few tests fail, a deployment is aborted, our team is going to spend precious time now, do we have a bug? let’s investigate, oh no — it seems that two tests were mutating the same seed data


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: tests are not independent and rely on some global hook to feed global DB data

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Mocha")
 
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

### :clap: Doing It Right Example: We can stay within the test, each test acts on its own set of data

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

# Seção 3️⃣: Teste de Frontend

## ⚪ ️ 3.1. Separar UI da funcionalidade

:white_check_mark: **Faça:** Ao focar no teste da lógica dos componentes, os detalhes da interface do usuário se tornam um ruído que deve ser extraído, para que seus testes possam se concentrar em dados puros. Na prática, extraia os dados desejados da marcação de uma maneira abstrata que não seja muito acoplada à implementação gráfica, afirme apenas dados puros (vs detalhes gráficos de HTML/CSS) e desative animações que diminuem a velocidade. Você pode cair na tentação de evitar renderizar e testar apenas a parte de trás da interface do usuário (por exemplo, serviços, ações, armazenamento), mas isso resultará em testes fictícios que não se assemelham à realidade e não revelam casos em que os dados corretos nem chegam na interface do usuário


<br/>

❌ **Caso contrário:** Os dados puramente calculados do seu teste podem estar prontos em 10 ms, mas o teste inteiro durará 500 ms (100 testes = 1 min) devido a alguma animação sofisticada e irrelevante


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Separando os detalhes da interface do usuário

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React-blue.svg
 "Exemplos com React") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React%20Testing%20Library-blue.svg
 "Exemplos com react-testing-library")

```javascript
test('When users-list is flagged to show only VIP, should display only VIP members', () => {
  // Arrange
  const allUsers = [
   { id: 1, name: 'Yoni Goldberg', vip: false }, 
   { id: 2, name: 'John Doe', vip: true }
  ];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true}/>);

  // Assert - Extract the data from the UI first
  const allRenderedUsers = getAllByTestId('user').map(uiElement => uiElement.textContent);
  const allRealVIPUsers = allUsers.filter((user) => user.vip).map((user) => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //compare data with data, no UI here
});

```

<br/>

### :thumbsdown: Exemplo Anti-padrão: Asserções misturam detalhes da UI e dados
```javascript
test('When flagging to show only VIP, should display only VIP members', () => {
  // Arrange
  const allUsers = [
   {id: 1, name: 'Yoni Goldberg', vip: false }, 
   {id: 2, name: 'John Doe', vip: true }
  ];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true}/>);

  // Assert - Mix UI & data in assertion
  expect(getAllByTestId('user')).toEqual('[<li data-testid="user">John Doe</li>]');
});

```

</details>




<br/><br/>


## ⚪ ️ 3.2 Consultar elementos HTML com base em atributos que provavelmente não serão alterados

:white_check_mark: **Faça*:** Consulte elementos HTML com base em atributos que provavelmente sobreviverão a alterações gráficas, diferentemente dos seletores CSS e sim como os rótulos de formulário. Se o elemento designado não tiver esses atributos, crie um atributo dedicado a teste  como 'test-id-submit-button'. Seguir essa rota não apenas garante que seus testes funcionais/lógicos nunca sejam quebrados devido a alterações de aparência, mas também fica claro para toda a equipe que esse elemento e atributo são utilizados por testes e não devem ser removidos

<br/>

❌ **Caso contrário:** Você deseja testar a funcionalidade de login que abrange muitos componentes, lógica e serviços, tudo está configurado perfeitamente - stubs, spies, chamadas Ajax são isoladas. Tudo parece perfeito. Em seguida, o teste falha porque o designer alterou a classe CSS da div de 'thick-border' para 'thin-border'

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Consultando um elemento usando um atributo dedicado para teste

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React-blue.svg
 "Exemplos com React")
 
```html
// the markup code (part of React component)
<h3>
  <Badge pill className="fixed_badge" variant="dark">
    <span data-testid="errorsLabel">{value}</span> <!-- note the attribute data-testid -->
  </Badge>
</h3>
```

```javascript
// this example is using react-testing-library
  test('Whenever no data is passed to metric, show 0 as default', () => {
    // Arrange
    const metricValue = undefined;

    // Act
    const { getByTestId } = render(<dashboardMetric value={undefined}/>);    
    
    expect(getByTestId('errorsLabel')).text()).toBe("0");
  });

```

<br/>

### :thumbsdown: Exemplo Anti-padrão: Confiando em atributos CSS
```html
<!-- the markup code (part of React component) -->
<span id="metric" className="d-flex-column">{value}</span> <!-- what if the designer changes the classs? -->
```

```javascript
// this exammple is using enzyme
test('Whenever no data is passed, error metric shows zero', () => {
    // ...
    
    expect(wrapper.find("[className='d-flex-column']").text()).toBe("0");
  });
```


</details>




<br/>

## ⚪ ️ 3.3 Sempre que possível, teste com um componente realista e totalmente renderizado

:white_check_mark: **Faça:** Sempre que tiver um tamanho razoável, teste seu componente de fora como os usuários, renderize a interface do usuário, atue sobre ela e afirme que a interface do usuário renderizada se comporta conforme o esperado. Evite todo tipo de simulação, renderização parcial e superficial - essa abordagem pode resultar em erros não capturados devido à falta de detalhes e dificultar a manutenção, pois os testes interferem nos internos (veja o marcador 'Favorecer o teste de caixa preta'). Se um dos componentes filhos estiver desacelerando significativamente (por exemplo, animação) ou complicando a instalação - considere substituí-lo explicitamente por um falso

Com tudo isso dito, uma palavra de cautela é necessária: essa técnica funciona para componentes pequenos/médios que contêm um tamanho razoável de componentes filhos. A renderização completa de um componente com muitos filhos dificultará o raciocínio sobre falhas de teste (análise de causa raiz) e poderá ficar muito lenta. Nesses casos, escreva apenas alguns testes contra esse componente pai pesado e mais testes contra seus filhos

<br/>

❌ **Caso contrário:** Ao entrar no interno de um componente, invocando seus métodos privados e verificando o estado interno - você teria que refatorar todos os testes ao refatorar a implementação dos componentes. Você realmente tem capacidade para esse nível de manutenção?


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Trabalhando realisticamente com um componente totalmente renderizado

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React-blue.svg
 "Exemplos com React") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Enzyme-blue.svg
 "Exemplos com Enzyme")
 
```javascript
class Calendar extends React.Component {
  static defaultProps = {showFilters: false}
  
  render() {
    return (
      <div>
        A filters panel with a button to hide/show filters
        <FiltersPanel showFilter={showFilters} title='Choose Filters'/>
      </div>
    )
  }
}

//Examples use React & Enzyme
test('Realistic approach: When clicked to show filters, filters are displayed', () => {
    // Arrange
    const wrapper = mount(<Calendar showFilters={false} />)

    // Act
    wrapper.find('button').simulate('click');

    // Assert
    expect(wrapper.text().includes('Choose Filter'));
    // This is how the user will approach this element: by text
})


```

### :thumbsdown: Exemplo Anti-padrão: Simulando a realidade com renderização superficial
```javascript

test('Shallow/mocked approach: When clicked to show filters, filters are displayed', () => {
    // Arrange
    const wrapper = shallow(<Calendar showFilters={false} title='Choose Filter'/>)

    // Act
    wrapper.find('filtersPanel').instance().showFilters();
    // Tap into the internals, bypass the UI and invoke a method. White-box approach

    // Assert
    expect(wrapper.find('Filter').props()).toEqual({title: 'Choose Filter'});
    // what if we change the prop name or don't pass anything relevant?
})

```

</details>

<br/>


## ⚪ ️ 3.4 Não durma, use o suporte incorporado de frameworks para eventos assíncronos. Também tente acelerar as coisas

:white_check_mark: **Faça:** Em muitos casos, o tempo de conclusão da unidade em teste é desconhecido (por exemplo, a animação suspende a aparência do elemento) - nesse caso, evite dormir (por exemplo, setTimeOut) e prefira métodos mais determinísticos que a maioria das plataformas fornece. Algumas bibliotecas permitem aguardar operações (por exemplo, [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), outras fornecem API para esperar como [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance). Às vezes, uma maneira mais elegante é esboçar o recurso lento, como a API, por exemplo, e depois que o momento da resposta se torna determinístico, o componente pode ser explicitamente renderizado novamente. Quando, dependendo de algum componente externo que dorme, pode ser útil [apressar o relógio](https://jestjs.io/docs/en/timer-mocks). Dormir é um padrão a ser evitado, porque força o teste a ser lento ou arriscado (ao esperar por um período muito curto). Sempre que dormir e pesquisar for inevitável e não há suporte do framework de teste, algumas bibliotecas do NPM, como [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) podem ajudar com uma solução semi-determinística 
<br/>

❌ **Caso contrário:** Ao dormir por um longo tempo, os testes serão uma ordem de magnitude mais lenta. Ao tentar dormir por pequenos números, o teste falha quando a unidade em teste não responde em tempo hábil. Portanto, tudo se resume a uma troca entre descamação e mau desempenho


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: API E2E que resolve somente quando as operações assíncronas são concluídas (Cypress)

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React-blue.svg
 "Exemplos com React") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React%20Testing%20Library-blue.svg
 "Exemplos com react-testing-library")

```javascript
// using Cypress
cy.get('#show-products').click()// navigate
cy.wait('@products')// wait for route to appear
// this line will get executed only when the route is ready

```

### :clap: Exemplo Fazendo Certo: Biblioteca de teste que aguarda elementos do DOM

```javascript
// @testing-library/dom
test('movie title appears', async () => {
    // element is initially not present...

    // wait for appearance
    await wait(() => {
        expect(getByText('the lion king')).toBeInTheDocument()
    })

    // wait for appearance and return the element
    const movie = await waitForElement(() => getByText('the lion king'))
})

```

### :thumbsdown: Exemplo Anti-padrão: código de suspensão personalizado
```javascript

test('movie title appears', async () => {
    // element is initially not present...

    // custom wait logic (caution: simplistic, no timeout)
    const interval = setInterval(() => {
        const found = getByText('the lion king');
        if(found){
            clearInterval(interval);
            expect(getByText('the lion king')).toBeInTheDocument();
        }
        
    }, 100);

    // wait for appearance and return the element
    const movie = await waitForElement(() => getByText('the lion king'))
})

```

</details>


<br/>

## ⚪ ️ 3.5. Veja como o conteúdo é servido na rede

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Google%20LightHouse-blue.svg
 "Exemplo com Lighthouse")

✅ **Faça:** Aplique um monitor ativo que garanta que o carregamento da página na rede real seja otimizado - isso inclui qualquer preocupação de UX, como carregamento lento da página ou pacote não minificado. O mercado de ferramentas de inspeção não é curto: ferramentas básicas como [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) podem ser facilmente configuradas para verificar se o servidor está ativo e responde sob um SLA razoável. Isso apenas arranha a superfície do que pode estar errado; portanto, é preferível optar por ferramentas especializadas em frontend(por exemplo, [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) e realizar análises mais ricas. O foco deve estar nos sintomas, nas métricas que afetam diretamente o UX, como o tempo de carregamento da página, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [ttempo até a página ficar interativa (TTI)](https://calibreapp.com/blog/time-to-interactive/). Além disso, também é possível observar causas técnicas, como garantir que o conteúdo seja compactado, tempo até o primeiro byte, otimizar imagens, garantir tamanho razoável de DOM, SSL e muitos outros. É aconselhável ter esses monitores avançados durante o desenvolvimento, como parte do CI e o mais importante - 24x7 nos servidores de produção/CDN

<br/>

❌ **Caso contrário:** Deve ser decepcionante perceber que, após um cuidado tão grande na criação de uma interface do usuário, testes 100% funcionais passando e empacotamento sofisticado - o UX é horrível e lento devido à configuração incorreta da CDN

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

### :clap: Exemplo Fazendo Certo: Relatório de inspeção de carregamento de página do Lighthouse

![](/assets/lighthouse2.png "Relatório de inspeção de carregamento de página do Lighthouse")


</details>


<br/>

## ⚪ ️ 3.6 Esboce recursos escamosos e lentos, como APIs de backend

:white_check_mark: **Faça:** Ao codificar seus testes convencionais (não os testes E2E), evite envolver qualquer recurso que esteja além de sua responsabilidade e controle como a API de backend e use esboços (por exemplo, teste duplo). Na prática, em vez de chamadas de rede reais para APIs, use alguma biblioteca de teste duplo (como [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) para esboçar a resposta da API. O principal benefício é evitar falhas - APIs de teste ou preparo, por definição, não são altamente estáveis ​​e, de tempos em tempos, serão reprovados em seus testes, embora SEU componente se comporte perfeitamente (o ambiente de produção não foi projetado para testes e geralmente limita as solicitações). Isso permitirá simular vários comportamentos da API que devem direcionar o comportamento do componente como quando nenhum dado foi encontrado ou o caso em que a API gera um erro. Por último, mas não menos importante, as chamadas de rede desacelerarão bastante os testes

<br/>

❌ **Caso contrário:** Um teste médio é executado em não mais do que alguns ms, uma chamada típica da API dura 100ms>, isso torna cada teste ~ 20x mais lento


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: fazendo o esboço ou interceptando chamadas de API
![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React-blue.svg
 "Exemplos com React") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com react-testing-library")
 
```javascript

// unit under test
export default function ProductsList() { 
    const [products, setProducts] = useState(false)

    const fetchProducts = async() => {
      const products = await axios.get('api/products')
      setProducts(products);
    }

    useEffect(() => {
      fetchProducts();
    }, []);

  return products ? <div>{products}</div> : <div data-testid='no-products-message'>No products</div>
}

// test
test('When no products exist, show the appropriate message', () => {
    // Arrange
    nock("api")
            .get(`/products`)
            .reply(404);

    // Act
    const {getByTestId} = render(<ProductsList/>);

    // Assert
    expect(getByTestId('no-products-message')).toBeTruthy();
});

```

</details>

<br/>

## ⚪ ️ 3.7 Tenha muito poucos testes de ponta a ponta que abrangem todo o sistema

:white_check_mark: **Faça:** Embora o E2E (ponta a ponta) geralmente signifique testes apenas da interface do usuário com um navegador real (consulte o item 3.6), para outros, eles significam testes que abrangem todo o sistema, incluindo o backend real. O último tipo de teste é altamente valioso, pois cobre erros de integração entre frontend e backend que podem ocorrer devido a um entendimento incorreto do esquema de troca. Eles também são um método eficiente para descobrir problemas de integração de backend para backend (por exemplo, o microsserviço A envia a mensagem errada para o microsserviço B) e até mesmo para detectar falhas de implantação - não há estruturas de backend para testes E2E que sejam tão amigáveis ​​e maduras quanto as estruturas de interface do usuário, como [Cypress](https://www.cypress.io/) e [Pupeteer](https://github.com/GoogleChrome/puppeteer). A desvantagem de tais testes é o alto custo de configuração de um ambiente com tantos componentes e principalmente sua fragilidade - com 50 microsserviços, mesmo se um falhar, todo o E2E falhou. Por esse motivo, devemos usar essa técnica com moderação e provavelmente ter de 1 a 10 desses e não mais. Dito isto, mesmo um pequeno número de testes E2E provavelmente capturará o tipo de problemas para os quais eles são direcionados - falhas de implantação e integração. É aconselhável executá-las em um ambiente de preparação semelhante à produção

<br/>

❌ **Caso contrário:** A interface do usuário pode investir muito em testar sua funcionalidade apenas para perceber muito tarde que a carga útil retornada pelo backend (o esquema de dados com o qual a interface do usuário precisa trabalhar) é muito diferente do esperado

<br/>

## ⚪ ️ 3.8 Acelere os testes do E2E reutilizando credenciais de login

:white_check_mark: **Faça:** Nos testes E2E que envolvem um back-end real e dependem de um token de usuário válido para chamadas de API, não vale a pena isolar o teste para um nível em que um usuário é criado e conectado a cada solicitação. Em vez disso, efetue login apenas uma vez antes do início da execução dos testes (ou seja, antes de tudo), salve o token em algum armazenamento local e reutilize-o nas solicitações. Isso parece violar um dos principais princípios de teste - mantenha o teste autônomo sem acoplamento de recursos. Embora essa seja uma preocupação válida, nos testes E2E o desempenho é uma preocupação importante e a criação de 1-3 solicitações de API antes de iniciar cada teste individual pode levar a um tempo de execução horrível. Reutilizar credenciais não significa que os testes precisam agir nos mesmos registros do usuário - se depender de registros do usuário (por exemplo, histórico de pagamentos do usuário do teste), certifique-se de gerar esses registros como parte do teste e evitar compartilhar sua existência com outros testes. Lembre-se também de que o backend pode ser falsificado - se seus testes estiverem focados no frontend, pode ser melhor isolá-lo e esboçar a API de backend (consulte o item 3.6).

<br/>

❌ **Caso contrário:** Dado 200 casos de teste e assumindo login=100ms = 20 segundos apenas para efetuar login novamente e novamente

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Fazer login antes de todos e não antes de cada

![](https://img.shields.io/badge/🔨%20Exaeplo%20usando%20Cypress-blue.svg
 "Usando Cypress para ilustrar a idea")

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

## ⚪ ️ 3.9 Faça um teste de fumaça E2E que viaja pelo mapa do site

:white_check_mark: **Faça:** Para monitoramento de produção e verificação de integridade do tempo de desenvolvimento, execute um único teste E2E que visite todas/a maioria das páginas do site e garanta que nenhuma quebre. Esse tipo de teste traz um ótimo retorno do investimento, pois é muito fácil de escrever e manter, mas pode detectar qualquer tipo de falha, incluindo problemas funcionais, de rede e de implantação. Outros estilos de verificação de fumaça e sanidade não são tão confiáveis ​​e exaustivos - algumas equipes de operações apenas fazem ping na página inicial (produção) ou desenvolvedores que executam muitos testes de integração os quais não descobrem problemas de empacotamento e de navegador. Nem precisa dizer que o teste de fumaça não substitui os testes funcionais, apenas visa servir como um detector de fumaça rápido

<br/>

❌ **Caso contrário:** Tudo pode parecer perfeito, todos os testes são aprovados, a verificação de integridade da produção também é positiva, mas o componente Payment teve algum problema de embalagem e apenas a rota /Payment não está sendo processada


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Fumaça viajando por todas as páginas
![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg
 "Using Cypress to illustrate the idea")
```javascript
it('When doing smoke testing over all page, should load them all successfully', () => {
    // exemplified using Cypress but can be implemented easily
    // using any E2E suite
    cy.visit('https://mysite.com/home');
    cy.contains('Home');
    cy.contains('https://mysite.com/Login');
    cy.contains('Login');
    cy.contains('https://mysite.com/About');
    cy.contains('About');
  })
```

</details>


<br/>

## ⚪ ️ 3.10 Expor os testes como um documento colaborativo vivo

:white_check_mark: **Faça:** Além de aumentar a confiabilidade do aplicativo, os testes trazem outra oportunidade atraente para a mesa - servem como documentação viva do aplicativo. Como os testes falam inerentemente em uma linguagem menos técnica e de produto/UX, usando as ferramentas certas, eles podem servir como um artefato de comunicação que alinha muito os colegas - desenvolvedores e seus clientes. Por exemplo, algumas estruturas permitem expressar o fluxo e as expectativas (ou seja, plano de testes) usando uma linguagem legível por humanos, para que qualquer parte interessada, incluindo gerentes de produto, possa ler, aprovar e colaborar nos testes que acabaram de se tornar o documento de requisitos dinâmicos. Essa técnica também está sendo chamada de 'teste de aceitação', pois permite ao cliente definir seus critérios de aceitação em linguagem simples. Isso é [BDD (teste orientado ao comportamento)](https://en.wikipedia.org/wiki/Behavior-driven_development) na sua forma mais pura. Um dos frameworks populares que permitem isso é [Cucumber que tem um sabor de JavaScript](https://github.com/cucumber/cucumber-js), veja o exemplo abaixo. Outra oportunidade semelhante, porém diferente, [StoryBook](https://storybook.js.org/), permite expor componentes da interface do usuário como um catálogo gráfico, onde é possível percorrer os vários estados de cada componente (por exemplo. renderizar uma grid sem filtros, renderizar essa grid com várias linhas ou sem nenhuma, etc.), ver como ele se parece e como acionar esse estado - isso também pode atrair as pessoas do produto, mas serve principalmente como documento ativo para desenvolvedores que consomem esses componentes.

❌ **Otherwise:** Depois de investir muitos recursos em testes, é uma pena não alavancar esse investimento e obter grande valor


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Descrevendo testes em linguagem humana usando cucumber-js

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Cocumber-blue.svg  "Exemplos usando Cucumber")
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

### :clap: Exemplo Fazendo Certo: Visualizando nossos componentes, seus vários estados e entradas usando o Storybook
![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Usando StoryBook")


</details>




## ⚪ ️ 3.11 Detecte problemas visuais com ferramentas automatizadas


:white_check_mark: **Faça:** Configure ferramentas automatizadas para capturar a tela da interface do usuário quando alterações forem apresentadas e detectar problemas visuais, como sobreposição ou quebra de conteúdo. Isso garante que não apenas os dados corretos sejam preparados, mas também que o usuário possa vê-los convenientemente. Essa técnica não é amplamente adotada, nossa mentalidade de teste se inclina para testes funcionais, mas é o visual que o usuário experimenta e, com tantos tipos de dispositivos, é muito fácil ignorar alguns erros desagradáveis ​​da interface do usuário. Algumas ferramentas gratuitas podem fornecer o básico - gerar e salvar capturas de tela para a inspeção dos olhos humanos. Embora essa abordagem possa ser suficiente para aplicativos pequenos, ela é falha como qualquer outro teste manual que exige mão de obra humana sempre que algo muda. Por outro lado, é bastante desafiador detectar problemas de interface do usuário automaticamente devido à falta de definição clara - é aqui que o campo de 'Regressão Visual' entra em cena e resolve esse quebra-cabeça comparando a interface antiga com as alterações mais recentes e detectando diferenças. Algumas ferramentas OSS/gratuitas podem fornecer algumas dessas funcionalidades (por exemplo, [wraith](https://github.com/BBC-News/wraith), [PhantomCSS]([https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)) mas pode cobrar um tempo significativo de configuração. A linha comercial de ferramentas (por exemplo [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) dá um passo adiante ao suavizar a instalação e incluir recursos avançados, como interface de gerenciamento, alerta, captura inteligente, eliminando o 'ruído visual' (por exemplo, anúncios, animações) e até mesmo a análise de causa raiz das alterações no DOM/css que levaram ao problema

<br/>

❌ **Caso contrário:** Quão boa é uma página de conteúdo que exibe ótimo conteúdo (100% nos testes aprovados), carrega instantaneamente, mas metade da área de conteúdo está oculta?


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Uma regressão visual típica - conteúdo correto que é mal servido

![alt text](assets/amazon-visual-regression.jpeg "Quebras de página na Amazon")

<br/>


### :clap: Exemplo Fazendo Certo: Configurando o wraith para capturar e comparar instantâneos da UI

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Wraith-blue.svg
 "Usando Cypress para ilustrar a idea")

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

### :clap: Exemplo Fazendo Certo: Usando Applitools para obter comparação de captura instantânea e outros recursos avançados

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20AppliTools-blue.svg
 "Usando Cypress to para ilustrar a idea") ![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Cypress-blue.svg
 "Usando Cypress para illustrar idea")

```javascript
import  *  as todoPage from  '../page-objects/todo-page';

describe('visual validation',  ()  =>  {

before(()  =>  todoPage.navigate());

beforeEach(()  =>  cy.eyesOpen({ appName:  'TAU TodoMVC'  }));

afterEach(()  =>  cy.eyesClose());

  

it('should look good',  ()  =>  {

cy.eyesCheckWindow('empty todo list');

  

todoPage.addTodo('Clean room');

  

todoPage.addTodo('Learn javascript');

  

cy.eyesCheckWindow('two todos');

  

todoPage.toggleTodo(0);

  

cy.eyesCheckWindow('mark as completed');

});

});
```




</details>



<br/><br/>

  
# Section 4️⃣: Measuring Test Effectiveness

<br/><br/>

## ⚪ ️ 4.1 Get enough coverage for being confident, ~80% seems to be the lucky number

:white_check_mark: **Do:** The purpose of testing is to get enough confidence for moving fast, obviously the more code is tested the more confident the team can be. Coverage is a measure of how many code lines (and branches, statements, etc) are being reached by the tests. So how much is enough? 10–30% is obviously too low to get any sense about the build correctness, on the other side 100% is very expensive and might shift your focus from the critical paths to the exotic corners of the code. The long answer is that it depends on many factors like the type of application — if you’re building the next generation of Airbus A380 than 100% is a must, for a cartoon pictures website 50% might be too much. Although most of the testing enthusiasts claim that the right coverage threshold is contextual, most of them also mention the number 80% as a thumb of a rule ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) that presumably should satisfy most of the applications.

Implementation tips: You may want to configure your continuous integration (CI) to have a coverage threshold ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) and stop a build that doesn’t stand to this standard (it’s also possible to configure threshold per component, see code example below). On top of this, consider detecting build coverage decrease (when a newly committed code has less coverage) — this will push developers raising or at least preserving the amount of tested code. All that said, coverage is only one measure, a quantitative based one, that is not enough to tell the robustness of your testing. And it can also be fooled as illustrated in the next bullets

<br/>


❌ **Otherwise:**  Confidence and numbers go hand in hand, without really knowing that you tested most of the system — there will also be some fear. and fear will slow you down


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: A typical coverage report
![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Doing It Right Example: Setting up coverage per component (using Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg
 "Using Cypress to illustrate the idea")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)

</details>



<br/><br/>

## ⚪ ️ 4.2 Inspect coverage reports to detect untested areas and other oddities

:white_check_mark: **Do:** Some issues sneak just under the radar and are really hard to find using traditional tools. These are not really bugs but more of surprising application behavior that might have a severe impact. For example, often some code areas are never or rarely being invoked — you thought that the ‘PricingCalculator’ class is always setting the product price but it turns out it is actually never invoked although we have 10000 products in DB and many sales… Code coverage reports help you realize whether the application behaves the way you believe it does. Other than that, it can also highlight which types of code is not tested — being informed that 80% of the code is tested doesn’t tell whether the critical parts are covered. Generating reports is easy — just run your app in production or during testing with coverage tracking and then see colorful reports that highlight how frequent each code area is invoked. If you take your time to glimpse into this data — you might find some gotchas
<br/>


❌ **Otherwise:** If you don’t know which parts of your code are left un-tested, you don’t know where the issues might come from


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: What’s wrong with this coverage report? based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report? based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

</details>


<br/><br/>

## ⚪ ️ 4.3 Measure logical coverage using mutation testing

:white_check_mark: **Do:**  The Traditional Coverage metric often lies: It may show you 100% code coverage, but none of your functions, even not one, return the right response. How come? it simply measures over which lines of code the test visited, but it doesn’t check if the tests actually tested anything — asserted for the right response. Like someone who’s traveling for business and showing his passport stamps — this doesn’t prove any work done, only that he visited few airports and hotels.

Mutation-based testing is here to help by measuring the amount of code that was actually TESTED not just VISITED. [Stryker](https://stryker-mutator.io/) is a JavaScript library for mutation testing and the implementation is really neat:

(1) it intentionally changes the code and “plants bugs”. For example the code newOrder.price===0 becomes newOrder.price!=0. This “bugs” are called mutations

(2) it runs the tests, if all succeed then we have a problem — the tests didn’t serve their purpose of discovering bugs, the mutations are so-called survived. If the tests failed, then great, the mutations were killed.

Knowing that all or most of the mutations were killed gives much higher confidence than traditional coverage and the setup time is similar
<br/>


❌ **Otherwise:** You’ll be fooled to believe that 85% coverage means your test will detect bugs in 85% of your code

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: 100% coverage, 0% testing

![](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg
 "Using Cypress to illustrate the idea")
```javascript
function addNewOrder(newOrder) {
    logger.log(`Adding new order ${newOrder}`);
    DB.save(newOrder);
    Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

    return {approved: true};
}

it("Test addNewOrder, don't use such test names", () => {
    addNewOrder({asignee: "John@mailer.com",price: 120});
});//Triggers 100% code coverage, but it doesn't check anything

```
<br/>

### :clap: Doing It Right Example: Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>



<br/><br/>

## ⚪ ️4.4 Preventing test code issues with Test linters

:white_check_mark: **Do:**  A set of ESLint plugins were built specifically for inspecting the tests code patterns and discover issues. For example, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) will warn when a test is written at the global level (not a son of a describe() statement) or when tests are [skipped](https://mochajs.org/#inclusive-tests) which might lead to a false belief that all tests are passing. Similarly, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) can, for example, warn when a test has no assertions at all (not checking anything)

<br/>


❌ **Otherwise:** Seeing 90% code coverage and 100% green tests will make your face wear a big smile only until you realize that many tests aren’t asserting for anything and many test suites were just skipped. Hopefully, you didn’t deploy anything based on this false observation


<br/>
<details><summary>✏ <b>Code Examples</b></summary>

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

  
# Section 5️⃣: CI and Other Quality Measures

<br/><br/>

## ⚪ ️ 5.1 Enrich your linters and abort builds that have linting issues

:white_check_mark: **Do:**  Linters are a free lunch, with 5 min setup you get for free an auto-pilot guarding your code and catching significant issue as you type. Gone are the days where linting was about cosmetics (no semi-colons!). Nowadays, Linters can catch severe issues like errors that are not thrown correctly and losing information. On top of your basic set of rules (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), consider including some specializing Linters like [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) that can discover tests without assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) can discover promises with no resolve (your code will never continue), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) which can discover eager regex expressions that might get used for DOS attacks, and [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) is capable of alarming when the code uses utility library methods that are part of the V8 core methods like Lodash._map(…)
<br/>


❌ **Otherwise:** Consider a rainy day where your production keeps crashing but the logs don’t display the error stack trace. What happened? Your code mistakenly threw a non-error object and the stack trace was lost, a good reason for banging your head against a brick wall. A 5min linter setup could detect this TYPO and save your day


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti Pattern Example: The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug
![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>




<br/><br/>

# ⚪ ️ 5.2 Shorten the feedback loop with local developer-CI

:white_check_mark: **Do:**   Using a CI with shiny quality inspections like testing, linting, vulnerabilities check, etc? Help developers run this pipeline also locally to solicit instant feedback and shorten the [feedback loop](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Why? an efficient testing process constitutes many and iterative loops: (1) try-outs -> (2) feedback -> (3) refactor. The faster the feedback is, the more improvement iterations a developer can perform per-module and perfect the results. On the flip, when the feedback is late to come fewer improvement iterations could be packed into a single day, the team might already move forward to another topic/task/module and might not be up for refining that module.

Practically, some CI vendors (Example: [CircleCI load CLI](https://circleci.com/docs/2.0/local-cli/)) allow running the pipeline locally. Some commercial tools like [wallaby provide highly-valuable & testing insights](https://wallabyjs.com/) as a developer prototype (no affiliation). Alternatively, you may just add npm script to package.json that runs all the quality commands (e.g. test, lint, vulnerabilities) — use tools like [concurrently](https://www.npmjs.com/package/concurrently) for parallelization and non-zero exit code if one of the tools failed. Now the developer should just invoke one command — e.g. ‘npm run quality’ — to get instant feedback. Consider also aborting a commit if the quality check failed using a githook ([husky can help](https://github.com/typicode/husky))
<br/>


❌ **Otherwise:** When the quality results arrive the day after the code, testing doesn’t become a fluent part of development rather an after the fact formal artifact


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap:  Doing It Right Example: npm scripts that perform code quality inspection, all are run in parallel on demand or when a developer is trying to push new code
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

# ⚪ ️5.3 Perform e2e testing over a true production-mirror

:white_check_mark: **Do:**   End to end (e2e) testing are the main challenge of every CI pipeline — creating an identical ephemeral production mirror on the fly with all the related cloud services can be tedious and expensive. Finding the best compromise is your game: [Docker-compose](https://serverless.com/) allows crafting isolated dockerized environment with identical containers using a single plain text file but the backing technology (e.g. networking, deployment model) is different from real-world productions. You may combine it with [‘AWS Local’](https://github.com/localstack/localstack) to work with a stub of the real AWS services. If you went [serverless](https://serverless.com/) multiple frameworks like serverless and [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) allows the local invocation of Faas code.

The huge Kubernetes eco-system is yet to formalize a standard convenient tool for local and CI-mirroring though many new tools are launched frequently. One approach is running a ‘minimized-Kubernetes’ using tools like [Minikube](https://kubernetes.io/docs/setup/minikube/) and [MicroK8s](https://microk8s.io/) which resemble the real thing only come with less overhead. Another approach is testing over a remote ‘real-Kubernetes’, some CI providers (e.g. [Codefresh](https://codefresh.io/)) has native integration with Kubernetes environment and make it easy to run the CI pipeline over the real thing, others allow custom scripting against a remote Kubernetes.
<br/>


❌ **Otherwise:** Using different technologies for production and testing demands maintaining two deployment models and keeps the developers and the ops team separated


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap:  Example: a CI pipeline that generates Kubernetes cluster on the fly <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>





<br/><br/>

## ⚪ ️5.4 Parallelize test execution
:white_check_mark: **Do:**    When done right, testing is your 24/7 friend providing almost instant feedback. In practice, executing 500 CPU-bounded unit test on a single thread can take too long. Luckily, modern test runners and CI platforms (like [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) and [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) can parallelize the test into multiple processes and achieve significant improvement in feedback time. Some CI vendors do also parallelize tests across containers (!) which shortens the feedback loop even further. Whether locally over multiple processes, or over some cloud CLI using multiple machines — parallelizing demand keeping the tests autonomous as each might run on different processes


❌ **Otherwise:** Getting test results 1 hour long after pushing new code, as you already code the next features, is a great recipe for making testing less relevant


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))
![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>




<br/><br/>

## ⚪ ️5.5 Stay away from legal issues using license and plagiarism check
:white_check_mark: **Do:**    Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like [license check](https://www.npmjs.com/package/license-checker) and [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stackoverflow and apparently violates some copyrights

❌ **Otherwise:** Unintentionally, developers might use packages with inappropriate licenses or copy paste commercial code and run into legal issues


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example:
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
:white_check_mark: **Do:**    Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like license check and plagiarism check (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stackoverflow and apparently violates some copyrights
<br/>


❌ **Otherwise:** Even the most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community tools such as [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), or commercial tools like [snyk](https://snyk.io/) (offer also a free community version). Both can be invoked from your CI on every build


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: NPM Audit result
![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>




<br/><br/>

## ⚪ ️5.7 Automate dependency updates
:white_check_mark: **Do:**   Yarn and npm latest introduction of package-lock.json introduced a serious challenge (the road to hell is paved with good intentions) — by default now, packages are no longer getting updates. Even a team running many fresh deployments with ‘npm install’ & ‘npm update’ won’t get any new updates. This leads to subpar dependent packages versions at best or to vulnerable code at worst. Teams now rely on developers goodwill and memory to manually update the package.json or use tools [like ncu](https://www.npmjs.com/package/npm-check-updates) manually. A more reliable way could be to automate the process of getting the most reliable dependency versions, though there are no silver bullet solutions yet there are two possible automation roads:

(1) CI can fail builds that have obsolete dependencies — using tools like [‘npm outdated’](https://docs.npmjs.com/cli/outdated) or ‘npm-check-updates (ncu)’ . Doing so will enforce developers to update dependencies.

(2) Use commercial tools that scan the code and automatically send pull requests with updated dependencies. One interesting question remaining is what should be the dependency update policy — updating on every patch generates too many overhead, updating right when a major is released might point to an unstable version (many packages found vulnerable on the very first days after being released, [see the](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope incident).

An efficient update policy may allow some ‘vesting period’ — let the code lag behind the @latest for some time and versions before considering the local copy as obsolete (e.g. local version is 1.3.1 and repository version is 1.3.8)
<br/>


❌ **Otherwise:** Your production will run packages that have been explicitly tagged by their author as risky


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap:  Example: [ncu](https://www.npmjs.com/package/npm-check-updates) can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions
![alt text](assets/bp-27-yoni-goldberg-npm.png "Nncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")


</details>


<br/><br/>

## ⚪ ️ 5.8 Other, non-Node related, CI tips
:white_check_mark: **Do:**    This post is focused on testing advice that is related to, or at least can be exemplified with Node JS. This bullet, however, groups few non-Node related tips that are well-known

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use a declarative syntax. This is the only option for most vendors but older versions of Jenkins allows using code or UI</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opt for a vendor that has native Docker support</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Fail early, run your fastest tests first. Create a ‘Smoke testing’ step/milestone that groups multiple fast inspections (e.g. linting, unit tests) and provide snappy feedback to the code committer</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Make it easy to skim-through all build artifacts including test reports, coverage reports, mutation reports, logs, etc</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Create multiple pipelines/jobs for each event, reuse steps between them. For example, configure a job for feature branch commits and a different one for master PR. Let each reuse logic using shared steps (most vendors provide some mechanism for code reuse</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Never embed secrets in a job declaration, grab them from a secret store or from the job’s configuration</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Explicitly bump version in a release build or at least ensure the developer did so</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Build only once and perform all the inspections over the single build artifact (e.g. Docker image)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Test in an ephemeral environment that doesn’t drift state between builds. Caching node_modules might be the only exception</li></ol>
<br/>


❌ **Otherwise:** You‘ll miss years of wisdom

<br/><br/>

## ⚪ ️ 5.9 Build matrix: Run the same CI steps using multiple Node versions
:white_check_mark: **Do:** Quality checking is about serendipity, the more ground you cover the luckier you get in detecting issues early. When developing reusable packages or running a multi-customer production with various configuration and Node versions, the CI must run the pipeline of tests over all the permutations of configurations. For example, assuming we use MySQL for some customers and Postgres for others — some CI vendors support a feature called ‘Matrix’ which allow running the suit of testing against all permutations of MySQL, Postgres and multiple Node version like 8, 9 and 10. This is done using configuration only without any additional effort (assuming you have testing or any other quality checks). Other CIs who doesn’t support Matrix might have extensions or tweaks to allow that
<br/>


❌ **Otherwise:** So after doing all that hard work of writing testing are we going to let bugs sneak in only because of configuration issues?


<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap:   Example: Using Travis (CI vendor) build definition to run the same test over multiple Node versions
<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# Team



## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Role:** Writer

**About:** I'm an independent consultant who works with 500 fortune corporates and garage startups on polishing their JS & Node.js applications. More than any other topic I'm fascinated by and aims to master the art of testing. I'm also the author of [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

<br/>

**Workshop:** 👨‍🏫 Want to learn all these practices and techniques at your offices (Europe & USA)? [Register here for my testing workshop](https://testjavascript.com/)
<br/>

**Follow:**

* [🐦 Twitter](https://twitter.com/goldbergyoni/)
* [📞 Contact](https://testjavascript.com/contact-2/)
* [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>


##  [Bruno Scheufler](https://github.com/BrunoScheufler)

**Role:** Tech reviewer and advisor

Took care to revise, improve, lint and polish all the texts 

**About:** full-stack web engineer, Node.js & GraphQL enthusiast
<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Role:** Concept, design and great advice

**About:** A savvy frontend developer, CSS expert and emojis freak
