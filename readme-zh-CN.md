<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 为什么本指南可以助你将测试能力提升到下一层级

<br/>

## 📗 45+ 最佳实践：非常全面彻底
这篇文章从 A 到 Z 给出了 JavaScript & Node.js 的稳定性指南。它为你整理总结了市面上大量的最佳博客文章、书籍以及工具。


## 🚢 进阶：在基础上前进 10000 公里
从基础领域跨上前往进阶话题的旅程，包括：在生产环境测试、编译测试、基于属性的测试以及很多策略 & 专业工具。如果你仔细阅读了本指南中的每个字，则你的测试能力将有可能大大超过平均水平。


## 🌐 全栈：前端、后端、CI、任何岗位
先了解通用的测试实践为其他应用层的打下基础。然后，在你自己的领域深入探索：前端/UI、后端、CI 甚至是他们所有的层面。

<br/>

### 作者 Yoni Goldberg
- 一位 JavaScript & Node.js 顾问
- 👨‍🏫 [我的测试网站](https://www.testjavascript.com/) - 在欧洲 & 美国了解 [我的测试网站](https://www.testjavascript.com/)
- [在 Twitter 关注我](https://twitter.com/goldbergyoni/)
- 来 [LA](https://js.la/), [Verona](https://2019.nodejsday.it/), [Kharkiv](https://kharkivjs.org/), [free webinar](https://zoom.us/webinar/register/1015657064375/WN_Lzvnuv4oQJOYey2jXNqX6A)听我的演讲。后续工作待定。
- [我的 JavaScript 质量新闻](https://testjavascript.com/newsletter/) - 战略层面的视野和信息


<br/><br/>

## `内容列表`

#### [`第 0 章：黄金法则`](#第-0-章黄金法则-1)

一条启发所有人的建议（特殊的 1 条）

#### [`第一章：测试剖析`](#第一章-测试剖析)

基础 - 搭建干净的测试（12 条）

#### [`第二章：后端测试`](#第二章-后端测试)

高效地编写后端和微服务的测试（8 条）

#### [`第三章：前端测试`](#第三章-前端测试)

为 UI（包括组件和 E2E 测试）编写测试（11 条）

#### [`第四章：度量测试效果`](#第四章-度量测试效果)

度量测试质量（4 条）

#### [`第五章：持续集成（CI）`](#第五章持续集成ci-1)

JS 领域的 CI 指南（9 条）

<br/><br/>


# 第 0 章：黄金法则

<br/>

## ⚪️ 0 黄金法则：设计瘦测试

:white_check_mark: **建议:** 测试代码与生产代码不同，要使它变得极其简单、短小、没有抽象、扁平化、使人愉悦、瘦。一段测试代码需要做到让人一眼就能看出其目的。

我们的思维空间被主体生产代码充满，因此无法腾出额外的“大脑空间”存放复杂的东西。如果向可怜的大脑中塞进其他复杂代码，将会使得整个部分变慢，而这个部分正是用来解决我们需要测试的问题的。这也是大部分团队放弃测试的原因。

另一方面，测试是一个友好的助手，一个你乐于与之合作、投资小汇报大的助手。科学证明我们有两套大脑系统：系统 1 用于无需努力的活动如在一个空旷的路上开车；系统 2 用于复杂和繁琐的工作如算一道数学表达式。将你的测试为系统 1 设计，当你看一段测试代码时，需要像改 HTML 文档一样简单而不是像计算 2 × (17 × 24)。

为了达到这个目的，我们可以通过选择性价比高、投入产出比（ROI）高的技术、工具以及测试对象。仅测试需要的内容，努力保持其灵活性，某些时候甚至值得去舍弃一些测试来换取灵活性和简洁性。

![alt text](/assets/headspace.png "We have no head room for additional complexity")

下面的大部分建议衍生自这一原则。

### 准备好开始了吗？


<br/><br/>

# 第一章: 测试剖析

<br/>

## ⚪ ️ 1.1 每个测试用例的名称必须包含三个部分

:white_check_mark: **建议:** 一个测试报告需要让不熟悉代码的人（测试、运维）明确知道新的变更是符合需求。因此测试名称需要从**需求层面**描述，并且包含三个部分：

(1) 被测的是什么？（比如 ProductsService.addNewProduct 方法）

(2) 在什么条件和场景下？（比如没有 向该方法传入 price 参数）

(3) 期望的结果是什么？（比如不允许添加该产品）

<br/>


❌ **否则:** 当一个名为“新增产品”的测试用例挂掉之后，你如何准确找到是哪里出问题了？

<br/>

**👇 Note:** 每一条后面会有一个 代码示例，有时候还会放一张图片说明。

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 一个包含三部分的用例名

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

### :clap: 正例: 一个包含三部分的用例名
![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️ 1.2 使用 AAA 模式构造测试内容

:white_check_mark: **建议:** 将你的测试内容划分为三个部分：布置，执行，断言 —— Arrange, Act & Assert (AAA)。这样读者就无需动用脑细胞理解你的测试内容了：

1st A - 准备（Arrange）：一些用于提供上下文的代码。可能包含：构造数据、添加 DB 记录、mocking/stubbing 对象，以及其他的准备代码；

2nd A - 执行（Act）：执行测试单元。通常一行代码。

3rd A - 断言（Assert）：保证得到的值符合预期。通常一行代码。


<br/>


❌ **否则:** 你不仅要花大量时间理解这段代码，而且本该是最简单的部分却耗费了你的大量脑细胞。

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 一个使用 AAA 模式构造的测试用例

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

### :thumbsdown: 反例: 没有分隔、一大坨、难以解释

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




## ⚪ ️1.3 用产品语言描述期望：使用 BDD 形式的断言

:white_check_mark: **建议:** 使用声明的方式写代码，可以使读者无脑 get 到重点。而如果你的代码使用各种条件逻辑包裹起来，则会增加读者的理解难度。因此，我们应尽量使用类似人类语言的形式描述如 `expect` 或 `should` 而不是自己写代码。如果 Chai 和 Jest 不包含你想要的断言，而且这种断言可被高度复用时，你可以考虑 [扩展 Jest 匹配器 (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) 或者写一个 [自定义 Chai 插件](https://www.chaijs.com/guide/plugins/)
<br/>


❌ **否则:** 团队的测试代码会越写越少，而且会用 .skip() 把一些讨厌的测试用例注释掉。

<br/>

<details><summary>✏ <b>代码示例</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")

  ### :thumbsdown: 反例: 为了了解该用例的目的，读者必须快速浏览冗长复杂的代码

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

### :clap: 正例: 快速浏览下面的声明式用例很轻松


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


## ⚪ ️  1.4 坚持黑盒测试：只测 public 方法

:white_check_mark: **建议:** 测试内部逻辑是无意义且浪费时间的。如果你的 代码/API 返回了正确的结果，你真的需要花三个小时时间去测试它内部究竟如何实现的，并且在之后维护这一堆脆弱的测试吗？每当测试一个公共方法时，其私有实现也会被隐式地测试，只有当存在某个问题(例如错误的输出)时测试才会中断。这种方法也称为`行为测试`。另一方面，如果你测试内部方法(白盒方法)—你的关注点将从组件的输出结果转移到具体的细节上，如果某天内部逻辑改变了，即使结果依然正确，你也要花精力去维护之前的测试逻辑，这无形中增加了维护成本。
<br/>


❌ **否则:** 你的代码将会像[狼来了](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf)一样：总是叫唤着“出问题啦”（比如一个因私有变量名改变导致的用例失败）。则人们必然会开始忽略 CI 的通知，直到某天真正的 bug 被忽略……

<br/>
<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 一个无脑测试内部方法的测试用例

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

## ⚪ ️ ️1.5 使用正确的测试替身（Test Double）：避免总用 stub 和 spy

:white_check_mark: **建议:**  测试替身是把双刃剑，他们在提供巨大价值的同时，耦合了应用的内部逻辑 (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[这里有一篇关于测试替身的文章: mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).<br />在使用测试替身前，问自己一个很简单的问题：我是用它来测试需求文档中定义的可见的功能或者可能可见的功能吗？如果不是，那就可能是白盒测试了。<br />举例来说，如果你想测试你的应用程序在支付服务宕机时的合理表现，你可以 stub 支付服务并触发一些“无响应”返回，以确保被测试的单元返回正确的值。这可以测试特定场景下的应用程序的行为、响应、输出结果。你也可以使用一个 spy 来断言当服务宕机时发送了一封电子邮件——这又是一个针对可能出现在需求文档中的行为的检查(“如果无法保存付款，请发送电子邮件”)。反过来，如果你 mock 的支付服务，并确保它被正确调用并传入正确的 JavaScript 类型，那么你的测试重点是内部的逻辑，它与应用的功能关系不大，而且可能会经常变化。

<br/>


❌ **否则:** 任何代码重构都要求搜索代码中的所有 mock 并相应地进行更新。测试变成了一种负担，而不是一个帮手。

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 关注内部实现的 mock
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

### :clap:正例: 使用 spy 关注于测试需求本身，而作为副作用不得不接触内部

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

## ⚪ ️1.6 不要“foo”，使用真实数据

:white_check_mark: **建议:**  生产环境中的 bug 通常是在一些特殊或者意外的输入下出现的——所以测试的输入数据越真实，越容易在早期抓住问题。使用现有的一些库（比如 [Faker](https://www.npmjs.com/package/faker)）去造“假”真数据来模拟生产环境数据的多样性和形式。比如，这些库可以生成真实的电话号码、用户名、信用卡、公司名等等。你还可以创建一些测试(在单元测试之上，而不是替代)生产随机 fakers 数据来扩展你的测试单元，甚至从生产环境中导入真实的数据。想要进阶的话，请看下一条：基于属性的测试。
<br/>


❌ **否则:** 你所有的用例都在 “foo” 之类的输入值下表现正确，结果上线后收到诸如  “[@3e2ddsf ]() . ##’ 1 fdsfds . fds432 AAAA” 之类的输入后挂掉了。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 一个用例因使用非真实数据而通过

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

### :clap:正例: 随机生成真实的输入数据

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

## ⚪ ️ 1.7 基于属性的测试：测试输入的多种组合

:white_check_mark: **建议:** 通常我们只会选择部分的数据样例去测试，即使是使用了上一节讲到的工具去模拟真实数据，我们也只覆盖到了一部分输入的组合(`method(‘’, true, 1), method(“string” , false” , 0)`)。然而在生产环境中，一个拥有 5 个参数的 API，可能会遇到上千种排列组合，而其中的某一种可能会把你的进程搞挂（[见 Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)）。如何自动生成这上千种组合并在它们出问题后 catch 到？基于属性的测试适用于这种需求：向你的测试单元传入所有可能的输入组合，以增加发现 bug 的可能。例如，给定一个方法 —— `addNewProduct(id, name, isDiscount)`，支持属性测试的库将使用一批`(number, string, boolean)`组合调用此方法，比如`(1，“iPhone”，false)`，`(2，“Galaxy”，true)`。您可以使用您最喜欢的测试运行器(Mocha、Jest等)，<br />通常，我们为每个测试选择一些输入样本。即使输入格式类似于现实世界的数据(见子弹“别foo”),我们只涉及几个输入组合(方法(“,真的,1),方法(“字符串”,假”,0)),然而,在生产中,一个API调用与成千上万的5个参数可以调用不同的排列,其中一个可能使我们的流程(见模糊测试)。如果您可以编写一个测试，自动发送1000个不同输入的排列组合，并捕获我们的代码未能返回正确响应的输入，那该怎么办?基于属性的测试就是这样一种技术:通过发送所有可能的输入组合到你的测试单元中，它增加了发现bug的偶然性。例如，给定一个方法—addNewProduct(id, name, isDiscount)—支持库将使用许多(number, string, boolean)组合调用此方法，比如(1，“iPhone”，false)，(2，“Galaxy”，true)。您可以使用您最喜欢的测试运行器(Mocha、Jest等)：比如 [js-verify](https://github.com/jsverify/jsverify) 或者 [testcheck](https://github.com/leebyron/testcheck-js) (文档比较好)。 更新: Nicolas Dubien 在下面的回复中建议 [了解下 fast-check](https://github.com/dubzzz/fast-check#readme) 它提供了更多的能力，似乎更易维护。
<br/>


❌ **否则:** 你无意中选择的输入数据只覆盖了没问题的代码路径。不幸的是，它没有真正发现了 bug。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap:  正例: 使用“fast-check”测试输入的组合

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with Jest")

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

## ⚪ ️ 1.8 snapshot：如果需要，仅使用短的行内快照

:white_check_mark: **建议:** 如果你需要 [快照测试](https://jestjs.io/docs/en/snapshot-testing)，仅使用端快照（比如 3-7 行），并且把它们作为测试的一部分（[内联快照](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)）而不是存放到外部文件中。遵循这条指导原则将确保您的测试保持自解释并且不那么脆弱。

另一方面，“经典”快照教程和工具鼓励我们在一些外部介质上存储大文件（如组件的渲染结果，API 的 JSON 结果），并确保每次运行测试时将新结果与保存的版本进行比较。打个比方，这么做有可能隐式地将我们的测试与包含 3000 个数据值的 1000 行内容关联起来，而这些数据值是测试编写者从来没有读过和考虑过的。这么做将会使得你的用例有 1000 个失败的理由 —— 常常改一行代码就会导致快照失效。这个频率有多高？对于每个空格，注释或少量的 CSS/HTML 更改。不仅如此，失败结果不会给出关于失败的任何提示，因为它只是检查 1000 行内容有没有改动，而且测试编写人员不得不将这一大堆他无法自己验证的长文档作为期望的 true。所有这些都是测试目标不明确、测试目标过多的症状。

这将会使得我们的测试带上一大堆我们以后可能不会再看的数据。这样做有什么问题？你的测试将有无数种理由失败，因为你放入了太多自己不需要关心的结果数据进去，而你又无法抽出足够的精力从结果的 diff 中判断当前表现是否符合期望。

仅在很少的场景下，长外部快照是可以接受的——当测试断言 schema 而不是数据时(提取值并关注其中的字段)，或者当快照的内容很少被更改时。

<br/>

❌ **否则:** 一个 UI 测试挂掉了。代码看起来 ok，屏幕上正确渲染了每个像素，发生了什么？- 你的测试发现跟之前的快照相比，新的快照 markdown 中多了一个空格……

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 为我们的用例耦合看不到的 2000 行代码

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

### :clap: 正例: 期望是可见且集中的
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

## ⚪ ️1.9 不要写全局的 fixtures 和 seeds，而是放在每个测试中

:white_check_mark: **建议:** 参照黄金法则，每条测试需要在它自己的 DB 行中运行避免互相污染。现实中，这条规则经常被打破：为了性能提升而在执行测试前全局初始化数据库([也被称为‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture))。尽管性能很重要，但是它可以通过后面讲的「分组件测试」缓和。为了减轻复杂度，我们可以在每个测试中只初始化自己需要的数据。除非性能问题真的非常显著，那么可以做一定的妥协——仅在全局放不会改变的数据（比如 query）。
<br/>


❌ **否则:** 一部分测试挂了，我们的团队花费大量宝贵时间后发现，是由于两个测试同时改变了同一个 seed 数据导致的。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 用例之间不独立，而是依赖同一个全局钩子来生成全局 DB 数据

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

### :clap: 正例: 每个用例操作它自己的数据集

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

## ⚪ ️ 1.10 不要 catch 错误，expect 它们
:white_check_mark: **建议:** 当你测试一些输入是否会触发错误时，使用 try-catch-finally 测试看起来似乎没问题。但结果会比较奇葩（会隐藏测试的意图和期望结果），并且把 tc 复杂化（比如下面的例子）。

一个更优雅的替代方法是使用 Chai断言 `expect(method).to.throw` (或者 Jest 的: `expect(method).toThrow()`)。必须保证异常包含一个表示错误类型的属性，否则如果只给出一个通用错误，应用程序没法展示足够的信息。
<br/>


❌ **否则:** 从测试报告（如 CI 报告）中查找出错的位置将会很痛苦。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 一个长测试用例，尝试使用 try-catch 断言错误

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

### :clap: 正例: 一个人类可读的期望，它很容易被理解，甚至可被 QA 或技术 PM 理解

```javascript
it.only("When no product name, it throws error 400", async() => {
  expect(addNewProduct)).to.eventually.throw(AppError).with.property('code', "InvalidInput");
});

```

</details>




<br/><br/>

## ⚪ ️ 1.11 为你的测试用例打标签

:white_check_mark: **建议:**  不同的测试需要在不同的场景中执行：快速冒烟、IO 测试、开发者保存或者提交文件后的测试、当一个新的 PR 提交后需要全量执行的端到端测试 等等。你可以用一些 #cold #api #sanity 之类的标签标注测试来达到这个目的，这样你就可以在测试时仅测试想要的子集。如在 mocha 中可以这样唤起用例组 `mocha — grep ‘sanity’` 。
<br/>


❌ **否则:** 执行所有的用例，包括执行大量 DB 查询的用例，开发者做的任何小改动都需要等待很长的时间，将会导致开发者不再想运行测试。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 将用例标记为‘#cold-test’使得用例执行者可以仅执行快的用例 (Cold===没有 IO 的快速测试，可以在开发人员打字时频繁执行)

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

## ⚪ ️1.12 其他常见的优秀测试习惯

:white_check_mark: **建议:**  本文主要讨论与 Node JS 相关的测试建议，或者至少可以用 Node JS 作为例子。然而，本小节整理了一些众所周知的与 Node 无关的技巧。

学习并实践 [TDD 原则](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/)——它对许多人来说非常有价值，但是如果它们不适合你的风格，不要害怕，你不是唯一一个。尝试在写代码之前使用 [red-green-refactor 风格](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html) 编写测试，确保每个测试只检查一项，当你发现一个 bug 时，在修复前新增一个测试在未来检测到它，让每一个测试在变绿之前至少失败一次，快速编写一个简单的代码模块以满足这个测试，然后逐渐将其重构至生产水平，避免任何依赖环境(路径、操作系统等)。

❌ **否则:** 你会错过数十年来智慧的结晶。

<br/><br/>


# 第二章: 后端测试

## ⚪ ️2.1 丰富您的测试组合：不局限于单元测试和测试金字塔

:white_check_mark: **建议:**  [测试金字塔](https://martinfowler.com/bliki/TestPyramid.html)，虽然已经有超过 10 年的历史了，但是它仍是一个很好的相关模型，它提出了三种测试类型，并且影响了大多数开发人员的测试策略。与此同时，大量闪亮的新测试技术出现了，并隐藏在测试金字塔的阴影下。考虑到近 10 年来我们所看到的所有巨变(微服务、云、无服务器)，这个非常老的模型是否仍能适用于所有类型的应用？测试界不应该考虑欢迎新的测试技术吗？

请不要误解，在 2019 年，测试金字塔、TDD、单测仍然是强大的技术，且对于大多数应用仍是最佳选择。但是像其他模型一样，尽管它有用，但是一定会在[某些时候出问题](https://en.wikipedia.org/wiki/All_models_are_wrong)。例如，我们有一个 IOT 应用，将许多事件注入一个 Kafka/RabbitMQ 这样的消息总线中，然后这些事件流入一些数据仓库并被分析 UI 查询。我们真的需要花费 50% 的测试预算去为这个几乎没有逻辑的集成中心化的应用写单测吗？随着应用类型(机器人、密码、Alexa-skills)的多样性增长，测试金字塔可能将不再是某些场景的最佳选择了。

是时候丰富你的测试组合并了解更多的测试类型了（下一节会给你一些小建议），这些类似于测试金字塔的思维模型与你所面临的现实问题更匹配（'嘿，我们的API 挂了，试试消费者驱动的合同测试！'），让您的测试多样化，比如建立基于风险分析的检查模型 —— 评估可能出现问题的位置，并提供一些预防措施以减轻这些潜在风险。

需要注意的是：软件世界中的 TDD 模型面临两个极端的态度，一些人鼓吹到处使用它，另一些人则认为它是魔鬼。 每个说绝对的人都是错的 :]

<br/>


❌ **否则:** 你将错过一些超高投入产出比的工具，比如 Fuzz、lint、mutation 这些工具只需 10 分钟配置就能贡献价值。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: Cindy Sridharan  在她的文章“测试微服务——理智的方式”中提出了一个丰富的测试组合
![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Example: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")


</details>




<br/><br/>

## ⚪ ️2.2 组件化测试可能是最有效的利器

:white_check_mark: **建议:** 应用的每个单元测试仅能覆盖应用的一小部分，覆盖全部会非常麻烦，而端到端测试可以很轻松地覆盖大量区域，但是比较脆弱而且很慢。何不找一个平衡点：写一些比单测大，但是比端到端测试小的测试。组件测试是测试世界的一颗遗珠——它找到了两个模式的最佳平衡点：不错的性能和使用 TDD 模式的可能性 + 真实且强大的覆盖率。

组件测试关注于微服务“单元”，他们反对 API，不 mock 任何属于微服务本身的东西（比如：真实的 DB，甚至是该 DB 的内存版本）但是 stub 所有外部的东西比如调用其他微服务。这么做，我们测试我们部署的部分，由外而内地覆盖应用，节省大量时间。

<br/>


❌ **否则:** 你可能花了好几天写单测，却发现仅得到了 20% 的系统覆盖率。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 使用 Supertest 测试 Express API (快速、覆盖很多层)
![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg
 "Examples with Jest")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 保证新的 release 不会破坏 API 的使用

:white_check_mark: **建议:**  你的微服务有很多的客户，而你为了兼容性运行着该服务的很多版本（keeping everyone happy）。当你改了某个字段后“砰！”，依赖该字段的几个重要的客户炸锅了。服务端满足所有客户的期望是非常难的——另一方面，客户无法发起测试，因为服务端控制着 release。 [Consumer-driven contracts and the framework PACT](https://docs.pact.io/) 诞生了，它以一种破坏性的方式规范了这一流程——不再由服务端定义测试计划，而是客户端决定服务端的测试！PACT 可以记录客户端的期望——“中间人（Broker）”，并放置到共享空间，服务端可以 pull 下来这写期望并利用 PACT 的库在所有的版本中检测是否有被破坏的契约——有客户端的期望没有被满足。通过这种方式，所有客户端-服务端不匹配的 API 将会在 构建/CI 阶段被 catch 到，从而减少你大量的烦恼。

<br/>


❌ **否则:** 所有的变更将带来繁琐的手动测试，导致开发者惧怕发布。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg
 "Examples with PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png )


</details>



<br/><br/>


## ⚪ ️ 2.4 单独测试你的中间件

:white_check_mark: **建议:** 许多人拒绝测试中间件，是因为它们仅占据系统的一小部分而且依赖真实的 Express server。这两个原因都不正确——中间件虽然小，但是影响全部或者大部分请求，而且可以被简单地作为纯函数测试（参数为 {req,res} JS 对象）。测试中间件函数，你仅需调用它，并且 spy ([比如使用 Sinon](https://www.npmjs.com/package/sinon)) {req,res} 的交互以保证函数执行了正确的行为。[node-mock-http](https://www.npmjs.com/package/node-mocks-http) 库更进一步：它还监听了 {req,res} 对象的行为。例如，它可以断言 res 对象上的 http 状态是否符合预期。（看下面的例子）
<br/>


❌ **否则:** Express 中间件上的一个 bug === 所有或者大部分请求的 bug


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap:正例: 隔离地测试中间件，不发出网络调用或唤醒整个Express机器

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

## ⚪ ️2.5 使用静态分析工具度量并指导重构

:white_check_mark: **建议:** 使用静态度量工具可以帮助你客观地提升代码质量并使其可维护。你可以将静态分析工具放在你的 CI 中。除了普通 linting 外，它的主要卖点是结合多文件的上下文来检查质量（例如：发现重复定义）、执行高级分析（例如：代码复杂度）以及跟踪 code issue 的历史和进度。有两个工具供你使用：[Sonarqube](https://www.sonarqube.org/) (2,600+ stars) and [Code Climate](https://codeclimate.com/) (1,500+ stars)

贡献:: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>


❌ **否则:** 由于代码质量差，再新的库和 feature 也无法拯救你的 bug 和性能。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例:   CodeClimate —— 一个用于发现复杂方法的商业工具

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg
 "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png " CodeClimat, a commercial tool that can identify complex methods:")

</details>




<br/><br/>

## ⚪ ️ 2.6 你是否准备好迎接 Node 相关的噪声

:white_check_mark: **建议:** 怪异的是，大部分软件测试仅关注逻辑和数据，但是最糟糕（而且很难减轻）的往往是基础设施问题。例如，你测试过当你的进程存储过载、服务器/进程挂掉时的表现吗？或者你的监控系统会检测到 API 减慢 50% 了吗？为了测试及减轻类似问题，Netflix 设立了 [噪声工程](https://principlesofchaos.org/)。它的目的是为我们的系统在故障问题下的健壮性提供意识、框架及工具。比如，著名的工具之一 [噪声猴子](https://github.com/Netflix/chaosmonkey)，随机地杀掉服务以保证我们的服务仍服务于用户，而不是仅依赖一个单独的服务器（Kubernetes 也有一个版本 [kube-monkey](https://github.com/asobti/kube-monkey) 用于杀掉 pods）。这些工具都是作用于服务器/平台层面，但如果你想测试及生产纯粹的 Node 噪声比如检查你的 Node 进程如何处理未知错误、未知的 promise rejection、v8 内存超过 1.7GB 的限制以及当事件循环经常卡住后你的 UX 是否仍正常运行？为了解决上面提到的这些问题， [node-chaos](https://github.com/i0natan/node-chaos-monkey)(alpha)提供了各种 Node 相关的噪声。
<br/>


❌ **否则:**  墨菲定律一定会无情地砸中你的产品，跑不掉的。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: Node-chaos 可以生成所有类型的 Node.js 问题，因此您可以测试您的应用程序对混乱的适应能力
![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 不要写全局的 fixtures 和 seeds，而是放在每个测试中

:white_check_mark: **建议:** 参照黄金法则，每条测试需要在它自己的 DB 行中运行避免互相污染。现实中，这条规则经常被打破：为了性能提升而在执行测试前全局初始化数据库([也被称为‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture))。尽管性能很重要，但是它可以通过后面讲的「分组件测试」缓和。为了减轻复杂度，我们可以在每个测试中只初始化自己需要的数据。除非性能问题真的非常显著，那么可以做一定的妥协——仅在全局放不会改变的数据（比如 query）。
<br/>


❌ **否则:** 一部分测试挂了，我们的团队花费大量宝贵时间后发现，是由于两个测试同时改变了同一个 seed 数据导致的。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 用例之间不独立，而是依赖同一个全局钩子来生成全局 DB 数据

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

### :clap: 正例: 每个用例操作它自己的数据集

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

# 第三章: 前端测试

## ⚪ ️ 3.1 将 UI 与功能分离

:white_check_mark: **建议:** 当专注于测试组件逻辑时，UI 细节就变成了应该剔除的噪音，这样您的测试就可以集中在纯数据上。实际上，通过抽象从代码中提取所需的数据将降低与图形实现的耦合，仅对纯数据 (vs HTML/CSS 图形细节) 断言，并禁用会拖慢速度的动画。您可能会试图避免渲染，仅测试 UI 后面的部分(例如，服务、操作、存储)，但这将导致测试与实际情况不太相符，「正确的数据根本无法到达 UI」这种问题就无法发现。


<br/>

❌ **否则:** 您的测试的纯计算数据可能在 10ms 内就准备好了，但是由于一些花哨和无关的动画，整个测试将持续500ms (100个测试 = 1分钟)


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 分离 UI 细节

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg
 "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg
 "Examples with react-testing-library")

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

### :thumbsdown: 反例: 混杂了 UI 细节和数据的断言
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


## ⚪ ️ 3.2 使用不太容易改变的属性去查询 HTML 元素

:white_check_mark: **建议:**通过不太同意受图形变更印象的属性查询 HTML 元素（例如 form label，而不是 CSS selector）。如果指定的元素没有这样的属性，则创建一个专用的测试属性，如“test-id-submit-button”。这样做不仅可以确保您的功能/逻辑测试不会因为外观变化而中断，而且整个团队可以清楚地看到，测试使用了这个元素和属性，不应该删除它。

<br/>

❌ **否则:** 你想要测试一个跨越许多组件、逻辑和服务的登录功能，一切都设置得很完美——stub、spy、Ajax 调用都是隔离的。所有似乎是完美的。然后测试失败，因为开发者将 div CSS 类从 'thick-border' 更改为 'thin-border'。

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 使用专用的 attrbiute 查询元素进行测试

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg
 "Examples with React")

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

### :thumbsdown: 反例: 依赖 css attribute
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

## ⚪ ️ 3.3 只要有可能，使用真实且完全渲染的组件进行测试

:white_check_mark: **建议:** 只要大小合适，就像用户那样从外部测试组件，完全渲染 UI，对其进行操作，并断言呈现的 UI 的行为符合预期。避免各种 mock、部分和 shallow render——这么做可能会由于缺乏细节导致未捕获的 bug，并且由于测试与内部的混在一起将增加维护成本(参见小结“多用黑盒测试”)。如果其中一个子组件明显拖慢测试(如动画)或使很难配置，可以考虑主动用伪组件替换它。

综上所述，需要注意的是: 这种技术适用于封装一定数量子组件的中小型组件。如果一个组件包含太多的子组件，那么将很难对失败测试进行定位(分析根本原因)，并且可能会变得过于缓慢。在这种情况下，只需针对胖父组件编写少量测试，而针对其子组件编写更多测试。

<br/>

❌ **否则:** 之前通过调用组件的私有方法来测试组件的内部状态。后续重构组件时你必须重构所有测试。你真的有能力进行这种程度的维护吗?


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 操作一个充分渲染的真实组件

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg
 "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Enzyme-blue.svg
 "Examples with Enzyme")

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

### :thumbsdown: 反例: 通过 shallow render 测试伪组件
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


## ⚪ ️ 3.4 不要 sleep，使用框架内置的对 async 事件的支持。并且尝试提效。

:white_check_mark: **建议:** 在许多情况下，被测试单元的完成时间是未知的 (例如，animation 挂起了元素表现 )——在这种情况下，不要 sleep (例如setTimeout)，并是使用大多数框架提供的更靠谱的方法。一些库允许等待操作 (例如 [Cypress .request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting))，另一些库提供用于等待的 API，如 [@testing-library/dom 方法 wait(expect(element))](https://testing-library.com/docs/guide-disappearance)。有时一种更优雅的方法是 stub 慢的资源，比如API，然后一旦响应时间变得确定，组件就可以显式地重新渲染。当依赖一些 sleep 的外部组件时，[加快时钟](https://jestjs.io/docs/en/timer-mocks)可能会提供帮助。sleep 是一种需要避免的模式，因为它会迫使您的测试变得缓慢或有风险(当等待的时间太短时)。当 sleep 和轮询不可避免且测试框架原生不支持时，一些npm库 (如 [wait-for-expect](https://www.npmjs.com/package/wait-for-expect)) 可以帮助解决半确定性问题。
<br/>

❌ **否则:** 当 sleep 时间长时，测试速度会慢一个数量级。当尝试缩短 sleep 时间时，如果被测试的单元没有及时响应，则测试将失败。这时你不得不在脆弱的测试和糟糕的性能之间进行权衡。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: E2E API 仅在异步完成后 resolve (Cypress)

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg
 "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg
 "Examples with react-testing-library")

```javascript
// using Cypress
cy.get('#show-products').click()// navigate
cy.wait('@products')// wait for route to appear
// this line will get executed only when the route is ready

```

### :clap: 正例: 测试库等待 DOM 元素

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

### :thumbsdown: 反例: 自己写 sleep 代码
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

## ⚪ ️ 3.5 观察内容是如何通过网络提供的

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg
 "Examples with Lighthouse")

✅ **建议:** 使用一些活动监视器，以确保在真实网络下的页面负载是最优的——这包括了一些用户体验问题：如缓慢的页面负载或未压缩的包。检查工具市场很丰富：像 [pingdom](https://www.pingdom.com/)、AWS CloudWatch、[gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) 这样的基础工具可以很容易地配置来监视服务器是否处于活动状态，并在合理的 SLA 下响应。不过这只解决了表面上的问题，因此最好选择专门用于前端的工具 (如 [lighthouse](https://developers.google.com/web/tools/lighthouse/)、[pagespeed](https://developers.google.com/speed/pagespeed/insights/)) 以进行更全面的分析。注意力应该放在症状和直接影响用户体验的指标上，比如页面加载时间、[有意义的绘制](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint)、[页面可交互(TTI) 时间](https://calibreapp.com/blog/time-to-interactive/)。最重要的是，你还可以关注技术原因，比如确保内容被压缩、第一个字节的时间、优化图像、确保合理的 DOM 大小、SSL 和许多其他方面。建议在开发期间使用这些丰富的监视器，作为 CI 的一部分，最重要的是在生产服务器/CDN上 24x7 使用它们。

<br/>

❌ **否则:** 在精心设计了一个UI、通过了100%的功能测试并进行了复杂的打包之后，用户体验却因为 CDN 的错误配置变得糟糕而缓慢。

<br/>

<details><summary>✏ <b>代码示例</b></summary>

### :clap: 正例: Lighthouse 页面加载检查报告

![](/assets/lighthouse2.png "Lighthouse page load inspection report")


</details>


<br/>

## ⚪ ️ 3.6 stub 古怪或缓慢的资源如后端 API

:white_check_mark: **建议:** 当编写你的主流测试 (不是 E2E 测试) 时，避免接触任何超出你职责和控制范围的资源，如后端 API，而是使用 stub(即测试替身)。使用一些测试替身库 (如[Sinon](https://sinonjs.org/)、[test double](https://www.npmjs.com/package/testdouble) 等) 来 stub API 响应，而不是真正的对API的网络调用。最大的好处是防止出现故障——测试或预发环境下 api 的定义不是很稳定，尽管组件的表现正确(生产环境不适合测试，它通常会限制请求)，但有时会请求失败。通过 stub 允许模拟各种 API 行为，比如当没有找到数据或 API 抛出错误时测试组件行为。最后但并非最不重要的原因是，网络调用将大大降低测试速度。

<br/>

❌ **否则:** 测试的平均时长不在是几毫秒，一个经典的 API 调用花费 100ms+，这使得每个用例变慢 ~20x。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: stub 或拦截 API 调用
![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg
 "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg
 "Examples with react-testing-library")

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

## ⚪ ️ 3.7 写几个跨越整个系统的端到端测试

:white_check_mark: **建议:** 虽然 E2E (端到端) 通常表示在真实浏览器中进行 UI 测试(见 3.6)，但某些情况下，它们表示覆盖整个系统的测试，包括真正的后端。后一种测试非常有价值，因为它们涵盖了前端和后端之间的集成 bug，这些 bug 可能是由于沟通 schema 时产生误会导致的。它们也是一种有效的方法来发现 backend-to-backend 集成问题 (例如微服务 A 将错误的信息发送给微服务 B) 甚至检测部署失败，目前后端没有像 [Cypress](https://www.cypress.io/) 和 [Pupeteer](https://github.com/GoogleChrome/puppeteer) 友好的 UI 框架一样友好且成熟的 E2E 框架。这种测试的缺点是，配置一个包含如此多组件的环境的成本很高，而且大多数组件都很脆弱——假设有 50 个微服务，即使其中一个失败，整个 E2E 也会失败。出于这个原因，我们应该少用这种技术，大概1-10个就够了。也就是说，即使是少量的 E2E 测试也很有可能捕获它们所针对的问题——部署和集成故障。建议在与生产环境相似的预发运行它们。

<br/>

❌ **否则:** UI 可能在测试它的功能上投入了大量的精力，但最后才意识到后端返回的有效负载 (UI 必须使用的数据模式) 与预期有很大的不同。

<br/>

## ⚪ ️ 3.8 通过复用登录凭证提速 E2E 测试

:white_check_mark: **建议:** 在涉及真实的后端并依赖有效的用户 token 进行 API 调用的 E2E 测试中，我们没有必要将测试按照「创建用户并在每个请求中登录」的级别隔离。相反，在测试执行开始之前只登录一次 (即 before-all hook)，将 token 保存在一些本地存储中，并在请求之间复用它。这似乎违反了核心测试原则之一——保持测试的自治，不要耦合资源。虽然这是一个合理的担忧，但在 E2E 测试中，性能是一个关键问题，在执行每个用例之前创建 1-3 个 API 请求可能会大大增加执行时间。复用凭证并不意味着测试必须基于相同的用户记录——如果依赖于用户记录 (例如测试用户付款历史记录)，那么要确保生成这些记录作为测试的一部分，并避免与其他测试共享它们。还要记住后端是可以 fake 的——如果你想重点测试前端，那么最好隔离它，然后 stub 后端 API (见 3.6 节)。

<br/>

❌ **否则:** 给定 200 个测试用例，假设登录耗时 100ms，则需要花费 20s 仅仅用于一遍遍登录。

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 在 before-all 而不是 before-each 中登录

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg
 "Using Cypress to illustrate the idea")

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

## ⚪ ️ 3.9 创建一个 E2E 冒烟测试，仅仅走一遍网站地图

:white_check_mark: **建议:** 为了监控生产环境以及开发时的完整性检查，运行一个 E2E 测试，该测试访问所有或大部分站点页面并确保没有被中断。这种测试投资回报率极高，因为它非常容易编写和维护，但可以检测任何类型的故障，包括功能、网络和部署问题。其他类型的冒烟和完备性检查并没有那么可靠和详尽——一些 ops 团队只是 ping 主页 (生产)，或者开发人员运行一些集成测试无法发现打包和浏览器问题。毫无疑问，烟雾测试不会取代功能测试，而只是作为一个快速的烟雾探测器。

<br/>

❌ **否则:** 一切似乎都很完美，所有的测试都通过了，生产环境健康检查也是 OK 的，但是支付组件有一些打包问题，只有 `/Payment` 路径没有渲染。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 一个跑一遍所有页面的冒烟测试
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

## ⚪ ️ 3.10 将测试以实时协作文档的形式公开

:white_check_mark: **建议:** 除了提高应用程序的可靠性，测试还带来了另一个极具吸引力的场景——作为实时应用文档。由于测试本质上使用的是一种技术含量较低的产品 / UX 语言，因此使用正确的工具可以将他们作为一个沟通媒介，便捷地协调了所有的同事——开发人员和他们的客户。例如，一些框架允许使用人类可读的语言来表达流程和期望 (即测试计划)，这样任何相关人员，包括产品经理，都可以阅读、批准和协作测试，这时测试就成为了实时的需求文档。这种技术也被称为“验收测试”，因为它允许客户用简单的语言定义他的验收标准。这是最纯粹的 [BDD (行为驱动测试)](https://en.wikipedia.org/wiki/Behavior-driven_development)。支持此功能的流行框架之一是 [Cucumber](https://github.com/cucumber/cucumber-js)，它具有 JavaScript 风格，参见下面的示例。另一个相似但不同的场景是 [StoryBook](https://storybook.js.org/)，它可以将 UI 组件公开为一个图形化的目录，用户可以浏览每个组件的各种状态(如一个栅格组件的 w/o filter，使其渲染多行或者 0 行，等等)，查看它的展示形式，以及如何触发状态——这也可以提供给产品人原，但主要是作为实时文档提供给消费这些组件的开发人员。

❌ **否则:** 你在测试上耗费了大量的资源，如果不利用这项投资来获取更大的价值，是很可惜的。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 使用 cucumber-js 以人类语言描述测试

![](https://img.shields.io/badge/🔨%20Example%20using%20Cocumber-blue.svg  "Examples using Cucumber")
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

### :clap: 正例: 使用 Storybook 展示我们的组件及其各种状态和输入
![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")


</details>




## ⚪ ️ 3.11 使用自动化工具检测可视化问题


:white_check_mark: **建议:** 设置自动化工具来抓取 UI 截屏，并在变更后检测内容重叠或中断等可视化问题。这样不仅可以确保数据的正确性，而且用户可以方便地看到它。这种技术没有被广泛采用，我们的测试思维更倾向于功能测试，但它代表了真实的用户体验，而且可以轻易地发现跨多设备类型的 UI bug。目前部分免费工具可以提供一些基础功能——生成和保存屏幕截图以供肉眼检查。虽然这种方法对于小应用来说可能已经足够了，但是它的缺陷与任何其他手动测试一样<br />：任何变更后都需要耗费人力来处理。另一方面，由于缺乏清晰的定义，自动检测 UI 问题非常具有挑战性——这就是“视觉回归”领域解决这个难题的切入点：对比旧 UI 与最新的更改并检测差异。一些开源/免费的工具可以提供这个能力 (例如: [wraith](https://github.com/BBC-News/wraith)、PhantomCSS) 但可能安装耗时比较久。一些商业工具 (如  [Applitools](https://applitools.com/)、[Percy.io](https://percy.io/)) 则更进一步，它们简化了安装过程，并封装了高级特性，如管理 UI、告警、通过去除“视觉噪音”(如广告、动画) 进行智能捕获，甚至可以分析引发问题的 DOM/css 变化的根本原因。

<br/>

❌ **否则:** 如何评判这样的页面好不好：内容显示正确 (100%测试通过)、加载迅速但有一半内容区域隐藏?


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 一个典型的视觉回归 —— 右侧内容展示异常

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>


### :clap: 正例: 配置 wraith 来捕获并比对 UI 快照

![](https://img.shields.io/badge/🔨%20Example%20using%20Wraith-blue.svg
 "Using Cypress to illustrate the idea")

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

### :clap: 正例: 使用 Applitools 获取快照比对以及进阶特性

![](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg
 "Using Cypress to illustrate the idea") ![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg
 "Using Cypress to illustrate the idea")

```javascript
import * as todoPage from '../page-objects/todo-page';

describe('visual validation', () => {
  before(() => todoPage.navigate());
  beforeEach(() => cy.eyesOpen({ appName: 'TAU TodoMVC' }));
  afterEach(() => cy.eyesClose());

  it('should look good', () => {
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


# 第四章: 度量测试效果

<br/><br/>

## ⚪ ️ 4.1 通过足够的覆盖率获取自信，~80% 看起来是个幸运数字

:white_check_mark: **建议:** 测试的目的是为了获取足够的自信去快速迭代，显然，越多代码被测试到，则我们团队越自信。覆盖率用于度量多少代码行（以及分支、语句等）被测试执行到。所以多少够了？10-30% 明显无法证明项目的正确性，而 100% 则非常耗时并且可能会使得你关注太多细枝末节的代码。我们的答案是取决于应用的类型——如果你正在建造 A380 的下一代，那么 100% 是必须的；而对于一个漫画网站，50% 可能太多了。尽管大部分测试拥趸们强调覆盖率门槛是依赖所处环境的，但是他们大部分提到 80% 是一个不错的规则（[Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)）大概可以满足大部分应用。

实现建议：你可能想在你的 CI 中设置覆盖率门槛，并阻止不满足要求的构建（也可以为每一个组件设置门槛，见下面的例子）。另外，我们可以监测构建的覆盖率下降（当新提交的代码的覆盖率较低时）——这将推动开发者提升或者至少保持被测试的代码数。说了这么多，覆盖率仅仅是一个可量化的度量值，它并不能确切地证明你的测试的健壮性，你也可能被它骗到（见下一节内容）。

<br/>


❌ **否则:**  信心和数字是相辅相成的，如果无法确保你的测试已经覆盖了了大部分的系统，那你将会害怕，害怕会让你慢下来。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 一个经典的覆盖率报告
![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: 正例: 为每个组件设置覆盖率 (使用 Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg
 "Using Cypress to illustrate the idea")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>



<br/><br/>

## ⚪ ️ 4.2 检查覆盖率报告，以发现未覆盖的区域和其他奇怪的地方

:white_check_mark: **建议:** 有些问题隐藏在雷达之下，而使用传统工具很难发现它们。它们通常不是真正的 bug，大多数情况下是应用的怪异表现，而这种表现可能造成严重影响。例如，一些代码区域几乎不会或很少被调用——你以为“PricingCalculator”类只会设置产品价格，结果他几乎不会被调用，即使我们的数据库中有 10000 件商品以及很多交易……代码覆盖率报告可以帮助你发现应用是否按照你的期望执行。初次之外，它高亮了那些类型的代码没有被测试到——80% 的代码被测试并不能说明你的关键部分被覆盖到。生成报告很简单——只需在构造或测试覆盖率时跑你的应用，然后看看花花绿绿的报告来告诉你每一片代码区域被多频繁地调到。如果你花一点时间看看这些数据——你可能会发现一些问题。

<br/>


❌ **否则:** 如果你不知道你的代码中有哪些部分没有被测试到，则你没法准确定位问题的来源。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 这份覆盖率报告有什么问题？基于一个真实的场景，我们跟踪了 QA 中的应用程序使用情况，并发现了一些有趣的登录模式(提示:登录失败的数量是不成比例的，有些地方显然有问题。最终表现为一些前端的 bug 不断触发后端登录API)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report? based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

</details>


<br/><br/>

## ⚪ ️ 4.3 使用「变异测试」度量逻辑覆盖率

:white_check_mark: **建议:**  传统覆盖率通常是骗人的：它可能显示了 100% 的代码覆盖率，但是你的所有的函数都没有返回正确的结果。怎么回事？它只是简单地度量你的测试代码访问过哪些代码行，而不会检查 tc 是否真正地测试了什么——断言了正确的返回。<br />基于变更的测试适用于这个需求。它度量了真正被**测试过**的代码而不是仅仅被**访问过**的。[Stryker](https://stryker-mutator.io/) 是一个用于变异测试的 JavaScript 库，而它的实现很巧妙：

(1) 它有意地改变代码并「植入 bug」。例如代码 newOrder.price===0 会被改成 newOrder.price!=0，这个 “bug”即成为变异。

(2) 它跑一遍用例，如果所有都成功了则说明有问题——这些用例没有真正实现他们发现 bug 的目的，这些变异即所谓的“存活”了。如果用例失败了，那么很棒，变异被杀掉了。

相对于传统覆盖率，得知所有或者大部分变异被杀掉会给予你更高的信心，而两者花费的时间差不多。
<br/>


❌ **否则:** 你会误以为 85% 的覆盖率代表你的测试会发现你代码中的 85% 的 bug.

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 100% 覆盖率, 0% 被测试到

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

### :clap: 正例: Stryker 报告，一个编译测试工具，发现并统计没有被测试到的代码（变异）

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>



<br/><br/>

## ⚪ ️4.4 使用 Test linter 防止测试代码问题

:white_check_mark: **建议:**  有一系列 ESLint 插件用于检查测试代码的风格并发现问题。比如 [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) 会警告一个写在 global 层的用例（不是 describe() 语句的子级），或者当测试被 [skip](https://mochajs.org/#inclusive-tests) 时会发出警告，这可能会导致你错误地认为所有测试都通过了。类似的，[eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) 可以在一个用例没有任何断言（不覆盖任何内容）时给出警告。

<br/>


❌ **否则:** 当你满足于 90% 的代码覆盖率和 100% 的绿色用例时，发现很多测试啥都没断言，很多测试直接被 skip 掉了。但愿你没有基于这个错误认知做过额外的构建。


<br/>
<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 一个充满错误的测试用例，幸运的是所有都被 linter 捕获了

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


# 第五章：持续集成（CI）以及其他质量度量手段

<br/><br/>

## ⚪ ️ 5.1 丰富你的 linter 并丢弃有 lint 问题的构建

:white_check_mark: **建议:**  只需五分钟配置，即可免费获取自动保护代码的工具来捕获代码中的显著问题。Lint 不再只是样式工具，现在的 linter 可以捕获很多严重的问题比如 error 没有被正确抛出以及信息丢失。在基础 rule(如 [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) 或 [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb))之上，我们可以考虑加入一些特殊的 linter，例如 [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) 可以发现用例没有写断言，[eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) 可以发现 promise 没有 resolve，[eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) 可以发现可能被 DOS 攻击的正则表达式，以及 [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) 擅长在代码使用 V8 核心方法后给出告警，如 Lodash._map(…)。

<br/>

❌ **否则:** 在某个下雨天，你的代码一直 crash 而日志没有显示错误堆栈信息。到底发生了什么？你的代码错误地抛了一个非 error 的对象，而堆栈 trace 丢失了，真让人头秃……只需要五分钟配置一个 linter 来发现这个书写错误即可节省你大量的时间。

<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :thumbsdown: 反例: 出错的对象被错误地抛出，没有显示这个错误的堆栈信息。好在 ESLint 捕获到了后面的生产错误
![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>




<br/><br/>

# ⚪ ️ 5.2 通过本地的开发 CI 来缩短反馈循环

:white_check_mark: **建议:**  在本地使用一个包含测试、Lint、稳定性检查等功能的 CI 可以帮助开发者迅速得到反馈并缩短[反馈循环](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/)。因为一个有效的测试流程包含很多迭代循环 (1) 尝试 -> (2) 反馈 -> (3) 重构。所以反馈越快，开发者可以在每个模块中可以执行的迭代就越多，并且可以得到更好的结果。反过来，如果反馈来得很慢，则一天只能执行很少的迭代，则团队可能会因急需执行下一个主题/任务/模块 而不再提炼当前模块。

目前已有一些 CI 供应商 (如: [CircleCI load CLI](https://circleci.com/docs/2.0/local-cli/)) 支持在本地执行 CI。一些商业工具如 [wallaby](https://wallabyjs.com/) 为开发原型提供了非常有用的测试能力。或者你可以仅仅在 package.json 中添加 npm 脚本来跑一些质量命令——使用工具如 [concurrently](https://www.npmjs.com/package/concurrently) 来并行执行，并在任何工具失败后抛出非 0 exit code。则开发者只需执行一个命令（如 `npm run quality` ）来快速获取反馈。可以用 githook 来取消没有通过质量检查的提交（[husky](https://github.com/typicode/husky) 可以帮到你）。
<br/>


❌ **否则:** 当质量检查结果在提交后第二天才收到反馈，则测试不再是开发的一部分了。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap:  正例: 用于执行代码质量检查的 npm 脚本，在主动触发或用户尝试提交新代码时并行执行。

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

# ⚪ ️5.3 在真实的生产环境镜像中执行端到端测试

:white_check_mark: **建议:**   端到端测试是每个 CI 的主要挑战——实时创建一个生产环境镜像并带上所有相关的云服务是很费时费力的。你需要找到最佳的折中：[Docker-compose](https://serverless.com/) 通过一个文本文件将独立的 docker 环境放置到相同的容器中，但是背后的技术（如网络、构建模型）与真实世界有所差别。你可以将其与[‘AWS Local’](https://github.com/localstack/localstack)结合在真实的 AWS 服务中使用。如果你使用了 [serverless](https://serverless.com/) 框架， [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html)允许本地调用 FaaS 代码。

Kubernetes 强大的生态系统还没有形成一个易用的标准工具用于本地和 CI 镜像，虽然经常推出许多新的工具。一种方法是使用像 [Minikube](https://kubernetes.io/docs/setup/minikube/) 和 [MicroK8s](https://microk8s.io/) 这样的工具来运行一个“最小化的 kubernetes”，这些工具更接近实际，但是开销更少。另一种方法是在远程的 “真实 Kubernetes” 上进行测试，一些 CI 提供商(例如 [Codefresh](https://codefresh.io/))与 Kubernetes 环境进行了本地集成，使得在真实环境中运行 CI 管道变得很容易，其他的则允许针对远程 Kubernetes 进行自定义脚本。

<br/>


❌ **否则:** 生产和测试环境使用不同的技术，需要维护两个部署模型，并将开发人员和 ops 团队分隔开来。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap:  正例: 动态生成 Kubernetes 集群的 CI 管道 <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">(贡献: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

```yaml
deploy:
stage: deploy
image: registry.gitlab.com/gitlab-examples/kubernetes-deploy
script:
- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN
- kubectl create ns $NAMESPACE
- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"
- mkdir .generated
- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"
- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"
- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml
- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml
environment:
name: test-for-ci
```

</details>





<br/><br/>

## ⚪ ️5.4 并行测试工作
:white_check_mark: **建议:**  只要操作合理，测试是你 7x24 小时的朋友，为你提供非常及时的反馈。实际上，在单个线程上执行 500 个单元测试可能需要很长时间。幸运的是，现代测试运行器和 CI 平台（如 [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) 和 [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)）可以将测试并行化为多个进程，以显著缩短反馈时间。 一些CI供应商也支持跨容器并行化测试，这进一步缩短了反馈循环。 无论是在本地多个进程，还是在使用多台机器的某些云 CLI 上 - 并行化需要保证测试用例的独立性，因为每个用例可能在不同的进程上运行。


❌ **否则:** 在推送新代码 1 小时后获得测试结果，而你已经在写下一个 feature 了。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: Mocha parallel & Jest 轻松地加速了传统的 Mocha，感谢并行测试([贡献:JavaScript测试运行基准](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))
![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>




<br/><br/>

## ⚪ ️5.5 使用许可证和抄袭检查避免法务问题
:white_check_mark: **建议:** 许可和抄袭问题可能不是您现在主要关注的问题，但为什么不在10分钟内加上这个能力呢？ 许多 npm 包，如 [license check](https://www.npmjs.com/package/license-checker) 和 [plagiarism check](https://www.npmjs.com/package/plagiarism-checker)（商业的，但是有免费选项）可以很容易地加入您的 CI 管道，并检查一些坑：依赖限制性许可证或从Stackoverflow复制粘贴的代码，或者很明显地侵犯了某些版权。

❌ **否则:** 无意中，开发人员可能会使用包含不适当许可证的软件包或复制粘贴商业代码并遇到法务问题。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例:
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

## ⚪ ️5.6 持续检查有漏洞的依赖
:white_check_mark: **建议:**  即使是最知名的依赖（如 Express）也存在已知的漏洞。 这可以通过使用社区工具（如 [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit)）或商业工具（如 [snyk](https://snyk.io/)）（也提供免费的社区版本）轻松解决。 可以在每次构建时都可以从 CI 调用他俩。

❌ **否则:** 在没有专用工具的帮助下保持代码远离漏洞，将需要不断关注有关新威胁的发布信息。 这相当乏味。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: NPM Audit 结果
![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>




<br/><br/>

## ⚪ ️5.7 自动升级依赖

:white_check_mark: **建议:**  Yarn 和 npm 最新推出的 package-lock.json 引入了一个严峻的问题（本意是好的，但却通往地狱） - 默认情况下，包将不再得到更新。即使团队使用 'npm install' 和 'npm update' 也不会获得任何更新。这理想情况下会导致依赖了不太好的包版本，或者最坏的情况引入易受攻击的代码。现在，团队依靠开发人员的善意和记忆来手动更新 package.json 或手动使用像 [ncu](https://www.npmjs.com/package/npm-check-updates) 这样的工具。而更靠谱的方式是自动获取最可靠的依赖版本，虽然没有最优解决方案，但有目前两种可能的自动化方式：

（1）CI 可以使 具有过时依赖 的构建失败 - 使用 '[npm outdated](https://docs.npmjs.com/cli/outdated)' 或 'npm-check-updates（ncu）' 等工具。这样做将强制开发人员更新依赖项。

（2）使用商业工具，他们可以扫描代码并自动发送更新依赖的 PR。剩下的一个有趣的问题是依赖更新策略—— 每个补丁的更新都会产生太多的开销，而大版本发布时更新可能会指向一个不稳定的版本（许多软件包在发布后的几天内被爆出漏洞，请[参阅](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope 事件）。

有效的更新策略可能允许一些“归属期”——让代码滞后 @latest 一段时间和版本，再将本地副本视为过时（例如本地版本为1.3.1且存储库版本为1.3.8）。

<br/>


❌ **否则:** 您的生产环境运行的包已被其作者明确标记为有风险。


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap:  正例: 可以手动或在 CI 管道中使用 [ncu](https://www.npmjs.com/package/npm-checkupdates) 来检测代码在最新版本之后的滞后程度

![alt text](assets/bp-27-yoni-goldberg-npm.png "Nncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")


</details>


<br/><br/>

## ⚪ ️ 5.8 其他的，与 Node 无关的，CI 小建议

:white_check_mark: **建议:**  本文的重点是多少与 Node JS 有点关系的测试建议。但是，本节整理了一些众所周知的与 Node 无关的技巧：

1. 使用声明性语法。这是大多数工具的唯一选择，但旧版本的 Jenkins 允许使用代码或 UI。
1. 选择具有本地 Docker 支持的工具。
1. 尽快失败，先运行最快的测试。设立一个“冒烟测试” 阶段/里程碑，对多个快速检查工具（如 linting，单元测试）进行分组，为代码提交者提供快速反馈。
1. 设法方便地浏览构建的所有产出，包括测试报告，覆盖率报告，变异报告，日志等。
1. 为每个事件创建多个管道/作业，提取他们的相同工作。例如，为功能分支的提交配置一个作业，为 master PR配置另一个。（大多数工具提供了一些代码重用的机制）
1. 永远不要在工作声明中加入机密信息，从机密库或工作的配置中获取它。
1. 在发布构建中明确目标版本号
1. 仅构建一次并对整个构建执行所有检查（例如Docker镜像）
1. 在一个临时的环境中进行测试，这个环境不会在不同构建之间产生状态漂移。缓存 node_modules 可能是惟一的例外。

<br/>


❌ **否则:** 你会错过多年来智慧的结晶

<br/><br/>

## ⚪ ️ 5.9 构建模型（Matrix）：使用多个 Node 版本执行同一个 CI 流程

:white_check_mark: **建议:** 质量检查是用于发现意外，你覆盖的部分越多，你就越可能尽早地发现问题。 在开发包或运行具有各种配置和 Node 版本的多客户生产环境时，CI 必须在所有配置的组合上运行测试管道。 例如，假设我们的某些客户使用 MySQL，另一批客户使用 Postgres。一些 CI 工具支持一种称为“Matrix”的功能，该功能可以针对 MySQL、Postgres 和多个 Node 版本（如8、9、10）的所有组合执行测试。 只要配置即可完成而无需任何额外工作。 其他不支持 Matrix 的 CI 可能可以通过扩展或一定调整来实现这个功能。
<br/>


❌ **否则:** 在辛辛苦苦写完所有用例编写之后，怎么可以因为配置问题而让漏洞溜进来？


<br/>

<details><summary>✏ <b>代码示例</b></summary>

<br/>

### :clap: 正例: 使用 Travis (CI 提供商) 构建配置，在多个 Node 版本上运行相同的测试

```yaml
language: node_js
node_js:
  - "7"
  - "6"
  - "5"
  - "4"
install:
  - npm install
script:
  - npm run test
```

</details>

<br/><br/>

# Team



## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Role:** 作者

**About:** 我是一名独立顾问，与 500 强企业和创业公司合作，完善他们的 JS 和 Node.js 应用。与其他任何话题相比，我更感兴趣的是掌握测试的艺术。我也是[Node.js 最佳实践](https://github.com/goldbergyoni/nodebestpractices)的作者。

<br/>

**Workshop:** 👨‍🏫 是否想在您自己的办公室中（欧洲和美国）学习所有这些实践和技术？ [在此处注册我的测试工作室]（https://testjavascript.com/）
<br/>

**关注:**

* [🐦 Twitter](https://twitter.com/goldbergyoni/)
* [📞 Contact](https://testjavascript.com/contact-2/)
* [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>


##  [Bruno Scheufler](https://github.com/BrunoScheufler)

**角色:** 技术评审人和顾问

致力于修改、完善、备注及优化所有文字。

**关于我:** 全栈 Web 工程师，Node.js 和 GraphQL 爱好者
<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Role:** 概念，设计以及提供好的建议

**About:** 优秀的前端开发者，CSS 专家，emoji 怪

## [Kyle Martin](https://github.com/js-kyle)

**Role:** 帮助保持本项目的运行，并审查与安全性有关的实践

**About:** 喜欢从事 Node.js 项目和 Web 应用安全性的工作。
