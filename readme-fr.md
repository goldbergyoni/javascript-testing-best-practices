<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 Pourquoi ce guide peut faire passer vos compétences de test au niveau supérieur

<br/>

## 📗 46+ bonnes pratiques : complet et exhaustif

Ceci est un guide complet pour Javascript & Node.js de A à Z. Il résume et organise pour vous les meilleurs articles de blogs, livres et outils du marché

## 🚢 Avancé : va bien au-delà des bases

Embarque pour un voyage qui va bien au-delà des bases et aborde des sujets avancés tels que les tests en production, les tests de mutations, les tests basés sur les propriétés et de nombreux autres outils stratégiques et professionnels. Si vous lisez chaque mot de ce guide, vos compétences de tests seront probablement bien au-dessus la moyenne.

## 🌐 Full-stack: front, backend, CI ...

Commence par comprendre les pratiques de tests omniprésentes qui sont à la base de tout niveau d'application. Ensuite, plonge dans ton domaine de prédilection : frontend/UI, backend, CI ou peut-être tous ça ?

<br/>

### Écrit par Yoni Goldberg

- Un consultant JavaScript & Node.js
- 📗 [Les tests Node.js & JavaScript de A à Z](https://www.testjavascript.com) - Mon cours en ligne complet avec plus de [10 heures de video](https://www.testjavascript.com), 14 types de tests et plus de 40 bonnes pratiques
- [Suis-moi sur Twitter ](https://twitter.com/goldbergyoni/)

<br/>

### Traductions - Lis dans la langue de ton choix
- 🇬🇧[Anglais](readme.md)
- 🇨🇳[Chinois](readme-zh-CN.md) - Traduit par [Yves yao](https://github.com/yvesyao)
- 🇰🇷[Coréen](readme.kr.md) - Traduit par [Rain Byun](https://github.com/ragubyun)
- 🇵🇱[Polonais](readme-pl.md) - Traduit par [Michal Biesiada](https://github.com/mbiesiad)
- 🇪🇸[Espagnol](readme-es.md) - Traduit par [Miguel G. Sanguino](https://github.com/sanguino)
- 🇧🇷[Portugais brésilien](readme-pt-br.md) - Traduit par [Iago Angelim Costa Cavalcante](https://github.com/iagocavalcante) , [Douglas Mariano Valero](https://github.com/DouglasMV) et [koooge](https://github.com/koooge)
- Envie de traduire dans ta propre langue ? Ouvres une issue 💜

<br/><br/>

## `Table des matières`

#### [`Section 0: La règle d'or`](#section-0️⃣-the-golden-rule)

Un seul conseil qui inspire tout les autres (1 point spécial)

#### [`Section 1: Anatomie d'un test`](#section-1-the-test-anatomy-1)

La base - structurer des tests propre (12 points)

#### [`Section 2: Backend`](#section-2️⃣-backend-testing)

Écrire efficacement des tests backend et de microservices (8 points)

#### [`Section 3: Frontend`](#section-3️⃣-frontend-testing)

Écrire des tests pour l'interface utilisateur, y compris des tests de composants et des tests E2E (11 points)

#### [`Section 4: Mesurer l'efficacité des tests`](#section-4️⃣-measuring-test-effectiveness)

Surveiller le surveillant - mesurer la qualité des tests (4 points)

#### [`Section 5: Intégration continue`](#section-5️⃣-ci-and-other-quality-measures)

Lignes directrices pour l'intégration continue dans le monde du JS (9 points)

<br/><br/>

# Section 0️⃣: La règle d'or

<br/>

## ⚪️ 0 La règle d'or: Concevoir des tests minimalistes

:white_check_mark: **Do:**
Le code des tests n'est pas comme le code de production - conçoit le pour être simple, court, sans abstraction, agréable à utiliser et minimaliste. En regardant le code d'un test, on doit pouvoir comprendre son but instantanément.

Nos esprits sont déjà occupés avec le code de production, on n'a pas "d'espace" pour de la complexité additionnelle. Si on essaye d'insérer un autre code compliqué dans nos pauvres cerveaux, l'équipe va être ralentie ce qui est en contradiction avec la raison pour laquelle on fait des tests. 
En pratique, c'est là que de nombreuses équipes abandonnent tout simplement les tests.

Les tests sont une opportunité pour autre chose - un assistant amical et souriant, un avec qui il est agréable de travailler et qui nous apporte beaucoup pour peu d'investissement. La science nous dit que l'on a deux systèmes cérébraux : le premier est utilisé pour les activités qui ne demandent pas d'effort comme conduire une voiture sur une route vide ; le deuxième sert aux opérations complexe et conscientes comme résoudre une équation mathématique. Conçois tes tests pour le premier système, lire un test doit _sembler_ aussi simple que de modifier un fichier HTML, et pas comme résoudre 2X(17 x 24).

On peut y arriver en sélectionnant des techniques, des outils et des cibles de tests qui sont rentables et offrent un bon retour sur investissement. Test seulement ce qui doit être testé, essaye de conserver de la souplesse, et parfois, il vaut même mieux supprimer quelques tests et échanger la fiabilité contre de l'agilité et de la simplicité.

![alt text](/assets/headspace.png "On a pas de place disponible pour une complexité supplémentaire")

La plupart des conseils ci-dessous sont des dérivés de ce principe.

### Prêt à commencer ?

<br/><br/>

# Section 1: Anatomie d'un test

<br/>

## ⚪ ️ 1.1 Chaque nom devrait contenir 3 parties

:white_check_mark: **À faire:** Un rapport de test devrait indiquer si la version actuelle de l'application correspond aux attentes pour des personnes qui ne sont pas forcément familier avec la base de code : le testeur, le dev ops qui deploie et toi dans 2 ans. Dans ce but, les noms des tests doivent expliciter les attentes et inclure 3 parties :

(1) Qu'est-ce qui est testé ? Par exemple, la méthode ProductService.addNewProduct

(2) Dans quel circonstance et scénario ? Par exemple, aucun prix n'est passé à la méthode

(3) Quel est le résultat attendu ? Par exemple, le produit n'est pas approuvé

<br/>

❌ **Autrement:** Un deploiement a échoué, un test appelé "Add product" à échoué. Est-ce que celà indique exactement ce qui ne fonctionne plus correctement ?

<br/>

**👇 Note:** Chaque point contient des exemples de codes et parfois une image d'illustration. Cliques pour agrandir.
<br/>

<details><summary>✏ <b>Code Examples</b></summary>
  
<br/>
  
### :clap: Bien faire les choses Exemple: Un nom de test constitué de 3 parties

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

### :clap: Bien faire les choses Exemple: Un nom de test constitué de 3 parties

![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/>
<details><summary>© <b>Credits & read-more</b></summary>
  1. <a href='https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html'>Roy Osherove - Naming standards for unit tests</a>
</details>

<br/><br/>

## ⚪ ️ 1.2 Structurer les tests avec le pattern AAA

:white_check_mark: **À faire:** Structures tes tests avec 3 sections séparés: Organiser, Agir & Vérifier (Arrange, Act & Assert: AAA). Suivre cette structure garantit que le lecteur n'utilise pas de "CPU" de cerveau pour comprendre le plan du test:

1er A - Organiser (Arrange): Tout le code permettant de configurer le système selon le scénario qui doit être simulé. Cela peut inclure d'instancier le constructeur de l'élément testé, ajouter des entrées en DB, mocking/stubbing des objets et autre codes de préparation

2ème A - Agir (Act): Exécute l'élément testé. En général 1 seule ligne de code

3éme A - Vérifier (Assert): Vérifier que les valeurs reçues correspondent aux attentes. En général 1 seule ligne de code

<br/>

❌ **Autrement:** Non seulement vous avez passé des heures à comprendre le code principal, mais en plus ce qui devait être la partie la plus simple de la journée (tester) vous tord le cerveau.


<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses Exemple: Un test structuré avec le pattern AAA

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

### :thumbsdown: Exemple d'anti pattern: Pas de séparation, un bloc, plus dur à interpréter

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

## ⚪ ️1.3 Décrire les attentes dans un language produit: Utiliser des assertions de type BDD

:white_check_mark: **À faire:** Coder tes tests dans un language déclaratif permet au lecteur de comprendre immédiatement sans effectuer un seul cycle de "CPU" de cerveau. Lorsque tu écris du code impératif remplit de logique conditionnelles, le lecteur est forcé d'utiliser plus de cycles de "CPU" de cerveau. Dans ce cas, codes les attentes dans un language similaire au language humain, dans un style déclaratif de type BDD avec `expect` ou `should` et sans utiliser de code custom. Si Chai et Jest n'incluent pas les assertions nécéssaires et qu'elles reviennent régulièrement, considère [d'étendre Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) ou d'écrire un [plugin Chai custom](https://www.chaijs.com/guide/plugins/)

<br/>

❌ **Autrement:** L'équipe écrira moins de tests et décorera ceux qui sont ennuyeux avec .skip()

<br/>

<details><summary>✏ <b>Exemple de code</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

### :thumbsdown: Exemple d'anti pattern: Le lecteur doit parcourir un long code impératif juste pour comprendre l'histoire du test

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

### :clap: Bien faire les choses Exemple: Parcourir le test déclaratif suivant est un jeu d'enfant

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

## ⚪ ️ 1.4 S'en tenir aux tests des boites noires: Ne teste que les méthodes publiques

:white_check_mark: **À faire:** Tester les composants internes apporte beaucoup de complexité pour presque rien. Si ton code/API délivre les bon resultats, est-ce que tu dois vraiment passer les 3 prochaines heures à tester COMMENT il fonctionne et maintenir ces tests ? À chaque fois qu'un comportement publique est testé, l'implementation privée est aussi testé implicitement, et test tests n'échoueront que si il y a un certain problème (par exemple: mauvais retour). Cette approche est aussi appelé `behavioral testing` (test de comportement). De l'autre coté, si tu dois tester les éléments internes (approche de la boîte blanche) - l'objectif passe de planifier le résultat du composant à des détails de bases, et votre test peut échouer à cause de refactoring mineurs alors que le résultat est toujours bon - cela augmente la charge de maintenance.
<br/>

❌ **Autrement:** Tes tests se comportent comme [l'enfant qui criait au loup](https://fr.wikipedia.org/wiki/L%27Enfant_qui_criait_au_loup): crier des faux positifs (par exemple, un test échoue parce qu'un nom de variable privé à été changé). Sans surprise, les gens vont rapidement ignorer les notifications, jusqu'à ce qu'un jour, un vrai beug soit ignoré

<br/>
<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Un cas qui test une méthode interne sans raison valable

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

## ⚪ ️ ️1.5 Choisir les bons "test doubles": Éviter les mocks en faveur des stubs et spies

:white_check_mark: **À faire:** Les "test doubles" sont un mal nécéssaire parce qu'il sont couplé aux composants internes mais apportent néanmoins beaucoup de valeur (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Retrouve ici un rappel à propos des "test doubles": mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Avant d'utiliser des "test doubles", pose toi une question trés simple: Est-ce que je l'utilise pour tester une fonctionnalité qui apparait, ou peut apparaitre, dans le document de spécification ? Si non, ça sent le test de boite blanche.

Par exemple, si tu veux tester que ton application se comporte correctement quand le service de paiement est coupé, tu peux faire un stub du service de paiement et déclencher une réponse de type 'No Response' pour vérifier que l'unité testée retourne la bonne valeur. Cela vérifie le comportement/réponse de notre application suivant un certain scénario. Tu peux aussi utiliser un spy pour vérifier qu'un email a bien été envoyé quand ce service était coupé - il s'agit encore une fois d'un test de comportement qui pourrait apparaitre dans les spécification ("Envoyer un email si le paiement n'as pas pu être enregistré"). 
D'un autre coté, si tu mock le service de paiement pour vérifié qu'il a bien été appelé avec le bon type Javascript, alors ton test est orienté sur des comportements internes qui n'ont rien à voir avec les fonctionnalités de l'application et changeront probablement fréquemment.
<br/>

❌ **Autrement:** Chaque refactoring du code implique de chercher l'ensemble des mock dans le code afin de les mettre à jour. Les tests deviennent une corvée plutôt qu'un ami aidant.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Les mocks se concentrent sur des composants internes

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

### :clap: Faire les choses bien, exemple : Les spies se concentrent sur les fonctionnalités requises mais touchent les composants internes par effet de bord

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

## 📗 Envie d'apprendre ces bonnes pratiques en vidéo ?

### Va voir mon cours en ligne [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/><br/>

## ⚪ ️1.6 Utilise des données réalistes

:white_check_mark: **À faire:** Souvent les beugs de production sont révélés par des entrées tres spécifiques et surprenantes. Plus les entrées de tests seront réalistes, plus il y a de chance de détecter les beugs tôt. Utilise une librairie dédiée comme [Faker](https://www.npmjs.com/package/faker) pour générer des pseudo-vrais données qui resemble aux données de production. Par exemple, ce type de librairie peut générer de façon réaliste des numéros de téléphones, noms d'utilisateur, cartes de crédit, nom de société et même du 'Lorem ipsum'. Tu peux aussi créer des tests (en plus des tests unitaires, par à leur place) qui utilise des fausses données randomisées pour pousser test tests, ou même importer de vrais données depuis ton environnement de production. Envie de passer au niveau supérieur ? Regarde le prochain point (property-based testing).
<br/>

❌ **Autrement:** Tout vos tests de développement vont montrer du vert à tord avec des entrées tels que "Foo", mais en production ils passeront au rouge lorsqu'un hacker passera une chaine de caractère tel que “@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA”
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Une suite de test qui passe à cause de données non réalistes
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

### :clap: Bien faire les choses, exemple : Données réalistes randomisés

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

## ⚪ ️ 1.7 Teste plusieurs combinaisons d'input avec le Property-based testing

:white_check_mark: **À faire:** En règle général, on choisit quelques valeurs d'entrées pour chaque test. Même lorsque le format des inputs est réaliste ( voir le point 'Utilise des données réalistes' ), on couvre seulement quelques combinaisons d'entrées. En revanche, en production, une API appelée avec 5 paramètres peut être invoquée avec des milliers de permutations différentes, l'une d'entre elle peut faire échouer notre processus ([voir le Fuzz testing](https://fr.wikipedia.org/wiki/Fuzzing)). Et si tu pouvais écrire un seul test qui envoie 1000 permutations d'entrées automatiquement et détecte pour lequel d'entre eux notre processus ne retourne pas la bonne valeur ? Le Property-based testing c'est une méthode qui fait exactement ça : En testant toute les combinaisons d'entrées possible on augmente les chance de détecter un beug. Par exemple, prenom une méthode : addNewProduct(id, name, isDiscount), la librairie appelera cette méthode avec plusieurs combinaisons de (number, string, boolean) tel que (1, “iPhone”, false), (2, “Galaxy”, true). Tu peux utiliser le property-based testing avec ta librairie de test préféré (Mocha, Jest ...etc) à l'aide de librairie tel que [js-verify](https://github.com/jsverify/jsverify) ou [testcheck](https://github.com/leebyron/testcheck-js) (meilleure documentation). MAJ: Nicolas Dubien à suggéré dans les commentaire de [regarder fast-check](https://github.com/dubzzz/fast-check#readme) qui semble offrir des fonctionnalitées supplémentaire et être activement maintenue.
<br/>

❌ **Autrement:** Inconsciemment, tu choisis des entrées de test qui ne couvrent que les cas qui fonctionnent correctement. Malheuresement, cela réduit l'efficacité tests et leur capacité a détecter des beugs.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Tester plusieurs permutations d'entrées avec "fast-check"

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

## ⚪ ️ 1.8 Si besoin, n'utilise que des snapshots courts et inline

:white_check_mark: **Do:** Quand il y a un besoin pour du [snapshot testing](https://jestjs.io/docs/en/snapshot-testing), utilise seulement des snapshots courts ( 3-7 lignes ) qui sont inclut dans le test ([Inline Snapshot](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)) et pas dans des fichiers externes. Respecter cette règle permettra à vos tests de rester auto-explicatif et moins fragile.

D'un autre coté, les tutoriels et outils 'classique' encouragent à stocker de gros fichiers (résultats d'API JSON, markup d'un composant) sur un emplacement externe et de s'assurer à chaque fois que le test est lancé, de comparer le résultat reçu avec la version sauvegardée. Cela peux, par exemple, implicitement coupler notre test à 1000 lignes avec 3000 valeurs que le lecteur du test ne verra jamais et auquel il ne pensera pas. Pourquoi est-ce que c'est mauvais ? En faisant ça, il y a 1000 raisons pour votre test d'échouer - Il suffit qu'une seule ligne change pour que le snapshot soit invalide, et celà arrivera probablement souvent. A quelle frequence ? Pour chaque espace, commentaire ou changement mineur dans le HTML/CSS. De plus, le nom du test ne donnera pas la moindre indication à propos de l'erreur vu qu'il vérifie simplement que les 1000 lignes n'ont pas changé. Cela encourage aussi celui qui écrit les tests à accepter comme valeur de success un long document qu'il ne pourra pas inspecter et vérifier. Tout ces points sont des symptomes d'un test obscure qui n'est pas ciblé et cherche à en faire trop.

Il faut noter qu'il y a quelques cas ou de long snapshots externes sont acceptable - Pour valideer un schema et pas des données ou concernant des documents qui ne changent presque jamais
<br/>

❌ **Sinon:** Un test UI échoue. Le code semble bon, l'écran rends parfaitement les pixels, que s'est-il passé ? Ton test de snapshot a trouvé une différence entre le document original et le document actuel - un simple espace à été ajouté dans le markdown...

<br/>

<details><summary>✏ <b>Exemples de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Coupler nos test à 2000 lignes de code qu'on ne voit pas

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

### :clap: Bien faire les choses, exemple: Les attentes sont claires et spécifiques

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

## ⚪ ️1.9 Éviter les fixtures et seeds globals, ajouter les données par test

:white_check_mark: **À faire:** En suivant la règle d'or (point 0), chaque test doit ajouter et agir sur son propre jeu d'entrée en base de donnée pour éviter d'être couplés et faciliter le raisonnement à propos de la logique du test. En réalité, cette règle est souvent violée par les testeurs qui remplissent la base de donnée avant de lancer les tests ([aussi connu sous le nom ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) afin d'améliorer les performances. Même si la performance est effectivement une inquiétude valide, elle peut être atténuée (voir "Component testing"), en revanche, la compléxité des tests est un chagrin bien plus douloureux qui devrait régir les autres considérations la plupart du temps.
En pratique, chaque cas testé doit explicitement ajouter les entrée en base de donnée dont il a besoin et n'agir que sur ces entrées. Si la performance devient une inquiétude critique - un compromis peut se trouver sous la forme de seeds pour les jeux de tests qui ne modifient pas les données (queries).

<br/>

❌ **Autrement:** Certains tests échoue, le déploiement est annulé, l'équipe va dépenser un temps précieux maintenant, est-ce qu'on a un bug ? Investiguons, oh non - il semble que deux tests modifiaient les même données

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: les tests ne sont pas indépendants et reposent sur un hook global pour des données globales en DB

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
before(async () => {
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

### :clap: Bien faire les choses, exemple: On peut rester dans le test, chaque test agis sur ses propres données

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

## ⚪ ️ 1.10 Ne catch pas les erreurs, prevois les

:white_check_mark: **À faire:** Lorsqu'on essaye de detecter que certaines entrées déclenchent une erreur, il peut sembler être une bonne idée d'utiliser try-catch-finally et de vérifier qu'on est passé dans le catch. Le résultat est un test étrange et verbeux (exemple plus bas) qui cache l'intention simple du test et le résultat attendu.

Une alternative plus élégante est d'utiliser l'assertion Chai dédiée : expect(method).to.throw (ou en Jest: expect(method).toThrow()). Il est également obligatoire de vérifier que l'exception contient une propriété qui indique le type d'erreur, sinon, en recevant un message d'erreur générique, l'application ne sera pas capable de faire beaucoup plus que de montrer un message décevant à l'utilisateur.
<br/>

❌ **Autrement:** Il sera compliqué de déduire du rapport de test ce qui s'est mal passé

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Un long test qui essaye de vérifier la présence d'une erreur avec try-catch

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

### :clap: Bien faire les choses, exemple: Un attente lisible qui peut être comprise simplement, peut être même par un QA ou PM technique

```javascript
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

</details>

<br/><br/>

## ⚪ ️ 1.11 Tag tes tests

:white_check_mark: **À faire:** Des tests différents doivent être lancés dans différents scénarios. Les tests de fumée (quick smoke), IO-less, doivent tourner à chaque fois qu'un développeur sauvegarde ou commit un fichier, les tests complets end-to-end sont en général lancés quand une nouvelle pull-request est soumise, etc.
On peux réaliser ça en taggant les tests avec des mots clefs comme #cold #api #sanity pour pouvoir utiliser grep et sélectionner les tests qui nous interesse. Par exemple, voila comment invoquer uniquement le groupe de test sanity avec Mocha : mocha - grep 'sanity'
<br/>

❌ **Autrement:** Lancer tout les tests, y compris ceux qui éxecutent des dizaines de requetes DB, a chaque fois qu'un développeur fait un petit changement peut être extremement lent et pousser les développeurs a ne pas utiliser les tests.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Tagger des tests avec '#cold-test' permet à celui qui les lance de n'executer que les tests rapide (cold = tests rapides qui ne font pas d'opérations IO et peuvent être executés souvent, meme pendant que le développeur code)

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

## ⚪ ️ 1.12 Catégorise tes tests sous au moins 2 niveaux

:white_check_mark: **À faire:** Applique une structure à ta suite de test pour qu'un visiteur occasionnel puisse facilement comprendre les attentes (Les tests sont la meilleure documentation) et les différents scénarios testés. Une méthode fréquence pour ça est de placer au moins 2 blocs 'describe' au dessus de vos tests : Le premier est pour le nom de l'unité testé et le deuxieme pour un niveau supplémentaire de catégorisation comme le scénario ou une catégorie (voir l'exemple de code plus bas). Cette organisation améliorera grandement vos rapports de tests: Le lecteur comprendra simplement les catégories de tests, examinera la section voulu et verra les corrélations entre les tests qui échouent. De plus, ce sera bien plus simple pour un développeur de naviguer dans le code d'une suite avec de nombreux tests. Il y a plusieurs structures alternatives pour les suites de tests que tu peux envisager comme [given-when-then](https://github.com/searls/jasmine-given) et [RITE](https://github.com/ericelliott/riteway)

<br/>

❌ **Autrement:** En regardant un rapport avec une longue liste de tests a plat, le lecteur devra lire un long texte pour comprendre les scénarios majeur et comprendre les liens entre les tests qui échouent. Imagine le cas suivant : Quand 7/100 tests échouent, regarder une liste à plat nécéssitera d'aller lire le contenu des tests qui échouent pour comprendre le lien entre eux. En revanche, dans un rapport hiérarchique ils pourrait tous etre au sein du même scénario ou d'une catégorie et le lecteur pourra rapidement déduire ce qui est, ou du moins où est, la cause de l'erreur.

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Structurer une suite avec le nom de l'unité testé et les scénarios mènera au rapport pratique montré ci-dessous
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

### :thumbsdown: Exemple d'anti-pattern: Une liste de tests à plat qui rend l'identification du problème difficile pour le lecteur

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

## ⚪ ️1.13 Autre bonnes pratiques génériques

:white_check_mark: **À faire:** Ce post se concentre sur des conseils de tests qui sont en rapport, ou au moins peuvent être présentés, avec Node JS. ce point, cependant, regroupe quelques conseils sans rapport avec Node qui sont bien connus.

Apprend et pratique [les principes TDD](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) - ils ont beaucoup de valeurs pour la plupart mais ne soit pas intimidés s'ils ne correspondent pas à ton style, tu n'es pas le seul. Envisage d'écrire les tests avec le code dans un [red-green-refactor style](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), vérifie que chaque test vérifie exactement une chose, quand tu trouves un bug - avant de le fixer, écrit un test qui détectera le bug à l'avenir, laisse chaque test échouer au moins une fois avant de devenir vert, commence un module en écrivant du code simple et rapide qui valident le test - puis refactor graduellement et passe le code a un niveau de production, évite toute dépendance à l'environnement (paths, OS, etc)
<br/>

❌ **Autrement:** Tu manqueras les perles de sagesses recueillies pendant des décennies.

<br/><br/>

# Section 2️⃣: Tests Backend

## ⚪ ️2.1 Enrichis ton portefeuille de test: Vois plus loin que les tests unitaire et la pyramide

:white_check_mark: **À faire:** La [pyramide de tests](https://martinfowler.com/bliki/TestPyramid.html), bien que vielle de plus de 10 ans, est un bon model qui suggère trois types de tests et influence la plupart des stratégies de tests des développeurs. Dans un même temps, une poignée de nouvelles techniques de tests brillantes ont émergés et sont dans l'ombre de la pyramide de tests. Étant donné l'étendu des changements que l'on a vu ces 10 dernières années (micro-services, cloud, serverless), est-il seulement possible qu'un vieux modèle soit adapté à *tout* les types d'applications ? Le monde du test ne devrait-il pas accueillir de nouvelles techniques ?

Ne vous méprenez pas, en 2019, la pyramide de tests, le TDD et les tests unitaires sont toujours une technique puissante et sont probablement le meilleur choix pour beaucoup d'applications. Seulement, comme les autres modèles, malgrés qu'il soit utile, [il doit être faux parfois](https://en.wikipedia.org/wiki/All_models_are_wrong). Par exemple, imagine une application IoT qui traite de nombreux évènement dans une queue (message-bus) comme Kafka/RabbitMQ, qui vont ensuite dans un entrepot de donnée puis sont lus par une UI d'analyse. Est-ce qu'on devrait vraiment dépenser 50% de notre budget de test pour écrire des tests unitaire sur une application qui est centrée sur l'intégration et n'as presque aucune logique ? Plus la diversité des applications augmente (bots, crypto, Alexa-skills) plus les chances sont grandes de trouver un scénario ou la pyramide de test n'est pas le meilleur choix.

Il est temps d'enrichir ton portefeuille de test et de devenir familier avec plus de types de tests (les prochains points suggèrent quelques idées), de modèles tels que celui de la pyramide de tests mais aussi d'associer les types de tests aux problèmes que tu rencontres dans le monde réel ('Hey, notre API est cassé, écrivons des consumer-driven contract testing!'), diversifie tes tests comme un investisseur qui construit sont portefeuille en se basant sur l'analyse des risques - estime où les problèmes risquent de se poser et applique des mesures de prévention pour réduire ces risques.

Un mot d'avertissement: l'argument du TDD dans le monde du développement à un visage typique de fausse dichotomie, certains disent de l'utiliser de partout, d'autres pensent que c'est le diable. Tous ceux qui parlent en absolu ont tord :]

<br/>

❌ **Autrement:** Tu va rater des outils avec un retour sur investissement incroyable, certains comme Fuzz, lint, ou mutation peuvent apporter de la valeur en 10 minutes

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Cindy Sridharan propose un portefeuille de tests riche dans ton excellent post 'Testing Microservices - the same way'

![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Example: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️2.2 Les tests de composant pourrait être ta meilleure affaire

:white_check_mark: **À faire:** Chaque test unitaire couvre une petite portion de l'application et il est couteux de couvrir l'ensemble, alors que les tests end-to-end couvrent facilement une grande partie mais sont lent, pourquoi ne pas appliquer une approche intermédiaire et écrire des tests qui sont plus gros que les tests unitaire mais plus petit que les tests end-to-end ? Les tests de composant (Component testing) sont méconnus du monde de test mais ils offrent le meilleur des deux mondes: des performances raisonnable et la possibilité d'appliquer le pattern TDD + une couverture correct et réaliste

Les tests de composant se concentre sur "l'unité" du microservice, ils fonctionnent sur l'API, ne mock rien qui appartient au microservice lui même (une vrai DB, ou au moins une version in-memory de cette DB) mais stub tout ce qui est externe, comme les appels à d'autres microservices. En fasant ça, on test ce que l'on déploie, on approche l'application de l'extérieur vers l'intérieur et on gagne en confiance dans un laps de temps raisonnable.

<br/>

❌ **Autrement:** Tu risque de passer de longues journée à écrire des tests unitaire pour te rendre compte que tu n'as que 20% de couverture

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Supertest permet d'approcher l'API Express (rapide et couvre plusieurs niveaux)

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 Vérifie que les nouvelles versions ne cassent pas l'API avec les tests de contrat

:white_check_mark: **À faire:** Ton microservice a plusieurs clients, et tu exécutes plusieurs versions du service pour des raisons de compatibilité (pour que tout le monde soit content). Puis tu changes un champs et 'boom!', un client important qui compte sur ce champs est en colère. C'est le Catch-22 du monde de l'intégration : Il est trés difficilé pour le coté serveur de considérer toute les attentes des clients. D'un autre coté, les clients ne peuvent pas réaliser de tests puisque le serveur controles les dates de sorties. [Les "consumer-driven contracts" et le framework PACT](https://docs.pact.io) sont nés pour formaliser ce processus avec une approche disruptive - ce n'est pas le serveur qui défini ses propres plan de test, mais le client qui défini les tests du ...serveur! PACT peut enregistrer les attentes du client et les placer dans un emplacement partagé, "broker", afin que le serveur puisse extraire les attentes et s'éxécuter sur chaque version en utilisant la librairie PACT pour détecter les contrats rompus - une attente du client qui n'est pas satisfaite. En faisant ça, toutes les incompatibilités d'API server-client sont repérés tôt pendant le build/CI et peuvent vous éviter beaucoup de frustration.
<br/>

❌ **Autrement:** L'alternative sont les tests manuels épuisants ou la peur du déploiement
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "Examples with PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪ ️ 2.4 Test tes middlewares de manière isolée

:white_check_mark: **À faire:** Beaucoup évitent les tests de Middleware parce qu'ils représentent une petite portion du systeme et requièrent un serveur express live. Ce sont deux mauvaises raisons - les Middlewares sont petit mais affectent toute ou la plupart des requetes et peuveunt être testés simplement en tant que fonction qui reçoit un objet JS {req,res}. Pour tester un middleware, il suffit de l'invoquer et d'espionner ([avec Sinon par exemple](https://www.npmjs.com/package/sinon) l'interaction avec l'object {req,res} pour s'assurer que la fonction a effectuée la bonne action. La librairie [node-mock-http](https://www.npmjs.com/package/node-mocks-http) va encore plus loin et prend en compte l'object {req,res} tout en surveillant son comportement. Par exemple, il peut vérifier que le status http qui à été défini sur l'objet res correspond aux attentes (voir l'exemple ci-dessous)
<br/>

❌ **Autrement:** Un bug dans un middleware Express === un bug dans toutes ou la plupart des requêtes
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Tester le middleware en isolation sans effectuer d'appel réseau et sans réveiller l'ensemble de la machine Express

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

## ⚪ ️2.5 Mesure et refactorise en utilisant des outils d'analyse statique

:white_check_mark: **À faire:** Utiliser des outils d'analye statique donne des moyens objectif d'améliorer la qualité et de garder le code maintenable. Tu peux ajouter un outil d'analyse statique à ton build CI pour l'annuler si il détecte un "code smell". Ses arguments de vente par rapport au linting simple sont la capacité d'inspecter la qualité dans le contexte de plusieurs fichiers (e.g. détécter des duplication), effectuer des analyses avancer (e.g. complexité du code) et suivre l'histoire et le progrés d'un problème de code. Deux exemples d'outils que tu peux utiliser sont [SonarQube](https://www.sonarqube.org/) (4,900+ [stars](https://github.com/SonarSource/sonarqube)) et [Code Climate](https://codeclimate.com/) (2,000+ [stars](https://github.com/codeclimate/codeclimate))

Credit: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **Autrement:** Avec du code de mauvaise qualité, les beugs et la performance seront toujours un problème qu'aucune nouvelle librairie ou fonctionnalitée de pointe ne peux corriger

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: CodeClimate, un outil commercial qui peux identifier des méthodes complexes:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimate, a commercial tool that can identify complex methods:")

</details>

<br/><br/>

## ⚪ ️ 2.6 Vérifies ta préparation pour le chaos liés a Node

:white_check_mark: **À faire:** Bizarrement, la plupart des tests software conçernent uniquement la logique et les données, mais certaines des pires choses qui peuvent arriver ( et qui sont vraiment difficile à atténuer ) sont les problèmes d'infrastructures. Par exemple, est-ce que tu as déjà testé ce qui arrivera quand la mémoire du processus est surchargée, ou quand le serveur/process tombe, est-ce que ton systeme de monitoring réalise quand l'API devient 50% plus lente ? Pour tester et atténuer ce type de choses - [l'ingénierie du Chaos](https://principlesofchaos.org/) est né de Netflix.
Il vise à fournir une sensibilisation, des frameworks et des outils pour tester la résilience de notre application aux problèmes chaotiques. Par exemple, l'un de ces fameux outils, [le chaos monkey](https://github.com/Netflix/chaosmonkey), tue aléatoirement des serveurs pour vérifier que notre service peut toujours servir les utilisateurs et ne repose pas sur un unique serveur ( Il y a aussi une version Kubernetes, [kube-monkey](https://github.com/asobti/kube-monkey), qui tue des pods). Tout ces outils fonctionnent au niveau de l'hébergeur/la plateforme, mais que se passe-t-il si tu veux générer un chaos Node pour vérifier comment ton process gère les erreurs non prévus, les rejets de promesse, la surcharge de mémoire v8 avec l'allocation maximum de 1.7Gb ou est-ce que ton UX reste satisfaisante si l'event loop est bloqué régulièrement ? Pour répondre à ça, j'ai écrit, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) qui fournit toute sorte d'actions chaotiques liées a Node.
<br/>

❌ **Autrement:** Pas d'échappatoire ici, la loi de Murphy heurtera votre production sans merci
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Le chaos-Node peut générer toute sortes de farces Node.js afin que tu puisses tester la résilience de ton application au chaos

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 Éviter les fixtures et seeds globals, ajouter les données par test

:white_check_mark: **À faire:** En suivant la règle d'or (point 0), chaque test doit ajouter et agir sur son propre jeu d'entrée en base de donnée pour éviter d'être couplés et faciliter le raisonnement à propos de la logique du test. En réalité, cette règle est souvent violée par les testeurs qui remplissent la base de donnée avant de lancer les tests (aussi connu sous le nom ‘test fixture’) afin d'améliorer les performances. Même si la performance est effectivement une inquiétude valide, elle peut être atténuée (voir "Component testing"), en revanche, la compléxité des tests est un chagrin bien plus douloureux qui devrait régir les autres considérations la plupart du temps. En pratique, chaque cas testé doit explicitement ajouter les entrée en base de donnée dont il a besoin et n'agir que sur ces entrées. Si la performance devient une inquiétude critique - un compromis peut se trouver sous la forme de seeds pour les jeux de tests qui ne modifient pas les données (queries).
<br/>

❌ **Autrement:** Certains tests échoue, le déploiement est annulé, l'équipe va dépenser un temps précieux maintenant, est-ce qu'on a un bug ? Investiguons, oh non - il semble que deux tests modifiaient les même données

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: les tests ne sont pas indépendants et reposent sur un hook global pour des données globales en DB

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
before(async () => {
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

### :clap: Bien faire les choses, exemple: On peut rester dans le test, chaque test agis sur ses propres données

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

# Section 3️⃣: Tests Frontend

## ⚪ ️ 3.1 Separer l'UI des fonctionnalités

:white_check_mark: **À faire:** Lorsqu'on veux tester la logique d'un composant, les détail UI deviennent du bruit qui devrait être extrait, afin que les tests se concentrent purement sur les données. En pratique, extrait les donnée désirés du markup d'un facon abstrait qui n'est pas torop complée avec l'iplémentation graphique, assert seulement les donnée (vs des détails graphiques HTML/CSS) et désactive les animations qui ralentissent. Tu peux être tenté d'éviter le rendu et ne tester que les parties derrière l'UI (e.g. services, actions, store) mais ils s'agira de tests fictionnels qui ne ressemblent pas à la réalité et ne révèleront pas les cas ou la bonne donnée n'arrive pas à l'UI.
<br/>

❌ **Autrement:** Les donnée calculée de ton tests peuvent être prêtes en 10ms, mais l'ensemble du tests durera 500ms (100 tests = 1 min) à cause d'animation qui ne nous concerne pas dans le cadre du test.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Séparer les détails UI

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

### :thumbsdown: Exemple d'anti pattern: L'assertion mélange des détails UX et les données

```javascript
test("When flagging to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Mix UI & data in assertion
  expect(getAllByTestId("user")).toEqual('[<li data-test-id="user">John Doe</li>]');
});
```

</details>

<br/><br/>

## ⚪ ️ 3.2 Query HTML elements based on attributes that are unlikely to change

:white_check_mark: **Do:** Query HTML elements based on attributes that are likely to survive graphic changes unlike CSS selectors and like form labels. If the designated element doesn't have such attributes, create a dedicated test attribute like 'test-id-submit-button'. Going this route not only ensures that your functional/logic tests never break because of look & feel changes but also it becomes clear to the entire team that this element and attribute are utilized by tests and shouldn't get removed

<br/>

❌ **Otherwise:** You want to test the login functionality that spans many components, logic and services, everything is set up perfectly - stubs, spies, Ajax calls are isolated. All seems perfect. Then the test fails because the designer changed the div CSS class from 'thick-border' to 'thin-border'

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Querying an element using a dedicated attribute for testing

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React")

```html
// the markup code (part of React component)
<h3>
  <Badge pill className="fixed_badge" variant="dark">
    <span data-test-id="errorsLabel">{value}</span>
    <!-- note the attribute data-test-id -->
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

### :thumbsdown: Anti-Pattern Example: Relying on CSS attributes

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

## ⚪ ️ 3.3 Whenever possible, test with a realistic and fully rendered component

:white_check_mark: **Do:** Whenever reasonably sized, test your component from outside like your users do, fully render the UI, act on it and assert that the rendered UI behaves as expected. Avoid all sort of mocking, partial and shallow rendering - this approach might result in untrapped bugs due to lack of details and harden the maintenance as the tests mess with the internals (see bullet 'Favour blackbox testing'). If one of the child components is significantly slowing down (e.g. animation) or complicating the setup - consider explicitly replacing it with a fake

With all that said, a word of caution is in order: this technique works for small/medium components that pack a reasonable size of child components. Fully rendering a component with too many children will make it hard to reason about test failures (root cause analysis) and might get too slow. In such cases, write only a few tests against that fat parent component and more tests against its children

<br/>

❌ **Otherwise:** When poking into a component's internal by invoking its private methods, and checking the inner state - you would have to refactor all tests when refactoring the components implementation. Do you really have a capacity for this level of maintenance?

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Working realistically with a fully rendered component

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

### :thumbsdown: Anti-Pattern Example: Mocking the reality with shallow rendering

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

## ⚪ ️ 3.4 Don't sleep, use frameworks built-in support for async events. Also try to speed things up

:white_check_mark: **Do:** In many cases, the unit under test completion time is just unknown (e.g. animation suspends element appearance) - in that case, avoid sleeping (e.g. setTimeOut) and prefer more deterministic methods that most platforms provide. Some libraries allows awaiting on operations (e.g. [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), other provide API for waiting like [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance). Sometimes a more elegant way is to stub the slow resource, like API for example, and then once the response moment becomes deterministic the component can be explicitly re-rendered. When depending upon some external component that sleeps, it might turn useful to [hurry-up the clock](https://jestjs.io/docs/en/timer-mocks). Sleeping is a pattern to avoid because it forces your test to be slow or risky (when waiting for a too short period). Whenever sleeping and polling is inevitable and there's no support from the testing framework, some npm libraries like [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) can help with a semi-deterministic solution
<br/>

❌ **Otherwise:** When sleeping for a long time, tests will be an order of magnitude slower. When trying to sleep for small numbers, test will fail when the unit under test didn't respond in a timely fashion. So it boils down to a trade-off between flakiness and bad performance

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: E2E API that resolves only when the async operations is done (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: Doing It Right Example: Testing library that waits for DOM elements

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

### :thumbsdown: Anti-Pattern Example: custom sleep code

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

## ⚪ ️ 3.5 Watch how the content is served over the network

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Examples with Lighthouse")

✅ **Do:** Apply some active monitor that ensures the page load under real network is optimized - this includes any UX concern like slow page load or un-minified bundle. The inspection tools market is no short: basic tools like [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) can be easily configured to watch whether the server is alive and response under a reasonable SLA. This only scratches the surface of what might get wrong, hence it's preferable to opt for tools that specialize in frontend (e.g. [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) and perform richer analysis. The focus should be on symptoms, metrics that directly affect the UX, like page load time, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [time until the page gets interactive (TTI)](https://calibreapp.com/blog/time-to-interactive/). On top of that, one may also watch for technical causes like ensuring the content is compressed, time to the first byte, optimize images, ensuring reasonable DOM size, SSL and many others. It's advisable to have these rich monitors both during development, as part of the CI and most important - 24x7 over the production's servers/CDN

<br/>

❌ **Otherwise:** It must be disappointing to realize that after such great care for crafting a UI, 100% functional tests passing and sophisticated bundling - the UX is horrible and slow due to CDN misconfiguration

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

### :clap: Doing It Right Example: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

</details>

<br/>

## ⚪ ️ 3.6 Stub flaky and slow resources like backend APIs

:white_check_mark: **Do:** When coding your mainstream tests (not E2E tests), avoid involving any resource that is beyond your responsibility and control like backend API and use stubs instead (i.e. test double). Practically, instead of real network calls to APIs, use some test double library (like [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) for stubbing the API response. The main benefit is preventing flakiness - testing or staging APIs by definition are not highly stable and from time to time will fail your tests although YOUR component behaves just fine (production env was not meant for testing and it usually throttles requests). Doing this will allow simulating various API behavior that should drive your component behavior as when no data was found or the case when API throws an error. Last but not least, network calls will greatly slow down the tests

<br/>

❌ **Otherwise:** The average test runs no longer than few ms, a typical API call last 100ms>, this makes each test ~20x slower

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Stubbing or intercepting API calls

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

  return products ? <div>{products}</div> : <div data-test-id="no-products-message">No products</div>;
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

:white_check_mark: **Do:** Although E2E (end-to-end) usually means UI-only testing with a real browser (See bullet 3.6), for other they mean tests that stretch the entire system including the real backend. The latter type of tests is highly valuable as they cover integration bugs between frontend and backend that might happen due to a wrong understanding of the exchange schema. They are also an efficient method to discover backend-to-backend integration issues (e.g. Microservice A sends the wrong message to Microservice B) and even to detect deployment failures - there are no backend frameworks for E2E testing that are as friendly and mature as UI frameworks like [Cypress](https://www.cypress.io/) and [Puppeteer](https://github.com/GoogleChrome/puppeteer). The downside of such tests is the high cost of configuring an environment with so many components, and mostly their brittleness - given 50 microservices, even if one fails then the entire E2E just failed. For that reason, we should use this technique sparingly and probably have 1-10 of those and no more. That said, even a small number of E2E tests are likely to catch the type of issues they are targeted for - deployment & integration faults. It's advisable to run those over a production-like staging environment

<br/>

❌ **Otherwise:** UI might invest much in testing its functionality only to realizes very late that the backend returned payload (the data schema the UI has to work with) is very different than expected

<br/>

## ⚪ ️ 3.8 Speed-up E2E tests by reusing login credentials

:white_check_mark: **Do:** In E2E tests that involve a real backend and rely on a valid user token for API calls, it doesn't payoff to isolate the test to a level where a user is created and logged-in in every request. Instead, login only once before the tests execution start (i.e. before-all hook), save the token in some local storage and reuse it across requests. This seem to violate one of the core testing principle - keep the test autonomous without resources coupling. While this is a valid worry, in E2E tests performance is a key concern and creating 1-3 API requests before starting each individual tests might lead to horrible execution time. Reusing credentials doesn't mean the tests have to act on the same user records - if relying on user records (e.g. test user payments history) than make sure to generate those records as part of the test and avoid sharing their existence with other tests. Also remember that the backend can be faked - if your tests are focused on the frontend it might be better to isolate it and stub the backend API (see bullet 3.6).

<br/>

❌ **Otherwise:** Given 200 test cases and assuming login=100ms = 20 seconds only for logging-in again and again

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Logging-in before-all and not before-each

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

:white_check_mark: **Do:** For production monitoring and development-time sanity check, run a single E2E test that visits all/most of the site pages and ensures no one breaks. This type of test brings a great return on investment as it's very easy to write and maintain, but it can detect any kind of failure including functional, network and deployment issues. Other styles of smoke and sanity checking are not as reliable and exhaustive - some ops teams just ping the home page (production) or developers who run many integration tests which don't discover packaging and browser issues. Goes without saying that the smoke test doesn't replace functional tests rather just aim to serve as a quick smoke detector

<br/>

❌ **Otherwise:** Everything might seem perfect, all tests pass, production health-check is also positive but the Payment component had some packaging issue and only the /Payment route is not rendering

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Smoke travelling across all pages

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

:white_check_mark: **Do:** Besides increasing app reliability, tests bring another attractive opportunity to the table - serve as live app documentation. Since tests inherently speak at a less-technical and product/UX language, using the right tools they can serve as a communication artifact that greatly aligns all the peers - developers and their customers. For example, some frameworks allow expressing the flow and expectations (i.e. tests plan) using a human-readable language so any stakeholder, including product managers, can read, approve and collaborate on the tests which just became the live requirements document. This technique is also being referred to as 'acceptance test' as it allows the customer to define his acceptance criteria in plain language. This is [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) at its purest form. One of the popular frameworks that enable this is [Cucumber which has a JavaScript flavor](https://github.com/cucumber/cucumber-js), see example below. Another similar yet different opportunity, [StoryBook](https://storybook.js.org/), allows exposing UI components as a graphic catalog where one can walk through the various states of each component (e.g. render a grid w/o filters, render that grid with multiple rows or with none, etc), see how it looks like, and how to trigger that state - this can appeal also to product folks but mostly serves as live doc for developers who consume those components.

❌ **Otherwise:** After investing top resources on testing, it's just a pity not to leverage this investment and win great value

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Describing tests in human-language using cucumber-js

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

### :clap: Doing It Right Example: Visualizing our components, their various states and inputs using Storybook

![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Detect visual issues with automated tools

:white_check_mark: **Do:** Setup automated tools to capture UI screenshots when changes are presented and detect visual issues like content overlapping or breaking. This ensures that not only the right data is prepared but also the user can conveniently see it. This technique is not widely adopted, our testing mindset leans toward functional tests but it's the visuals what the user experience and with so many device types it's very easy to overlook some nasty UI bug. Some free tools can provide the basics - generate and save screenshots for the inspection of human eyes. While this approach might be sufficient for small apps, it's flawed as any other manual testing that demands human labor anytime something changes. On the other hand, it's quite challenging to detect UI issues automatically due to the lack of clear definition - this is where the field of 'Visual Regression' chime in and solve this puzzle by comparing old UI with the latest changes and detect differences. Some OSS/free tools can provide some of this functionality (e.g. [wraith](https://github.com/BBC-News/wraith), [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>) but might charge significant setup time. The commercial line of tools (e.g. [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) takes is a step further by smoothing the installation and packing advanced features like management UI, alerting, smart capturing by eliminating 'visual noise' (e.g. ads, animations) and even root cause analysis of the DOM/CSS changes that led to the issue

<br/>

❌ **Otherwise:** How good is a content page that display great content (100% tests passed), loads instantly but half of the content area is hidden?

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: A typical visual regression - right content that is served badly

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Doing It Right Example: Configuring wraith to capture and compare UI snapshots

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

### :clap: Doing It Right Example: Using Applitools to get snapshot comparison and other advanced features

![](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg "Using Applitools") ![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

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

# Section 4️⃣: Measuring Test Effectiveness

<br/><br/>

## ⚪ ️ 4.1 Get enough coverage for being confident, ~80% seems to be the lucky number

:white_check_mark: **Do:** The purpose of testing is to get enough confidence for moving fast, obviously the more code is tested the more confident the team can be. Coverage is a measure of how many code lines (and branches, statements, etc) are being reached by the tests. So how much is enough? 10–30% is obviously too low to get any sense about the build correctness, on the other side 100% is very expensive and might shift your focus from the critical paths to the exotic corners of the code. The long answer is that it depends on many factors like the type of application — if you’re building the next generation of Airbus A380 than 100% is a must, for a cartoon pictures website 50% might be too much. Although most of the testing enthusiasts claim that the right coverage threshold is contextual, most of them also mention the number 80% as a thumb of a rule ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) that presumably should satisfy most of the applications.

Implementation tips: You may want to configure your continuous integration (CI) to have a coverage threshold ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) and stop a build that doesn’t stand to this standard (it’s also possible to configure threshold per component, see code example below). On top of this, consider detecting build coverage decrease (when a newly committed code has less coverage) — this will push developers raising or at least preserving the amount of tested code. All that said, coverage is only one measure, a quantitative based one, that is not enough to tell the robustness of your testing. And it can also be fooled as illustrated in the next bullets

<br/>

❌ **Otherwise:** Confidence and numbers go hand in hand, without really knowing that you tested most of the system — there will also be some fear and fear will slow you down

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: A typical coverage report

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Doing It Right Example: Setting up coverage per component (using Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Using Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Inspect coverage reports to detect untested areas and other oddities

:white_check_mark: **Do:** Some issues sneak just under the radar and are really hard to find using traditional tools. These are not really bugs but more of surprising application behavior that might have a severe impact. For example, often some code areas are never or rarely being invoked — you thought that the ‘PricingCalculator’ class is always setting the product price but it turns out it is actually never invoked although we have 10000 products in DB and many sales… Code coverage reports help you realize whether the application behaves the way you believe it does. Other than that, it can also highlight which types of code is not tested — being informed that 80% of the code is tested doesn’t tell whether the critical parts are covered. Generating reports is easy — just run your app in production or during testing with coverage tracking and then see colorful reports that highlight how frequent each code area is invoked. If you take your time to glimpse into this data — you might find some gotchas
<br/>

❌ **Otherwise:** If you don’t know which parts of your code are left un-tested, you don’t know where the issues might come from

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: What’s wrong with this coverage report?

Based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Measure logical coverage using mutation testing

:white_check_mark: **Do:** The Traditional Coverage metric often lies: It may show you 100% code coverage, but none of your functions, even not one, return the right response. How come? it simply measures over which lines of code the test visited, but it doesn’t check if the tests actually tested anything — asserted for the right response. Like someone who’s traveling for business and showing his passport stamps — this doesn’t prove any work done, only that he visited few airports and hotels.

Mutation-based testing is here to help by measuring the amount of code that was actually TESTED not just VISITED. [Stryker](https://stryker-mutator.io/) is a JavaScript library for mutation testing and the implementation is really neat:

(1) it intentionally changes the code and “plants bugs”. For example the code newOrder.price===0 becomes newOrder.price!=0. This “bugs” are called mutations

(2) it runs the tests, if all succeed then we have a problem — the tests didn’t serve their purpose of discovering bugs, the mutations are so-called survived. If the tests failed, then great, the mutations were killed.

Knowing that all or most of the mutations were killed gives much higher confidence than traditional coverage and the setup time is similar
<br/>

❌ **Otherwise:** You’ll be fooled to believe that 85% coverage means your test will detect bugs in 85% of your code

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: 100% coverage, 0% testing

![](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg "Using Stryker")

```javascript
function addNewOrder(newOrder) {
  logger.log(`Adding new order ${newOrder}`);
  DB.save(newOrder);
  Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

  return { approved: true };
}

it("Test addNewOrder, don't use such test names", () => {
  addNewOrder({ assignee: "John@mailer.com", price: 120 });
}); //Triggers 100% code coverage, but it doesn't check anything
```

<br/>

### :clap: Doing It Right Example: Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>

<br/><br/>

## ⚪ ️4.4 Preventing test code issues with Test linters

:white_check_mark: **Do:** A set of ESLint plugins were built specifically for inspecting the tests code patterns and discover issues. For example, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) will warn when a test is written at the global level (not a son of a describe() statement) or when tests are [skipped](https://mochajs.org/#inclusive-tests) which might lead to a false belief that all tests are passing. Similarly, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) can, for example, warn when a test has no assertions at all (not checking anything)

<br/>

❌ **Otherwise:** Seeing 90% code coverage and 100% green tests will make your face wear a big smile only until you realize that many tests aren’t asserting for anything and many test suites were just skipped. Hopefully, you didn’t deploy anything based on this false observation

<br/>
<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: A test case full of errors, luckily all are caught by Linters

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

:white_check_mark: **Do:** Linters are a free lunch, with 5 min setup you get for free an auto-pilot guarding your code and catching significant issue as you type. Gone are the days where linting was about cosmetics (no semi-colons!). Nowadays, Linters can catch severe issues like errors that are not thrown correctly and losing information. On top of your basic set of rules (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), consider including some specializing Linters like [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) that can discover tests without assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) can discover promises with no resolve (your code will never continue), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) which can discover eager regex expressions that might get used for DOS attacks, and [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) is capable of alarming when the code uses utility library methods that are part of the V8 core methods like Lodash.\_map(…)
<br/>

❌ **Otherwise:** Consider a rainy day where your production keeps crashing but the logs don’t display the error stack trace. What happened? Your code mistakenly threw a non-error object and the stack trace was lost, a good reason for banging your head against a brick wall. A 5 min linter setup could detect this TYPO and save your day

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>

<br/><br/>

## ⚪ ️ 5.2 Shorten the feedback loop with local developer-CI

:white_check_mark: **Do:** Using a CI with shiny quality inspections like testing, linting, vulnerabilities check, etc? Help developers run this pipeline also locally to solicit instant feedback and shorten the [feedback loop](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Why? an efficient testing process constitutes many and iterative loops: (1) try-outs -> (2) feedback -> (3) refactor. The faster the feedback is, the more improvement iterations a developer can perform per-module and perfect the results. On the flip, when the feedback is late to come fewer improvement iterations could be packed into a single day, the team might already move forward to another topic/task/module and might not be up for refining that module.

Practically, some CI vendors (Example: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/)) allow running the pipeline locally. Some commercial tools like [wallaby provide highly-valuable & testing insights](https://wallabyjs.com/) as a developer prototype (no affiliation). Alternatively, you may just add npm script to package.json that runs all the quality commands (e.g. test, lint, vulnerabilities) — use tools like [concurrently](https://www.npmjs.com/package/concurrently) for parallelization and non-zero exit code if one of the tools failed. Now the developer should just invoke one command — e.g. ‘npm run quality’ — to get instant feedback. Consider also aborting a commit if the quality check failed using a githook ([husky can help](https://github.com/typicode/husky))
<br/>

❌ **Otherwise:** When the quality results arrive the day after the code, testing doesn’t become a fluent part of development rather an after the fact formal artifact

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: npm scripts that perform code quality inspection, all are run in parallel on demand or when a developer is trying to push new code

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

:white_check_mark: **Do:** End to end (e2e) testing are the main challenge of every CI pipeline — creating an identical ephemeral production mirror on the fly with all the related cloud services can be tedious and expensive. Finding the best compromise is your game: [Docker-compose](https://serverless.com/) allows crafting isolated dockerized environment with identical containers using a single plain text file but the backing technology (e.g. networking, deployment model) is different from real-world productions. You may combine it with [‘AWS Local’](https://github.com/localstack/localstack) to work with a stub of the real AWS services. If you went [serverless](https://serverless.com/) multiple frameworks like serverless and [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) allows the local invocation of FaaS code.

The huge Kubernetes ecosystem is yet to formalize a standard convenient tool for local and CI-mirroring though many new tools are launched frequently. One approach is running a ‘minimized-Kubernetes’ using tools like [Minikube](https://kubernetes.io/docs/setup/minikube/) and [MicroK8s](https://microk8s.io/) which resemble the real thing only come with less overhead. Another approach is testing over a remote ‘real-Kubernetes’, some CI providers (e.g. [Codefresh](https://codefresh.io/)) has native integration with Kubernetes environment and make it easy to run the CI pipeline over the real thing, others allow custom scripting against a remote Kubernetes.
<br/>

❌ **Otherwise:** Using different technologies for production and testing demands maintaining two deployment models and keeps the developers and the ops team separated

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: a CI pipeline that generates Kubernetes cluster on the fly <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Parallelize test execution

:white_check_mark: **Do:** When done right, testing is your 24/7 friend providing almost instant feedback. In practice, executing 500 CPU-bounded unit test on a single thread can take too long. Luckily, modern test runners and CI platforms (like [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) and [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) can parallelize the test into multiple processes and achieve significant improvement in feedback time. Some CI vendors do also parallelize tests across containers (!) which shortens the feedback loop even further. Whether locally over multiple processes, or over some cloud CLI using multiple machines — parallelizing demand keeping the tests autonomous as each might run on different processes

❌ **Otherwise:** Getting test results 1 hour long after pushing new code, as you already code the next features, is a great recipe for making testing less relevant

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Stay away from legal issues using license and plagiarism check

:white_check_mark: **Do:** Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like [license check](https://www.npmjs.com/package/license-checker) and [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stack Overflow and apparently violates some copyrights

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

:white_check_mark: **Do:** Even the most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community tools such as [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), or commercial tools like [snyk](https://snyk.io/) (offer also a free community version). Both can be invoked from your CI on every build

❌ **Otherwise:** Keeping your code clean from vulnerabilities without dedicated tools will require to constantly follow online publications about new threats. Quite tedious

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: NPM Audit result

![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>

<br/><br/>

## ⚪ ️5.7 Automate dependency updates

:white_check_mark: **Do:** Yarn and npm latest introduction of package-lock.json introduced a serious challenge (the road to hell is paved with good intentions) — by default now, packages are no longer getting updates. Even a team running many fresh deployments with ‘npm install’ & ‘npm update’ won’t get any new updates. This leads to subpar dependent packages versions at best or to vulnerable code at worst. Teams now rely on developers goodwill and memory to manually update the package.json or use tools [like ncu](https://www.npmjs.com/package/npm-check-updates) manually. A more reliable way could be to automate the process of getting the most reliable dependency versions, though there are no silver bullet solutions yet there are two possible automation roads:

(1) CI can fail builds that have obsolete dependencies — using tools like [‘npm outdated’](https://docs.npmjs.com/cli/outdated) or ‘npm-check-updates (ncu)’ . Doing so will enforce developers to update dependencies.

(2) Use commercial tools that scan the code and automatically send pull requests with updated dependencies. One interesting question remaining is what should be the dependency update policy — updating on every patch generates too many overhead, updating right when a major is released might point to an unstable version (many packages found vulnerable on the very first days after being released, [see the](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope incident).

An efficient update policy may allow some ‘vesting period’ — let the code lag behind the @latest for some time and versions before considering the local copy as obsolete (e.g. local version is 1.3.1 and repository version is 1.3.8)
<br/>

❌ **Otherwise:** Your production will run packages that have been explicitly tagged by their author as risky

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: [ncu](https://www.npmjs.com/package/npm-check-updates) can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")

</details>

<br/><br/>

## ⚪ ️ 5.8 Other, non-Node related, CI tips

:white_check_mark: **Do:** This post is focused on testing advice that is related to, or at least can be exemplified with Node JS. This bullet, however, groups few non-Node related tips that are well-known

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use a declarative syntax. This is the only option for most vendors but older versions of Jenkins allows using code or UI</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opt for a vendor that has native Docker support</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Fail early, run your fastest tests first. Create a ‘Smoke testing’ step/milestone that groups multiple fast inspections (e.g. linting, unit tests) and provide snappy feedback to the code committer</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Make it easy to skim-through all build artifacts including test reports, coverage reports, mutation reports, logs, etc</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Create multiple pipelines/jobs for each event, reuse steps between them. For example, configure a job for feature branch commits and a different one for master PR. Let each reuse logic using shared steps (most vendors provide some mechanism for code reuse)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Never embed secrets in a job declaration, grab them from a secret store or from the job’s configuration</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Explicitly bump version in a release build or at least ensure the developer did so</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Build only once and perform all the inspections over the single build artifact (e.g. Docker image)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Test in an ephemeral environment that doesn’t drift state between builds. Caching node_modules might be the only exception</li></ol>
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

### :clap: Example: Using Travis (CI vendor) build definition to run the same test over multiple Node versions

<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# Team

## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Role:** Writer

**About:** I'm an independent consultant who works with Fortune 500 companies and garage startups on polishing their JS & Node.js applications. More than any other topic I'm fascinated by and aims to master the art of testing. I'm also the author of [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

**📗 Online Course:** Liked this guide and wish to take your testing skills to the extreme? Consider visiting my comprehensive course [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/>

**Follow:**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 Contact](https://testjavascript.com/contact-2/)
- [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**Role:** Tech reviewer and advisor

Took care to revise, improve, lint and polish all the texts

**About:** full-stack web engineer, Node.js & GraphQL enthusiast

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Role:** Concept, design and great advice

**About:** A savvy frontend developer, CSS expert and emojis freak

## [Kyle Martin](https://github.com/js-kyle)

**Role:** Helps keep this project running, and reviews security related practices

**About:** Loves working on Node.js projects and web application security.

## Contributors ✨

Thanks goes to these wonderful people who have contributed to this repository!

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://geospatialscott.blogspot.com/"><img src="https://avatars3.githubusercontent.com/u/1326248?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Scott Davis</b></sub></a><br /><a href="#content-stdavis" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AdrienRedon"><img src="https://avatars2.githubusercontent.com/u/5978436?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Adrien REDON</b></sub></a><br /><a href="#content-AdrienRedon" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/NoriSte"><img src="https://avatars0.githubusercontent.com/u/173663?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Stefano Magni</b></sub></a><br /><a href="#content-NoriSte" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.joer.im"><img src="https://avatars2.githubusercontent.com/u/47742486?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yeoh Joer</b></sub></a><br /><a href="#content-yjoer" title="Content">🖋</a></td>
    <td align="center"><a href="http://jhonnymoreira.dev"><img src="https://avatars0.githubusercontent.com/u/2177742?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jhonny Moreira</b></sub></a><br /><a href="#content-jhonnymoreira" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Germanika"><img src="https://avatars2.githubusercontent.com/u/8846678?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ian Germann</b></sub></a><br /><a href="#content-Germanika" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AbdelrahmanHafez"><img src="https://avatars3.githubusercontent.com/u/19984935?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Hafez</b></sub></a><br /><a href="#content-AbdelrahmanHafez" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.ruxandrafediuc.com"><img src="https://avatars1.githubusercontent.com/u/11021586?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ruxandra Fediuc</b></sub></a><br /><a href="#content-ruxandrafed" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jacklee814"><img src="https://avatars0.githubusercontent.com/u/9951291?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jack</b></sub></a><br /><a href="#content-jacklee814" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.petercarrero.com"><img src="https://avatars0.githubusercontent.com/u/231727?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Peter Carrero</b></sub></a><br /><a href="#content-aloyr" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/huhgawz"><img src="https://avatars3.githubusercontent.com/u/369338?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Huhgawz</b></sub></a><br /><a href="#content-huhgawz" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/haakonmb"><img src="https://avatars1.githubusercontent.com/u/7099302?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Haakon Borch</b></sub></a><br /><a href="#content-haakonmb" title="Content">🖋</a></td>
    <td align="center"><a href="https://jaimemendoza.com/"><img src="https://avatars3.githubusercontent.com/u/5395811?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jaime Mendoza</b></sub></a><br /><a href="#content-jaimemendozadev" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/camerondunford"><img src="https://avatars0.githubusercontent.com/u/840612?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Cameron Dunford</b></sub></a><br /><a href="#content-camerondunford" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/shadowspawn"><img src="https://avatars1.githubusercontent.com/u/15719847?v=4?s=100" width="100px;" alt=""/><br /><sub><b>John Gee</b></sub></a><br /><a href="#content-shadowspawn" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/aurelijusrozenas"><img src="https://avatars0.githubusercontent.com/u/3273544?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Aurelijus Rožėnas</b></sub></a><br /><a href="#content-aurelijusrozenas" title="Content">🖋</a></td>
    <td align="center"><a href="http://aaronshivers.com"><img src="https://avatars2.githubusercontent.com/u/42848750?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Aaron</b></sub></a><br /><a href="#content-aaronshivers" title="Content">🖋</a></td>
    <td align="center"><a href="https://tomdoes.tech/"><img src="https://avatars1.githubusercontent.com/u/8683577?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Tom Nagle</b></sub></a><br /><a href="#content-tomanagle" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/yvesyao"><img src="https://avatars0.githubusercontent.com/u/7723729?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yves yao</b></sub></a><br /><a href="#content-yvesyao" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Userbit"><img src="https://avatars1.githubusercontent.com/u/34487074?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Userbit</b></sub></a><br /><a href="#content-Userbit" title="Content">🖋</a></td>
    <td align="center"><a href="https://glaucialemos.netlify.com/"><img src="https://avatars0.githubusercontent.com/u/1631477?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Glaucia Lemos</b></sub></a><br /><a href="#maintenance-glaucia86" title="Maintenance">🚧</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://twitter.com/koooge"><img src="https://avatars2.githubusercontent.com/u/7419215?v=4?s=100" width="100px;" alt=""/><br /><sub><b>koooge</b></sub></a><br /><a href="#content-koooge" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/michalbiesiada"><img src="https://avatars0.githubusercontent.com/u/18367606?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Michal</b></sub></a><br /><a href="#content-mbiesiad" title="Content">🖋</a></td>
    <td align="center"><a href="http://roywalker.me"><img src="https://avatars0.githubusercontent.com/u/611846?v=4?s=100" width="100px;" alt=""/><br /><sub><b>roywalker</b></sub></a><br /><a href="#content-roywalker" title="Content">🖋</a></td>
    <td align="center"><a href="https://dangen-effy.github.io/"><img src="https://avatars3.githubusercontent.com/u/23185799?v=4?s=100" width="100px;" alt=""/><br /><sub><b>dangen</b></sub></a><br /><a href="#content-dangen-effy" title="Content">🖋</a></td>
    <td align="center"><a href="https://dev.to/mbiesiad"><img src="https://avatars1.githubusercontent.com/u/60202305?v=4?s=100" width="100px;" alt=""/><br /><sub><b>biesiadamich</b></sub></a><br /><a href="#content-biesiadamich" title="Content">🖋</a></td>
    <td align="center"><a href="https://tarojsx.github.io"><img src="https://avatars3.githubusercontent.com/u/127009?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yanlin Jiang</b></sub></a><br /><a href="#content-cncolder" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/sanguino"><img src="https://avatars2.githubusercontent.com/u/2077168?v=4?s=100" width="100px;" alt=""/><br /><sub><b>sanguino</b></sub></a><br /><a href="#content-sanguino" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/MorganGeek"><img src="https://avatars0.githubusercontent.com/u/3721240?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Morgan</b></sub></a><br /><a href="#content-MorganGeek" title="Content">🖋</a></td>
    <td align="center"><a href="https://luk4s.dev"><img src="https://avatars0.githubusercontent.com/u/8350985?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Lukas Bischof</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=lukasbischof" title="Tests">⚠️</a> <a href="#content-lukasbischof" title="Content">🖋</a></td>
    <td align="center"><a href="https://juanmaruiz.surge.sh"><img src="https://avatars2.githubusercontent.com/u/1837650?v=4?s=100" width="100px;" alt=""/><br /><sub><b>JuanMa Ruiz</b></sub></a><br /><a href="#content-JuanMaRuiz" title="Content">🖋</a></td>
    <td align="center"><a href="https://luisangelorjr.com.br"><img src="https://avatars3.githubusercontent.com/u/22268900?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Luís Ângelo Rodrigues Jr.</b></sub></a><br /><a href="#content-luisangelorjr" title="Content">🖋</a></td>
    <td align="center"><a href="https://jfernandezpe.wordpress.com/"><img src="https://avatars0.githubusercontent.com/u/12046620?v=4?s=100" width="100px;" alt=""/><br /><sub><b>José Fernández</b></sub></a><br /><a href="#content-jfernandezpe" title="Content">🖋</a></td>
    <td align="center"><a href="http://www.linkedin.com/in/AlejandroGutierrezB"><img src="https://avatars3.githubusercontent.com/u/56408597?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alejandro Gutierrez Barcenilla</b></sub></a><br /><a href="#content-AlejandroGutierrezB" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jasonandmonte"><img src="https://avatars1.githubusercontent.com/u/30088000?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jason</b></sub></a><br /><a href="#content-jasonandmonte" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/otavionetoca"><img src="https://avatars.githubusercontent.com/u/11263232?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Otavio Araujo</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=otavionetoca" title="Tests">⚠️</a> <a href="#content-otavionetoca" title="Content">🖋</a></td>
    <td align="center"><a href="https://contributor.pw"><img src="https://avatars.githubusercontent.com/u/5027939?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alex Ivanov</b></sub></a><br /><a href="#content-contributorpw" title="Content">🖋</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->