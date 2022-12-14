<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 Comment ce guide peut faire passer vos compétences de test au niveau supérieur

<br/>

## 📗 46+ bonnes pratiques : complet et exhaustif

Ceci est un guide complet pour Javascript & Node.js de A à Z. Il résume et organise pour vous les meilleurs articles de blogs, livres et outils du marché

## 🚢 Avancé : va bien au-delà des bases

Embarque pour un voyage qui va bien au-delà des bases et aborde des sujets avancés tels que les tests en production, les tests de mutations, les tests basés sur les propriétés et de nombreux autres outils stratégiques et professionnels. Si vous lisez chaque mot de ce guide, vos compétences de tests seront probablement bien au-dessus la moyenne.

## 🌐 Full-stack: front, backend, CI ...

Commence par comprendre les pratiques de tests omniprésentes qui sont à la base de tout niveau d'application. Ensuite, plonge dans ton domaine de prédilection : frontend/UI, backend, CI ou peut-être tous ça à la fois ?

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
- 🇺🇦[Ukrainian](readme-ua.md) - Traduit par [Serhii Shramko](https://github.com/Shramkoweb)
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

:white_check_mark: **À faire:**
Le code des tests n'est pas comme le code de production - conçoit le pour être simple, court, sans abstraction, agréable à utiliser et minimaliste. En regardant le code d'un test, on doit pouvoir comprendre son but instantanément.

Nos esprits sont déjà occupés avec le code de production, on n'a pas "d'espace" pour de la complexité additionnelle. Si on essaye d'insérer un autre code compliqué dans nos pauvres cerveaux, l'équipe va être ralentie ce qui est en contradiction avec la raison pour laquelle on fait des tests. 
En pratique, c'est là que de nombreuses équipes abandonnent tout simplement les tests.

Les tests sont une opportunité pour autre chose - un assistant amical et souriant, un avec qui il est agréable de travailler et qui nous apporte beaucoup pour peu d'investissement. La science nous dit que l'on a deux systèmes cérébraux : le premier est utilisé pour les activités qui ne demandent pas d'effort comme conduire une voiture sur une route vide ; le deuxième sert aux opérations complexes et conscientes comme résoudre une équation mathématique. Conçois tes tests pour le premier système, lire un test doit _sembler_ aussi simple que de modifier un fichier HTML, et pas comme résoudre 2X(17 x 24).

On peut y arriver en sélectionnant des techniques, des outils et des cibles de tests qui sont rentables et offrent un bon retour sur investissement. Test seulement ce qui doit être testé, essaye de conserver de la souplesse, et parfois, il vaut même mieux supprimer quelques tests et échanger la fiabilité contre de l'agilité et de la simplicité.

![alt text](/assets/headspace.png "On a pas de place disponible pour une complexité supplémentaire")

La plupart des conseils ci-dessous sont des dérivés de ce principe.

### Prêt à commencer ?

<br/><br/>

# Section 1: Anatomie d'un test

<br/>

## ⚪ ️ 1.1 Chaque nom devrait contenir 3 parties

:white_check_mark: **À faire:** Un rapport de test devrait indiquer si la version actuelle de l'application correspond aux attentes pour des personnes qui ne sont pas forcément familières avec la base de code : le testeur, le dev ops qui déploie et toi dans 2 ans. Dans ce but, les noms des tests doivent expliciter les attentes et inclure 3 parties :

(1) Qu'est-ce qui est testé ? Par exemple, la méthode ProductService.addNewProduct

(2) Dans quelle circonstance et scénario ? Par exemple, aucun prix n'est passé à la méthode

(3) Quel est le résultat attendu ? Par exemple, le produit n'est pas approuvé

<br/>

❌ **Autrement:** Un déploiement a échoué, un test appelé "Add product" à échoué. Est-ce que cela indique exactement ce qui ne fonctionne plus correctement ?

<br/>

**👇 Note:** Chaque point contient des exemples de codes et parfois une image d'illustration. Cliques pour agrandir.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>
  
<br/>
  
### :clap: Bien faire les choses, exemple: Un nom de test constitué de 3 parties

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

### :clap: Bien faire les choses, exemple: Un nom de test constitué de 3 parties

![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/>
<details><summary>© <b>Credits & read-more</b></summary>
  1. <a href='https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html'>Roy Osherove - Naming standards for unit tests</a>
</details>

<br/><br/>

## ⚪ ️ 1.2 Structurer les tests avec le pattern AAA

:white_check_mark: **À faire:** Structure tes tests avec 3 sections séparées: Organiser, Agir & Vérifier (Arrange, Act & Assert: AAA). Suivre cette structure garantit que le lecteur n'utilise pas de "CPU" de cerveau pour comprendre le plan du test :

1er A - Organiser (Arrange): Tout le code permettant de configurer le système selon le scénario qui doit être simulé. Cela peut inclure d'instancier le constructeur de l'élément testé, ajouter des entrées en DB, mocking/stubbing des objets et autres codes de préparation

2ème A - Agir (Act): Exécute l'élément testé. En général 1 seule ligne de code

3éme A - Vérifier (Assert): Vérifier que les valeurs reçues correspondent aux attentes. En général 1 seule ligne de code

<br/>

❌ **Autrement:** Non seulement, vous avez passé des heures à comprendre le code principal, mais en plus ce qui devait être la partie la plus simple de la journée (tester) vous tord le cerveau.


<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Un test structuré avec le pattern AAA

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

:white_check_mark: **À faire:** Coder tes tests dans un langage déclaratif permet au lecteur de comprendre immédiatement sans effectuer un seul cycle de "CPU" de cerveau. Lorsque tu écris du code impératif remplis de logique conditionnelles, le lecteur est forcé d'utiliser plus de cycles de "CPU" de cerveau. Dans ce cas, code les attentes dans un langage similaire au langage humain, dans un style déclaratif de type BDD avec `expect` ou `should` et sans utiliser de code custom. Si Chai et Jest n'incluent pas les assertions nécessaires et qu'elles reviennent régulièrement, considère [d'étendre Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) ou d'écrire un [plugin Chai custom](https://www.chaijs.com/guide/plugins/)

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

### :clap: Bien faire les choses, exemple: Parcourir le test déclaratif suivant est un jeu d'enfant

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

## ⚪ ️ 1.4 S'en tenir aux tests des boites noires : Ne tester que les méthodes publiques

:white_check_mark: **À faire:** Tester les composants internes apporte beaucoup de complexité pour presque rien. Si ton code/API délivre les bon résultats, est-ce que tu dois vraiment passer les 3 prochaines heures à tester COMMENT il fonctionne et maintenir ces tests ? À chaque fois qu'un comportement publique est testé, l'implémentation privée est aussi testé implicitement, et test tests n'échoueront que si il y a un certain problème (par exemple: mauvais retour). Cette approche est aussi appelée `behavioral testing` (test de comportement). De l'autre côté, si tu dois tester les éléments internes (approche de la boîte blanche) - l'objectif passe de planifier le résultat du composant à des détails de bases, et votre test peut échouer à cause de refactoring mineurs alors que le résultat est toujours bon - cela augmente la charge de maintenance.
<br/>

❌ **Autrement:** Tes tests se comportent comme [l'enfant qui criait au loup](https://fr.wikipedia.org/wiki/L%27Enfant_qui_criait_au_loup): crier des faux positifs (par exemple, un test échoue parce qu'un nom de variable privé a été changé). Sans surprise, les gens vont rapidement ignorer les notifications, jusqu'à ce qu'un jour, un vrai bug soit ignoré

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

:white_check_mark: **À faire:** Les "test doubles" sont un mal nécessaire parce qu'ils sont couplés aux composants internes mais apportent néanmoins beaucoup de valeur (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Retrouve ici un rappel à propos des "test doubles": mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Avant d'utiliser des "test doubles", pose toi une question très simple: Est-ce que je l'utilise pour tester une fonctionnalité qui apparaît, ou peut apparaître, dans le document de spécification ? Si non, ça sent le test de boite blanche.

Par exemple, si tu veux tester que ton application se comporte correctement quand le service de paiement est coupé, tu peux faire un stub du service de paiement et déclencher une réponse de type 'No Response' pour vérifier que l'unité testée retourne la bonne valeur. Cela vérifie le comportement/réponse de notre application suivant un certain scénario. Tu peux aussi utiliser un spy pour vérifier qu'un email a bien été envoyé quand ce service était coupé - il s'agit encore une fois d'un test de comportement qui pourrait apparaître dans les spécifications ("Envoyer un email si le paiement n'as pas pu être enregistré"). 
D'un autre côté, si tu mock le service de paiement pour vérifier qu'il a bien été appelé avec le bon type Javascript, alors ton test est orienté sur des comportements internes qui n'ont rien à voir avec les fonctionnalités de l'application et changeront probablement fréquemment.
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

### :clap: Bien faire les choses, exemple : Les spies se concentrent sur les fonctionnalités requises mais touchent les composants internes par effet de bord

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

## ⚪ ️1.6 Utiliser des données réalistes

:white_check_mark: **À faire:** Souvent les bugs de production sont révélés par des entrées très spécifiques et surprenantes. Plus les entrées de tests seront réalistes, plus il y a de chance de détecter les bugs tôt. Utilise une librairie dédiée comme [Faker](https://www.npmjs.com/package/faker) pour générer des pseudo-vrais données qui ressemble aux données de production. Par exemple, ce type de librairie peut générer de façon réaliste des numéros de téléphone, noms d'utilisateur, cartes de crédit, nom de société et même du 'Lorem ipsum'. Tu peux aussi créer des tests (en plus des tests unitaires, par à leur place) qui utilise des fausses données randomisées pour pousser test tests, ou même importer de vraies données depuis ton environnement de production. Envie de passer au niveau supérieur ? Regarde le prochain point (property-based testing).
<br/>

❌ **Autrement:** Tout vos tests de développement vont montrer du vert à tort avec des entrées tels que "Foo", mais en production ils passeront au rouge lorsqu'un hacker passera une chaine de caractère tel que “@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA”
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

## ⚪ ️ 1.7 Tester plusieurs combinaisons d'input avec le Property-based testing

:white_check_mark: **À faire:** En règle général, on choisit quelques valeurs d'entrées pour chaque test. Même lorsque le format des inputs est réaliste (voir le point 'Utiliser des données réalistes'), on couvre seulement quelques combinaisons d'entrées. En revanche, en production, une API appelée avec 5 paramètres peut être invoquée avec des milliers de permutations différentes, l'une d'entre elle peut faire échouer notre processus ([voir le Fuzz testing](https://fr.wikipedia.org/wiki/Fuzzing)). Et si tu pouvais écrire un seul test qui envoie 1000 permutations d'entrées automatiquement et détecte pour lequel d'entre eux notre processus ne retourne pas la bonne valeur ? Le Property-based testing c'est une méthode qui fait exactement ça : En testant toutes les combinaisons d'entrées possible on augmente les chance de détecter un bug. Par exemple, prenons une méthode : addNewProduct(id, name, isDiscount), la librairie appellera cette méthode avec plusieurs combinaisons de (number, string, boolean) tel que (1, “iPhone”, false), (2, “Galaxy”, true). Tu peux utiliser le property-based testing avec ta librairie de test préféré (Mocha, Jest ...etc) à l'aide de librairie tel que [js-verify](https://github.com/jsverify/jsverify) ou [testcheck](https://github.com/leebyron/testcheck-js) (meilleure documentation). MAJ: Nicolas Dubien à suggéré dans les commentaire de [regarder fast-check](https://github.com/dubzzz/fast-check#readme) qui semble offrir des fonctionnalitées supplémentaire et être activement maintenue.
<br/>

❌ **Autrement:** Inconsciemment, tu choisis des entrées de test qui ne couvrent que les cas qui fonctionnent correctement. Malheureusement, cela réduit l'efficacité tests et leur capacité a détecter des bugs.
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

## ⚪ ️ 1.8 Si besoin, n'utiliser que des snapshots courts et inline

:white_check_mark: **Do:** Quand il y a un besoin pour du [snapshot testing](https://jestjs.io/docs/en/snapshot-testing), utilise seulement des snapshots courts (3-7 lignes) qui sont inclut dans le test ([Inline Snapshot](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)) et pas dans des fichiers externes. Respecter cette règle permettra à vos tests de rester auto-explicatif et moins fragile.

D'un autre côté, les tutoriels et outils 'classique' encouragent à stocker de gros fichiers (résultats d'API JSON, markup d'un composant) sur un emplacement externe et de s'assurer à chaque fois que le test est lancé, de comparer le résultat reçu avec la version sauvegardée. Cela peut, par exemple, implicitement coupler notre test à 1000 lignes avec 3000 valeurs que le lecteur du test ne verra jamais et auquel il ne pensera pas. Pourquoi est-ce que c'est mauvais ? En faisant ça, il y a 1000 raisons pour votre test d'échouer - Il suffit qu'une seule ligne change pour que le snapshot soit invalide, et cela arrivera probablement souvent. À quelle fréquence ? Pour chaque espace, commentaire ou changement mineur dans le HTML/CSS. De plus, le nom du test ne donnera pas la moindre indication à propos de l'erreur vu qu'il vérifie simplement que les 1000 lignes n'ont pas changé. Cela encourage aussi celui qui écrit les tests à accepter comme valeur de succès un long document qu'il ne pourra pas inspecter et vérifier. Tous ces points sont des symptômes d'un test obscure qui n'est pas ciblé et cherche à en faire trop.

Il faut noter qu'il y a quelques cas ou de long snapshots externes sont acceptable - Pour valider un schéma et pas des données ou concernant des documents qui ne changent presque jamais
<br/>

❌ **Sinon:** Un test UI échoue. Le code semble bon, l'écran rend parfaitement les pixels, que s'est-il passé ? Ton test de snapshot a trouvé une différence entre le document original et le document actuel - un simple espace a été ajouté dans le markdown...

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Coupler nos tests à 2000 lignes de code qu'on ne voit pas

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

:white_check_mark: **À faire:** En suivant la règle d'or (point 0), chaque test doit ajouter et agir sur son propre jeu d'entrée en base de données pour éviter d'être couplés et faciliter le raisonnement à propos de la logique du test. En réalité, cette règle est souvent violée par les testeurs qui remplissent la base de données avant de lancer les tests ([aussi connu sous le nom ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) afin d'améliorer les performances. Même si la performance est effectivement une inquiétude valide, elle peut être atténuée (voir "Component testing"), en revanche, la complexité des tests est une peine bien plus douloureuse qui devrait régir les autres considérations la plupart du temps.
En pratique, chaque cas testé doit explicitement ajouter les entrées en base de données dont il a besoin et n'agir que sur ces entrées. Si la performance devient une inquiétude critique - un compromis peut se trouver sous la forme de seeds pour les jeux de tests qui ne modifient pas les données (queries).

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

## ⚪ ️ 1.10 Ne pas catcher les erreurs, les prévoir

:white_check_mark: **À faire:** Lorsqu'on essaye de détecter que certaines entrées déclenchent une erreur, il peut sembler être une bonne idée d'utiliser try-catch-finally et de vérifier qu'on est passé dans le catch. Le résultat est un test étrange et verbeux (exemple plus bas) qui cache l'intention simple du test et le résultat attendu.

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

## ⚪ ️ 1.11 Taguer tes tests

:white_check_mark: **À faire:** Des tests différents doivent être lancés dans différents scénarios. Les tests de fumée (quick smoke), IO-less, doivent tourner à chaque fois qu'un développeur sauvegarde ou commit un fichier, les tests complets end-to-end sont en général lancés quand une nouvelle pull-request est soumise, etc.
On peut réaliser ça en taggant les tests avec des mots clefs comme #cold #api #sanity pour pouvoir utiliser grep et sélectionner les tests qui nous interesse. Par exemple, voilà comment invoquer uniquement le groupe de test 'sanity' avec Mocha : mocha - grep 'sanity'
<br/>

❌ **Autrement:** Lancer tous les tests, y compris ceux qui exécutent des dizaines de requêtes DB, à chaque fois qu'un développeur fait un petit changement peut être extrêmement lent et pousser les développeurs a ne pas utiliser les tests.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Taguer des tests avec '#cold-test' permet à celui qui les lance de n'executer que les tests rapide (cold = tests rapides qui ne font pas d'opérations IO et peuvent être executés souvent, meme pendant que le développeur code)

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

## ⚪ ️ 1.12 Catégoriser tes tests sous au moins 2 niveaux

:white_check_mark: **À faire:** Applique une structure à ta suite de tests pour qu'un visiteur occasionnel puisse facilement comprendre les attentes (Les tests sont la meilleure documentation) et les différents scénarios testés. Une méthode fréquence pour ça est de placer au moins 2 blocs 'describe' au-dessus de vos tests : Le premier est pour le nom de l'unité testé et le deuxième pour un niveau supplémentaire de catégorisation comme le scénario ou une catégorie (voir l'exemple de code plus bas). Cette organisation améliorera grandement vos rapports de tests: Le lecteur comprendra simplement les catégories de tests, examinera la section voulue et verra les corrélations entre les tests qui échouent. De plus, ce sera bien plus simple pour un développeur de naviguer dans le code d'une suite avec de nombreux tests. Il y a plusieurs structures alternatives pour les suites de tests que tu peux envisager comme [given-when-then](https://github.com/searls/jasmine-given) et [RITE](https://github.com/ericelliott/riteway)

<br/>

❌ **Autrement:** En regardant un rapport avec une longue liste de tests a plat, le lecteur devra lire un long texte pour comprendre les scénarios majeurs et comprendre les liens entre les tests qui échouent. Imagine le cas suivant : Quand 7/100 tests échouent, regarder une liste à plat nécessitera d'aller lire le contenu des tests qui échouent pour comprendre le lien entre eux. En revanche, dans un rapport hiérarchique, ils pourraient tous être au sein du même scénario ou d'une catégorie et le lecteur pourra rapidement déduire ce qui est, ou du moins où est, la cause de l'erreur.

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

:white_check_mark: **À faire:** Ce post se concentre sur des conseils de tests qui sont en rapport, ou au moins peuvent être présentés, avec Node JS. Ce point, cependant, regroupe quelques conseils sans rapport avec Node qui sont bien connus.

Apprends et pratique [les principes TDD](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) - ils ont beaucoup de valeurs pour la plupart, mais ne soit pas intimidés s'ils ne correspondent pas à ton style, tu n'es pas le seul. Envisage d'écrire les tests avec le code dans un [red-green-refactor style](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), vérifie que chaque test vérifie exactement une chose, quand tu trouves un bug - avant de le fixer, écrit un test qui détectera le bug à l'avenir, laisse chaque test échouer au moins une fois avant de devenir vert, commence un module en écrivant du code simple et rapide qui valide le test - puis refactor graduellement et passe le code a un niveau de production, évite toute dépendance à l'environnement (paths, OS, etc)
<br/>

❌ **Autrement:** Tu manqueras les perles de sagesses recueillies pendant des décennies.

<br/><br/>

# Section 2️⃣: Tests Backend

## ⚪ ️2.1 Enrichis ton portefeuille de test: Vois plus loin que les tests unitaire et la pyramide

:white_check_mark: **À faire:** La [pyramide de tests](https://martinfowler.com/bliki/TestPyramid.html), bien que vielle de plus de 10 ans, est un bon modèle qui suggère trois types de tests et influence la plupart des stratégies de tests des développeurs. Dans un même temps, une poignée de nouvelles techniques de tests brillantes ont émergé et sont dans l'ombre de la pyramide de tests. Étant donné l'étendu des changements que l'on a vu ces 10 dernières années (micro-services, cloud, serverless), est-il seulement possible qu'un vieux modèle soit adapté à *tout* les types d'applications ? Le monde du test ne devrait-il pas accueillir de nouvelles techniques ?

Ne vous méprenez pas, en 2019, la pyramide de tests, le TDD et les tests unitaires sont toujours une technique puissante et sont probablement le meilleur choix pour beaucoup d'applications. Seulement, comme les autres modèles, malgré qu'il soit utile, [il doit être faux parfois](https://en.wikipedia.org/wiki/All_models_are_wrong). Par exemple, imagine une application IoT qui traite de nombreux événements dans une queue (message-bus) comme Kafka/RabbitMQ, qui vont ensuite dans un entrepot de donnée puis sont lus par une UI d'analyse. Est-ce qu'on devrait vraiment dépenser 50% de notre budget de test pour écrire des tests unitaires sur une application qui est centrée sur l'intégration et n'a presque aucune logique ? Plus la diversité des applications augmente (bots, crypto, Alexa-skills) plus les chances sont grandes de trouver un scénario ou la pyramide de test n'est pas le meilleur choix.

Il est temps d'enrichir ton portefeuille de test et de devenir familier avec plus de types de tests (les prochains points suggèrent quelques idées), des modèles tels que celui de la pyramide de tests mais aussi d'associer les types de tests aux problèmes que tu rencontres dans le monde réel ('Hey, notre API est cassé, écrivons des consumer-driven contract testing!'), diversifie tes tests comme un investisseur qui construit son portefeuille en se basant sur l'analyse des risques - estime où les problèmes risquent de se poser et applique des mesures de prévention pour réduire ces risques.

Un mot d'avertissement: l'argument du TDD dans le monde du développement à un visage typique de fausse dichotomie, certains disent de l'utiliser de partout, d'autres pensent que c'est le diable. Tous ceux qui parlent en absolu ont tord :]

<br/>

❌ **Autrement:** Tu va rater des outils avec un retour sur investissement incroyable, certains comme Fuzz, lint, ou mutation peuvent apporter de la valeur en 10 minutes

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Cindy Sridharan propose un portefeuille de tests riche dans son excellent post 'Testing Microservices - the same way'

![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Example: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️2.2 Les tests de composant pourrait être ton meilleur arrangement

:white_check_mark: **À faire:** Chaque test unitaire couvre une petite portion de l'application et il est coûteux de couvrir l'ensemble, alors que les tests end-to-end couvrent facilement une grande partie mais sont lent, pourquoi ne pas appliquer une approche intermédiaire et écrire des tests qui sont plus gros que les tests unitaires mais plus petits que les tests end-to-end ? Les tests de composant (Component testing) sont méconnus du monde de test mais ils offrent le meilleur des deux mondes: des performances raisonnable et la possibilité d'appliquer le pattern TDD + une couverture correcte et réaliste

Les tests de composant se concentrent sur "l'unité" du microservice, ils fonctionnent sur l'API, ne mock rien qui appartient au microservice lui-même (une vrai DB, ou au moins une version in-memory de cette DB) mais stub tout ce qui est externe, comme les appels à d'autres microservices. En faisant ça, on test ce que l'on déploie, on approche l'application de l'extérieur vers l'intérieur et on gagne en confiance dans un laps de temps raisonnable.

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

## ⚪ ️2.3 Vérifier que les nouvelles versions ne cassent pas l'API avec les tests de contrat

:white_check_mark: **À faire:** Ton microservice a plusieurs clients, et tu exécutes plusieurs versions du service pour des raisons de compatibilité (pour que tout le monde soit content). Puis tu changes un champ et 'boom!', un client important qui compte sur ce champ est en colère. C'est le Catch-22 du monde de l'intégration : Il est très difficile pour le coté serveur de considérer toutes les attentes des clients. D'un autre coté, les clients ne peuvent pas réaliser de tests puisque le serveur contrôles les dates de sorties. [Les "consumer-driven contracts" et le framework PACT](https://docs.pact.io) sont nés pour formaliser ce processus avec une approche disruptive - ce n'est pas le serveur qui définit ses propres plans de test, mais le client qui définit les tests du ...serveur! PACT peut enregistrer les attentes du client et les placer dans un emplacement partagé, "broker", afin que le serveur puisse extraire les attentes et s'exécuter sur chaque version en utilisant la librairie PACT pour détecter les contrats rompus - une attente du client qui n'est pas satisfaite. En faisant ça, toutes les incompatibilités d'API server-client sont repérés tôt pendant le build/CI et peuvent vous éviter beaucoup de frustration.
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

## ⚪ ️ 2.4 Tester tes middlewares de manière isolée

:white_check_mark: **À faire:** Beaucoup évitent les tests de Middleware parce qu'ils représentent une petite portion du système et requièrent un serveur express live. Ce sont deux mauvaises raisons - les Middlewares sont petits, mais affectent toute ou la plupart des requêtes et peuvent être testés simplement en tant que fonction qui reçoit un objet JS {req,res}. Pour tester un middleware, il suffit de l'invoquer et d'espionner ([avec Sinon par exemple](https://www.npmjs.com/package/sinon) l'interaction avec l'objet {req,res} pour s'assurer que la fonction a effectuée la bonne action. La librairie [node-mock-http](https://www.npmjs.com/package/node-mocks-http) va encore plus loin et prend en compte l'objet {req,res} tout en surveillant son comportement. Par exemple, il peut vérifier que le status http qui à été défini sur l'objet res correspond aux attentes (voir l'exemple ci-dessous)
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

## ⚪ ️2.5 Mesurer et refactoriser en utilisant des outils d'analyse statique

:white_check_mark: **À faire:** Utiliser des outils d'analyse statique donne des moyens objectif d'améliorer la qualité et de garder le code maintenable. Tu peux ajouter un outil d'analyse statique à ton build CI pour l'annuler si il détecte un "code smell". Ses arguments de vente par rapport au linting simple sont la capacité d'inspecter la qualité dans le contexte de plusieurs fichiers (e.g. détecter des duplications), effectuer des analyses avancées (e.g. complexité du code) et suivre l'histoire et le progrés d'un problème de code. Deux exemples d'outils que tu peux utiliser sont [SonarQube](https://www.sonarqube.org/) (4,900+ [stars](https://github.com/SonarSource/sonarqube)) et [Code Climate](https://codeclimate.com/) (2,000+ [stars](https://github.com/codeclimate/codeclimate))

Credit: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **Autrement:** Avec du code de mauvaise qualité, les bugs et la performance seront toujours un problème qu'aucune nouvelle librairie ou fonctionnalité de pointe ne peux corriger

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: CodeClimate, un outil commercial qui peux identifier des méthodes complexes:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimate, a commercial tool that can identify complex methods:")

</details>

<br/><br/>

## ⚪ ️ 2.6 Vérifier ta préparation pour le chaos liés a Node

:white_check_mark: **À faire:** Bizarrement, la plupart des tests software concernent uniquement la logique et les données, mais certaines des pires choses qui peuvent arriver ( et qui sont vraiment difficile à atténuer ) sont les problèmes d'infrastructures. Par exemple, est-ce que tu as déjà testé ce qui arrivera quand la mémoire du processus est surchargée, ou quand le serveur/process tombe, est-ce que ton système de monitoring détecte lorsque l'API devient 50% plus lente ? Pour tester et atténuer ce type de choses - [l'ingénierie du Chaos](https://principlesofchaos.org/) est né de Netflix.
Il vise à fournir une sensibilisation, des frameworks et des outils pour tester la résilience de notre application aux problèmes chaotiques. Par exemple, l'un de ces fameux outils, [le chaos monkey](https://github.com/Netflix/chaosmonkey), tue aléatoirement des serveurs pour vérifier que notre service peut toujours servir les utilisateurs et ne repose pas sur un unique serveur ( Il y a aussi une version Kubernetes, [kube-monkey](https://github.com/asobti/kube-monkey), qui tue des pods). Tous ces outils fonctionnent au niveau de l'hébergeur/la plateforme, mais que se passe-t-il si tu veux générer un chaos Node pour vérifier comment ton process gère les erreurs non prévus, les rejets de promesse, la surcharge de mémoire v8 avec l'allocation maximum de 1.7Gb ou est-ce que ton UX reste satisfaisante si l'event loop est bloqué régulièrement ? Pour répondre à ça, j'ai écrit, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) qui fournit toute sorte d'actions chaotiques liées a Node.
<br/>

❌ **Autrement:** Pas d'échappatoire ici, la loi de Murphy heurtera votre production sans merci
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Le chaos-Node peut générer toute sortes de d'erreurs Node.js afin que tu puisses tester la résilience de ton application au chaos

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 Éviter les fixtures et seeds globals, ajouter les données par test

:white_check_mark: **À faire:** En suivant la règle d'or (point 0), chaque test doit ajouter et agir sur son propre jeu d'entrée en base de données pour éviter d'être couplés et faciliter le raisonnement à propos de la logique du test. En réalité, cette règle est souvent violée par les testeurs qui remplissent la base de données avant de lancer les tests (aussi connu sous le nom ‘test fixture’) afin d'améliorer les performances. Même si la performance est effectivement une inquiétude valide, elle peut être atténuée (voir "Component testing"), en revanche, la complexité des tests est un chagrin bien plus douloureux qui devrait régir les autres considérations la plupart du temps. En pratique, chaque cas testé doit explicitement ajouter les entrées en base de données dont il a besoin et n'agir que sur ces entrées. Si la performance devient une inquiétude critique - un compromis peut se trouver sous la forme de seeds pour les jeux de tests qui ne modifient pas les données (queries).
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

:white_check_mark: **À faire:** Lorsqu'on veut tester la logique d'un composant, les détails UI deviennent du bruit qui devrait être extrait, afin que les tests se concentrent purement sur les données. En pratique, extrait les données désirées du markup d'une façon abstraite qui n'est pas trop couplée avec l'implémentation graphique, assert seulement les données (vs des détails graphiques HTML/CSS) et désactive les animations qui ralentissent. Tu peux être tenté d'éviter le rendu et ne tester que les parties derrière l'UI (e.g. services, actions, store) mais il s'agira de tests fictionnels qui ne ressemblent pas à la réalité et ne révéleront pas les cas ou la bonne donnée n'arrive pas à l'UI.
<br/>

❌ **Autrement:** Les données calculées de ton test peuvent être prêtes en 10ms, mais l'ensemble du test durera 500ms (100 tests = 1 min) à cause d'animation qui ne nous concerne pas dans le cadre du test.
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

## ⚪ ️ 3.2 Query les éléments HTML en te basant sur des attributs qui ont peu de chance de changer

:white_check_mark: **À faire:** Query les éléments HTML en te basant sur des attributs qui ont de grandes chances de survivre à un changement graphique, contrairement aux sélecteurs CSS ou aux labels des forms. Si l'élément n'as pas d'attribut de ce type, crée un attribut dédié au test comme 'test-id-submit-sutton'. Utiliser cette méthode permet non seulement d'être sûr que vos tests fonctionnels/logique ne cassent pas à cause d'un changement visuel mais il devient également plus clair pour toute votre équipe que cet élément et son attribut sont utilisés par les tests et ne devraient pas être supprimés.
<br/>

❌ **Autrement:** Tu veux tester la fonctionnalité de connexion qui couvre de nombreux composants, logiques et services, tout est configuré parfaitement - subs, spies, les appels Ajax sont isolés. Tout semble parfait. Puis le test échoue car le designer à changé la class CSS du div de 'thick-border' à 'thin-border'

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Query un élément en utilisant un attribut dédié aux tests

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

### :thumbsdown: Exemple d'anti pattern: Compter sur les attributs CSS

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

## ⚪ ️ 3.3 Lorsque c'est possible, tester avec un composant réaliste et totalement rendu

:white_check_mark: **Do:** Lorsqu'ils sont de taille raisonnable, tests tes composants de l'extérieur comme le font tes utilisateurs, rend complètement l'UI, agit dessus, et vérifie que l'UI rendu se comporte comme on l'attend.
Évite toute sorte de mocking, de rendu partiels ou superficiel - cette approche peut résulter en bugs non détectés à cause du manque de détails et rendre plus difficile la maintenance des tests puisque les tests modifient les propriétés interne (voir le point 'Privilégier les tests blackbox'). Si l'un des composants enfants ralentis significativement (e.g animations) ou complique la configuration - considère de le remplacer explicitement avec un faux.

Maintenant que c'est dit, une mise en garde s'impose: cette technique fonctionne pour des petit/moyens composants qui ont un nombre raisonnable de composants enfants. Rendre complètement un composant avec trop d'enfants compliquera le raisonnement à propos des échecs de tests (analyse de la cause originelle) et peut être trop lent. Dans ces cas, écrit seulement quelques tests pour ce parent, et plus de tests pour ses enfants.

<br/>

❌ **Autrement:** Lorsque tu fouilles dans les détails internes du composant en invoquant ses méthodes privées, et en vérifiant l'état interne - tu devras refactoriser tous les tests lorsque tu refactorisera l'implémentation du composant. Est-ce que tu as vraiment la capacité de tenir ce niveau de maintenance ?

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Travailler de façon réaliste sur un composant complètement rendu

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

### :thumbsdown: Exemple d'anti pattern: Mocker la réalité avec un rendu superficiel

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

## ⚪ ️ 3.4 Ne pas attendre, utiliser la gestion des évènements asynchrone implémenté dans les frameworks. Essayer aussi d'accélérer les choses

:white_check_mark: **À faire:** Souvent, le temps de complétion de l'unité qu'on test est inconnu (e.g animations qui suspendent l'apparition d'éléments) - Dans ce cas, évite d'attendre (e.g. setTimeOut ) et préfère des méthodes déterministe que la plupart des frameworks fournissent. Certaines librairies permettent d'attendre certaines opérations (e.g. [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), d'autres fournissent une API pour attendre comme [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance).
Parfois il est plus élégant de stub la ressource lente, comme une API, une fois que le moment de réponse devient déterminé, le composant peut être re-rendu explicitement. Lorsque l'on dépend d'un composant externe qui attend, il peut être utile d'[accélérer l'horloge](https://jestjs.io/docs/en/timer-mocks).
Attendre est un pattern à éviter puisqu'il force tes tests à être lent ou risqué ( s'ils n'attendent pas assez longtemps ). À chaque fois qu'attendre ou requêter sont inévitable et qu'il n'y a pas de support de la part du framework de test, des librairies comme [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) peuvent aider avec une solution demi-déterministe.
<br/>

❌ **Autrement:** En attendant pour un long moment, les tests seront plus lent. En attendant trop peu, les tests échoueront si l'unité testée n'a pas répondu dans les temps. Cela se résume donc à un compromis entre l'instabilité et les mauvaises performances.

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: E2E API qui se résoud uniquement lorsque l'opération asynchrone est terminée (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: Bien faire les choses, exemple: Librairie de tests qui attend les éléments du DOM

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

### :thumbsdown: Exemple d'anti pattern: Code custom qui attend

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

## ⚪ ️ 3.5 Regarder comment le contenu est servi sur le réseau

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Examples with Lighthouse")

✅ **À faire:** Applique un monitoring active qui s'assure que le chargement de la page sur un vrai réseau est optimisé - ça inclue les questions UX comme un chargement lent ou un bundle non minifié. Le marché des outils d'inspection n'est pas petit: des outils basiques comme pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) peuvent être configuré rapidement pour vérifier sur le server est disponible et répond sous un délai raisonnable. Cela ne fait qu'effleurer la surface de ce qui pourrait aller mal, il est donc préférable de choisir des outils spécialisés pour le frontend (e.g [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) et d'effectuer une analyse plus complète. L'attention doit être portée sur les symptômes, les métriques qui affectent directement l'expérience utilisateur, comme le temps de chargement d'une page, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [le temps jusqu'à ce que la page devienne intéractive (TTI)](https://calibreapp.com/blog/time-to-interactive/). En plus de ça, on peut également surveiller les causes techniques, comme s'assurer que le contenu est complet, le temps jusqu'au premier byte, l'optimisation des images, s'assurer d'une taille de DOM raisonnable, SSL et autres. Il est recommandable d'avoir ces monitorings complets à la fois pendant le développement, dans le processus CI et surtout - 24h/24 7j/7 sur les serveurs/CDN de production
<br/>

❌ **Autrement:** Il doit être décevant de se rendre compte qu'après tout le soin apporté à la création d'une interface utilisateur, des tests 100% fonctionnels réussis et des bundles sophistiqué - l'expérience utilisateur est horrible et lente à cause d'une mauvaise configuration du CDN.

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

### :clap: Bien faire les choses, exemple: Rapport d'inspection du temps de chargement avec Lighthouse

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

</details>

<br/>

## ⚪ ️ 3.6 Stub les ressources lente ou incertaine comme l'API backend

:white_check_mark: **À faire:** Lorsque tu codes tes tests mainstream ( pas les tests E2E ), évite d'impliquer toute ressource qui n'est pas sous ta responsabilité et sous ton contrôle comme l'API et utilise des stubs à la place (i.e. test double). En pratique, à la place de vrais appels à une API, utilise une librairie de tests double ( comme [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) pour simuler la réponse. L'avantage principal est d'éviter les comportements incertains - les APIs de tests ou de staging par définition ne sont pas toujours stable et de temps en temps peuvent faire échouer tes tests même si ton composant se comporte bien (l'environnement de production n'a pas été fait pour les tests et limite généralement les requêtes). Faire ça permettra de simuler plusieurs comportements d'API qui devrait diriger le comportement de ton composant, comme lorsqu'aucune donnée n'est trouvée ou que l'API émet une erreur. Enfin et surtout, les appels réseau vont énormément ralentir les tests.
<br/>

❌ **Autrement:** Le test moyen ne tourne pas plus de quelques ms, un API call moyen dure environ 100ms. Cela rend les tests ~20x plus lent.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Stub ou intercepter les appels API
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

## ⚪ ️ 3.7 Avoir quelques tests end-to-end qui lancent le système entier

:white_check_mark: **À faire:** Même si E2E (end-to-end) veut généralement dire test UI avec un vrai navigateur (voir point 3.6), pour d'autre ils signifient des tests qui englobent le système entier, en incluant le vrai backend. Ce type de tests a beaucoup de valeurs puisqu'ils couvrent les erreurs d'intégrations entre le frontend et le backend à cause d'une mauvaise compréhension des schémas d'échanges. Ils sont aussi un moyen efficace de découvrir des erreurs d'intégrations entre backends (e.g. le microservice A qui envoie le mauvais message au microservice B) et même de détecter des erreurs de déploiement - Il n'y a pas de framework backend pour les tests E2E qui soit aussi simple et mature que les frameworks UI comme [Cypress](https://www.cypress.io/) and [Puppeteer](https://github.com/GoogleChrome/puppeteer). Le point négatif de ces tests, c'est le haut cout de configuration pour un environnement avec autant de composants, et surtout leur fragilité - avec 50 microservices, même si un seul échoue l'ensemble du test E2E échoue. Pour cette raison, cette technique doit être utilisée avec parcimonie, il ne faut pas avoir plus de 1-10 tests de ce type. Ceci dit, même un petit nombre de tests E2E sont susceptibles de détecter les problèmes pour lesquels ils sont en place - les défauts de déploiement et d'intégration. Il est conseillé de les exécuter sur un environnement de pré-production.

<br/>

❌ **Autrement:** L'UI peut investir beaucoup en testant ces fonctionnalités seulement pour réaliser que les données retournées par le backend sont différentes de ce qui était attendu
<br/>

## ⚪ ️ 3.8 Accélérer les tests E2E en réutilisant les informations d'authentification

:white_check_mark: **à faire:** Dans des tests E2E qui incluent un vrai backend et utilisent un token utilisateur valide pour les appels API, ce n'est pas rentable d'isoler les tests à un niveau ou l'utilisateur est créé et authentifié à chaque requete. À la place, authentifie l'utilisateur une seule fois avant que l'exécution des tests commence (i.e before-all hook), enregistre le token en local et réutilise le dans les requetes. Ça semble violer un des principes de test principal - garder les tests autonomes sans associer les ressources. Même si c'est une inquiétude valide, dans les tests E2E la performance est une inquiétude clé et créer 1-3 requêtes API avant chaque test peut mener a un temps d'execution horrible. Réutiliser les informations d'authentification ne veut pas dire que les tests doivent agir sur la même entrée utilisateur - si le test compte sur les entrées utilisateur (e.g. test l'historique de paiement d'un utilisateur) alors assure toi de générer ces entrées dans le test et évite de les partager avec d'autres tests. Rappelle-toi aussi que le backend peut être simulé - Si les tests se concentrent sur le frontend, il vaut mieux les isoler et simuler l'API backend (voir point 3.6). 
<br/>

❌ **Autrement:** Si on prend 200 cas de tests et qu'on estime l'authentification à 100ms = 20 secondes simplement pour s'authentifier encore et encore

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Se connecter dans le before-all pas dans le before-each
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

## ⚪ ️ 3.9 Avoir un test E2E qui parcours juste les pages du site

:white_check_mark: **À faire:** Pour le suivi de production et la vérification pendant le développement, lance un seul test E2E qui visite toute ou la plupart des pages du site et vérifie qu'aucune n'échoue. Ce type de test apporte un bon retour sur investissement puisqu'il est très simple à écrire et maintenir, mais peut détecter tout type d'erreur en incluant les problèmes fonctionnels, de réseau ou de déploiement. Les autres types de smoke test et sanity check ne sont pas aussi fiable et exhaustifs - certaines équipes opérationnelles ne font que ping la page d'accueil (production) ou les développeurs qui lancent plusieurs tests d'intégrations qui ne révèlent pas les problèmes de packaging ou liés au navigateur. Il est évident que ce smoke test ne remplace pas les tests fonctionnels, mais il sert à détecter rapidement les problèmes.

<br/>

❌ **Autrement:** Tout peut sembler parfait, tous les tests passent, le health-check de production est également positif, mais le composant de paiement a eu des erreurs de packaging et seul la route /payment ne s'affiche pas

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Smoke test qui parcours toute les pages

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

## ⚪ ️ 3.10 Exposer les tests comme un document collaboratif

:white_check_mark: **À faire:** En plus d'améliorer la stabilité de l'application, les tests apportent une autre opportunité intéressante - ils servent comment une documentation de l'app.
Puisque les tests parlent naturellement à un niveau moins technique avec un langage plus produit/UX, en utilisant les bons outils, ils peuvent être utilisés comme un outil de communication qui aligne toute l'équipe - les développeurs et les clients.
Par exemple, certains frameworks permettent d'exprimer les parcours et les attentes (i.e les plans de tests) en utilisant un langage lisible par l'humain, donc chaque personne impliquée, y compris les product manager, peuvent lire, approuver et communiquer sur les tests qui sont juste devenu le document de spécification. Cette technique s'appelle aussi 'test d'acceptance' puisqu'il permet au client de définir ses critères de validité en langage simple. Il s'agit de [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) dans sa forme la plus pure. L'un des frameworks populaire qui permet ça est [Cucumber qui a un goût de Javascript](https://github.com/cucumber/cucumber-js), voir l'exemple ci-dessous. Une autre opportunité similaire, [StoryBook](https://storybook.js.org/) permet d'exposer les composants UI comme un catalogue graphique dans lequel on peut se promener à travers les différents états de chaque composant (e.g afficher une grille avec ou sans filtre, l'afficher avec plusieurs lignes ou aucune, etc), voir à quoi il ressemble, et comment déclencher cet état - cela peut servir aux équipe produit mais sert surtout de documentation aux développeurs qui utilisent ces composants

❌ **Autrement:** Après avoir investi des ressources dans les tests, ce serait juste dommage de ne pas se servir de cet investissement pour apporter encore plus de valeur

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Décrire les tests dans un language humain avec cucumber-js
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

### :clap: Bien faire les choses, exemple: Visualiser nos composants, leurs états et entrées en utilisant Storybook
![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Détecter les problèmes visuels avec des outils automatisés

:white_check_mark: **À faire:** Configure des outils automatisés pour capturer des screenshots de l'UI quand des changements sont présentés et détecter les problèmes visuels comme du contenu qui se superpose ou qui est cassé. Cela permet de vérifier que non seulement les bonnes données sont présente mais également que l'utilisateur peut les voir correctement. Cette technique n'est pas très courante, notre état d'esprit quand on pense aux tests est tourné sur les tests fonctionnels mais c'est le visuel que l'utilisateur expérimente et avec le nombre d'appareils différents disponible il est simple de rater un bug UI important. Certains outils gratuits procurent les bases - générer et enregistrer les screenshots pour qu'ils soient inspectés par un humain. Même si cette approche peut être suffisante pour de petites apps, son défaut comme tout test manuel est qu'il demande une intervention humaine à chaque fois que quelque chose change. D'un autre côté, il est assez difficile de détecter des problèmes UI automatiquement à cause du manque de définition claire - C'est ici que le domaine de 'Visual Regression' entre en jeu et résout ce problème en comparant d'ancienne UI avec les changements les plus récent pour détecter les différences. Certains outils gratuits peuvent fournir certaines de ces fonctionnalités (e.g [wraith](https://github.com/BBC-News/wraith), [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>)) mais peuvent demander un temps de configuration considérable. Les outils commerciaux (e.g. [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) vont un peu plus loin en simplifiant l'installation et en apportant des fonctionnalités avancés comme la gestion de l'UI, des alertes, de la capture automatique en éliminant le "bruit visuel" (e.g. pubs, animations) et même l'analyse du changement DOM/CSS qui a provoqué ce problème.

<br/>

❌ **Autrement:** Quelle est la qualité d'une page qui affiche un bon contenu (100% des tests passent), charge instantanément mais dont la moitié du contenu est cachée ?

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Une régression visuelle typique - le bon contenu qui est mal servi

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Bien faire les choses, exemple: Configurer wraith pour capturer et comparer les snapshots de l'UI

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

### :clap: Bien faire les choses, exemple: Utiliser Applitools pour obtenir des comparaisons de snapshots et d'autres fonctionnalités avancées

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

# Section 4️⃣: Mesurer l'efficacité des tests

<br/><br/>

## ⚪ ️ 4.1 Avoir assez de couverture pour être confiant, ~80% semble être le nombre magique

:white_check_mark: **À faire:** Le but des tests est d'être assez confiant pour avancer rapidement, évidemment, plus le code est testé plus l'équipe peut être confiante. La couverture (coverage) est une mesure du nombre de lignes de code (et branches, statements, etc) sont atteint par les tests. À partir de quand est-ce suffisant ? 10-30% est évidemment trop bas pour avoir la moindre idée de la validité du build, d'un autre côté 100% est vraiment coûteux et peut dévier votre intérêt des parties importantes pour des coins exotiques du code. La réponse longue est que ça dépend de plusieurs facteurs comme le type de l'application - si tu construis la prochaine génération d'Airbus A380 alors 100% est obligatoire, pour un site d'image de dessin animé 50% peut être déjà trop. Même si la plupart des amateurs de tests assurent que le bon seuil dépend du contexte, la plupart d'entre eux mentionnent également le nombre 80% est une bonne règle générale ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) qui devrait répondre au besoin de la plupart des applications.

Conseil d'implémentation: Tu peux vouloir configurer ton intégration continue pour qu'elle ait un seuil de couverture ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) et arrêter les builds qui ne répondent pas à ce standard (il est également possible de configurer un seuil par composant, voir l'exemple ci-dessous). En plus de ça, envisage de détecter les baisses de couverture (quand un nouveau commit à une couverture inférieure) - cela poussera les développeurs à augmenter ou au moins à conserver la même quantité de code testé. Maintenant que c'est dit, la couverture n'est qu'une mesure, une quantitative, ce n'est pas assez pour dire si vos tests sont robustes. Et il peut aussi être biaisé comme on le verra dans le point suivant

<br/>

❌ **Autrement:** La confiance et les nombres vont ensemble, sans vraiment savoir si tu testes la majorité du système, il y aura de la peur, et la peur va te ralentir

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Exemple: Un rapport de couverture classique

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Bien faire les choses, exemple: Configurer la couverture par composant (avec Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Using Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Inspecter les rapports de couverture pour détecter les sections qui ne sont pas testées et autres bizarreries

:white_check_mark: **À faire:** Certains problèmes passent juste sous le radar et sont difficiles à détecter en utilisant des outils traditionnels. Ce ne sont pas vraiment des bugs mais plutôt des comportement surprenants de l'application qui peuvent avoir un impact important. Par exemple, souvent certaines parties du code sont rarement voir jamais invoquées - tu penses que la classe 'PricingCalculator' s'occupe toujours de déterminer le prix du produit mais il se trouve qu'elle n'est jamais invoquée alors qu'on a plus de 10000 produits en base de données et de nombreuses ventes ... Les rapports de couvertures t'aident à déterminer si l'application se comporte comme tu penses qu'elle le fait. En plus de ça, ils peuvent aussi montrer le type de code qui n'est pas testé - Être informé que 80% du code est testé n'indique pas si les parties critiques sont couvertes. Générer des rapports est simple - lance juste ton application en production ou pendant les tests avec le tracking de couverture activé et récupère des rapports qui montrent à quelle fréquence chaque partie du code est invoquée. Si tu prends ton temps pour regarder ces données, tu pourras trouver des pièges
<br/>

❌ **Autrement:** Si tu ne sais pas quelles parties du code ne sont pas couvertes par les tests, tu ne sais pas d'où peuvent venir les problèmes

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Qu'est-ce qui ne va pas dans ce rapport de couverture ?

Basé sur un scénario réel, où nous avont tracké l'usage de notre application en QA et detecté un pattern intéressant sur l'authentification (indice: la quantité d'erreur de connexion n'est pas proportionnelle, quelque chose ne va pas. Finalement il s'est avéré qu'un bug front-end n'arrétait pas d'appeler l'API d'authentification)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Mesurer la couverture logique en utilisant les tests de mutations

:white_check_mark: **À faire:** Les données de couverture traditionnelles mentent souvent: elles peuvent montrer 100% de couverture, mais aucune de tes fonctions, pas même une seule, ne retourne la bonne réponse. Pourquoi ? Il mesure simplement le nombre de lignes de code que les tests ont visitées, mais ils ne vérifient pas si les tests ont effectivement testé quelque chose et vérifié la réponse. Comme quelqu'un qui effectuerai un voyage d'affaires et qui montre les tampons sur son passeport - Cela ne prouve pas qu'il a travaillé, seulement qu'il a visité quelques aéroports et hôtels.

Les tests de mutations sont là pour aider à mesurer la quantité de code qui a effectivement été TESTÉ et pas juste VISITÉ. [Stryker](https://stryker-mutator.io/) est une librairie Javascript pour les tests de mutation et son implémentation est très soignée :

(1) Il change volontairement le code et "implante des bugs". Par exemple, le code newOrder.price === 0 devient newOrder.price != 0. Ces "bugs" sont appelés des mutations

(2) Il lance les tests, si tous réussissent, alors on a un problème - Les tests n'ont pas remplis leur rôle en découvrant les bugs, les mutations sont dites survivantes. Si les tests échouent, c'est bon, les mutations ont été tuées.

Savoir que toute ou la plupart des mutations ont été tués donne une meilleure confiance qu'un rapport de couverture traditionnel et le temps de configuration est similaire.
<br/>

❌ **Autrement:** Tu seras dupé en croyant que 85% de couverture de code signifie que tes tests détecteront les bugs dans 85% du code

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: 100% de couverture, 0% testé

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

### :clap: Bien faire les choses, exemple: Un rapport Stryker, un outil pour les tests de mutations, qui détecte et compte la quantité de code qui n'est pas testé (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>

<br/><br/>

## ⚪ ️4.4 Éviter les problèmes dans le code de test avec les Test linters

:white_check_mark: **À faire:** Un groupe de plugins ESLint ont été développés spécifiquement pour inspecter le code de test et détecter les problèmes. Par exemple, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) t'avertiras lorsqu'un test est écrit à un niveau global (pas un enfant d'une déclaration describe()) ou lorsque les tests sont [sautés](https://mochajs.org/#inclusive-tests), ce qui peut conduire à une fausse croyance que les tests passent. De façon similaire, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) peut avertir lorsqu'un test n'a pas d'assertion (ne vérifie rien)
<br/>

❌ **Autrement:** Voir 90% de couverture de code et 100% de tests verts fera apparaître un grand sourire sur ton visage, jusqu'à ce que tu réalises que de nombreux tests ne vérifient rien et que plusieurs suites de tests ont été sautées. Avec un peu de chance, tu n'as rien déployé basé sur de fausses observations

<br/>
<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Un cas de test plein d'erreur, heuresement toutes détectés par les Linters

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

# Section 5️⃣: CI et autres mesures de qualité

<br/><br/>

## ⚪ ️ 5.1 Enrichir ses linter et annuler les builds qui ont des problèmes de lint

:white_check_mark: **À faire:** Les linters sont un bonus gratuit, avec 5 minutes de configurations, tu as gratuitement un auto-pilote qui surveille ton code et repère les problèmes pendant que tu tapes. Les jours où les linters étaient réservés à l'esthétique sont terminés (pas de point-virgules!). De nos jours, les linters peuvent détecter des problèmes sérieux comme des erreurs qui ne sont pas thrown correctement et les pertes d'informations. En plus de ta liste de règles basiques (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), considère d'ajouter des linters spécialisés comme [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) qui peux détecter les tests sans assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) qui détecte les promesses qui ne se resolvent pas (le code ne va jamais continuer), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) qui peut découvrir les regex qui peuvent être utilisé pour des attaques DOS, et [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) qui est capable de t'indiquer lorsque le code utilise une méthode de librairie qui fait partie des méthodes du cœur V8 comme Lodash.\_map(...)

<br/>

❌ **Autrement:** Imagine un jour de pluie ou ta production n'arrête pas de crasher mais les logs ne montrent aucune stack trace d'erreur. Qu'est-ce qu'il s'est passé ? Ton code a malencontreusement émis un objet qui n'était pas une erreur et la stack trace a été perdu, une bonne raison de se taper la tête contre les murs. 5 minutes de configuration d'un linter pourraient permettre de détecter cette erreur et sauver la journée

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :thumbsdown: Exemple d'anti pattern: Le mauvais objet d'erreur est émit par erreur, aucune stack-trace ne va apparaitre pour cette erreur. Heuresement, ESLint catch le prochain beug de production

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>

<br/><br/>

## ⚪ ️ 5.2 Raccourcir la boucle de retours avec du CI local pour les développeurs

:white_check_mark: **À faire:** Tu utilises un outil de CI avec une bonne inspection de qualité comme des tests, du linting, des checks de vulnérabilités, etc ? Aide les développeurs à lancer également cette pipeline en local pour solliciter un retour instantané et raccourcir la [boucle de feedback](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Pourquoi ? Un processus de tests efficace constitue de nombreuses boucles itératives: (1) essai -> (2) retours -> (3) refactoriser. Plus le retour est rapide, plus le développeur peut effectuer d'itérations d'améliorations par modules et perfectionner le résultat. D'un autre côté, lorsque les retours sont lent à arriver, moins d'améliorations peuvent être effectuées au sein d'une journée, l'équipe peut être déjà passée à un autre sujet/tache/module et peut ne pas être prête a affiner ce module.

En pratique, certains fournisseurs de CI (Exemple: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/)) autorisent le lancement de la pipeline en local. Certains outils commerciaux comme [wallaby fournissent des informations de valeur et des tests](https://wallabyjs.com/) pendant que le développeur prototype (pas d'affiliation). Alternativement, tu peux simplement ajouter un script npm au package.json qui lance toute les commandes de qualités (e.g. tests, lint, vulnérabilités) - utilise des outils comme [concurrently](https://www.npmjs.com/package/concurrently) pour la parallélisation et des code de retour différents de 0 si l'un des outils échoue. Maintenant le développeur peut juste lancer une commande - e.g. 'npm run quality' - pour recevoir un retour instantané. Envisage également d'annuler un commit si le contrôle de qualité ne passe pas en utilisant githook ([husky can help](https://github.com/typicode/husky))
<br/>

❌ **Autrement:** Quand les résultats de qualité arrivent le jour suivant le développement, les tests ne sont pas une partie fluide du développement mais plutôt une étape formelle après coup
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Script npm qui effectue une inspection de la qualité du code, tout est lancé en parallèle sur demande ou lorsque le développeur essaye de push du code

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

## ⚪ ️5.3 Effectuer des tests e2e sur un vrai miroir de production

:white_check_mark: **À faire:** Les tests end to end (E2E) sont le défi principal de chaque pipeline CI - créer un miroir éphémère de la production à la volée avec tous les services clouds lié peut être fastidieux et coûteux. Le jeu est de trouver le meilleur compromis: [Docker-compose](https://serverless.com/) permet de créer des environnement dockerisés isolés avec des containers identiques en utilisant un simple fichier text mais la technologie backend (e.g réseau, modèle de déploiement) est différent de la vrai production. Tu peux l'associer à [‘AWS Local’](https://github.com/localstack/localstack) pour travailler avec un stub des services AWS. Si tu es [serverless](https://serverless.com/), plusieurs frameworks comme serverless et [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) permettent l'invocation locale de code FaaS.

Le large écosystème de Kubernetes doit encore formaliser un outil standard pour la mise en miroir locale et CI, bien que de nombreux nouveaux outils soient lancés fréquemment. Une des approches est de lancer un 'minimized-Kubernetes' en utilisant des outils comme [Minikube](https://kubernetes.io/docs/setup/minikube/) et [MicroK8s](https://microk8s.io/). Une autre approche est de tester avec un 'vrai-Kebernetes' distant, certains fournisseurs CI (e.g. [Codefresh](https://codefresh.io/)) ont une intégration native avec l'environnement Kubernetes et rendent simple le lancement d'une pipeline CI sur le vrai environnement, d'autres permettent d'exécuter des scripts custom sur le Kubernetes distant.
<br/>

❌ **Autrement:** Utiliser des technologies différentes pour la production et pour les tests demande de maintenir deux modèles de déploiement et créer une séparation entre l'équipe dev et l'équipe ops.
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Exemple: Une pipeline CI qui génère un cluster Kubernetes à la volée <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Paralléliser l'exécution des tests

:white_check_mark: **À faire:** Lorsque c'est fait correctement, les tests sont tes amis 24/7 en fournissant un retour quasi instantané. En pratique, exécuter 500 tests unitaires liés au processeur sur un seul thread peut prendre trop longtemps. Heureusement, les outils de tests et les plateformes CI moderne (comme [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) et [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) peuvent paralléliser les tests sur plusieurs processus et améliorer significativement le temps de retour. Certains fournisseurs CI font également de la parallélisation de tests à travers des containers (!) ce qui raccourcis encore plus la boucle de retour. Que ce soit localement sur plusieurs processus, ou sur un serveur Cloud avec plusieurs machines - paralléliser demande de garder les tests autonomes puisqu'ils peuvent tourner sur différents processus.

❌ **Autrement:** Obtenir les résultats de tests 1h après avoir publié du nouveau code, pendant que tu es déjà en train de coder la fonctionnalité suivante, est une bonne recette pour rendre les tests moins pertinents
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple: Mocha parallel & Jest distancent facilement le Mocha traditionnel grace à la parallélisation ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Rester loin des problèmes légaux en utilisants des vérifications de license et de plagiat

:white_check_mark: **À faire:** Les problèmes de licences et de plagiat ne sont probablement pas au centre de votre attention pour l'instant, mais pourquoi ne pas cocher également cette case en 10 minutes ? Plusieurs packages npm comme [license check](https://www.npmjs.com/package/license-checker) et [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commerciaux avec un essai gratuit) peuvent être facilement intégré dans ta pipeline CI et inspecter les problèmes tels que les dépendances avec des licences restrictives ou du code qui a été copié-collé à partir de Stack Overflow et qui violerai certains droits d'auteur

❌ **Autrement:** Involontairement, les développeurs peuvent utiliser un package avec une license inapproprié, ou copier/coller du code commercial et tomber sur des problèmes légaux
<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Bien faire les choses, exemple:

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

## ⚪ ️5.6 Inspecter constamment les dépendences vulnérables

:white_check_mark: **À faire:** Même les dépendances les plus réputées comme Express ont des vulnérabilités connues. Cela peut être apprivoisé facilement avec des outils de la communauté comme [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), ou des outils commerciaux comme [snyk](https://snyk.io/) (qui offre également une version de la communauté gratuite). Les deux peuvent être appelés depuis ton CI à chaque build

❌ **Autrement:** Garder ton code exempt de vulnérabilités sans les outils appropriés demande de suivre constamment les publications en ligne à propos des nouvelles menaces. Plutôt fastidieux.

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Exemple: Résultat d'audit Npm

![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>

<br/><br/>

## ⚪ ️5.7 Automatiser les mises-à-jour de dépendences

:white_check_mark: **À faire:** L'introduction récente du package-lock.json par Yarn et npm à introduit un vrai défi (la route vers l'enfer est pavée de bonnes intentions) - par défaut maintenant, les packages ne sont pas mis à jour. Même une équipe qui lance plusieurs nouveaux déploiements avec 'npm install' & 'npm update' n'aura pas de nouvelles mise à jour. Cela conduit au mieux, à des dépendances à des packages de qualité inférieure, au pire à du code vulnérable. Les équipes dépendent maintenant de la bonne volonté et de la mémoire des développeur pour mettre à jour manuellement le package.json ou utiliser des outils [comme ncu](https://www.npmjs.com/package/npm-check-updates). Une méthode plus fiable pourrait être d'automatiser le processus de récupération des versions de dépendances les plus fiables, bien qu'il n'y ait pas de solutions miracle, il y a deux possibilités d'automatisation:

(1) Le CI peut faire échouer les builds qui ont des dépendances obsolètes - en utilisant des outils comme [‘npm outdated’](https://docs.npmjs.com/cli/outdated) ou 'npm-check-updates (ncu)'. Faire ça forcera les développeurs à mettre à jour les dépendances.

(2) Utiliser un outil commercial qui peut scanner le code et envoyer automatiquement une pull-request avec les dépendances mises à jour. La question intéressante restante est, quel devrait être la politique de mises à jour - Mettre à jour chaque patch génère trop de surcharge, mettre à jour juste après une release majeure peut introduire une version instable (de nombreuses vulnérabilités sont découverte dans les premiers jours après la release, [voir l'incident](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope).

Une politique de mise à jour efficace peut autoriser une 'période d'acquisition' - laisser le code en retard par rapport à @latest pour quelque temps et versions avant de considérer la copie locale comme obsolète (e.g la version locale est 1.3.1 et la version du repo est 1.3.8)
<br/>

❌ **Autrement:** Ta production utilisera des packages qui ont été taggé explicitement par leurs auteurs comme risquées

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Exemple: [ncu](https://www.npmjs.com/package/npm-check-updates) peut être utilisé manuellement ou dans une pipeline CI pour détecter à quel point le code est en retard vis a vis des dernières versions

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")

</details>

<br/><br/>

## ⚪ ️ 5.8 Autres conseils CI, sans rapports avec Node

:white_check_mark: **À faire:** Ce post se concentre sur les conseils de tests qui sont en lien avec, ou peuvent être illustrés, avec Node JS. Ce point, cependant, regroupe quelques conseils sans rapports avec Node qui sont bien connus

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Utilise une syntaxe déclarative. C'est la seule option pour la plupart des fournisseurs mais d'anciennes versions de Jenkins autorisent l'utilisation du code ou de l'UI</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Choisis un fournisseur qui a une intégration Docker native</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Échoue rapidement, lance les tests les plus rapides d'abord. Crée des 'tests de fumée' pour certaines étapes qui regroupe plusieurs inspections rapide (e.g liting, tests unitaires) et fourni des commentaires rapides à celui qui commit le code</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Facilite le parcours des informations de build, cela inclut les rapports de tests, de couverture, de mutation, les logs ..etc</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Crée plusieurs pipelines/jobs pour chaque événement, réutiliser les étapes entre eux. Par exemple, configure un job pour les commits de features sur une branche et un différent pour une PR sur master. Laisse chacun réutiliser la logique en utilisant des étapes partagées (la plupart des fournisseurs ont des mécanismes pour réutiliser le code)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Ne mets jamais de secrets dans la déclaration du job, récupère-les depuis un secret store ou depuis les configurations du job</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Augmente explicitement la version dans un build de release, ou au moins vérifie que le développeur l'a fait</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Build une fois et effectue toute les inspections sur l'artefact de build (e.g. Docker image)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Test dans un environnement éphémère qui ne change pas d'état entre les builds. Le cache des nodes peut être la seule exception</li></ol>
<br/>

❌ **Autrement:** Tu rateras des années de sagesse

<br/><br/>

## ⚪ ️ 5.9 Structure de build: Lancer les mêmes étapes CI sur plusieurs versions de Node

:white_check_mark: **À faire:** Le contrôle de qualité est un jeu de hasard, plus tu couvres de terrain, plus tu as de chance de détecter les problèmes rapidement. Quand tu développes des packages réutilisable ou que tu lances une production avec plusieurs clients qui ont différentes configurations et versions de Node, le CI doit lancer la pipeline de tests sur toutes les configurations possible. Par exemple, imaginons qu'on utilise MySQL pour certains clients et Postgres pour d'autres - Certains fournisseurs CI supportent une fonctionnalitée appelée 'Matrix' qui permet de lancer les tests contre toutes les permutations de MySQL, Postgres et plusieurs versions de Node comme 8, 9 et 10. Cela peut se faire en utilisant seulement des configurations sans efforts supplémentaire (en considérant que tu as des tests ou d'autres contrôles de qualités). D'autres CIs qui ne supportent pas Matrix peuvent avoir des extensions qui permettent ça
<br/>

❌ **Autrement:** Après avoir fait tout le travail d'écrire des tests, va-t-on laisser passer des bugs seulement à cause de problèmes de configurations ?

<br/>

<details><summary>✏ <b>Exemple de code</b></summary>

<br/>

### :clap: Exemple: Utiliser les définition de build de Travis (fournisseur CI) pour lancer le même test sur plusieurs versions de Node

<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# L'équipe

## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Rôle:** Auteur

**À propos:** Je suis un consultant indépendant qui travaille avec des entreprises Fortune 500 et des startups pour peaufiner leurs applications JS et Node.JS. Plus qu'aucun autre sujet, je suis fasciné par et vise à maîtriser l'art du test. Je suis aussi l'auteur de [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

**📗 Cours en ligne:** Tu aimes ce guide et tu veux pousser tes compétences de test à l'extreme ? Pense à regarder mon cours complet [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/>

**Me suivre:**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 Contact](https://testjavascript.com/contact-2/)
- [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**Rôle:** Réviseur et conseiller technique

A pris soin de revoir, améliorer, linter et peaufiner tout les textes

**À propos:** Ingénieur web full-stack, passioné par Node.js et GraphQL

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Rôle:** Concept, design et bons conseils

**À propos:** Un développeur front-end averti, expert CSS et maniaque des émojis

## [Kyle Martin](https://github.com/js-kyle)

**Rôle:** Aide à faire tourner ce projet, et revois les pratiques liés à la sécurité

**À propos:** Aime travailler sur des projets Node.JS et la sécurité des applications web.

## Contributors ✨

Merci à ces merveilleuses personnes qui ont contribué à ce repo!

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
