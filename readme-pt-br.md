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

Um único conselho que inspira todos os outros (1 tópico especial)

#### [`Seção 1: A Anatomia do Teste`](#section-1-the-test-anatomy-1)

A fundação - estruturando testes limpos (12 tópicos)

#### [`Seção 2: Backend`](#section-2️⃣-backend-testing)

Escrevendo testes de back-end e microsserviços com eficiência (8 tópicos)

#### [`Seção 3: Frontend`](#section-3️⃣-frontend-testing)

Escrevendo testes para interface do usuário da web, incluindo testes de componentes e E2E (11 tópicos)

#### [`Seção 4: Metrificando Testes Efetivamente`](#section-4️⃣-measuring-test-effectiveness)

Observando o vigia - medindo a qualidade do teste (4 tópicos)

#### [`Seção 5: Integração Contínua`](#section-5️⃣-ci-and-other-quality-measures)

Diretrizes para CI no mundo JS (9 tópicos)


<br/><br/>


# Seção 0️⃣: A Regra de Ouro

<br/>

## ⚪️ 0. A Regra de Ouro: Design para testes enxutos

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
  calculateVAT(priceWithoutVAT){
    return {finalPrice: priceWithoutVAT * 1.2};
    //Alterar o formato do resultado ou o nome da chave acima fará com que os testes falhem
  }
  //método público
  getPrice(productId){
    const desiredProduct= DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
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

### :clap:  Exemplo Fazendo Certo: Testando muitas permutações de entrada com “mocha-testcheck”

![](https://img.shields.io/badge/🔧%20Exemplo%20usando%20Mocha-blue.svg
 "Exemplos usando Mocha")

```javascript
require('mocha-testcheck').install();
const {expect} = require('chai');

describe('Product service', () => {
  describe('Adding new', () => {
    //isso será executado 100 vezes com diferentes propriedades aleatórias
    check.it('Add new product with random yet valid properties, always successful',
      gen.int, gen.string, (id, name) => {
        expect(addNewProduct(id, name).status).to.equal('approved');
      });
  })
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
receivedPage tree = renderer
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
  //teste está adicionando novos registros novos e atuando apenas nos registros
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
  const result = await addNewProduct({name:'nest'});}
catch (error) {
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
  expect(addNewProduct)).to.eventually.throw(AppError).with.property('code', "InvalidInput");
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

  
# Section 4️⃣: Medindo a eficácia dos testes

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


##  [Bruno Scheufler](https://github.com/BrunoScheufler)

**Função:** Revisor e consultor técnico

Teve o cuidado de revisar, melhorar, usar lint e polir todos os textos

**Sobre:** full-stack web engineer, entusiasta de Node.js e GraphQL
<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Função:** Conceito, design e ótimos conselhos

**Sobre:** Um desenvolvedor front-end esclarecido, especialista em CSS e emojis
