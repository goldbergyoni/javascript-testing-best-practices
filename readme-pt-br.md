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

<br/>

### Traduções - leia em seu próprio idioma
* 🇨🇳[Chinese](readme-zh-CN.md) - cortesia de [Yves yao](https://github.com/yvesyao)
* 🇰🇷[Korean](readme.kr.md) - cortesia de [Rain Byun](https://github.com/ragubyun)
* Deseja traduzir para o seu próprio idioma? abra uma issue 💜


<br/><br/>

## `Índice`

#### [`Seção 0: A Regra de ouro`](#seção-0️⃣-a-regra-de-ouro)

Um único conselho que inspira todos os outros (1 tópico especial)

#### [`Seção 1: A Anatomia do Teste`](#seção-1-a-anatomia-do-teste)

A fundação - estruturando testes limpos (12 tópicos)

#### [`Seção 2: Teste de Backend`](#seção-2️⃣-teste-de-backend)

Escrevendo testes de back-end e microsserviços com eficiência (8 tópicos)

#### [`Seção 3: Teste de Frontend`](#seção-3️⃣-teste-de-frontend)

Escrevendo testes para interface do usuário da web, incluindo testes de componentes e E2E (11 tópicos)

#### [`Seção 4: Medindo a Eficácia dos Testes`](#seção-4️⃣-medindo-a-eficácia-dos-testes)

Observando o vigia - medindo a qualidade do teste (4 tópicos)

#### [`Seção 5: Integração Contínua`](#section-5️⃣-ci-and-other-quality-measures)

Diretrizes para CI no mundo JS (9 tópicos)


<br/><br/>


# Seção 0️⃣: A Regra de Ouro

<br/>

## ⚪️ 0 A Regra de Ouro: Design para testes enxutos

:white_check_mark: **Faça:**
O código de teste não é como o código de produção - projete-o para ser simples, curto, sem abstrações, plano, agradável de se trabalhar, enxuto. Deve-se olhar para um teste e obter a intenção instantaneamente.

Nossas mentes estão cheias com o código principal de produção, não temos 'espaço de sobra' para complexidade adicional. Se tentarmos espremer outro código desafiador em nosso cérebro fraco, a equipe ficará mais lenta, o que vai de encontro com a razão pela qual fazemos os testes. Na prática é aqui que muitas equipes abandonam os testes.

Os testes são uma oportunidade para outra coisa - um assistente amigável e sorridente, que é agradável de trabalhar e oferece grande valor para um investimento tão pequeno. A ciência diz que temos dois sistemas cerebrais: o sistema 1, usado para atividades sem esforço, como dirigir um carro em uma estrada vazia, e o sistema 2, destinado a operações complexas e conscientes, como resolver uma equação matemática. Projete seu teste para o sistema 1, ao analisar o código de teste, ele deve parecer tão fácil quanto modificar um documento HTML e não como resolver um equação 2X (17 × 24).

Isso pode ser alcançado através de técnicas, ferramentas e alvos de teste selecionados de forma econômica, que são econômicos e proporcionam um ótimo ROI. Teste apenas o necessário, esforce-se para mantê-lo ágil, às vezes vale a pena abandonar alguns testes e trocar a confiabilidade por agilidade e simplicidade.

![alt text](/assets/headspace.png "Não temos espaço para complexidade adicional")
 
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

**👇 Nota:** Cada tópico possui exemplos de código e alguns tem ilustrações. Clique para expandir
<details><summary>✏ <b>Códigos de Exemplo</b></summary>
  
<br/>
  
### :clap: Exemplo Fazendo Certo: um nome de teste que constitui 3 partes

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Mocha-blue.svg
 "Usando o Mocha para ilustrar a ideia")

```javascript
//1. unidade em teste
describe('Products Service', function() {
  describe('Add new product', function() {
    //2. cenário e 3. expectativa
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});

```
<br/>

### :clap: Exemplo Fazendo Certo: um nome de teste que constitui 3 partes
![alt text](/assets/bp-1-3-parts.jpeg "Um nome de teste que constitui 3 partes")

</details>

<br/><br/>

## ⚪ ️ 1.2 Testes de estrutura pelo padrão em inglês AAA

:white_check_mark: **Faça:** Estruture seus testes com 3 seções bem separadas: Ajeitar, Atuar e Afirmar (AAA). Seguir essa estrutura garante que o leitor não gaste CPU do cérebro na compreensão do plano de teste:

1st A - Ajeitar: todo o código de configuração para levar o sistema ao cenário que o teste pretende simular. Isso pode incluir instanciar a unidade sob o construtor de teste, adicionar registros de banco de dados, mockar/stubbing de objetos e qualquer outro código de preparação

2nd A - Atuar: Execute teste em unidade. Geralmente 1 linha de código

3rd A - Afirmar: Garanta que o valor recebido satisfaça a expectativa. Geralmente 1 linha de código


<br/>


❌ **Caso contrário:** Você não gasta apenas longas horas diárias para entender o código principal, agora também o que deveria ter sido a parte simples do dia (teste) estica seu cérebro

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Um teste estruturado com o padrão AAA

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com Jest") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Examples com Mocha")
  
```javascript
describe('Customer classifier', () => {
    test('When customer spent more than 500$, should be classified as premium', () => {
        //Ajeitar
        const customerToClassify = {spent:505, joined: new Date(), id:1}
        const DBStub = sinon.stub(dataAccess, "getCustomer")
            .reply({id:1, classification: 'regular'});

        //Atuar
        const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);

        //Afirmar
        expect(receivedClassification).toMatch('premium');
    });
});
```

<br/>

### :thumbsdown: Exemplo Anti-padrão: Sem separação, um grande volume, mais difícil de interpretar

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




## ⚪ ️1.3 Descrever expectativas em um idioma do produto: use afirmações no estilo BDD

:white_check_mark: **Faça:** Codificar seus testes em um estilo declarativo permite que o leitor entenda instantaneamente, sem gastar nem um único ciclo de CPU do cérebro. Quando você escreve um código imperativo, repleto de lógica condicional, o leitor entra em um estado mental de esforço. Nesse sentido, codifique a expectativa em uma linguagem humana, estilo declarativo de BDD usando expect ou should e não usando código personalizado. Se Chai e Jest não incluem a afirmação desejada e são altamente repetíveis, considere [estender o Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) ou escrever um [plugin Chai personalizado](https://www.chaijs.com/guide/plugins/)
<br/>


❌ **Caso Contrário:** A equipe escreverá menos testes e decorará os irritantes com .skip()

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos com Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com Jest")
  
  ### :thumbsdown: Exemplo Anti-padrão: O leitor deve percorrer códigos não tão curtos e imperativos apenas para chegar a história do teste

```javascript
test("When asking for an admin, ensure only ordered admins in results" , () => {
    //supondo que adicionamos aqui dois administradores "admin1", "admin2" e "user1"
    const allAdmins = getUsers({adminOnly:true});

    let admin1Found, adming2Found = false;

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

### :clap: Exemplo Fazendo Certo: Percorrer o teste declarativo a seguir é fácil


```javascript
it("When asking for an admin, ensure only ordered admins in results" , () => {
    //supondo que adicionamos aqui dois administradores
    const allAdmins = getUsers({adminOnly:true});

    expect(allAdmins).to.include.ordered.members(["admin1" , "admin2"])
  .but.not.include.ordered.members(["user1"]);
});

```

</details>


<br/><br/>


## ⚪ ️  1.4 Atenha-se ao teste de caixa preta: teste apenas métodos públicos

:white_check_mark: **Faça:** Testar os componentes internos gera uma enorme sobrecarga por quase nada. Se o seu código/API fornecer os resultados certos, você deve realmente investir suas próximas 3 horas em testes de COMO funcionou internamente e depois manter esses testes frágeis? Sempre que um comportamento público é verificado, a implementação privada também é implicitamente testada e seus testes serão interrompidos apenas se houver um determinado problema (por exemplo, saída incorreta). Essa abordagem também é chamada de teste comportamental. Por outro lado, se você testar os componentes internos (abordagem de caixa branca) — seu foco muda do planejamento do resultado do componente para detalhes minuciosos e seu teste pode ser interrompido devido a pequenas refatorações de código, embora os resultados sejam bons- isso aumenta drasticamente a carga de manutenção
<br/>


❌ **Caso Contrário:** Seu teste se comporta como [O Pastor Mentiroso e o Lobo](https://pt.wikipedia.org/wiki/O_Pastor_Mentiroso_e_o_Lobo): gera falsos positivos (por exemplo, um teste falha porque um nome de variável privada foi alterado). Sem surpresa, as pessoas logo começarão a ignorar as notificações de IC até que um dia um bug real seja ignorado…

<br/>
<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Um caso de teste está testando os internos sem um bom motivo
![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos com Mocha & Chai")
```javascript
class ProductService{
  //esse método é usado apenas internamente
  //Alterar este nome fará com que os testes falhem
  calculateVATAdd(priceWithoutVAT){
    return {finalPrice: priceWithoutVAT * 1.2};
    //Alterar o formato do resultado ou o nome da chave acima fará com que os testes falhem
  }
  //método público
  getPrice(productId){
    const desiredProduct= DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
    return finalPrice;
  }
}


it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
    //Não é necessário permitir que os usuários calculem o VAT, apenas mostrem o preço final. No entanto, insistimos aqui falsamente para testar os internos da classe
    expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});

```

</details>




<br/><br/>

## ⚪ ️ ️1.5 Escolha os dublês de teste certos: evite mocks a favor de stubs e spies

:white_check_mark: **Faça:**  Os dublês de teste são um mal necessário, porque são acoplados às aplicações internas, no entanto, alguns fornecem um imenso valor (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Leia aqui um lembrete sobre dublês de teste: mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Antes de usar dublês de teste, faça uma pergunta muito simples: Eu o uso para testar funcionalidades que aparecem ou podem aparecer no documento de requisitos? Se não, isso cheira a teste de caixa branca.

Por exemplo, se você quiser testar se seu aplicativo se comporta razoavelmente quando o serviço de pagamento estiver inativo, você pode desconsiderar (stub) o serviço de pagamento e acionar um retorno ‘No Response’ para garantir que a unidade em teste retorne o valor correto. Isso verifica o comportamento/resposta/resultado do aplicativo em certos cenários. Você também pode usar um spy para afirmar que um email foi enviado quando esse serviço está inoperante — isso é novamente uma verificação comportamental que provavelmente aparecerá em um documento de requisitos (“Envie um email se o pagamento não puder ser salvo”). Por outro lado, se você criar um mock do serviço de pagamento e garantir que ele foi chamado com os tipos de JavaScript certos— então seu teste será focado em itens internos que não tem nada a ver com a funcionalidade do aplicativo e provavelmente mudarão frequentemente
<br/>


❌ **Caso Contrário:** Qualquer refatoração de código exige a pesquisa de todas as simulações no código e a atualização em conformidade. Os testes se tornam um fardo e não um amigo útil

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Mocks foca nos internos
![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Sinon-blue.svg
 "Exemplo com Sinon")
```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
    //Suponha que já adicionamos um produto
    const dataAccessMock = sinon.mock(DAL);
    //hmmm RUIM: testar os internos é realmente nosso principal objetivo aqui, não apenas um efeito colateral
    dataAccessMock.expects("deleteProduct").once().withArgs(DBConfig, theProductWeJustAdded, true, false);
    new ProductService().deletePrice(theProductWeJustAdded);
    dataAccessMock.verify();
});
```
<br/>

### :clap: Exemplo Fazendo Certo: spies concentram-se em testar os requisitos, mas como efeito colateral inevitavelmente tocam os internos

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
    //Suponha que já adicionamos aqui um produto
    const spy = sinon.spy(Emailer.prototype, "sendEmail");
    new ProductService().deletePrice(theProductWeJustAdded);
    //hmmm OK: lidamos com internos? Sim, mas como efeito colateral do teste dos requisitos (envio de um email)
    expect(spy.calledOnce).to.be.true;
});
```

</details>



<br/><br/>

## ⚪ ️1.6 Não use “foo”, use dados de entrada realistas

:white_check_mark: **Faça:**  Muitas vezes, os bugs de produção são revelados com informações muito específicas e surpreendentes— quanto mais realista for a entrada de teste, maiores serão as chances de detectar bugs mais cedo. Use bibliotecas dedicadas como [Faker](https://www.npmjs.com/package/faker) gerar dados pseudo-reais que se assemelham à variedade e forma dos dados de produção. Por exemplo, essas bibliotecas podem gerar números de telefone, nomes de usuários, cartões de crédito, nomes de empresas e até mesmo textos 'lorem ipsum' realistas. Você também pode criar alguns testes (além dos testes de unidade) que randomizam os dados dos fakers para esticar sua unidade sob teste ou até importar dados reais do seu ambiente de produção. Quer elevar para o próximo nível? Veja o próximo tópico (teste baseado em propriedades).
<br/>


❌ **Caso Contrário:** Todos os seus testes de desenvolvimento parecerão falsamente verdes quando você usar entradas sintéticas como “Foo”, mas a produção poderá ficar vermelha quando um hacker passar uma string desagradável como “@ 3e2ddsf. ## '1 fdsfds. fds432 AAAA ”


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Uma suíte de testes aprovada devido a dados não realistas

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com Jest")
 
 
```javascript
const addProduct = (name, price) =>{
  const productNameRegexNoSpace = /^\S*$/;//nenhum espaço em branco permitido

  if(!productNameRegexNoSpace.test(name))
    return false;//esse caminho nunca foi alcançado devido a entradas não realistas

    //alguma lógica aqui
    return true;
};

test("Wrong: When adding new product with valid properties, get successful confirmation", async () => {
    //A string "Foo" usada em todos os testes nunca dispara um resultado falso
    const addProductResult = addProduct("Foo", 5);
    expect(addProductResult).toBe(true);
    //Positivo-falso: a operação foi bem-sucedida porque nunca tentamos com
    //nome de produto longo incluindo espaços
});

```
<br/>

### :clap: Exemplo Fazendo Certo: Randomizando entrada realista
```javascript
it("Better: When adding new valid product, get successful confirmation", async () => {
    const addProductResult = addProduct(faker.commerce.productName(), faker.random.number());
    //Entrada aleatória gerada: {'Sleek Cotton Computer',  85481}
    expect(addProductResult).to.be.true;
    //O teste falhou, a entrada aleatória acionou um caminho que nunca planejamos.
    //Descobrimos um bug cedo!
});
```

</details>




<br/><br/>

## ⚪ ️ 1.7 Teste muitas combinações de entrada usando testes baseados em propriedades

:white_check_mark: **Faça:** Normalmente, escolhemos algumas amostras de entrada para cada teste. Mesmo quando o formato de entrada se assemelha a dados do mundo real (veja o tópico ‘Não use foo’), cobrimos apenas algumas combinações de entrada (method(‘’, true, 1), method(“string” , false” , 0)), No entanto, em produção, uma API chamada com 5 parâmetros pode ser chamada com milhares de permutações diferentes, uma delas pode tornar nosso processo inativo ([consulte Teste do Fuzz](https://pt.wikipedia.org/wiki/Fuzzing)). E se você pudesse escrever um único teste que envie 1000 permutações de entradas diferentes automaticamente e capte para qual entrada nosso código falhou em retornar a resposta correta? O teste baseado em propriedades é uma técnica que faz exatamente isso: ao enviar todas as combinações de entradas possíveis para sua unidade em teste, aumenta a possibilidade de encontrar um bug. Por exemplo, dado um método — addNewProduct(id, name, isDiscount) — as bibliotecas de suporte chamarão esse método com muitas combinações de (number, string, boolean) como (1, “iPhone”, false), (2, “Galaxy”, true). Você pode executar testes baseados em propriedades usando seu test runner favorito (Mocha, Jest, etc) usando bibliotecas como [js-verify](https://github.com/jsverify/jsverify) ou [testcheck](https://github.com/leebyron/testcheck-js) (documentação muito melhor). Atualização: Nicolas Dubien sugere nos comentários abaixo [verificar check-fast](https://github.com/dubzzz/fast-check#readme) que parece oferecer alguns recursos adicionais e também ser mantido ativamente
<br/>


❌ **Caso Contrário:** Inconscientemente, você escolhe as entradas de teste que cobrem apenas os caminhos de código que funcionam bem. Infelizmente, isso diminui a eficiência dos testes como veículo para expor caminhos de bugs que funcionam bem.


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap:  Exemplo Fazendo Certo: Testando muitas permutações de entrada com “fast-check”

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos usando Jest")

```javascript
import fc from "fast-check";

describe("Product service", () => {
  describe("Adding new", () => {
    //isso será executado 100 vezes com diferentes propriedades aleatórias
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

## ⚪ ️ 1.8 Se necessário, use apenas snapshots curtas e em linha

:white_check_mark: **Faça:** Quando houver necessidade de [testes de snapshot](https://jestjs.io/docs/en/snapshot-testing), use apenas snapshots curtas e focadas (ou seja, 3-7 linhas) incluídas como parte do teste ([Snapshot em Linha](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)) e não dentro de arquivos externos. Manter essa diretriz garantirá que seus testes continuem auto-explicativos e menos frágeis.

Por outro lado, os tutoriais e ferramentas de "clássicos de snapshot" incentivam o armazenamento de arquivos grandes (por exemplo. marcação de renderização de componente, resultado JSON da API) em algum meio externo e garantir, sempre que o teste for executado, que seja comparado o resultado recebido com a versão salva. Isso, por exemplo, pode implicitamente associar nosso teste a 1000 linhas com 3000 valores de dados sobre os quais o autor do teste nunca leu e argumentou. Por que isso está errado? Ao fazer isso, existem 1000 razões para o seu teste falhar - basta alterar uma única linha para que a snapshot fique inválida e é provável que isso aconteça muito. Com que frequência? Para cada espaço, comentário ou pequena alteração de CSS/HTML. Não apenas isso, o nome do teste não daria uma pista sobre a falha, pois apenas verifica se 1000 linhas não foram alteradas; também incentiva o redator do teste a aceitar como a verdade desejada um longo documento que ele não pôde inspecionar e verificar. Todos estes são sintomas de teste obscuro e ansioso, que não são focados e têm como objetivo alcançar muito

Vale ressaltar que existem poucos casos em que snapshots longos e externos são aceitáveis - ao afirmar no schema e não nos dados (extrair valores e focar em campos) ou quando o documento recebido raramente muda
<br/>

❌ **Caso Contrário:** Um teste de UI falha. O código parece correto, a tela renderiza pixels perfeitos, o que aconteceu? seu teste de snapshot acabou de encontrar uma diferença do documento de origem para o atual recebido - um único caractere de espaço foi adicionado ao markdown... 

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Acoplando nosso teste a 2000 linhas de código invisíveis

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com Jest")
 
```javascript
it('TestJavaScript.com is renderd correctly', ()  => {

//Ajeitar

//Atuar
const receivedPage = renderer
.create(  <DisplayPage page  =  "http://www.testjavascript.com"  > Test JavaScript < /DisplayPage>)
.toJSON();

//Afirmar
expect(receivedPage).toMatchSnapshot();
//Agora mantemos implicitamente um documento com 2000 linhas
//cada quebra de linha ou comentário adicional - interromperá este teste

});
```
<br/>

### :clap: Exemplo Fazendo Certo: As expectativas são visíveis e focadas
```javascript
it('When visiting TestJavaScript.com home page, a menu is displayed', () => {
//Ajeitar

//Atuar
const receivedPage tree = renderer
.create(  <DisplayPage page  =  "http://www.testjavascript.com"  > Test JavaScript < /DisplayPage>)
.toJSON();

//Afirmar

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

## ⚪ ️1.9 Evite acessórios de teste e sementes globais, adicione dados por teste

:white_check_mark: **Faça:** Seguindo a regra de ouro (tópico 0), cada teste deve adicionar e agir em seu próprio conjunto de linhas de banco de dados para evitar o acoplamento e raciocinar facilmente sobre o fluxo de teste. Na realidade, isso geralmente é violado por testadores que propagam o banco de dados com dados antes de executar os testes ([também conhecido como "acessórios de teste"](https://en.wikipedia.org/wiki/Test_fixture)) por uma questão de melhoria de desempenho. Embora o desempenho seja realmente uma preocupação válida— pode ser mitigado (consulte o tópico "Teste de componentes"), no entanto, a complexidade do teste é uma tarefa muito dolorosa que deve governar outras considerações na maioria das vezes. Na prática, faça com que cada caso de teste inclua explicitamente os registros do banco de dados necessários e atue somente nesses registros. Se o desempenho se tornar uma preocupação crítica — um compromisso equilibrado pode vir na forma de propagação do único conjunto de testes que não está alterando dados (por exemplo, consultas)
<br/>


❌ **Caso Contrário:** Poucos testes falham, uma implantação é abortada, nossa equipe gastará um tempo precioso agora, temos um bug? Vamos investigar, oh não - parece que dois testes estavam modificando os mesmos dados iniciais


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: testes não são independentes e dependem de algum gancho global para alimentar dados globais de banco de dados

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos com Mocha")
 
```javascript
before(() => {
  //adicionando dados de sites e administradores ao nosso banco de dados. Onde estão os dados? lado de fora. Em alguma estrutura json ou de migração externa
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //Eu sei que o nome do site "portal" existe - eu vi nos arquivos de sementes
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //Eu sei que o nome do site "portal" existe - eu vi nos arquivos de sementes
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Falha! O teste anterior altera o nome :[
});

```
<br/>

### :clap: Exemplo Fazendo Certo: Podemos permanecer dentro do teste, cada teste atua em seu próprio conjunto de dados

```javascript
it("When updating site name, get successful confirmation", async () => {
  //teste está adicionando registros novos e atuando apenas nos registros
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });
  
  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");
  
  expect(updateNameResult).to.be(true);
});

```

</details>


<br/>

## ⚪ ️ 1.10 Não pegue erros, espere-os
:white_check_mark: **Faça:**   Ao tentar afirmar que alguma entrada aciona um erro, pode parecer correto usar try-catch-finally e afirmar que a entramos na cláusula catch. O resultado é um caso de teste estranho e detalhado (exemplo abaixo) que oculta a intenção simples do teste e as expectativas do resultado

Uma alternativa mais elegante é o uso da asserção Chai dedicada de uma linha: expect(method).to.throw (ou no Jest: expect(method).toThrow()). É absolutamente obrigatório também garantir que a exceção contenha uma propriedade que indique o tipo de erro; caso contrário, apenas um erro genérico que o aplicativo não poderá fazer muito, em vez de mostrar uma mensagem decepcionante ao usuário
<br/>


❌ **Caso contrário:** Será um desafio deduzir dos relatórios de teste (por exemplo, relatórios de IC) o que deu errado


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Um longo caso de teste que tenta afirmar a existência de erro com try-catch

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos com Mocha")
 
```javascript
it("When no product name, it throws error 400", async() => {
let errorWeExceptFor = null;
try {
  const result = await addNewProduct({});
  } catch (error) {
  expect(error.code).to.equal('InvalidInput');
  errorWeExceptFor = error;
}
expect(errorWeExceptFor).not.to.be.null;
//se essa afirmação falhar, os resultados/relatórios dos testes mostrarão apenas
//que algum valor é null, não haverá uma palavra sobre um erro de ausência
});

```
<br/>

### :clap: Exemplo Fazendo Certo: Uma expectativa legível por humanos que pode ser entendida facilmente, talvez até pelo controle de qualidade ou pelo gerente de produto

```javascript
it.only("When no product name, it throws error 400", async() => {
  await expect(addNewProduct({})).to.eventually.throw(AppError).with.property('code', "InvalidInput");
});

```

</details>




<br/><br/>

## ⚪ ️ 1.11 Marque seus testes

:white_check_mark: **Faça:**  Testes diferentes devem ser executados em diferentes cenários: testes rápidos de fumaça, sem IO, devem ser executados quando um desenvolvedor salva ou dá commit em um arquivo, testes completos de ponta a ponta geralmente são executados quando uma nova pull request é enviada, etc. Isso pode ser alcançado marcando testes com palavras-chave como #cold #api #sanity para que você possa selecionar com sua ferramenta de teste e chamar o subconjunto desejado. Por exemplo, é assim que você invocaria apenas o grupo de teste de sanidade com Mocha: mocha — grep ‘sanity’
<br/>


❌ **Caso Contrário:** A execução de todos os testes, incluindo testes que executam dezenas de consultas ao banco de dados, sempre que um desenvolvedor faz uma pequena alteração pode ser extremamente lenta e mantém os desenvolvedores longe de executar testes


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Marcando testes como ‘#cold-test’ permite que a ferramenta de teste execute apenas testes rápidos (Cold===testes rápidos que não fazem IO e podem ser executados com freqüência, mesmo quando o desenvolvedor está digitando)

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com Jest")
```javascript
//esse teste é rápido (sem banco de dados) e estamos marcando de forma correspondente
//agora o usuário/IC pode executá-lo com frequência
describe('Order service', function() {
  describe('Add new order #cold-test #sanity', function() {
    test('Scenario - no currency was supplied. Expectation - Use the default currency #sanity', function() {
      //lógica de código aqui
    });
  });
});


```

</details>




<br/><br/>

## ⚪ ️1.12 Outra boa higiene genérica para testes
:white_check_mark: **Faça:**  Esta postagem é focada em conselhos de teste relacionados ou pelo menos podem ser exemplificados com Node JS. Este tópico, no entanto, agrupa algumas dicas não relacionadas a Node que são bem conhecidas

Aprenda e pratique [princípios TDD](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) — eles são extremamente valiosos para muitos, mas não se intimidem se não se encaixarem no seu estilo, você não é o único. Considere escrever os testes antes do código em um [estilo vermelho-verde-refatorar](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), certifique-se de que cada teste verifica exatamente uma coisa, quando você encontrar um erro—antes de corrigir, escreva um teste que detectará esse erro no futuro, deixe que cada teste falhe pelo menos uma vez antes de ficar verde, inicie um módulo escrevendo um código rápido e simplista que satisfaça o teste - refatore gradualmente e leve-o a um nível de produção, evitar qualquer dependência do ambiente (caminhos, SO, etc)
<br/>


❌ **Caso Contrário:** Você sentirá falta das pérolas de sabedoria que foram coletadas por décadas

<br/><br/>


# Seção 2️⃣: Teste de Backend

## ⚪ ️2.1 Enriqueça seu portfólio de testes: Olhe além dos testes de unidade e da pirâmide

:white_check_mark: **Faça:**  A [pirâmide de testes](https://martinfowler.com/bliki/TestPyramid.html), apesar de ter 10> anos de idade, é um modelo excelente e relevante que sugere três tipos de teste e influencia a estratégia de teste da maioria dos desenvolvedores. Ao mesmo tempo, mais de um punhado de novas e brilhantes técnicas de teste surgiram e estão escondidas nas sombras da pirâmide de testes. Dadas todas as mudanças dramáticas que vimos nos últimos 10 anos (Microsserviços, cloud, serverless), é possível que um modelo bastante antigo seja adequado a *todos* os tipos de aplicações? O mundo dos testes não deveria considerar acolher novas técnicas de teste?

Não me interpretem mal, em 2019 a pirâmide de testes, TDD e testes de unidade ainda são técnicas poderosas e provavelmente são as mais compatíveis para muitas aplicações. Apenas como qualquer outro modelo, apesar de sua utilidade, [às vezes está errado](https://en.wikipedia.org/wiki/All_models_are_wrong). Por exemplo, considere um aplicativo IOT que ingere muitos eventos em um padronizador de mensagens como Kafka/RabbitMQ, que fluem para algum armazenamento de dados e, eventualmente, são consultados por algum UI. Deveríamos realmente gastar 50% do nosso orçamento em testes escrevendo testes de unidade para um aplicativo centrado na integração e quase sem lógica? À medida que a diversidade de tipos de aplicativos aumenta (bots, crypto, Alexa-skills) maiores são as chances de encontrar cenários em que a pirâmide de teste não é a melhor correspondência.

É hora de enriquecer seu portfólio de testes e se familiarizar com mais tipos de modelos mentais de testes (os próximos tópicos sugerem poucas idéias), como a pirâmide de testes, mas também combinar tipos de teste com problemas do mundo real que você está enfrentando (‘Ei, nossa API está quebrada, vamos escrever testes de contrato orientados ao consumidor!’), diversifique seus testes como um investidor que constrói um portfólio com base na análise de risco — avaliar onde os problemas podem surgir e combinar algumas medidas de prevenção para mitigar esses riscos potenciais

Uma palavra de cautela: o argumento TDD no mundo do software tem uma cara típica de dicotomia, alguns pregam para usá-lo em todo lugar, outros acham que ele é o diabo. Todo mundo que fala em absoluto está errado :]

<br/>


❌ **Caso Contrário:** Você perderá algumas ferramentas com um ROI incrível, algumas como Fuzz, lint e mutation podem fornecer valor em 10 minutos


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Cindy Sridharan sugere um rico portfólio de testes em seu incrível post "Testing Microservices - the sane way"
![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan sugere um rico portfólio de testes em seu incrível post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Example: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Além dos testes de unidade: 5 tipos de teste Node.JS brilhante (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "Um nome de teste que constitui 3 partes")


</details>




<br/><br/>

## ⚪ ️2.2 O teste de componentes pode ser o seu melhor caso

:white_check_mark: **Faça:** Cada teste de unidade cobre uma pequena parte do aplicativo e é caro cobrir o todo, enquanto os testes de ponta-a-ponta cobrem muito terreno, mas são escamosos e mais lentos, por que não aplicar uma abordagem equilibrada e escrever testes maiores que os testes unitários, mas menores que os testes de ponta-a-ponta? Teste de componentes é a música desconhecida do mundo dos testes— eles fornecem o melhor dos dois mundos: desempenho razoável e possibilidade de aplicar padrões TDD + cobertura realista e ótima.

Os testes de componentes concentram-se na 'unidade' do Microsservico, eles trabalham contra a API, não fazem mock de nada que pertença ao próprio Microsserviço (por exemplo. banco de dados real ou pelo menos a versão na memória desse banco de dados) mas fazem stub (desconsideram) qualquer coisa externa como chamadas para outros Microsserviços. Ao fazer isso, testamos o que implementamos, abordamos o aplicativo de fora para dentro e obtemos grande confiança em um período de tempo razoável.
<br/>


❌ **Caso Contrário:** Você pode passar longos dias escrevendo testes de unidade para descobrir que possui apenas 20% de cobertura do sistema


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: O Supertest permite abordar a API Express em processo (rápido e cobre muitas camadas)

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos com Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) permite abordar a API Express em processo (rápido e cobre muitas camadas)")

</details>

<br/><br/>

## ⚪ ️2.3 Verifique se os novos releases não quebram a API em uso

:white_check_mark: **Faça:**  Então, seu Microsserviço possui vários clientes e você executa várias versões do serviço por motivos de compatibilidade (mantendo todos felizes). Então você muda algum campo e ‘boom!’, algum cliente importante que depende desse campo fica irritado. Este é o Catch-22 do mundo da integração: É muito desafiador para o lado do servidor considerar todas as múltiplas expectativas dos clientes— Por outro lado, os clientes não podem realizar nenhum teste porque o servidor controla as datas de lançamento. [Contratos orientados ao consumidor e o framework PACT](https://docs.pact.io/) nasceram para formalizar esse processo com uma abordagem muito perturbadora — não é o servidor que define o plano de teste por si mesmo, mas o cliente define os testes do… servidor! PACT pode gravar a expectativa do cliente e colocar em um local compartilhado, “corretor”, para que o servidor possa puxar as expectativas e executar em cada build usando a biblioteca PACT para detectar contratos quebrados— uma expectativa do cliente que não é atendida. Ao fazer isso, todas as incompatibilidades da API do servidor-cliente são detectadas cedo durante a compilação/IC e podem poupar muita frustração
<br/>


❌ **Caso Contrário:** As alternativas são exaustivos testes manuais ou medo de implantação


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo:

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20PACT-blue.svg
 "Exemplos com PACT")
 
![alt text](assets/bp-14-testing-best-practices-contract-flow.png )


</details>



<br/><br/>


## ⚪ ️ 2.4 Teste seus Middlewares isoladamente

:white_check_mark: **Faça:** Muitos evitam os testes de Middleware porque representam uma pequena parte do sistema e requerem um servidor Express ativo. Ambas as razões estão erradas — Os Middlewares são pequenos, mas afetam todas ou a maioria das solicitações e podem ser testados facilmente como funções puras que recebem objetos JS {req, res}. Para testar uma função de middleware, basta invocá-la e espionar ([usando o Sinon por exemplo](https://www.npmjs.com/package/sinon)) na interação com os objetos {req, res} para garantir que a função executou a ação correta. A biblioteca [node-mock-http](https://www.npmjs.com/package/node-mocks-http) vai ainda mais longe e fatora os objetos {req, res}, além de espionar seu comportamento. Por exemplo, ela pode afirmar se o status http que foi definido no objeto res corresponde à expectativa (veja o exemplo abaixo)
<br/>


❌ **Caso Contrário:** Um bug no middleware Express === um bug em todas ou na maioria das solicitações


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Testando o middleware isoladamente sem emitir chamadas de rede e acordar toda a máquina Express

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Jest-blue.svg
 "Exemplos com Jest")

```javascript
//o middleware que queremos testar
const unitUnderTest = require('./middleware')
const httpMocks = require('node-mocks-http');
//Sintaxe Jest, equivalente a describe() & it() no Mocha
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

## ⚪ ️2.5 Meça e refatore usando ferramentas de análise estática
:white_check_mark: **Faça:** O uso de ferramentas de análise estática ajuda a fornecer maneiras objetivas de melhorar a qualidade do código e manter seu código sustentável. Você pode adicionar ferramentas de análise estática à sua compilação de IC para abortar quando encontrar mal cheiros no código. Suas principais vantagens em relação a usar simplesmente um linter são a capacidade de inspecionar a qualidade no contexto de vários arquivos (por exemplo. detectar duplicações), executar análise avançada (por exemplo, complexidade do código) e seguir o histórico e o progresso dos problemas de código. Dois exemplos de ferramentas que você pode usar são: [Sonarqube](https://www.sonarqube.org/) (2,600+ [stars](https://github.com/SonarSource/sonarqube)) e [Code Climate](https://codeclimate.com/) (1,500+ [stars](https://github.com/codeclimate/codeclimate))

Créditos:: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>


❌ **Caso Contrário:** Com baixa qualidade de código, bugs e desempenho sempre serão um problema que nenhuma nova biblioteca brilhante ou recursos avançados podem corrigir


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo:  CodeClimate, uma ferramenta comercial que pode identificar métodos complexos:

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Code%20Climate-blue.svg
 "Exemplos com CodeClimate")
 
![alt text](assets/bp-16-yoni-goldberg-quality.png " CodeClimat, uma ferramenta comercial que pode identificar métodos complexos:")

</details>




<br/><br/>

## ⚪ ️ 2.6 Verifique sua preparação para o caos relacionado ao Node
:white_check_mark: **Faça:** Estranhamente, a maioria dos testes de software trata apenas de lógica e dados, mas algumas das piores coisas que acontecem (e são realmente difíceis de mitigar) são questões de infra-estrutura. Por exemplo, você já testou o que acontece quando a memória do processo está sobrecarregada, ou quando o servidor/processo morre, ou o seu sistema de monitoramento percebe quando a API fica 50% mais lenta?. Para testar e mitigar esse tipo de coisas ruins — [Chaos engineering](https://principlesofchaos.org/) nasceu pela Netflix. O objetivo é fornecer conscientização, frameworks e ferramentas para testar a resiliência de nosso aplicativo para problemas caóticos. Por exemplo, uma de suas famosas ferramentas, [o chaos monkey](https://github.com/Netflix/chaosmonkey), mata servidores aleatoriamente para garantir que nosso serviço ainda possa atender usuários e não depender em um único servidor (existe também uma versão para Kubernetes, [kube-monkey](https://github.com/asobti/kube-monkey), que mata pods). Todas essas ferramentas funcionam no nível de hospedagem/plataforma, mas e se você quiser testar e gerar o caos puro do Node, por exemplo verificar como o processo do nó lida com erros não detectados, rejeições de promises não tratadas, Memória do v8 sobrecarregada com o máximo permitido de 1,7 GB ou se o seu UX permanece satisfatório quando o loop de eventos é bloqueado com frequência? para resolver isso que escrevi, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) que fornece todos os tipos de atos caóticos relacionados ao Node
<br/>


❌ **Caso Contrário:**  Não há escapatória aqui, a lei de Murphy afetará sua produção sem piedade


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: : O Node-Chaos pode gerar todo tipo de pegadinha do Node.js, para que você possa testar a resiliência do seu aplicativo ao caos
![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "O Node-Chaos pode gerar todo tipo de pegadinha do Node.js, para que você possa testar a resiliência do seu aplicativo ao caos")

</details>

<br/>

## ⚪ ️2.7 Evite acessórios de teste e sementes globais, adicione dados por teste

:white_check_mark: **Faça:** Seguindo a regra de ouro (tópico 0), cada teste deve adicionar e agir em seu próprio conjunto de linhas de banco de dados para evitar o acoplamento e raciocinar facilmente sobre o fluxo de teste. Na realidade, isso geralmente é violado por testadores que propagam o banco de dados com dados antes de executar os testes (também conhecido como "acessórios de teste") por uma questão de melhoria de desempenho. Embora o desempenho seja realmente uma preocupação válida— pode ser mitigado (consulte o tópico "Teste de componentes"), no entanto, a complexidade do teste é uma tarefa muito dolorosa que deve governar outras considerações na maioria das vezes. Na prática, faça com que cada caso de teste inclua explicitamente os registros do banco de dados necessários e atue somente nesses registros. Se o desempenho se tornar uma preocupação crítica — um compromisso equilibrado pode vir na forma de propagação do único conjunto de testes que não está alterando dados (por exemplo, consultas)
<br/>


❌ **Caso Contrário:** Poucos testes falham, uma implantação é abortada, nossa equipe gastará um tempo precioso agora, temos um bug? Vamos investigar, oh não - parece que dois testes estavam modificando os mesmos dados iniciais


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: exemplo Anti-padrão: testes não são independentes e dependem de algum gancho global para alimentar dados globais de banco de dados

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos com Mocha")
 
```javascript
before(() => {
  //adicionando dados de sites e administradores ao nosso banco de dados. Onde estão os dados? Do lado de fora. Em alguma estrutura json ou de migração externa
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //Eu sei que o nome do site "portal" existe - eu vi nos arquivos de sementes
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //Eu sei que o nome do site "portal" existe - eu vi nos arquivos de sementes
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Falha! O teste anterior altera o nome :[
});

```
<br/>

### :clap: Exemplo Fazendo Certo: Podemos permanecer dentro do teste, cada teste atua em seu próprio conjunto de dados

```javascript
it("When updating site name, get successful confirmation", async () => {
  //teste está adicionando registros novos e atuando apenas nos registros
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

## ⚪ ️ 3.1 Separar UI da funcionalidade

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

### :thumbsdown: Exemplo Anti-padrão: Afirmações misturam detalhes da UI e dados
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
    
    expect(getByTestId('errorsLabel').text()).toBe("0");
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

:white_check_mark: **Faça:** Sempre que tiver um tamanho razoável, teste seu componente de fora como os usuários, renderize a interface do usuário, atue sobre ela e afirme que a interface do usuário renderizada se comporta conforme o esperado. Evite todo tipo de simulação, renderização parcial e superficial - essa abordagem pode resultar em erros não capturados devido à falta de detalhes e dificultar a manutenção, pois os testes interferem nos internos (veja o tópico 'Favorecer o teste de caixa preta'). Se um dos componentes filhos estiver desacelerando significativamente (por exemplo, animação) ou complicando a instalação - considere substituí-lo explicitamente por um falso

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

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Cypress-blue.svg
 "Usando Cypress para ilustrar a ideia")
![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React%20Testing%20Library-blue.svg
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

## ⚪ ️ 3.5 Veja como o conteúdo é servido na rede

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
 "Exemplos com React") ![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20React%20Testing%20Library.svg
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

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Cucumber-blue.svg  "Exemplos usando Cucumber")
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

![alt text](assets/story-book.jpg "Storybook")


</details>

<br/><br/>


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
 "Usando Wraith")

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
 "Usando AppliTools") ![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Cypress-blue.svg
 "Usando Cypress para illustrar idea")

```javascript
import  *  as todoPage from  '../page-objects/todo-page';

describe('visual validation',  ()  =>  {
  before(()  =>  todoPage.navigate());
  beforeEach(()  =>  cy.eyesOpen({ appName: 'TAU TodoMVC' }));
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

  
# Seção 4️⃣: Medindo a Eficácia dos Testes

<br/><br/>

## ⚪ ️ 4.1 Obtenha cobertura suficiente para ter confiança, ~ 80% parece ser o número da sorte

:white_check_mark: **Faça:** O objetivo do teste é obter confiança suficiente para avançar rapidamente, obviamente, quanto mais código for testado, mais confiante a equipe pode ter. Cobertura é uma medida de quantas linhas de código (e ramificações, instruções etc.) estão sendo alcançadas pelos testes. Então, quanto é suficiente? 10-30% é obviamente muito baixo para ter noção da correção da compilação, por outro lado, 100% é muito caro e pode mudar seu foco dos caminhos críticos para os cantos exóticos do código. A resposta longa é que depende de muitos fatores, como o tipo de aplicativo - se você está construindo a próxima geração do Airbus A380, 100% é uma obrigação, para um site de imagens de desenhos animados 50% pode ser demais. Embora a maioria dos entusiastas do teste afirme que o limite de cobertura correto é contextual, a maioria deles também menciona o número 80% como a regra de ouro ([Fowler: “na casa dos 80% ou 90%”](https://martinfowler.com/bliki/TestCoverage.html)) que presumivelmente, deve satisfazer a maioria das aplicações.

Dicas de implementação: Convém configurar sua integração contínua (CI) para ter um limite mínimo de cobertura ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) e interrompa uma compilação que não atenda a esse padrão (também é possível configurar o limite por componente, veja o exemplo de código abaixo). Além disso, considere detectar uma diminuição na cobertura da construção (quando um código recém-confirmado tem menos cobertura) — isso fará com que os desenvolvedores aumentem ou, pelo menos, preservem a quantidade de código testado. Tudo isso dito, a cobertura é apenas uma medida, quantitativa, que não é suficiente para demonstrar a robustez dos seus testes. E também pode ser enganada, como ilustrado nos próximos tópicos

<br/>


❌ **Caso contrário:**  Confiança e números andam de mãos dadas, sem realmente saber que você testou a maior parte do sistema - haverá também algum medo. e o medo vai atrasá-lo


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo: um relatório de cobertura típico
![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "Um relatório de cobertura típico")

<br/>

### :clap: Exemplo Fazendo Certo: Configurando a cobertura por componente (usando o Jest)

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Jest-blue.svg
 "Usando Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Configurando a cobertura por componente (usando o Jest)")

</details>



<br/><br/>

## ⚪ ️ 4.2 Inspecionar relatórios de cobertura para detectar áreas não testadas e outras esquisitices

:white_check_mark: **Faça:** Alguns problemas se escondem logo abaixo do radar e são realmente difíceis de encontrar usando ferramentas tradicionais. Esses não são realmente erros, mas um comportamento surpreendente do aplicativo que pode ter um impacto grave. Por exemplo, geralmente algumas áreas de código nunca ou raramente são invocadas — você pensou que a classe 'PricingCalculator' está sempre definindo o preço do produto, mas, na verdade, nunca é invocada, embora tenhamos 10000 produtos no banco de dados e muitas vendas... Os relatórios de cobertura de código ajudam a perceber se o aplicativo se comporta da maneira que você acredita. Além disso, ele também pode destacar quais tipos de código não foram testados—ser informado que 80% do código é testado não informa se as partes críticas estão cobertas. Gerar relatórios é fácil—basta executar seu aplicativo em produção ou durante o teste com rastreamento de cobertura e ver relatórios coloridos que destacam a frequência com que cada área de código é invocada. Se você dedicar um tempo para vislumbrar esses dados—poderá encontrar algumas pegadinhas
<br/>


❌ **Caso contrário:** Se você não sabe quais partes do seu código são deixadas sem teste, não sabe de onde os problemas podem surgir


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: O que há de errado com este relatório de cobertura?

Com base em um cenário do mundo real, onde rastreamos o uso de nossos aplicativos no controle de qualidade e descobrimos padrões de login interessantes (Dica: a quantidade de falhas de login não é proporcional, algo está claramente errado. Por fim, verificou-se que algum bug do frontend continua atingindo a API de login do back-end)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png " que há de errado com este relatório de cobertura?")

</details>


<br/><br/>

## ⚪ ️ 4.3 Meça a cobertura lógica usando teste de mutação

:white_check_mark: **Faça:**  A métrica de cobertura tradicional geralmente mente: Pode mostrar 100% de cobertura do código, mas nenhuma de suas funções, nem mesmo uma, retorna a resposta correta. Por quê? Ele simplesmente mede sobre quais linhas de código o teste visitou, mas não verifica se os testes realmente testaram alguma coisa— afirmou para a resposta certa. Como alguém que viaja a negócios e mostra seus carimbos de passaporte—isso não prova nenhum trabalho, apenas que ele visitou alguns aeroportos e hotéis.

O teste baseado em mutação está aqui para ajudar, medindo a quantidade de código que foi realmente TESTADO e não apenas VISITADO. [Stryker](https://stryker-mutator.io/) é uma biblioteca JavaScript para teste de mutação e a implementação é realmente legal:

(1) intencionalmente altera o código e "planta bugs". Por exemplo, o código newOrder.price===0 torna-se newOrder.price!=0. Esses "bugs" são chamados de mutações

(2) executa os testes, se todos tiverem sucesso, então temos um problema— os testes não serviram ao seu propósito de descobrir bugs, as mutações são chamadas sobreviventes. Se os testes falharem, então ótimo, as mutações foram mortas.

Saber que todas ou a maioria das mutações foram mortas dá uma confiança muito maior do que a cobertura tradicional e o tempo de instalação é semelhante
<br/>


❌ **Caso contrário:** Você ficará enganado ao acreditar que 85% de cobertura significa que seu teste detectará bugs em 85% do seu código

<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: 100% de cobertura, 0% de teste

![](https://img.shields.io/badge/🔨%20Exemplo%20usando%20Stryker-blue.svg
 "Usando Stryker")
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

### :clap: Exemplo Fazendo Certo: Stryker reports, uma ferramenta para teste de mutação, detecta e conta a quantidade de código que não foi testado (mutações)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, uma ferramenta para teste de mutação, detecta e conta a quantidade de código que não foi testado (mutações)")

</details>



<br/><br/>

## ⚪ ️4.4 Impedindo problemas de código de teste com os linters de teste

:white_check_mark: **Faça:**  Um conjunto de plugins ESLint foi construído especificamente para inspecionar os padrões de código de testes e descobrir problemas. Por exemplo, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) avisará quando um teste for escrito em nível global (não é filho de uma declaração describe()) ou quando os testes são [pulados](https://mochajs.org/#inclusive-tests) o que pode levar a uma falsa crença de que todos os testes estão passando. Similarmente, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) pode, por exemplo, avisar quando um teste não tem afirmações (não verificando nada)

<br/>


❌ **Caso contrário:** Ver 90% de cobertura de código e 100% de testes verdes fará com que seu rosto seja um grande sorriso apenas até você perceber que muitos testes não afirmam nada e que muitos conjuntos de testes foram ignorados. Tomara que você não tenha implantado nada com base nessa observação falsa


<br/>
<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: Um caso de teste cheio de erros, felizmente, todos são pegos por Linters

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

  
# Seção 5️⃣: IC e Outras Medidas de Qualidade

<br/><br/>

## ⚪ ️ 5.1 Enriqueça seus linters e aborte construções que tenham problemas de lint

:white_check_mark: **Faça:**  Linters são um almoço grátis, com 5 minutos de configuração, você obtém gratuitamente um piloto automático que protege seu código e captura de problemas significativos enquanto digita. Já se foram os dias em que linting era apenas por beleza (sem ponto e vírgula!). Hoje em dia, Linters podem detectar problemas graves, como erros que não são lançados corretamente e perda de informações. Além do seu conjunto básico de regras (como [ESLint padrão](https://www.npmjs.com/package/eslint-plugin-standard) ou [estilo Airbnb](https://www.npmjs.com/package/eslint-config-airbnb)), considere incluir alguns Linters especializados como [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) que pode descobrir testes sem asserções, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) pode descobrir promessas sem resolução (seu código nunca vai continuar), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) que pode descobrir expressões regulares inseguras que podem ser usadas para ataques do DOS e[eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) é capaz de alarmar quando o código usa métodos da biblioteca de utilitários que fazem parte dos métodos principais do V8, como Lodash._map(…)
<br/>


❌ **Caso Contrário:** Considere um dia chuvoso em que sua produção continua travando, mas os logs não exibem o rastreamento do stack de erros. O que aconteceu? Seu código lançou um objeto sem erro por engano e o rastreamento do stack foi perdido, uma boa razão para bater a cabeça contra uma parede de tijolos. Uma configuração de linter de 5 minutos pode detectar esse erro de DIGITAÇÃO e salvar seu dia


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :thumbsdown: Exemplo Anti-padrão: O objeto sem a propriedade erro é lançado por engano, nenhum rastreamento do stack será exibido para esse erro. Felizmente, o ESLint capta o próximo bug de produção
![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "O objeto sem a propriedade erro é lançado por engano, nenhum rastreamento do stack será exibido para esse erro. Felizmente, o ESLint capta o próximo bug de produção")

</details>




<br/><br/>

# ⚪ ️ 5.2 Encurte o ciclo de feedback com o IC de desenvolvedor local

:white_check_mark: **Faça:**   Usando uma IC com inspeções de qualidade brilhantes, como testes, linting, verificação de vulnerabilidades, etc? Ajude os desenvolvedores a executar esse pipeline também localmente para solicitar feedback instantâneo e diminuir o [ciclo de feedback](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Por quê? um processo de teste eficiente constitui muitos loops iterativos: (1) tentativas -> (2) feedback -> (3) refatoração. Quanto mais rápido o feedback, mais iterações de aprimoramento um desenvolvedor pode executar por módulo e aperfeiçoar os resultados. Por outro lado, quando o feedback chegar atrasado, menos iterações de melhoria poderão ser agrupadas em um único dia, a equipe já pode ter avançado para outro tópico/tarefa/módulo e pode não estar apta a refinar esse módulo.

Na prática alguns fornecedores de IC (exemplo: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/)) permitir a execução do pipeline localmente. Algumas ferramentas comerciais como [wallaby fornece informações valiosas e intuições de teste](https://wallabyjs.com/) como um protótipo de desenvolvedor (sem afiliação). Como alternativa, você pode apenas adicionar um npm script no package.json que executa todos os comandos de qualidade (por exemplo teste, lint, vulnerabilidades) — use ferramentas como [concurrently](https://www.npmjs.com/package/concurrently) para paralelismo e código de saída diferente de zero, se uma das ferramentas falhar. Agora o desenvolvedor deve apenas chamar um comando— por exemplo ‘npm run quality’ — para obter feedback instantâneo. Considere também abortar um commit se a verificação de qualidade falhar usando um githook ([husky pode ajudar](https://github.com/typicode/husky))
<br/>


❌ **Caso Contrário:** Quando os resultados da qualidade chegam no dia seguinte ao código, o teste não se torna uma parte fluente do desenvolvimento, e sim um artefato formal após o fato


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap:  Exemplo Fazendo Certo: npm scripts que realizam inspeção de qualidade de código, todos são executados em paralelo sob demanda ou quando um desenvolvedor está tentando enviar um novo código
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

# ⚪ ️5.3 Realize testes e2eem um verdadeiro espelho de produção

:white_check_mark: **Faça:**   Os testes de ponta a ponta (e2e) são o principal desafio de cada pipeline de IC—criar um espelho efêmero idêntico de produção em tempo real com todos os serviços em nuvem relacionados pode ser entediante e caro. Encontrar o melhor comprometimento é o seu jogo: [Docker-compose](https://serverless.com/) permite criar ambiente docker isolado com contêineres idênticos usando um único arquivo de texto sem formatação, mas as tecnologias de suporte (por exemplo. rede, modelo de implantação) é diferente das produções do mundo real. Você pode combiná-lo com [‘AWS Local’](https://github.com/localstack/localstack) para trabalhar com um esboço dos serviços reais da AWS. Se você usar [serverless](https://serverless.com/) vários frameworks como serverless e [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) permite a chamada local de códigos FaaS.

O enorme ecossistema Kubernetes ainda não formalizou uma ferramenta conveniente padrão para espelhamento local e de IC, embora muitas novas ferramentas sejam lançadas com frequência. Uma abordagem é executar ‘minimized-Kubernetes’ usando ferramentas como [Minikube](https://kubernetes.io/docs/setup/minikube/) e [MicroK8s](https://microk8s.io/) que se assemelham-se à coisa real só vêm com menos sobrecarga. Outra abordagem é testar em um ambiente remoto ‘real-Kubernetes’, alguns provedores de IC (por exemplo, [Codefresh](https://codefresh.io/)) possuem integração nativa com ambiente Kubernetes e facilitam a execução do pipeline do IC sobre o ambiente real, outros permitem scripts personalizados em um Kubernetes remoto.
<br/>


❌ **Caso Contrário:** O uso de tecnologias diferentes para demandas de produção e teste mantém dois modelos de implantação e mantém os desenvolvedores e a equipe de operações separados


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap:  Exemplo: um pipeline de IC que gera clusters Kubernetes em tempo real <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Créditos: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>





<br/><br/>

## ⚪ ️5.4 Paralelizar a execução do teste
:white_check_mark: **Faça:**    Quando bem feito, o teste é seu amigo 24/7, fornecendo feedback quase instantâneo. Na prática, a execução de 500 testes de unidade limitados à CPU em um único thread pode levar muito tempo. Felizmente, executores de teste modernos e plataformas de IC (como [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) e [extenções Mocha](https://github.com/yandex/mocha-parallel-tests)) podem paralelizar os testes em vários processos e obter uma melhoria significativa no tempo de feedback. Alguns fornecedores de IC também paralelam testes entre contêineres (!) o que reduz ainda mais o ciclo de feedback. Seja localmente em vários processos ou em alguma ILC na nuvem usando várias máquinas— paralelizando a demanda, mantendo os testes autônomos, pois cada um pode ser executado em diferentes processos


❌ **Caso Contrário:** Obter resultados de testes 1 hora após o envio do novo código, enquanto você codifica os próximos recursos, é uma ótima receita para tornar os testes menos relevantes


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo: Mocha parallel & Jest superam facilmente o Mocha tradicional graças ao teste de paralelização ([Créditos: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))
![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest superam facilmente o Mocha tradicional graças ao teste de paralelização (Créditos: JavaScript Test-Runners Benchmark)")

</details>




<br/><br/>

## ⚪ ️5.5 Fique longe de questões legais usando licença e verificação de plágio
:white_check_mark: **Faça:**    Problemas de licenciamento e plágio provavelmente não são sua principal preocupação no momento, mas por que não resolver isso também em 10 minutos? Um monte de pacotes npm como [license check](https://www.npmjs.com/package/license-checker) e [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (comercial com plano gratuito) podem ser facilmente incorporado ao seu pipeline de IC e inspecionar problemas, como dependências com licenças restritivas ou código que foi copiado e colado do Stackoverflow e aparentemente viola alguns direitos autorais

❌ **Caso Contrário:** Involuntariamente, os desenvolvedores podem usar pacotes com licenças inadequadas ou copiar e colar código comercial e enfrentar problemas legais


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap: Exemplo Fazendo Certo:
```javascript
//instale license-checker no seu ambiente IC ou também localmente
npm install -g license-checker

//solicite que verifique todas as licenças e falhe com o código de saída diferente de 0 se encontrar uma licença não autorizada. O sistema de IC deve detectar essa falha e interromper a construção
license-checker --summary --failOn BSD

```

<br/>

![alt text](assets/bp-25-nodejs-licsense.png)


</details>



<br/><br/>

## ⚪ ️5.6 Inspecionar constantemente as dependências vulneráveis
:white_check_mark: **Faça:**  Mesmo as dependências mais respeitáveis, como o Express, têm vulnerabilidades conhecidas. Isso pode ser facilmente domado usando ferramentas da comunidade, como [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), ou ferramentas comerciais como [snyk](https://snyk.io/) (oferece também uma versão comunitária gratuita). Ambos podem ser chamados a partir do seu IC em cada build

❌ **Caso Contrário:** Para manter seu código livre de vulnerabilidades sem ferramentas dedicadas, é necessário seguir constantemente as publicações on-line sobre novas ameaças. Bastante tedioso


<br/>

<details><summary>✏ <b>Códigos de Exemplos</b></summary>

<br/>

### :clap: Exemplo: Resultado de NPM Audit
![alt text](assets/bp-26-npm-audit-snyk.png "Resultado de NPM Audit")

</details>




<br/><br/>

## ⚪ ️5.7 Automatize atualizações de dependência
:white_check_mark: **Faça:**   Yarn e npm recentemente incluiram package-lock.json que introduziu um sério desafio (o caminho para o inferno é pavimentado com boas intenções) — por padrão agora, os pacotes não estão mais recebendo atualizações. Mesmo uma equipe executando muitas implantações novas com ‘npm install’ & ‘npm update’ não receberão novas atualizações. Isso leva a versões abaixo dos pacotes de dependência, na melhor das hipóteses, ou ao código vulnerável, na pior das hipóteses. As equipes agora contam com a boa vontade e a memória dos desenvolvedores para atualizar manualmente o package.json ou usar ferramentas [como ncu](https://www.npmjs.com/package/npm-check-updates) manualmente. Uma maneira mais confiável seria automatizar o processo de obtenção das versões de dependência mais confiáveis, embora não haja uma solução certeira ainda, existem duas vias de automação possíveis:

(1) O IC pode falhar nas construções que possuem dependências obsoletas — usando ferramentas como [‘npm outdated’](https://docs.npmjs.com/cli/outdated) ou ‘npm-check-updates (ncu)’ . Fazer isso forçará os desenvolvedores a atualizar dependências.

(2) Use ferramentas comerciais que varrem o código e enviam automaticamente pull requests com dependências atualizadas. Uma questão interessante que resta é qual deve ser a política de atualização de dependência— a atualização em cada patch gera muitos custos indiretos; a atualização quando uma versão nova é lançado pode apontar para uma versão instável (muitos pacotes são descobertos como vulneráveis ​​nos primeiros dias após o lançamento, [veja o](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) incidente do eslint-scope).

Uma política de atualização eficiente pode permitir um ‘período de acomodação’ — deixe o código ficar atrás do @latest por algum tempo e versões antes de considerar a cópia local como obsoleta (por exemplo. versão local é 1.3.1 e a versão do repositório é 1.3.8)
<br/>


❌ **Caso Contrário:** Sua produção executará pacotes que foram explicitamente marcados pelo autor como arriscados


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap:  Exemplo: [ncu](https://www.npmjs.com/package/npm-check-updates) pode ser usado manualmente ou em um pipeline de IC para detectar quanto o código está atrasado em relação às versões mais recentes
![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu pode ser usado manualmente ou em um pipeline de IC para detectar quanto o código está atrasado em relação às versões mais recentes")


</details>


<br/><br/>

## ⚪ ️ 5.8 Outras dicas de IC não relacionadas ao Node
:white_check_mark: **Faça:**    Esta postagem é focada em conselhos de teste relacionados ou pelo menos podem ser exemplificados com o Node JS. Este marcador, no entanto, agrupa algumas dicas não relacionadas ao nó que são bem conhecidas

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use uma sintaxe declarativa. Essa é a única opção para a maioria dos fornecedores, mas as versões mais antigas do Jenkins permitem o uso de código ou interface do usuário.</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opte por um fornecedor que tenha suporte nativo ao Docker</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Falhe cedo, execute seus testes mais rápidos primeiro. Crie uma etapa/meta de "Teste de fumaça" que agrupe várias inspeções rápidas (por exemplo linting, testes unitários) e fornecer feedback instantâneo para o responsável pelo código</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Facilite a varredura de todos os artefatos de construção, incluindo relatórios de teste, relatórios de cobertura, relatórios de mutação, logs, etc.</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Crie vários pipelines/trabalhos para cada evento, reutilize as etapas entre eles. Por exemplo, configure um trabalho para commits de branches de recursos e outro para PR na master. Permita que cada uma reutilize a lógica usando etapas compartilhadas (a maioria dos fornecedores fornece algum mecanismo para reutilização de código)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Nunca incorpore segredos em uma declaração de trabalho, pegue-os em um armazenamento secreto ou na configuração do trabalho</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Explicitamente aumente a versão em uma compilação de versão ou pelo menos garanta que o desenvolvedor o fez</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Compileapenas uma vez e execute todas as inspeções no artefato de construção único (por exemplo, imagem do Docker)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Teste em um ambiente efêmero que não varia de estado entre compilações. Armazenar em cache node_modules pode ser a única exceção</li></ol>
<br/>


❌ **Caso Contrário:** Você perderá anos de sabedoria

<br/><br/>

## ⚪ ️ 5.9 Matriz de construção: execute as mesmas etapas de IC usando várias versões do Node
:white_check_mark: **Faça:** A verificação da qualidade é sobre acaso, quanto mais você cobrir, mais sorte terá na detecção de problemas mais cedo. Ao desenvolver pacotes reutilizáveis ​​ou executar uma produção de vários clientes com várias configurações e versões do Node, o IC deve executar o pipeline de testes em todas as permutações de configurações. Por exemplo, supondo que usamos o MySQL para alguns clientes e o Postgres para outros — alguns fornecedores de IC suportam um recurso chamado "Matriz" que permitem executar o processo de teste contra todas as permutações do MySQL, Postgres e várias versões do Node, como 8, 9 e 10. Isso é feito usando a configuração apenas sem nenhum esforço adicional (supondo que você tenha testes ou quaisquer outras verificações de qualidade). Outros ICs que não suportam Matrix podem ter extensões ou ajustes para permitir isso
<br/>


❌ **Caso Contrário:** Então, depois de fazer todo esse trabalho duro de escrever testes, vamos permitir que os bugs entrem apenas por causa de problemas de configuração?


<br/>

<details><summary>✏ <b>Códigos de Exemplo</b></summary>

<br/>

### :clap:   Exemplo: Usando a definição de construção do Travis (fornecedor de IC) para executar o mesmo teste em várias versões do Node
<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# Time



## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Função:** Escritor

**Sobre:** Sou um consultor independente que trabalha com 500 empresas afortunadas e startups de garagem para aprimorar seus aplicativos JS & Node.js. Mais do que qualquer outro tópico, me fascina e tenho como objetivo dominar a arte de testar. Eu também sou o autor de [Melhores práticas do Node.js.](https://github.com/goldbergyoni/nodebestpractices)

<br/>

**Oficina:** 👨‍🏫 Deseja aprender todas essas práticas e técnicas em seus escritórios (Europa & EUA)? [Registre-se aqui para minha oficina de testes](https://testjavascript.com/)
<br/>

**Siga:**

* [🐦 Twitter](https://twitter.com/goldbergyoni/)
* [📞 Contato](https://testjavascript.com/contact-2/)
* [✉️ Boletim de Notícias](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**Função:** Revisor e consultor técnico

Teve o cuidado de revisar, melhorar, usar lint e polir todos os textos

**Sobre:** full-stack web engineer, entusiasta de Node.js e GraphQL
<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Função:** Conceito, design e ótimos conselhos

**Sobre:** Um desenvolvedor front-end esclarecido, especialista em CSS e emojis

## [Kyle Martin](https://github.com/js-kyle)

**Função:** Ajuda a manter esse projeto em execução e analisa práticas relacionadas à segurança

**Sobre:** Adora trabalhar em projetos Node.js. e segurança de aplicativos da web.

## Contribuidores ✨
Agradecemos a essas pessoas maravilhosas que contribuíram para este repositório!
<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table>
</table>
<!-- ALL-CONTRIBUTORS-LIST:END -->
<table>
  <tr>
    <td align="center"><a href="http://geospatialscott.blogspot.com/"><img src="https://avatars3.githubusercontent.com/u/1326248?v=4" width="100px;" alt="Scott Davis"/><br /><sub><b>Scott Davis</b></sub></a><br /><a href="#content-stdavis" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AdrienRedon"><img src="https://avatars2.githubusercontent.com/u/5978436?v=4" width="100px;" alt="Adrien REDON"/><br /><sub><b>Adrien REDON</b></sub></a><br /><a href="#content-AdrienRedon" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/NoriSte"><img src="https://avatars0.githubusercontent.com/u/173663?v=4" width="100px;" alt="Stefano Magni"/><br /><sub><b>Stefano Magni</b></sub></a><br /><a href="#content-NoriSte" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.joer.im"><img src="https://avatars2.githubusercontent.com/u/47742486?v=4" width="100px;" alt="Yeoh Joer"/><br /><sub><b>Yeoh Joer</b></sub></a><br /><a href="#content-yjoer" title="Content">🖋</a></td>
    <td align="center"><a href="http://jhonnymoreira.dev"><img src="https://avatars0.githubusercontent.com/u/2177742?v=4" width="100px;" alt="Jhonny Moreira"/><br /><sub><b>Jhonny Moreira</b></sub></a><br /><a href="#content-jhonnymoreira" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Germanika"><img src="https://avatars2.githubusercontent.com/u/8846678?v=4" width="100px;" alt="Ian Germann"/><br /><sub><b>Ian Germann</b></sub></a><br /><a href="#content-Germanika" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AbdelrahmanHafez"><img src="https://avatars3.githubusercontent.com/u/19984935?v=4" width="100px;" alt="Hafez"/><br /><sub><b>Hafez</b></sub></a><br /><a href="#content-AbdelrahmanHafez" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.ruxandrafediuc.com"><img src="https://avatars1.githubusercontent.com/u/11021586?v=4" width="100px;" alt="Ruxandra Fediuc"/><br /><sub><b>Ruxandra Fediuc</b></sub></a><br /><a href="#content-ruxandrafed" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jacklee814"><img src="https://avatars0.githubusercontent.com/u/9951291?v=4" width="100px;" alt="Jack"/><br /><sub><b>Jack</b></sub></a><br /><a href="#content-jacklee814" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.petercarrero.com"><img src="https://avatars0.githubusercontent.com/u/231727?v=4" width="100px;" alt="Peter Carrero"/><br /><sub><b>Peter Carrero</b></sub></a><br /><a href="#content-aloyr" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/huhgawz"><img src="https://avatars3.githubusercontent.com/u/369338?v=4" width="100px;" alt="Huhgawz"/><br /><sub><b>Huhgawz</b></sub></a><br /><a href="#content-huhgawz" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/haakonmb"><img src="https://avatars1.githubusercontent.com/u/7099302?v=4" width="100px;" alt="Haakon Borch"/><br /><sub><b>Haakon Borch</b></sub></a><br /><a href="#content-haakonmb" title="Content">🖋</a></td>
    <td align="center"><a href="https://jaimemendoza.com/"><img src="https://avatars3.githubusercontent.com/u/5395811?v=4" width="100px;" alt="Jaime Mendoza"/><br /><sub><b>Jaime Mendoza</b></sub></a><br /><a href="#content-jaimemendozadev" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/camerondunford"><img src="https://avatars0.githubusercontent.com/u/840612?v=4" width="100px;" alt="Cameron Dunford"/><br /><sub><b>Cameron Dunford</b></sub></a><br /><a href="#content-camerondunford" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/shadowspawn"><img src="https://avatars1.githubusercontent.com/u/15719847?v=4" width="100px;" alt="John Gee"/><br /><sub><b>John Gee</b></sub></a><br /><a href="#content-shadowspawn" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/aurelijusrozenas"><img src="https://avatars0.githubusercontent.com/u/3273544?v=4" width="100px;" alt="Aurelijus Rožėnas"/><br /><sub><b>Aurelijus Rožėnas</b></sub></a><br /><a href="#content-aurelijusrozenas" title="Content">🖋</a></td>
    <td align="center"><a href="http://aaronshivers.com"><img src="https://avatars2.githubusercontent.com/u/42848750?v=4" width="100px;" alt="Aaron"/><br /><sub><b>Aaron</b></sub></a><br /><a href="#content-aaronshivers" title="Content">🖋</a></td>
    <td align="center"><a href="https://tomdoes.tech/"><img src="https://avatars1.githubusercontent.com/u/8683577?v=4" width="100px;" alt="Tom Nagle"/><br /><sub><b>Tom Nagle</b></sub></a><br /><a href="#content-tomanagle" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/yvesyao"><img src="https://avatars0.githubusercontent.com/u/7723729?v=4" width="100px;" alt="Yves yao"/><br /><sub><b>Yves yao</b></sub></a><br /><a href="#content-yvesyao" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Userbit"><img src="https://avatars1.githubusercontent.com/u/34487074?v=4" width="100px;" alt="Userbit"/><br /><sub><b>Userbit</b></sub></a><br /><a href="#content-Userbit" title="Content">🖋</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->
