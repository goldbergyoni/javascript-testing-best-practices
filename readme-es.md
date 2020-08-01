<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 Por qué esta guia puede hacerte llevar tus habilidades de testing al siguiente nivel

<br/>

## 📗 45+ buenas practicas: Super comprensiva y exhaustiva

Esta es una guia completa para Javascript y Node de la A a la Z. Resumen y selecciona docenas de los mejores post de blogs, libros, y herramientas ofrecidas por el mercado

## 🚢 Advanzado: Va 10.000 kilometros más allá de lo basico

Súbete a un viaje que va más allá de lo básico, llegando a temas avanzados como testeando en producción, mutation testing, property-based testing y muchas otras herramientas estratégicas y profesionales. Si lees esta guía completamente es probable que tus habilidades de testing este por encima de la media

## 🌐 Full-stack: front, backend, CI, cualquier cosa

Empieza por comprender las tecnicas de testing ubicuas que son la base de cualquier nivel de aplicación. Luego, profundice en tu área de elección: frontend/UI, backend, CI o tal vez todos.

<br/>

### Escrita por Yoni Goldberg

- Consultor JavaScript & Node.js
- 📗 [Testing Node.js & JavaScript de la A a la Z](https://www.testjavascript.com) - Mi curso completamente online con más de [10 horas de video](https://www.testjavascript.com), 14 tipos de test y más de 40 buenas practicas
- [Sigueme en Twitter ](https://twitter.com/goldbergyoni/)

<br/>

### Traducciones - leelas en tu propio idioma

- 🇨🇳[Chino](readme-zh-CN.md) - cortesia de [Yves yao](https://github.com/yvesyao)
- 🇰🇷[Coreano](readme.kr.md) - cortesia de [Rain Byun](https://github.com/ragubyun)
- 🇵🇱[Polaco](readme-pl.md) - cortesia de [Michal Biesiada](https://github.com/mbiesiad)
- Quieres traducir a tu propio lenguaje? porfavor abre una issue 💜

<br/><br/>

## `Tabla de Contenidos`

#### [`Sección 0: La Regla de Oro`](#section-0️⃣-the-golden-rule)

Un solo consejo que inspira a todos los demás (1 apartado especial)

#### [`Sección 1: La Anatomía de un Test`](#section-1-the-test-anatomy-1)

La base - estructurando tests claros (12 apartados)

#### [`Sección 2: Backend`](#section-2️⃣-backend-testing)

Escribiendo test de backend y Microservicios eficientemente (8 apartados)

#### [`Sección 3: Frontend`](#section-3️⃣-frontend-testing)

Escribiendo test para web UI incluyendo test de componente y E2E (11 apartados)

#### [`Sección 4: Midiendo la Efectividad de los Tests`](#section-4️⃣-measuring-test-effectiveness)

Vigilando al vigilante - midiendo la calidad de los test (4 apartados)

#### [`Sección 5: Integración Continua`](#section-5️⃣-ci-and-other-quality-measures)

Pautas para Integracion Continua en el mundo de JS (9 apartados)

<br/><br/>

# Sección 0️⃣: La Regla de Oro

<br/>

## ⚪️ 0 La Regla de Oro: Diseñando testing ligero

:white_check_mark: **Haz:**
El código de los test no es como el código de producción - diséñelo para que sea simple, corto, sin abstracciones, plano, agradable de trabajar, ligero. Uno debe mirar un test y entender la intención al instante.

Nuestras mentes están llenas por el código de producción, no tenemos espacio de cabeza para añadir más cosas complejas. Si intentamos introducir otro código desafiante en nuestro cerebro, ralentizará al todo el equipo, lo que va en contra de la razón por la que hacemos testing. Prácticamente aquí es donde muchos equipos simplemente abandonan el testing.

Los test son una oportunidad de tener algo más: un asistente amable y sonriente, con el que es un placer trabajar y da mucho valor a cambio de una inversión tan pequeña. La ciencia nos dice que tenemos dos sistemas cerebrales: el sistema 1 se usa para actividades sin esfuerzo como conducir un automóvil en una carretera vacía y el sistema 2, que está destinado a operaciones complejas y conscientes como resolver una ecuación matemática. Diseña tus test para el sistema 1, cuando observes el código de un test, debería parecer tan fácil como modificar un documento HTML y no como resolver 2X(17 × 24).

Esto se puede lograr mediante la seleccion de técnicas cuidadosamente, herramientas y objetivos de test que son rentables y proporcionan un gran retorno de la inversión. Testee solo lo que sea necesario, esfuércese por mantenerlo ágil, a veces incluso vale la pena abandonar algunos test y cambiar la confiabilidad por agilidad y simplicidad.

![alt text](/assets/headspace.png "No tenemos espacio para la más complejidad")

La mayoría de los siguientes consejos son derivados de este principio.

### ¿Listo para empezar?

<br/><br/>

# Sección 1: La Anatomía de un Test

<br/>

## ⚪ ️ 1.1 Incluye 3 partes en los nombres de tus test

:white_check_mark: **Haz:** El reporte de un test debe indicar si la revisión de la aplicación actual cumple los requisitos para las personas que no están necesariamente familiarizadas con el código: el tester, el DevOps que está desplegangolo y el futuro tú de dentro de dos años. Esto se puede lograr si los test hablan al nivel de los requisitos e incluyen 3 partes:

(1) ¿Qué se está testeando? Por ejemplo, el método ProductsService.addNewProduct

(2) ¿Bajo qué escenario y circunstancias? Por ejemplo, no se pasa ningún precio al método

(3) ¿Cuál es el resultado esperado? Por ejemplo, el nuevo producto no está aprobado

<br/>

❌ **De lo contrario:** Un despliegue simplemente ha fallado, un test llamado "Agregar producto" ha fallado. ¿Esto te dice exactamente qué está funcionando mal?

<br/>

**👇 Nota:** Cada apartado tiene ejemplos de código y, en ocasiones, también una imagen ilustrativa. Haga clic para ampliar
<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>
  
<br/>
  
### :clap: Ejemplo de cómo hacerlo correctamente: Un nombre de test que consta de 3 partes

![](https://img.shields.io/badge/🔨%20Example%20using%20Mocha-blue.svg "Ejemplo usando Mocha para ilustrar la idea")

```javascript
//1. unidad que esta siendo testeada
describe('Products Service', function() {
  describe('Add new product', function() {
    //2. escenario y 3. quá se espera
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});

```

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Un nombre de test que consta de 3 partes

![alt text](/assets/bp-1-3-parts.jpeg "Un nombre de test que consta de 3 partes")

</details>

<br/>
<details><summary>© <b>Creditos y más información</b></summary>
  1. <a href='https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html'>Roy Osherove - Naming standards for unit tests</a>
</details>

<br/><br/>

## ⚪ ️ 1.2 Estructura tus test con el patron AAA

:white_check_mark: **Haz:** Estructura tus test con 3 secciones bien separadas Arreglar u organizar, Actuar y Afirmar (AAA en inglés Arrange, Act & Assert). Seguir esta estructura garantiza que quien lea nuestro test  no gaste CPU-cerebro en comprender los test:

1st A - Arreglar: configura el código acercarte al escenario que el test pretende simular. Esto podría incluir crear instancias de la unidad bajo el constructor del test, agregar registros de base de datos, mocks y stubs de objetos y cualquier otro código necesario

2nd A - Actuar: Ejecuta la unidad en test. Normalmente 1 línea de código

3rd A - Afirmar: Comprobar que el valor recibido satisface las expectativas. Normalmente 1 línea de código

<br/>

❌ **De lo contrario:** No solo emplearas horas comprendiendo el código principal, si no que lo que deberia haber sido la parate mas simple del día (testing) ha estrujado tu cerebro

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Un test estructurado con el patron AAA

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest") ![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

```javascript
describe("Customer classifier", () => {
  test("When customer spent more than 500$, should be classified as premium", () => {
    //Arreglar / organizar
    const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
    const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });

    //Actuar
    const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);

    //Afirmar
    expect(receivedClassification).toMatch("premium");
  });
});
```

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Sin separación, una pieza, más dificil de interpretar

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

## ⚪ ️1.3 Describe las expectativas en el lenguaje del producto.: usa aserciones estilo BDD

:white_check_mark: **Haz:** Escribir el código de tus test de forma declarativa permite que aquel que lo lea tenga al instante la idea sin tener que catar CPU-cerebro. Cuando escribes el código de los test de forma imperativa estará lleno de condiciones lógicas y obligas al que lo lee a gastar mucho más tiempo en comprenderlo. En este caso, escribe el código de la forma más humana, de forma declarativa BDD usando `expect` o `should` y sin usar código personalizado. Si Chai o Jest no incluyen las aserciones que deseas y se hace muy repetitivo, siempre puede usar [extender Jest matcher (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) o escribir un [plugin de Chai](https://www.chaijs.com/guide/plugins/)
<br/>

❌ **De lo contrario:** El equipo escribirá menos test y acabará marcando los test más molestos con .skip()

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha y Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

### :thumbsdown: Ejemplo Anti Patrón: quien lea nuestro test deberá hojear un código largo e imperativo para conocer la historia del test

```javascript
test("When asking for an admin, ensure only ordered admins in results", () => {
  //presuponiendo que hayamos agregado aquí dos administradores "admin1", "admin2" y "user1"
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

### :clap: Ejemplo de cómo hacerlo correctamente: Ojear el siguiente test declarativo es muy sencillo

```javascript
it("When asking for an admin, ensure only ordered admins in results", () => {
  //presuponiendo que hayamos agregado aquí dos administradores
  const allAdmins = getUsers({ adminOnly: true });

  expect(allAdmins)
    .to.include.ordered.members(["admin1", "admin2"])
    .but.not.include.ordered.members(["user1"]);
});
```

</details>

<br/><br/>

## ⚪ ️ 1.4 Acercarse al testing caja-negra: Testea solo metodos publicos

:white_check_mark: **Haz:** Testear las partes internas suele traer un gasto extra enorme para muy poco beneficio. Si tu código/API comprueba todo los resultado correctamente, ¿deberias perder las proximas 3 horas en comprobar como esta funcionando internamente y despues mantener esos test tan fragiles? Cada vez que se comprueba un comportamiento publico, la implementacion privada es implicitamente testeada y tus test se romperan solo si hay un problema concreto (por ejemplo una salida incorrecta). Este enfoque tambien es conocido como `behavioral testing` (testing de comportamiento). Por otro lado, si se testean las partes internas (caja-blanca) tu enfoque cambia de planificar la salida del componente a detalles minusculos, y tus test pueden romperse debido a refactors de código menores sin que se rompan los test de salida, por lo que aumenta tremendamente el mantenimiento de los mismos.<br/>

❌ **De lo contrario:** Tus test se comportaran como la fabula [que viene el lobo](https://es.wikipedia.org/wiki/El_pastor_mentiroso): gritando falsos positivos (por ejemplo, un test dalla por que se cambio el nombre a una variable provada). Como es de esperar, la gente empezara a ingnorar estos test hasta que un día ignoren un test de verdad...

<br/>
<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Un test esta testeando la parte interna sin ninguna razón aparente

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha & Chai")

```javascript
class ProductService {
  //este metodo es usado solo internamente
  //Cambiarle el nombre causara que el test falle
  calculateVATAdd(priceWithoutVAT) {
    return { finalPrice: priceWithoutVAT * 1.2 };
    //Cambiar el formatos de salida o nombre de la clave a continuacion hara que el test falle
  }
  //public method
  getPrice(productId) {
    const desiredProduct = DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
    return finalPrice;
  }
}

it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
  //No hay ningún requisito para permitir a los usuarios calcular el IVA, solo existe el de mostrar el precio final al usuario. Sin embargo, falsamente insistimos en testear las partes privadas de la clase.
  expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});
```

</details>

<br/><br/>

## ⚪ ️ ️1.5 Eligiendo los dobles de los test correctamente: Evita mocks en favor de stubs y spies

:white_check_mark: **Haz:** Los dobles de los test son un mal necesario por que estan acoplados a las tripas de la aplicacion, sin embargo, algunos proporcionan un valor inmenso (<a href="https://martinfowler.com/articles/mocksArentStubs.html" data-href="https://martinfowler.com/articles/mocksArentStubs.html" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Aquí tienes un recordatorio sobre los dobles de los test: mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)</a>).

Antes de usar un doble, hazte una simple pregunta: ¿Lo voy a usar para testear una funcionalidad que aparece, o puede aparecer, en el documento de requisitos? Si no, eso huele que estas testeando partes privadas.

Por ejemplo, si quieres testear que tu app se comporta razonablemente cuando el servicio de pagos está caido, deberias hacer un stub del servicio de pagos y devolver un 'Sin respuesta' para asegurar que la unidad que está siendo testeada devuelve el valor correcto. Esto verifica que el comportamiento/respuesta/resultado de nuesta app en ciertos escenarios. Tambien podrias usar un spy para asegurar que un email ha sifo enviado cuando este servicio está caidom — esto es nuevamente una verificacion de comportamiento que probablemente aparezca en el documento de requisitos ("Enviar un correo electrónico si no se pudo guardar el pago"). En el lado opuesto, si se mockea el servicio de pagos y se asegura que se haya llamado con el tipado correcto — entonces tu test esta comprobando cosas internas que tienen nada que ver con la funcionalidad de la app y es muy probable que cambien con frecuencia
<br/>

❌ **De lo contrario:** Cualquier refactor de codigo te exigirá buscar todos los mocks que tengas y tendras que actualizarlos en consecuencia. Los test pasan de ser un amigo útil a una carga más

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Mocks centrados en la parte interna

![](https://img.shields.io/badge/🔧%20Example%20using%20Sinon-blue.svg "Ejemplos con Sinon")

```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
  //Asumimos que ya hemos añadido un producto
  const dataAccessMock = sinon.mock(DAL);
  //hmmm MAL: testear las partes internas es nuestro principal objetivo, en vez de ser un efecto secundario
  dataAccessMock
    .expects("deleteProduct")
    .once()
    .withArgs(DBConfig, theProductWeJustAdded, true, false);
  new ProductService().deletePrice(theProductWeJustAdded);
  dataAccessMock.verify();
});
```

<br/>

### :clap:Ejemplo de cómo hacerlo correctamente: los spies se centran en testear los requisitos pero como efecto secundario inevitable se estan testeando las partes internas

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
  //Asumimos que ya hemos añadido un producto
  const spy = sinon.spy(Emailer.prototype, "sendEmail");
  new ProductService().deletePrice(theProductWeJustAdded);
  //hmmm OK: ¿Testeamos las partes internas? Si, pero como efecto secundario de hacer test de los requisitos (enviar un email)
  expect(spy.calledOnce).to.be.true;
});
```

</details>

<br/><br/>

## 📗 ¿Quieres aprender todas esto con video en directo?

### Visita el curso online [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/><br/>

## ⚪ ️1.6 No uses “foo”, usa datos realistas

:white_check_mark: **Haz:** A menudo, los bugs de producción se revelan bajo una entrada muy específica y sorprendente: cuanto más realista sea la entrada de un test, mayores serán las posibilidades de detectar bugs temprano. Utiliza librerias dedicadas como [Faker] (https://www.npmjs.com/package/faker) para generar datos pseudo-reales que se asemejan en variedad y forma a los datos de prodcucción. Por ejemplo, dichas librerias pueden generar números de teléfono realistas, nombres de usuario, tarjetas de crédito, nombres de empresas e incluso texto "lorem ipsum". También puedes crear algunos test (además de los test unitarios, no como un reemplazo) que aleatorizan los datos falsos para estirar la unidad que estamos testeando o incluso importar datos reales de su entorno de producción. ¿Quieres llevarlo al siguiente nivel? Vea la próxima sección (test basados en propiedades).
<br/>

❌ **De lo contrario:** Todo tus test de desarrollo estaran en falsos verdes cuando uses datos sinteticos como "Foo", pero luego en produccion pueden ponerse en rojo cuando un hacker use cadenas extrañas como “@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA”

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Un conjunto de test que dan ok debido a datos no realistas

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

```javascript
const addProduct = (name, price) => {
  const productNameRegexNoSpace = /^\S*$/; //no se admiten espacios

  if (!productNameRegexNoSpace.test(name)) return false; //esta rama nunca se testeara debido a inputs sinteticos

  //algo de logica aquí
  return true;
};

test("Wrong: When adding new product with valid properties, get successful confirmation", async () => {
  //La cadena "Foo" que es usada en todo los test, nunca provocara un resutado false
  const addProductResult = addProduct("Foo", 5);
  expect(addProductResult).toBe(true);
  //Falso positivo: la operación tuvo éxito porque nunca lo intentamos con un 
  //nombre de producto largo que incluya espacios
});
```

<br/>

### :clap:Ejemplo de cómo hacerlo correctamente: Generando datos de entrada realistas

```javascript
it("Better: When adding new valid product, get successful confirmation", async () => {
  const addProductResult = addProduct(faker.commerce.productName(), faker.random.number());
  //Datos de entrada generados aleatoreamente: {'Sleek Cotton Computer',  85481}
  expect(addProductResult).to.be.true;
  //El test falla, El valor de entrada random ha provocado que se vaya por un camino que nunca planeamos
  //!Hemos descubierto un bug muy pronto!
});
```

</details>

<br/><br/>

## ⚪ ️ 1.7 Testea muchas combinaciones de entrada utilizando test basados en propiedades

:white_check_mark: **Haz:** Por lo general elegimos pocos datos de entrada por cada test. Incluso cuando el formato de entrada se parece a datos reales (ver sección "no uses foo"), cubrimos solo unas pocas combinaciones de datos de entrada (method(‘’, true, 1), method(“string” , false” , 0)), Sin embargo, en producción, un API que es llamada con 5 parametros puede ser invocada por miles de permutaciones diferentes, una sola puede hacer que nuestro poceso falle ([ver Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)). ¿Qué tal si pudieras escribir un solo test que envíe 1000 permutaciones de diferentes entradas automáticamente y capture qué entrada hace que código no devuelva la respuesta correcta? Los test basados en propiedades son una técnica que hace exactamente eso: al enviar todas las combinaciones de entrada posibles a la unidad que está siendo testada, aumenta la probabilidad de encontrar un bug. Por ejemplo, dado un metodo — addNewProduct(id, name, isDiscount) — las librerias compatibles llamaran a ese metodo con muchas combinaciones (numeros, textos y boleanos) como (1, “iPhone”, false), (2, “Galaxy”, true). Puedes ejecutar test basados en propiedades usando nuestra libreria de esta favorita (Mocha, Jest, etc) como [js-verify](https://github.com/jsverify/jsverify) o [testcheck](https://github.com/leebyron/testcheck-js) (mucho mejor documentada). Actualizado: Nicolas Dubien sugiere en los comentarios [checkout fast-check](https://github.com/dubzzz/fast-check#readme) que parece ofecer caracteristicas adicionales y es activamente mantenida.
<br/>

❌ **De lo contrario:** Inconscientemente, eliges los datos de entradas para tus test que cubren solo las ramas de código que funcionan bien. Desafortunadamente, esto disminuye la eficiencia de los test como vehículo para detectar bugs.

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Testear muchos datos de entrada permutados con “fast-check”

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

```javascript
import fc from "fast-check";

describe("Product service", () => {
  describe("Adding new", () => {
    //esto ejecutara 100 veces con diferentes prodiedades al azar
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

## ⚪ ️ 1.8 Si lo necesitas, usa solo snapshots cortos y en el propio test

:white_check_mark: **Haz:** Cuando hay necesidad de usar [snapshot testing](https://jestjs.io/docs/es-ES/snapshot-testing), usa solo snapshots cortos y bien enfocados (por ejemplo 3-7 lineas) y que esten incluidos en el propio test ([Inline Snapshot](https://jestjs.io/docs/es-ES/snapshot-testing#inline-snapshots)) y no como ficheros externos. Mantener esta dirección te garantiza que tus test se explican por si mismos y a la vez que sean menos fragiles.

Por otro lado, los tutoriales y herramientas basados en ‘classic snapshots’ tienden a guardar ficheros muy grandes en medios externos (por ejemplo component rendering markup, API JSON result) cada vez que se ejecutan los test para comparar los resultados recividos con la version guardada. Esto, por ejemplo, puede aosciar nuestro test a 1000 lineas con 3000 valores de datoa que quien este escribiendo test jamas leera ni razonará. ¿Por qué está mal esto? Al hacerlo, hay 1000 razones para que tu test falle - tan solo el cambio de una linea de código es suficiente para que el snapshoot se invalide y es muy probable que esto ocurra a menudo. ¿Como de frecuente? cada espacio, comentatio o pequeño cambio de css/html. Y no solo eso, el nombre del test no nos va a dar ni una sola pista de que está fallando, solo verifica que esas 1000 lineas han cambiado. Además obliga a quien escribe los test a asumir como correcto un fichero enorme que no ha podido inspeccionar y corroborar. Todo estos son sintomas de una prueba oscura que no está bien enfocada y trata de cubrir demasiadas cosas a la vez

Vale la pena señalar que hay algunos casos en los que los snapshoots grandes y externos son buenos - cuando comporbamos el esquema y no los datos (ignorando los valores y centrandonos en los campos) o en los casos en el que el documento no va a cambiar apenas en el tiempo.
<br/>

❌ **De lo contrario:** Un test UI falla. El codigo parece correcto, la pantalla esta pintando todos los pixels correctamente, ¿que ha pasado? tu test de snapshoot ha encontrado una diferencia entre el origen y lo que ha recibido al ejecutarse: simplemente hay un espacio añadido en cualquier parte... 

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Acoplando nuestro test a un fichero no revisado de 2000 lineas de código

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

```javascript
it("TestJavaScript.com is renderd correctly", () => {
  //Arreglar

  //Actuar
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  //Afirmar
  expect(receivedPage).toMatchSnapshot();
  //Ahora nosotros implicitamente mantenemos un fichero de 2000 lineas
  //cada salto de linea o comentario añadido van a romper nuestro test
});
```

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Lo experado es visible y esta enfocado

```javascript
it("When visiting TestJavaScript.com home page, a menu is displayed", () => {
  //Arreglar

  //Actuar
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
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

## ⚪ ️1.9 Evitar fixtures globales y seeds, añade datos por cada test

:white_check_mark: **Haz:** Siguiendo la regla de oro (sección 0), cada test debe añadir y actuar en su propio conjunto de filas DB para evitar el acoplamiento y poder explicar fácilmente sobre el flujo del test. En realidad muchos testers se saltan esta regla al añadir datos a la DB solo una vez antes de ejecutar los test ([tambien conocido como ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) a favor de mejorar el rendimiento. Si bien el rendimiento es una preocupación válida — puede mitigarse de otras formas (consulte la sección "test de componentes"), sin embargo, la complegidad del test es más dolorosa que otras consideraciones la mayoria de las veces. De manera practica, haga que cada test añada explicitamente los registros que necesitas y actua sobre ellos. Si el rendimiento se convierte en algo critico — se puede llegar al compromiso de utilizar los mismos datos en un conjunto de test siempre que no se muten los datos (por ejemplo en queries).

<br/>

❌ **De lo contrario:** FMuchos test fallaran, un despliegue se aborta, nuestro equipo perdera mucho tiempo, ¿tenemos un bug? vamos a investigar, ah no — parece que dos test estan mutando el mismo dato

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: tests no son independientes y dependenden de una inserción global de datos en la DB

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

```javascript
before(async () => {
  //añadiendo datos de sites y admin a nuestra DB. ¿Donde estan los datos? fuera. En un json extermo o en un modelo da migración
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //Se que el nombre de site "portal" existe, — lo he visto en seed.json
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //Se que el nombre de site "portal" existe, — lo he visto en seed.json
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Fallo! El test anterior ha cambiado el nombre :[
});

```

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Podemos permanecer dentro de nuestro test, cada test actua sobre su propio conjunto de datos

```javascript
it("When updating site name, get successful confirmation", async () => {
  //el test esta añadiendo registors nuevos cada vez y actuando solo en esos registros
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });

  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");

  expect(updateNameResult).to.be(true);
});
```

</details>

<br/>

## ⚪ ️ 1.10 No capures errores, esperalos

:white_check_mark: **Haz:** Cuando queremos comprobar que una entrada lanza un error, nos puede parecer correcto usar try-catch-finally y afirmar que se entra por el catch. El resultado es un test incomodo y verboso (ejemplo a continuación) que nos oculta la intencion de un test muy simple y las expectativas del resultado

Una alternativa más elegante seria usar solo la aserción de una sola linea que tiene Chai: expect(method).to.throw (o en Jest: expect(method).toThrow()). Es totalmente obligatorio también asegurarse de que la excepción contenga una propiedad que indique el tipo de error, de lo contratio, lanzando solo un error generico, la app no podra hacer mucho mas que mostrarle un error decepcionante para el usuario

<br/>

❌ **De lo contrario:** Sería muy dificil deducir a partir de los reportes de test (por ejemplo, reporte de CI) que es lo que ha salido mal

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Un test largo que trata de afirmar la existencia de un error con try-catch

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

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
  //si esta afirmación falla, el resultado/reporte del testsolo mostrará
  //que algunos valores es null, no se monstrara que falta una excepción
});
```

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Una afirmacion legible para una persona puede ser comprendida facilmente, tanto por el QA como por el PM

```javascript
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

</details>

<br/><br/>

## ⚪ ️ 1.11 Tagea tus test

:white_check_mark: **Haz:** Deben ejecutarse diferentes tests en diferentes escenarios: quick smoke, IO-less, los tests deben ejecutarse cuando un desarrollador guarda o hace commit de un fichero, los test end-to-end suelen ejecutarse cuando un nuevo pull request es añadido, etc. Esto se puede lograr etiquetando los test con tags como #cold #api #sanity para que se pueda filtrar e invocar solo el subconjunto deseado. Por ejemplo, así es como se ejecutan solo el grupo sanity test con Mocha: mocha — grep ‘sanity’

<br/>

❌ **De lo contrario:** Ejecutar todos los test, incluidos los test que realizan docenas de queries a DB, cada vez que un desarrollador hace un pequeño cambio, puede ser extremadamente lento y provocar que los desarrolladores ignoren correr los test.

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Tagear los test como ‘#cold-test’ permite que el test runner ejecute solo los test más rápidos (Cold===tests rapidos que no estan haciendo operaciones de IO y que pueden ser ejecutados con frecuencia incluso mientras el desarrollador está escribiendo)

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

```javascript
//este test es rapido (sin DB) y lo estamos tageando correctamente
//ahora el usuario/CI puede ejecutarlo con frecuencia
describe("Order service", function() {
  describe("Add new order #cold-test #sanity", function() {
    test("Scenario - no currency was supplied. Expectation - Use the default currency #sanity", function() {
      //logica aquí
    });
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.12 Categoriza los test en al menos 2 niveles

:white_check_mark: **Haz:** Aplique cierta estructura a su conjunto de test para que un visitante ocasional pueda comprender facilmente los requisitos (los test siempre son la mejor documentación) y los diversos escenarios que estamos testeando. Una practica comun para esto es crear al menos 2 bloques 'describe' antes de tus test: el primero es para el nombre de la unidad que está siendo testeada y el segundo es para un nivel adicional de categorización como el escenario o las categorias personalizadas (ver ejemplos de código y pantallazos más abajo). Hacerlo también mejorará los reportes de los test: quien los lea deducirá facilmente las categorias de los test, profundizará en aquellas que lo desee y podrá relacionar mejor los test fallidos. Además, será mucho más fácil para un desarollador navegar a traves del codigo de un cojunto de test amplio. Existen múltiples formas de estructurar tus test que deben ser consideradas, como [given-when-then](https://github.com/searls/jasmine-given) y [RITE](https://github.com/ericelliott/riteway)

<br/>

❌ **De lo contrario:** Cuando nos enfrentamos a un reporte con una lista plana de test, tendremos que leer rápidamente textos largos para determinar los escenarios principales y relacionar los test fallidos. Considera el siguiente caso: Cuando 7/100 test fallan, revisar una lista plana te exige leer el tesxto de las pruebas que fallan para ver como se relacionan entre ellas y que tienen en común. Sin embargo, en un reporte jerarquizado, si los 7 estan bajo un mismo flujo o categoria, puedes saber rápidamente cual o donde puede estar la causa raiz del fallo

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Estructurando un conjunto de test con el nombre de la unidad testada y los escenarios nos conducirá al reporte que se muestra a continuación

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

```javascript
// Unida que se está testeando
describe("Transfer service", () => {
  //Escenario
  describe("When no credit", () => {
    //Esperado
    test("Then the response status should decline", () => {});

    //Esperado
    test("Then it should send email to admin", () => {});
  });
});
```

![alt text](assets/hierarchical-report.png)

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Una lista plana de test hará mas dificil a quien lo lea el identificat las historias de usuario y detectar los test que estan fallando

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Mocha")

```javascript
test("Then the response status should decline", () => {});

test("Then it should send email", () => {});

test("Then there should not be a new transfer record", () => {});
```

![alt text](assets/flat-report.png)

<br/>

</details>

<br/><br/>

## ⚪ ️1.13 Otras buenas practicas genéricas sobre higiene de los test

:white_check_mark: **Haz:** Esta publicación se centra en consejos de test relacionados con, o al menos, que se pueden ejemplificar en Node JS. Sin embargo, esta sección agrupa algunos consejos no relacionados con Node que son bien conocidos

Aprenda y practique [principios TDD](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) — son extremadamente valiosos para muchos pero no te dejes intimidar si no se ajustan a tu estilo, no eres el único. Considera escribir los test antes que el código con el [estilo rojo-verde-refactor](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html), te asegura que cada test chequea exactamente una cosa, cuando encuentras un bug — antes de corregirlo escribe un test que lo detecte como bug en el futuro, dejando que cada test falle al menos una vez antes de convertirlo en un verde, comienza el inicio de un modulo escribieno código muy simple y rapodamente, que satisfaga el test, luego lo refatorizamos gradualmente hasta que nuestro código tenga el nivel deseado en producción, evitando siempre cualquier dependencia con el entorno (rutas en disco, sistema operativo, etc)
<br/>

❌ **De lo contrario:** Echarás de menos las perlas de sabiduría que se han ido recolectando durante décadas

<br/><br/>

# Section 2️⃣: Backend Testing

## ⚪ ️2.1 Enrich your testing portfolio: Look beyond unit tests and the pyramid

:white_check_mark: **Haz:** La [pirámide de test](https://martinfowler.com/bliki/TestPyramid.html), con 10> años de antiguedad, es un modelo excelente y relevante que sugiere tres tipos de test e influye en la estrategia de testeo de la mayoría de los desarrolladores. Al mismo tiempo, surgieron un puñado de nuevas y brillantes técnicas de testeo que se esconden en las sombras de la pirámide de test. Dados todos los cambios que hemos visto en los últimos 10 años (Microservicios, cloud, serverless), ¿es posible que un modelo algo antiguo se adapte a *todos* los tipos de aplicaciones? ¿No debería el mundo del testing considerar aceptar nuevas técnicas?

No me malinterpretes, en 2019 la pirámide de test, el TDD y los test unitarios siguen siendo una técnica buena y probablemente sean la mejor combinación para muchas aplicaciones. Solo como cualquier otro modelo, a pesar de su utilidad, [a veces debe estar equivocado] (https://en.wikipedia.org/wiki/All_models_are_wrong). Por ejemplo, considere una aplicación IOT que ingiere muchos eventos en un bus de mensajes como Kafka / RabbitMQ, que luego fluyen a algún data-warehouse y finalmente son consultados por alguna UI de análisis. ¿Realmente deberíamos gastar el 50% de nuestro presupuesto para tests en escribir tests unitarios para una aplicación que esté centrada en la integración y apenas tenga lógica? A medida que aumenta la diversidad de tipos de aplicaciones (bots, criptografía, Alexa-skills), aumentan las posibilidades de encontrar escenarios en los que la pirámide de test no sea la mejor opción.

Es hora de enriquecer el abanico de tests y familiarizarse con más tipos de tests (las siguientes secciones sugieren algunas ideas), modelos como la pirámide de test, pero también hacer coincidir los tipos de test con los problemas del mundo real al que te enfrentas ('Hola, nuestra API está rota, ¡escribamos contract testing dirigidos al consumidor!'), diversifica tus test como un inversor que construye una cartera de inversión basada en el análisis de riesgos — evalúa dónde pueden surgir problemas y combina algunas medidas de prevención para mitigar esos riesgos potenciales

Una advertencia: el TDD en el mundo del software adopta una cara de falsa dicotomía, algunos predican que debemos usarlo en todas partes, otros piensan que es el diablo. Todos los que hablan en absoluto están equivocados:]

<br/>

❌ **De lo contrario:** Te perderás algunas herramientas con un ROI increíble, algunas como Fuzz, lint y mutation pueden proporcionar valor en 10 minutos

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Cindy Sridharan sugiere un portfolio de test amplio en su increíble publicación ‘Testing Microservices — the same way’

![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan sugiere un portfolio de test amplio en su increíble publicación ‘Testing Microservices — the same way’")

<strong class="markup--strong markup--p-strong">☺️Ejemplo: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "Un nombre de test que consta de 3 partes")

</details>

<br/><br/>

## ⚪ ️2.2 Component testing might be your best affair

:white_check_mark: **Haz:** 

Cada test unitario cubre una pequeña parte de la aplicación y cubrirla totalmente cuesta muchisimo, mientras que los test end-to-end cubren facilmente mucho terreno, pero son costosas y más lentas, ¿por qué no aplicar un enfoque equilibrado y escribir test más grandes que test unitarios pero más pequeñas que las pruebas end-to-end? Los test de componente es la canción no cantada del mundo del testing — proporcionan lo mejor de ambos mundos: rendimiento razonable y la posibilidad de aplicar patrones TDD + cobertura realista.

Los test de componente se centran en la 'unidad' de Microservicios, funcionan contra la API, no mockean nada que pertenezca al Microservico en sí (por ejemplo, DB real, o al menos la versión en memoria de esa DB) pero hace stub de cualquier cosa que sea externa como llamadas a otros microservicios. Al hacerlo, probamos lo que desplegamos, nos acercamos a la aplicación de fuera a dentro y obtenemos una gran confianza en un período de tiempo razonable.

<br/>

❌ **De lo contrario:** Puedes pasar muchos días escribiendo test unitarios para descubrir que solo tiene un 20% de cobertura del sistema

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Supertest permite acercarse al API Express in-process (rápido y cubre muchas capas)


![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) permite acercarse al API Express in-process (rápido y cubre muchas capas)")

</details>

<br/><br/>

## ⚪ ️2.3 Ensure new releases don’t break the API using

:white_check_mark: **Haz:** Pongamos que tu Microservicio tiene multiples consumidores, y tenemos en ejecucion diferentes versiones del servicio por compatibilidad (para que todos estén contentos). Luego cambias un campo y "¡boom!", uno de los consumidores que necesita ese campo se cabrea. Este es el Catch-22 del mundo de la integración: es muy difícil para el lado del servidor considerar todas las expectativas de todos los consumidores. Por otro lado, los consumidores no pueden realizar ninguna prueba porque el servidor controla las fechas de release. [Contratos dirigidos por el consumidor y el framework PACT] (https://docs.pact.io/) nacieron para regularizar este proceso con un enfoque muy disruptivo: no es el servidor quien define los test de sí mismo, sino que son los consumidores quienes definen las pruebas de ¡el servidor! PACT puede registrar las expectativas del consumidor y dejarlas en una ubicación compartida, "broker", para que el servidor pueda cogerlas y cumplir con las expectativas y ejecutar cada construcción utilizando la libreria PACT para detectar contratos incumplidos — una expectativa de consumidor no cumplida. Al hacerlo, todos los desajustes de la API cliente-servidor se detectan muyt pronto durante la construcción / CI y pueden ahorrarte mucha frustración.

<br/>

❌ **De lo contrario:** Las alternativas son pruebas manuales agotadoras o miedo al despliegue

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "Ejemplos con PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪ ️ 2.4 Test your middlewares in isolation

:white_check_mark: **Haz:** Muchos evitan los test de middleware porque representan una pequeña porción del sistema y requieren ejecutar un servidor Express. Ambas razones son incorrectas — los middlewares son pequeños pero afectan a todas o la mayoría de las solicitudes y pueden testearse fácilmente como funciones puras que obtienen {req, res} objetos JS. Para testear una función de middleware se debe invocar y usar spy ([usando Sinon, por ejemplo] (https://www.npmjs.com/package/sinon)) sobre la interacción con los objetos {req, res} para garantizar que nuestra función middleware realiz la acción correcta. La libreria [node-mock-http] (https://www.npmjs.com/package/node-mocks-http) lo lleva aún más lejos y factoriza los objetos {req, res} ademas de añadir el spy. Por ejemplo, puede afirmar si el estado http que se estableció en el objeto res coincide con el esperado (consulta el ejemplo a continuación)

<br/>

❌ **De lo contrario:** Un bug en un middleware de Express === un bug todas o casi todas las peticiones

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap:Ejemplo de cómo hacerlo correctamente: Probar un middleware de forma aislada sin emitir llamadas de red y evitar tener que levantar Express

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

```javascript
//ek middleware que queremos testear
const unitUnderTest = require("./middleware");
const httpMocks = require("node-mocks-http");
//Sintaxis de Jest, equivalente a describe() e it() en Mocha
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

## ⚪ ️2.5 Mide y refactoriza utilizando herramientas de análisis estático

:white_check_mark: **Haz:** El uso de herramientas de análisis estático ayuda proporcionando formas objetivas para mejorar la calidad del código y a tener el código mantenible. Puede agregar herramientas de análisis estático a su pipeline de CI para abortar cuando encuentre code smells. Sus principales beneficios sobre el linter plano son la habilidad de analizar la calidad en el contexto de multiples ficheros (por ejemplo encontrar duplicados), realizando analisis avanzados (por ejemplo complegidad del código) y siguiendo el historial y el progreso de cada problema. Dos ejemplos de herramientas que puedes usar son [Sonarqube](https://www.sonarqube.org/) (2,600+ [estrellas](https://github.com/SonarSource/sonarqube)) y [Code Climate](https://codeclimate.com/) (1,500+ [estrellas](https://github.com/codeclimate/codeclimate))

Crédito: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **De lo contrario:** Con una mala calidad de código, los bugs y el rendimiento siempre serán un problema que ninguna libreria completamente nueva o características punteras van a poder solucionar

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: CodeClimate, una herramienta comercial que puede identificar metodos complejos:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Ejemplos con CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimat, una herramienta comercial que puede identificar metodos complejos:")

</details>

<br/><br/>

## ⚪ ️ 2.6 Compueba tu predisposicion al caos relacionado con Node

:white_check_mark: **Haz:** Extrañamente, la matroia de los test de software son acerca de logica y datos, pero los errores más grabes (y que son muy dificiles de resolver) son problemas de infraestructura. Por ejemplo, ¿alguna vez has testeado que pasa cuando se sobrecarga la memoria? ¿o cuando el servidor/proceso muere? ¿o tu sitema de monitorización es capar de darse cuenta cuando la API es un 50% más lenta de lo normal? Para probar y evitar este tipo de problemas — [Chaos engineering](https://principlesofchaos.org/) fue creado por Netflix. Su objetivo es proporcionar conciencia, frameworks, y herramientas para testear la resiliencia de nuestras aplicaciones en problmeas caoticos. Por ejemplo, una de las herramientas mas conocidas [the chaos monkey](https://github.com/Netflix/chaosmonkey), mata servidores de forma aleatoria para comprobar si nuestro servicio aun puede dar servicio a los usuarios y asegurar que no depende de un solo servido (hay tambien una version de kubernetes, [kube-monkey](https://github.com/asobti/kube-monkey), que mata pods en vez de servidores. Todas estas herramientas funcionan a nivel de hosting/plataforma, pero ¿qué pasa si deseas probar y generar caos a nivel Node puramente como comprobar como tu proceso Node hace frente a errores no controlados, o a rejects de promesas no capturados, o sobrecarga de la memoeria de v8 por encima del máximo de 1.7GB o si la UX sigue siendo bueno si se satura el event loop? Para todo esto he escrito [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) que proporciona todo tipo de formas de crear el caos en Node
<br/>

❌ **De lo contrario:** No hay escapatoria, la ley de Murphy afectará a producción sin piedad

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: : Node-chaos puede generar todo tipo de problemas en Node.js de tal manera que puedas probar la relsiliencia de tu app al caos

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos puede generar todo tipo de problemas en Node.js de tal manera que puedas probar la relsiliencia de tu app al caos")

</details>

<br/>

## ⚪ ️2.7 Evitar fixtures globales y seeds, añade datos por cada test

:white_check_mark: **Haz:** Siguiendo la regla de oro (sección 0), cada test debe añadir y actuar en su propio conjunto de filas DB para evitar el acoplamiento y poder explicar fácilmente sobre el flujo del test. En realidad muchos testers se saltan esta regla al añadir datos a la DB solo una vez antes de ejecutar los test ([tambien conocido como ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) a favor de mejorar el rendimiento. Si bien el rendimiento es una preocupación válida — puede mitigarse de otras formas (consulte la sección "test de componentes"), sin embargo, la complegidad del test es más dolorosa que otras consideraciones la mayoria de las veces. De manera practica, haga que cada test añada explicitamente los registros que necesitas y actua sobre ellos. Si el rendimiento se convierte en algo critico — se puede llegar al compromiso de utilizar los mismos datos en un conjunto de test siempre que no se muten los datos (por ejemplo en queries).

<br/>

❌ **De lo contrario:** FMuchos test fallaran, un despliegue se aborta, nuestro equipo perdera mucho tiempo, ¿tenemos un bug? vamos a investigar, ah no — parece que dos test estan mutando el mismo dato

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: tests no son independientes y dependenden de una inserción global de datos en la DB

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

```javascript
before(async () => {
  //añadiendo datos de sites y admin a nuestra DB. ¿Donde estan los datos? fuera. En un json extermo o en un modelo da migración
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //Se que el nombre de site "portal" existe, — lo he visto en seed.json
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //Se que el nombre de site "portal" existe, — lo he visto en seed.json
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Fallo! El test anterior ha cambiado el nombre :[
});

```

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Podemos permanecer dentro de nuestro test, cada test actua sobre su propio conjunto de datos

```javascript
it("When updating site name, get successful confirmation", async () => {
  //el test esta añadiendo registors nuevos cada vez y actuando solo en esos registros
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });

  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");

  expect(updateNameResult).to.be(true);
});
```

</details>

<br/><br/>

# Section 3️⃣: Frontend Testing

## ⚪ ️ 3.1 Separate UI from functionality

:white_check_mark: **Haz:** Al centrarnos en testear la lógica del component, los detalles de la interfaz de usuario solo pueden entorpecernos, por lo qu debes abstraerte de ellos y que los test se centren en datos puros. En la practica, extrae los datos que necesites de una manera abstracta sin que este acoplada a la interfaz grafica, haz aserciones de los datos puros (vs detalles visuales en HTML/CSS) y desactiva las animaciones que pueden hacer lenta la interfaz. En este punto podrias pensar en desactivar la interfaz y solo hacer test de la parte back del UI (por ejemplo servicios, acciones, store) pero esto solo dará como resultado test ficticios, diferentes a la realidad y no desvelaran casos en los que los datos correctos no llegan a la interfaz de usuario.

<br/>

❌ **De lo contrario:** Los datos calculados puros de tu test pueden estar listos en 10ms, pero luego todo el test tarda 500ms (100 tests = 1 min) debido a alguna animación irrelevante

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Separar los detalles de UI

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Ejemplos con React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Ejemplos con react-testing-library")

```javascript
test("When users-list is flagged to show only VIP, should display only VIP members", () => {
  // Arreglar
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Actuar
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Afirmar - Extrae los datos de la UI primero
  const allRenderedUsers = getAllByTestId("user").map(uiElement => uiElement.textContent);
  const allRealVIPUsers = allUsers.filter(user => user.vip).map(user => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //compara datos con datos, aqui no hay UI
});
```

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Mezcla de datos y detalles de la UI en las aserciones

```javascript
test("When flagging to show only VIP, should display only VIP members", () => {
  // Arreglar
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Actuar
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Afirmar - Mezcla de UI y datos en las aserciones
  expect(getAllByTestId("user")).toEqual('[<li data-testid="user">John Doe</li>]');
});
```

</details>

<br/><br/>

## ⚪ ️ 3.2 Consulta elementos HTML basandote en atributos que no deberian cambiar

:white_check_mark: **Haz:** Consulta elementos HTML basandote en attributos que deberian permanecer intactos a cambios graficos al contrario que selectores CSS y etiquetas de los formularios. Si el elemento designado no tiene esos attributos, crea un atributo dedicado solamente a los test como 'test-id-submit-button'. Seguir este patron no solo asegura que tus test funcionales/logicos no se rompan nunca por cambios esteticos, sino que tambien queda claro a cualquier desarrollador que ese elemento y atributo estan ahi por y para los test y no deben eliminarse

<br/>

❌ **De lo contrario:** Quieres testear el login de tu app que tiene muchos componentes, lógica, servicios, y todo esta bien configurado - stubs, spies, las llamadas Ajax estan aisladas. All seems perfect. Entonces el test falla porque el diseñador ha cambiado la clase de un div de 'thick-border' a 'thin-border'

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Consultar un elemento utilizando un atributo solo para testing

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Ejemplos con React")

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
// este ejemplo está usando react-testing-library
test("Whenever no data is passed to metric, show 0 as default", () => {
  // Arreglar
  const metricValue = undefined;

  // Actuar
  const { getByTestId } = render(<dashboardMetric value={undefined} />);

  expect(getByTestId("errorsLabel").text()).toBe("0");
});
```

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Confiando en attributos CSS

```html
<!-- the markup code (part of React component) -->
<span id="metric" className="d-flex-column">{value}</span>
<!-- what if the designer changes the classs? -->
```

```javascript
// este ejemplo está usando enzyme
test("Whenever no data is passed, error metric shows zero", () => {
  // ...

  expect(wrapper.find("[className='d-flex-column']").text()).toBe("0");
});
```

</details>

<br/>

## ⚪ ️ 3.3 Siempre que sea posible, testea con un componente real y totalmente renderizado

:white_check_mark: **Haz:** Siempre que tenga un tamaño razonable, testea tu componente como lo hacen tus usuarios, renderiza completamente la interfaz de usuario, actúa sobre ella y comprueba que la interfaz se comporta como esperabas. Evita todo tipo de mocks, partials o shadow rendering - hacerlo puede provocar bugs no detectados debido a la falta de detalles y dificultará el mantenimiento a medida que los test interfieren con las partes internas (consulte la sección 'Acercarse al testing caja-negra'). Si uno de los componentes hijos ralentiza significativamente tu test (por ejemplo por una animación) o complica el setup, considera reemplazarlo explícitamente por un fake

Con todo esto tambien es necesario tener ciertas precauciones: esta técnica funciona para componentes pequeños / medianos que contienen un número razonable de componentes hijos. Renderizar completamente un componente con demasiados hijos hará que sea difícil analizar los fallos de los test (análisis de causa raíz) y puede ser demasiado lento. En estos casos, escribe los menos test que necesites contra ese componente principal y más test contra sus hijos

<br/>

❌ **De lo contrario:** Al hurgar en las partes internas de un componente, invocando sus metodos privados y verificando el estado interno - tendras que refactorizar todos los test siempre que refactorices los componentes ¿Realmente quieres dedicar ese tiempo en hacer este mantenimiento?

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Trabajando con un componente totalmente renderizado

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Ejemplos con React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Enzyme-blue.svg "Ejemplos con Enzyme")

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
  // Arreglar
  const wrapper = mount(<Calendar showFilters={false} />);

  // Actuar
  wrapper.find("button").simulate("click");

  // Afirmar
  expect(wrapper.text().includes("Choose Filter"));
  // Así es como el usuario abordará este elemento: por texto
});
```

### :thumbsdown: Ejemplo Anti Patrón: Mockeando con renderizado superficial (shallow rendering)

```javascript
test("Shallow/mocked approach: When clicked to show filters, filters are displayed", () => {
  // Arreglar
  const wrapper = shallow(<Calendar showFilters={false} title="Choose Filter" />);

  // Actuar
  wrapper
    .find("filtersPanel")
    .instance()
    .showFilters();
  // Aprovecha las partes internas, saltandote la UI e invocando el metodo ditectamente. 
  // Aproximación caja-blanca

  // Afirmar
  expect(wrapper.find("Filter").props()).toEqual({ title: "Choose Filter" });
  // ¿Qué pasa si cambiamos el nombre de la prop o si no pasamos nada relevante?
});
```

</details>

<br/>

## ⚪ ️ 3.4 No pauses, usa soporte del framewok para eventos asincronos. Tambien intenta acelerar las cosas

:white_check_mark: **Haz:** En muchos casos, el tiempo que tarda una unidad bajo test es desconocido (por ejemplo, la animación elimina la visualización de un elemento) - en este caso, evita esperar (por ejemplo stTimeOut) y elige metodos mas deterministas que la mayoria de las plataformas proveen. Algunas librerias permiten esperar en operaciones (por ejemplo [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), otras proveen un API para esperar como [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance). A veces, una forma más elegante es hacer stub del recurso lento, como una API por ejemplo, con lo que el momento de respuesta se vuelve determinista., y volvemos a poder renderizar el componente directamente. Cuando tengas dependencias con algun componente externo que espera, puede ser util modificar el tiempo con librerias como [hurry-up the clock](https://jestjs.io/docs/en/timer-mocks). Esperar es algo que debemos evitar siempre, por que fuerza que tu test sea lento o tenga ciertos riesgos (cuando esperas un tiempo muy bajo). Siempre que sea inevitable esperar y hacer polling, y el framework de testing no tenga soporte, algunas librerias de npm pueden ayudar con soluciones semi-deterministas, como [wait-for-expect](https://www.npmjs.com/package/wait-for-expect)

<br/>

❌ **De lo contrario:** Cuando se espera mucho tiempo, los tests seran un orden de magnitud más lentos. Cuando intentes espera tiempos bajos, los test fallarán cuando la unidad bajo test no haya respondido a tiempo. Por tanto, se reduce a balancear entre puntos debiles y el rendimiento malo.

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: API E2E que se resuelve solo cuando se realizan las operaciones asíncronas (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Usando Cypress para ilustrar la idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Ejemplos con react-testing-library")

```javascript
// usando Cypress
cy.get("#show-products").click(); // navegar
cy.wait("@products"); // esperar a que la ruta aparezca
// esta linea será ejecutada solo cuando la ruta haya teminado
```

### :clap: Ejemplo de cómo hacerlo correctamente: Libreria de testing que espera a elementos del DOM

```javascript
// @testing-library/dom
test("movie title appears", async () => {
  // el elemento no esta presente al comenzar...

  // esperando a que este disponible
  await wait(() => {
    expect(getByText("the lion king")).toBeInTheDocument();
  });

  // esperando que este disponible para devolver el elemento
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

### :thumbsdown: Ejemplo Anti Patrón: codigo de espera propio

```javascript
test("movie title appears", async () => {
  // el elemento no esta presente al comenzar...

  // espera con logica propia (precaución: simplista, sin tiempo de espera)
  const interval = setInterval(() => {
    const found = getByText("the lion king");
    if (found) {
      clearInterval(interval);
      expect(getByText("the lion king")).toBeInTheDocument();
    }
  }, 100);

  // esperando que este disponible para devolver el elemento
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

</details>

<br/>

## ⚪ ️ 3.5 Observa como se sirve tu contenido a nivel de red

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Ejemplos con Lighthouse")

✅ **Haz:** Usa un monitor que garantize que la carga de la página esté optimizada - esto incluye cualquier problema de UX como descarga lenta o un paquete no minimizado. El mercado de herramientas de este tipo no es pequeño: herramientas basicas como [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) se puede configurar para ver si el servidor esta corriendo y respondiendo dentro de un SLA razonable. Esto solo rallar la superficie, podria haber muchimas cosas mal, portante es mejor optar por herramientas especializadas en frontend, (por ejemplo [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) y hagan un analis mucho más amplio. El foco debe ponerse en los sintomas y metricas que afecten directamente a UX, como el tiempo de carga, [render mínimo](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [tiempo hasta que la pagina es manejable (TTI)](https://calibreapp.com/blog/time-to-interactive/). Sobre todo esto, tambien debes estar atento a posibles causas tecnicas, como garantizar que el contenido sea comprimido, tiempo hasta el primer byte, optimizar imagenes, asegurar un tamaño del DOM razonable, SSL, y muchos más. Es aconsejable tener toda esta monitorización durante el desarrollo, como parte del CI y mucho más importante - 24x7 en los servidores de producción / CDN

<br/>

❌ **De lo contrario:** Es muy decepcionante darse cuenta de que después de haber tenido mucho cuidado y trabajo en crear una interfaz, pasen el 100% de los test funcionales y un pipeline sofisticado - el UX es horrible y lento por culpa de un CDN mal configurado

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

### :clap: Ejemplo de cómo hacerlo correctamente: reporte de carga de la pagina con Lighthouse

![](/assets/lighthouse2.png "Reporte de carga de la pagina con Lighthouse")

</details>

<br/>

## ⚪ ️ 3.6 Usa stubs para recursos lentos como el API de back-end

:white_check_mark: **Haz:** Cuando programas tus test principales (no los test E2E), evita interactuar con cualquier recurse que este fuera de tu responsabilidad y control, como las API de back-end y usar stubs en su lugar (es decir, un doble de test). De forma practica, en vez de hacer llamadas de red reales al API, utiliza alguna libreria (como [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) para stubear las repuestas de API. El principal beneficio es evitar la inestabilidad - testeando o suplantando APIs, por definición, no son muy estables y de vez en cuando fallarán los test, aunque TU componente se comporte bien (en producción generalmente se aceleran las respuestas, pero no esta pensado para hacer test). Hacerlo te permitirá simular varios compartamientos de API que deberían definir el comportamiento de nuestro componente para caminos no felices, por ejemplo cuando no se encuentran datos o cuando API devuelve un error. Por último, pero no por ello menos importante, las peticiones de red hacen más lentos nuestros test

<br/>

❌ **De lo contrario:** La media de ejecución de los test no dura más de unos pocos ms, una llamada a API estandar dura 100ms>, lo que lo hace cada test ~20x más lento

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Stubear or interceptar las llamadas a API

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Ejemplos con React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Ejemplos con react-testing-library")

```javascript
// unidad testeada
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
  // Arreglar
  nock("api")
    .get(`/products`)
    .reply(404);

  // Actuar
  const { getByTestId } = render(<ProductsList />);

  // Afirmar
  expect(getByTestId("no-products-message")).toBeTruthy();
});
```

</details>

<br/>

## ⚪ ️ 3.7 Haz muy pocos test end-to-end que abarquen todo el sistema

:white_check_mark: **Haz:** Aunque E2E (end-to-end) para algunos significa solo hacer test de UI en navegador de verdad (ver el punto 3.6), para otros significa que impliquen todo el sistema, incluido el backend real. Esto es muy valioso ya que te cubren errores de integracion entre el frontend y el backend que pueden ocurrir por diferencias de opinion en el esquema de datos. También son un método eficientes para sacar errores de integración entre backends (por ejemplo, microservicio A envia datos erroneso al microservicio B) e incluso para detectar fallos de despliegue - actualmente no hay herramientas para test E2E solo backend tan amigables y maduras como las de UI como [Cypress](https://www.cypress.io/) y [Pupeteer](https://github.com/GoogleChrome/puppeteer). La desventaja de estos test es su coste alto, tener un entorno configurado con todos los componentes, la fragilidad de los test - si tenemos 50 microservicios, solo con que falle uno, los test E2E fallan. Por estas razones tenmos que usar moderadamente esta tecnica y probablemente tener entre 1 y 10  test de este tipo. Dicho esto, incluso una cantidad pequeña de test E2E es probablemente que detecten el tipo de problemas a los que estan realmente dirigidos: despligue e integración. Es aconsejable que se ejecuten en un entorno lo mas parecido a produción

<br/>

❌ **De lo contrario:** Pudes invertir mucho en testear la funcionalidad de la UI para darte cuenta demasiado tarde que el backend devuelve un contrato (el esquema de datos con el que la UI trabaja) muy diferente al esperado

<br/>

## ⚪ ️ 3.8 Acelera los test E2E reutilizando las credenciales de login

:white_check_mark: **Haz:** En los test E2E que involucren un backend real que usa un token para identicarse en las llamadas a API, no vale la pena aislat el test tanto como para que se cree un usuario y se haga login en cada test. En vez de esto, haz login una vez antes de ejecutar todos los test (en el before-all) guarda el token en de forma local y reutilizalo en cada petición. Esto parece violar unos de los principios básicos - manten los test autonomos sin acoplamiento de recursos. Lo que es cierto, pero en los test E2E el rendimiento es clave, y crear 1-3 peticiones a API antes de empezar cada test individual puede llevarnos a unos tiempos de ejecución horribles. Reutilizar las credenciales no significa que las pruebas tengan que actuar sobre los mismos registros de usuario - si se basan en ellos (por ejemplo, testeando el historial de pagos), asegurate de crear los registro como parte del test y evita compartirlos con otros test. Y siempre recuerda que el backend puede ser sustituido - si tus test estan focalizado en el frontend puede ser mejor aislarlos y descomnectar las API de backend (consulta el punto 3.6)

<br/>

❌ **De lo contrario:** Dados 200 test y asumiendo que un login son 100ms = 20 segusdos solo para hacer el mismo login una y otra vez

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Logandose en before-all y no en before-each

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Usando Cypress para ilustrar la idea")

```javascript
let authenticationToken;

// ocurre antes de ejecutar TODOS los test
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

// ocurre antes de CADA test
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

## ⚪ ️ 3.9 Haz un test E2E que navegue toda la página (smoke test)

:white_check_mark: **Haz:** Para el monitoreo de producción y verificar que nada se rompe en tiempo de desarrollo (sanity check), ejecuta un único test E2E que visite todas o la mayoría de las páginas y se asegure que ninguna se rompe. Este tipo de test proporciona un gran retorno de la inversión ya que es un bastante sencillo de crear y mantener y puede detecta cualquier tipo de fallo, incluido funcionales, red y despliegue. Otras formas de hacer smoke y sanity checks no son tan confiables y exhaustivas - algunso equipos de operaciones simplemente hacen ping a la página de inicio (en producción) o desarrolladores que tiene muchos test de integración que no levanta errores de construcción o de navegador. No hace falta decir que esta prueba no sustituye los test funcionales, solo siver como detector de humo rápido.

<br/>

❌ **De lo contrario:** Todo puede parecer estar bien, todos los test pasan, el health-check de produción está ok también, pero el componente de pago se construyó mal y simplemente la ruta /Payment no se renderiza

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Navegando a todas las páginas

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Usando Cypress para ilustrar la idea")

```javascript
it("When doing smoke testing over all page, should load them all successfully", () => {
  // ejemplificado con Cypress pero puede implementarse
  // facilmente usando cualquier herramienta E2E
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

## ⚪ ️ 3.10 Exponer los tes como un documento colaborativo vivo

:white_check_mark: **Haz:** Además de aumentar la confiabilidad de la aplicación, los test te dan otra caracteristica muy atractiva - sirven de documentación viva. Dado que los test hablan en un leguaje menos tecnico y sobre el producto y UX, usar las herramientas correctas puede servir como un artefacto de comunicación que alina en gran medida a desarrolladores y su cliente. Por ejemplo, algunos frameworks permiten expresar el flujo y las expectativas (el test plan) utilizando un lenguaje legible para que cualquier stakeholder, incluyendo los product managers, pueden leer, aprobar y colaborar en los test convirtiendose en el documento de requerimentos vivo. Esta tecnica tambien se la conoce como 'test de aceptación', ya que permite al cliente definir sus criterios de aceptación en un leguaje sencillo. Esto es [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) en su forma más pura. Uno de los frameworks más populares para aesto es [Cucumber que tiene su sabor en JavaScript](https://github.com/cucumber/cucumber-js), ver el ejemplo más abajo. Otra forma similar pero diferente, [StoryBook](https://storybook.js.org/), permite exponer los componentes UI como un catalogo grafico, donde cualquiera puede recorrer los diferentes estados de cada componente (por ejemplo renderizar una cuadricula sin filtro, con multiples filas o con ninguna, etc), ver como queda y como se activa ese estado - esto también puede atraer a la gente de producto pero sobre todo siver como documentación viva para los desarrolladores que consumen esos componentes

❌ **De lo contrario:** Despues de invertir los mejores recursos en los test, es una pena no aprovechar ese tiempo y ganar un gran valor como es la documentación

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Describiendo test en un lenguaje para humanos usando cucumber-js

![](https://img.shields.io/badge/🔨%20Example%20using%20Cucumber-blue.svg "Examples using Cucumber")

```javascript
// así es como se pueden describir los test con cucumber: lenguaje sencillo que permite a cualquiera comprenderlos y colaborar

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

### :clap: Ejemplo de cómo hacerlo correctamente: Visualizando nuestros componentes, sus diversos estados y entradas usando Storybook

![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Usando StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Detecta problemas visuales con herramientas automatizadas

:white_check_mark: **Haz:** Configure herramientas automatizadas para capturar screenshoots de UI cuando se presenten cambios y detecte problemas visuales como contenido superpuesto o roto. Esto garantiza que no solo se muestren los datos correctos si no que el usuario los vea correctamente. Está tecnica no es ampliamente usada, nuestra mentalidad nos lleva a los test funcionales, pero es lo visual lo que el usuario experimenta y con la cantidad de dispositivos es relativamente facil pasar por alto algunos bugs en la UI. Algunas herramientas gratuítas pueden proporcionar lo básico - generar y guardar screenshots para la inspeccion manual por una persona. Mientras este enfoque podria ser suficiente para aplicaciones pequeñas, no es valido como cualquier otro test manual que exige trabajo de una persona cada vez que algo cambia. Por otro lado, es bastante dificil detectar problemas de UI automaticamente debido a que no está claramente deficini - aquí es donde interviene el campo de la 'Regresion Visual' a resolver este rompecabezas de comparar la UI antigua con los últimos cambios y detectar diferencias. Alguas erramientas OSS/gratuitas pueden proporcionar parte de esta funcionalidad (por ejemplo [wraith](https://github.com/BBC-News/wraith), [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>) pero podrian conllevar un tiempo de configuración muy alto. Algunas herramientas comerciales (por ejemplo [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) dan un paso más reducir la instalacion y contener funciones avanzadas como interfaces de administración, alertas, captura intelegiente que elimina el 'ruido visual' (por ejemplo, banners, animaciones) e incluso llegan a adelantar el analisis de la causa raiz de los cambios del DOM / css que han causado el problema.

<br/>

❌ **De lo contrario:** ¿Como de bien hecha una pagina que muestra buen contendo (100% test ok), carga de forma instantanea pero la mitad del area de contenido está oculto?

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Una regresion visual estandar - contenido correcto que se muestra mal

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Configurando wraith para capturar y comparar snapshots de UI

![](https://img.shields.io/badge/🔨%20Example%20using%20Wraith-blue.svg "Usando Wraith")

```
​# Añade tantos dominios como sea necesario. La key actuará como etiqueta

domains:
  english: "http://www.mysite.com"​

​# escribe los anchos de pantalla a continuación, por ejemplo

screen_widths:

  - 600​
  - 768​
  - 1024​
  - 1280​

​# escribe las URL de la página a constinuación, por ejemplo
paths:
  about:
    path: /about
    selector: '.about'​
  subscribe:
      selector: '.subscribe'​
    path: /subscribe
```

### :clap: Ejemplo de cómo hacerlo correctamente: Usando Applitools para hacer comparación de snapshoots y otras funciones avanzadas

![](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg "Using AppliTools") ![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Usando Cypress para ilustrar la idea")

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

# Section 4️⃣: Midiendo la efectividad de los Test

<br/><br/>

## ⚪ ️ 4.1 Completa una cobertura suficiente que de confianza, ~80% parece el numero de la suerte

:white_check_mark: **Haz:** El proposito de los test es tener suficiente confianza para moverse rápido, obviamente cuando más código se pruebe, más confianza tendremos en el equipo. La cobertura nos mide cuantas lineas de código (y ramas, declaraciones, etc) se alcanzan mediante los test. Entonces, cuanta es suficiente? Obviamente 10-30% es demasiado bajo para tener alguna idea de que puedes tener que corregir, y por otro lado el 100% es muy caro y puede cambiar el foco de los caminos criticos a rincones apenas usados del código. La respuesta larga es que depende de muchos dactores como el tipo de aplicación - si estas construyendo la siguiente generación del Airbus A380 un 100% es obligatorio, pero para una web de dibujos animados, el 50% podria hasta ser demasiado. Aunque la mayoria de los entusiastas de los test dicen que el porcentaje de cobertura correcto es contextual, la mayoria de ellos comentan que el 80% como la regla correcta ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) que posiblemente debería satisfacer la mayotia de aplicaciones.

Consejos de implementación: es posible que quieras configurar la integracion continua (CI) para que tenga un umbral de cobertura ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) y que pare el pipeline cuando no cumpla el estandar (también es posible configurar el porcentaje por compoente, vease el ejemplo a continuación). Ademas de esto, deberias considerar detectar la bajada de cobertura (cuando un nuevo commit tiene menos cobertura que antes) - esto empujara a los desarrolladores a aumentar o al menos preservar la cantidad de código con test. Y también puede ser engañado como se puestra en los siguientes puntos.

<br/>

❌ **De lo contrario:** La confianza y los números van de la mano, sin saber realmente que se ha testeado la mayor parte del sistema - habrá algo de miedo y el miedo te retrasará

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Example: Un reporte de cobertura típico

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "Un reporte de cobertura típico")

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Configurar cobertura por componente (usando Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Usando Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Configurar cobertura por componente (usando Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Inspecciona los reportes de cobertura para detectar áreas no testadas y otras cosas raras.

:white_check_mark: **Haz:** Algunos problemas se ocultan por debajo del radar y son realmente difíciles de encontrar utilizando herramientas tradicionales. Estos no son realmente bugs sino más bien un comportamientos curiosos de la aplicación que podrían tener un gran impacto. Por ejemplo, a menudo algunas áreas de código no se invocan nunca o rara vez - puedes pensar que la clase 'PricingCalculator' siempre determina el precio del producto, pero resulta que en realidad nunca se invoca, aunque tenemos 10000 productos en DB y muchas ventas… Los reportes de nos ayudan a darnos cuenta de si la aplicación se comporta de la manera que esperamos. Aparte de eso, también podemos resaltar qué tipos de código no se testean: que el 80% del código se testea, no nos indica si las partes críticas están cubiertas. Generar reportes es fácil: simplemente ejecute su aplicación en producción o durante test con cobertura y luego revisa los reportes que resaltan la frecuencia con la que se invoca cada parte del código. Si le dedicas un tiempo para echar un vistazo a estos datos, puedes encontrar algunas errores

<br/>

❌ **De lo contrario:** Si no sabes qué trozos de código no se testean, no sabes dónde pueden aparecer problemas

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: ¿Qué hay mal en este reporte de cobertura?

Basado en un escenario real en el que rastreamos el uso de nuestra aplicación en el control de calidad y descubrimos patrones de login interesantes (Sugerencia: la cantidad de fallos de login no es proporcional, algo está claramente mal. Finalmente, resultó que algún error de la interfaz provocaba que se siguiera llamando al API de login en segundo plano)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "¿Qué hay mal en este reporte de cobertura?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Mide la cobertura lógica usando mutation testing

:white_check_mark: **Haz:** La métrica de cobertura tradicional a menudo miente: puede mostrarle una cobertura de código del 100%, pero ninguna de sus funciones, ni siquiera una, devuelve la respuesta correcta. ¿Cómo? simplemente mide sobre qué líneas de código se paso en los test, pero no verifica si laos test realmente han comprobado algo - asercionando la respuesta correcta. Como alguien que viaja por negocios y muestra su pasaporte, esto no prueba que haya realizado ningun trabajo, solo que ha visitado ciertos aeropuertos y hoteles.

Los test basados en mutaciones nos ayudan midiendo la cantidad de código que en realidad se TESTEÓ, no solo VISITADO. [Stryker] (https://stryker-mutator.io/) es una libreria JavaScript para test de mutación y la implementación es realmente clara:

(1) cambia intencionalmente el código y "planta bugs". Por ejemplo, el código newOrder.price === 0 se convierte en newOrder.price! = 0. Estos "bugs" se llaman mutaciones.

(2) ejecuta los test, si todo va bien, entonces tenemos un problema - los test no cumplen su propósito de descubrir bugs, las mutaciones se denominan supervivientes. Si los test fallaron, entonces genial, las mutaciones fueron asesinadas.

Saber que todas o la mayoría de las mutaciones fueron asesinadas da mucha más confianza que la cobertura tradicional y el tiempo de configuración es muy similar
<br/>

❌ **De lo contrario:** Te engañas si crees que una cobertura del 85% significa que tus test detectarán errores en el 85% de tu código

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: 100% de cobertura, 0% testeado

![](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg "Usando Stryker")

```javascript
function addNewOrder(newOrder) {
  logger.log(`Adding new order ${newOrder}`);
  DB.save(newOrder);
  Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

  return { approved: true };
}

it("Test addNewOrder, don't use such test names", () => {
  addNewOrder({ asignee: "John@mailer.com", price: 120 });
}); //Genera un 100% cobertura de código, pero no comprueba nada
```

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Los reportes de Stryker, una herramienta para test de mutación, detecta y cuenta la cantidad de código que no se testea (Mutaciones)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Los reportes de Stryker, una herramienta para test de mutación, detecta y cuenta la cantidad de código que no se testea (Mutaciones)")

</details>

<br/><br/>

## ⚪ ️4.4 Prevención de problemas de código de test con linters para test

:white_check_mark: **Haz:** ESLint tiene un conjunto de plugins específicos para inspeccionar patrones de código de test y descubrir problemas. Por ejemplo, [eslint-plugin-mocha] (https://www.npmjs.com/package/eslint-plugin-mocha) avisará cuando un test se escriba a nivel global (no es hijo de un describe () ) o cuando se omiten los test (https://mochajs.org/#inclusive-tests), lo que puede llevar a creer erroneamenre de que todas los test están ok. Del mismo modo, [eslint-plugin-jest] (https://github.com/jest-community/eslint-plugin-jest) puede, por ejemplo, advertir cuando una prueba no tiene aserciones (sin verificar nada)

<br/>

❌ **De lo contrario:** Ver un 90% de cobertura de código y 100% de pruebas verdes te provocara una sonrisa hasta que te das cuenta de que muchas pruebas no asercionan nada y muchas test simplemente se omitieron. Con suerte, no desplegó nada basado en esta falsa observación

<br/>
<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: Un test lleno de errores, afortunadamente detectados por el linter

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

# Section 5️⃣: CI y otras medidas de calidad

<br/><br/>

## ⚪ ️ 5.1 Enriquece tus linters y cancela las construciones que tienen problemas de linter

:white_check_mark: **Haz:** Los linters son comida gratis, con una configuración de 5 minutos, obtienes gratis un piloto automático que vigila tu código y detecta problemas importantes mientras escribes. Atrás quedaron los días en los que el linter era solo maquillaje (¡no hay punto y coma!). Hoy en día, los linters pueden detectar problemas graves como errores que no se lanzan correctamente y perder información. Además de su conjunto básico de reglas (como [estándar ESLint] (https://www.npmjs.com/package/eslint-plugin-standard) o [estilo Airbnb] (https://www.npmjs.com/package / eslint-config-airbnb)), considera incluir algunos conjuntos de reglas especializadas como [eslint-plugin-chai-expect] (https://www.npmjs.com/package/eslint-plugin-chai-expect) que pueden descubrir tests sin aserciones, [eslint-plugin-promise] (https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) puede descubrir promesas sin resolución (su código nunca continuará), [eslint-plugin -security] (https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) que puede descubrir expresiones regulares que podrían usarse para ataques DOS, y [eslint-plugin-you-dont- need-lodash-underscore] (https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) es capaz de avisar cuando el código utiliza métodos de librerias de utilidades que forman parte de V8, métodos básicos como Lodash.\_map (...)

<br/>

❌ **De lo contrario:** Considera un día lluvioso donde producción sigue fallando pero los registros no muestran el call stack de errores. ¿Que pasa? Tu código emite por error un objeto sin error y se perdió el trazado, una buena razón para golpearse la cabeza contra una pared de ladrillos. Una configuración de linter de 5 minutos podría detectar este GAZAPO y salvarte el día

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: El objeto de Error es emitido, no parece ninguna traza pora este error. Por suerte, ESLint detecta el siguiente error de producción

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "El objeto de Error es emitido, no parece ninguna traza pora este error. Por suerte, ESLint detecta el siguiente error de producción")

</details>

<br/><br/>

## ⚪ ️ 5.2 Acorta el tiempo de feedback con local developer-CI

:white_check_mark: **Haz:** Tienes un pipeline de CI con test, linter, verificación de vulnerabilidades, etc.? Ayuda a los desarrolladores a ejecutarlo también localmente para solicitar comentarios instantáneos y acortar el [ciclo de feedback] (https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2 -circuitos de retroalimentacion/). ¿Por qué? un proceso de prueba eficiente constituye muchos bucles iterativos: (1) tests -> (2) feedback -> (3) refactor. Cuanto más rápido sea el feedback, más iteraciones de mejora puede realizar un desarrollador por módulo y perfeccionar los resultados. Por otro lado, cuando el feedback tarda en llegar, se podrían realizar menos iteraciones de mejora en un solo día, el equipo podría estar ya haciendo otra cosa / tarea / módulo y podría no estar listo para refinar ese módulo

En la practica, algunos proveedores de CI (Ejemplo: [CircleCI CLI local] (https://circleci.com/docs/2.0/local-cli/)) permiten ejecutar el pipeline localmente. Algunas herramientas comerciales como [wallaby proporcionan información valiosa y de test] (https://wallabyjs.com/) para el desarrollador sin coste. Alternativamente, puedes agregar scripts npm en el package.json para ejecutar todos los comandos de calidad (por ejemplo, test, linter, vulnerabilidades) - usa herramientas como [concurrently] (https://www.npmjs.com/package/concurrently) para paralelizarlas y que código de salida sea distinto de cero si falla alguna de las herramientas. Ahora el desarrollador solo debe invocar un comando - por ejemplo "npm run quality": para obtener feedback en el acto. Considera también cancelar un commit si el control de calidad falla usando un githook ([husky puede ayudar] (https://github.com/typicode/husky))

<br/>

❌ **De lo contrario:** Cuando los resultados de calidad llegan un día más tarde que el código, los test no se convierten en una parte fluida del desarrollo, sino en algo formal posterior al mismo

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Scripts npm que realizan una inspección de calidad del código, todos se ejecutan en paralelo a demanda o cuando un desarrollador está tratando de hacer commit/push de código nuevo

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

## ⚪ ️5.3 Realiza test e2e sobre un espejo de producción

:white_check_mark: **Haz:** Los test End to end (e2e) testing son el principal desafio de un pipeline CI - crear un entorno espejo de produccion efimero que se genere sobre la marcha con todos los servicios necesarios puede ser tedioso y muy costoso. Buscando la mejor opcion: [Docker-compose](https://docs.docker.com/compose/) permite crear un entorno dockerizado aislado con mismos contenedores usando un unico fichero de texto plano, pero con la tecnologia por debajo (redes, despliegues) ser diferentes a las de produccion. Puedes combinarlo con [‘AWS Local’](https://github.com/localstack/localstack) para trabajr en hacer stubs de servicios AWS de verdad. Si usas [serverless](https://serverless.com/) existen multiple frameworks como serverless and [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) que te permiten invocar código Faas en local

El enorme ecosistema de Kubernetes aún no tiene una herramienta estandar para la duplicación en local y CI, aunque salen herramientas nuevas cada día. Un enfoque puede ser ejecutar implementaciones de 'kubernetes reducidos' con [Minikube](https://kubernetes.io/docs/setup/minikube/) o [MicroK8s](https://microk8s.io/) que es igual que el kubernetes completo pero con menos complejidad. Otro enfoque es tener un kubernetes de verdad remoto para test, algunso proveedores de CI (por ejemplo [Codefresh](https://codefresh.io/)) tiene integración nativa con entronos kubernetes y pueden facilmente ejecutar el pipeline CI sobre algo más real, otro permiten ejecutar scripts customizado contra kubernetes remotos

<br/>

❌ **De lo contrario:** El uso de diferentes tecnologías para la producción y los test exige mantener dos modelos de implementación y mantiene a los desarrolladores y al equipo de operaciones separados

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo: un pipeline de CI que genera un clúster de Kubernetes al vuelo <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credito: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Parallelizar la ejecución de los test

:white_check_mark: **Haz:** Cuando se hace correctamente, los test son tu amigo 24/7 propocionando feedback instantaneo. En la practica, ejecutar 500 test unitarios en un solo proceso en CPU puede llevar demasiado tiempo. Afortunadamente, los test runner más modernos y las plataformas de CI (como [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) y [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) pueden paralelizar los test en multiples procesos y lograr una mejora importante en el tiempo en entregar feedback. Algunos proveedores de CI también paralelizan las pruebas en contenedores (!) lo que acorta aún más la entrega de feedback. Ya sea localmente con multiples procesos, o sobre algun CLI en cloud usando multiples maquinas - pararelizar la demanda manteniendo los test autonomos para que cada uno pueda ejecutarse en diferentes procesos

❌ **De lo contrario:** Obtener el resultado de los test en 1 hora despues de hacer push de código nuevo, mientras desarrollas nuevas funcionalidades, es la mejor receta para quitarle relevancia a los test

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Mocha parallel y Jest superan facilmente al Mocha tradicional gracias a la paralelización de la ejecución de los test ([Credito: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel y Jest superan facilmente al Mocha tradicional gracias a la paralelización de la ejecución de los test (Credito: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Mantente al margen de problemas legales usando la verificación de licencia y plagio

:white_check_mark: **Haz:** Los problemas de licencias y plagio seguramente no son tu prioridad ahora mismo, pero ¿por que no hacer check en esta tarea en solo 10 minutos? Existen muchos paquetes npm como [license check](https://www.npmjs.com/package/license-checker) y [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial pero con plan gratuito) que puedes integrar facilmente en tu pipeline CI e inspeccionar en busca de problemas como dependencias con licencias restrictivas, o código que fue copiado y pegado de stackoverflow que aparentemente viola algunos copyrights

❌ **De lo contrario:** Sin querer, los desarrolladores pueden usar paquete con licencias inapropiadas o copiar y pegar código comercial y encontrarse con problemas legales

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente:

```javascript
//instala license-checker en tu entorno de CI o localmente
npm install -g license-checker

//pidele que escanee todas las licencias y que termine con un codigo distindo de 0 si encuentra una licencia no autorizada. De esta forma el pipeline de CI puede detectarlo y detenerse
license-checker --summary --failOn BSD

```

<br/>

![alt text](assets/bp-25-nodejs-licsense.png)

</details>

<br/><br/>

## ⚪ ️5.6 Verifica constantemente las dependencias vulnerables

:white_check_mark: **Haz:** Incluso las dependencias más conocidas como express, tiene vulnerabilidades conocidas. Puedes dominarlas facilmente usando herramientas libres como [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), o commerciales como [snyk](https://snyk.io/) (que tiene una version community gratuita). Ambas pueden ser ejecutadas desde tu CI en cada construcción

❌ **De lo contrario:** Mantener tu código limpio de vulnerabilidades sin herramientas dedicadas requiere que estes revisando constantemente las nuevas versiones. Muy tedioso

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo: resultado de NPM Audit

![alt text](assets/bp-26-npm-audit-snyk.png "resultado de NPM Audit")

</details>

<br/><br/>

## ⚪ ️5.7 Automatiza la actualización de dependencias

:white_check_mark: **Haz:** La introducción en yarn and npm de package-lock.json introduce un desafio muy importante ( el camino al infierno esta lleno de buenas intenciones) — por defecto ahora, lo paquetes no se auto actualiza más. Incluso en un equipo que ejecute un 'npm install' limpio y 'npm update' no van a caer nuevas actualizaciones. Esto conduce a veriones de paquetes desactualizadas en el mejor de los casos, y en el peor, a codigo vulnerable. Los equipos pasan a depender de la buena voluntad y memoria de los desarrolladores para actualizar el package.json a mano o a utilizar herramientas como [ncu](https://www.npmjs.com/package/npm-check-updates) manualmente. Una formula mucho mejor seria automatizar el proceso de actualizar las versiones de las dependenecias en las que más confiamos, pero no hay una solucion perfecta, existen dos caminos para esta actualización:

(1) Podemos hacer que el CI falle con dependencias obsoletas — usando herramientas como [‘npm outdated’](https://docs.npmjs.com/cli/outdated) o ‘npm-check-updates (ncu)’. Hacerlo obligará a los desarrolladores a actualizar las dependencias

(2) Usar alguna de las herramientas comerciales que escanean nuestro codigo y envian automaticamente pull-request con actualización de dependencias. Una pregunta interesante que nos queda es cual va a ser la politica de estas actualizaciones: si actualizamos cada parche se genera mucha sobrecarga, y hacerlo cuando haya una version major nos lleva directos a usar verisones inestables o incompatibles (mucho paquetes muestran vulnerabilidades justo despues de salir una version nueva [lee sobre](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) el incidente de eslint-scope).

Una politica de actualizaciones eficiente puede permitir cierto 'periodo de concesion' - deja pasar versiones quedandote por detras de @latest un tiempo antes de considerar que tu versión en local está obsoleta (por ejemplo, la versión que tienes en local es 1.3.1 y la versión del repositorio del paquete es 1.3.8)

<br/>

❌ **De lo contrario:** Producción estara ejecutando versiones de paquetes que han sido marcadas por los propios autores como version con riesgos

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo: [ncu](https://www.npmjs.com/package/npm-check-updates) puede ser usado a mano o en un pipline de CI para detectar en que medida el lag de retraso contra la versión @latest

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu puede ser usado a mano o en un pipline de CI para detectar en que medida el lag de retraso contra la versión @latest")

</details>

<br/><br/>

## ⚪ ️ 5.8 Otros consejos de CI no relacionados con Node

:white_check_mark: **Haz:** Esta publicación se centra en los consejos sobre testing que están relacionados, o al menos pueden ejemplificarse con el Node JS. Sin embargo, este punto agrupa algunos consejos no relacionados con Node que son bien conocidos

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use una sintaxis declarativa. Esta es la única opción para la mayoría de los pipelines de CI, pero las versiones antiguas de Jenkins permiten usar código o incluos una interfaz de usuario</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opte por un CI que tenga soporte nativo de Docker</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Falla antes, ejecuta tus test más rápidas primero. Crea un paso / hito de 'Smoke testing' que agrupe múltiples verificaciones rápidas (por ejemplo, linter, test unitarios) y que proporcione comentarios rápidamente al desarrollador que haya commiteado</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Facilite la exploración de todos las partes de construcción, incluidos reportes de test, informes de cobertura, informes de mutación, registros, etc.</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Crea múltiples pipelines / jobs para cada evento y reutilice los pasos entre ellos. Por ejemplo, configure un job para confirmaciones de commits a ramas de desarrollo y uno diferente para la rama master. Permita la reutilización de la logica usando pasos compartidos en los pipelines (la mayoría de los proveedores proporcionan algún mecanismo para la reutilización de código)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Nunca uses secretos directamente en la declaración del job, traelos de un store de secretos o de la configuración del propio job</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Suba explícitamente la versión de una release o al menos asegúrate de que el desarrollador lo hizo</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Construye solo una vez y realiza todas las inspecciones sobre el artefacto construido único (por ejemplo, imagen Docker)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Testea en un entorno efímero que no arrastre el estado entre las construcciones. El almacenamiento en caché de node_modules podría ser la única excepción</li></ol>
<br/>

❌ **De lo contrario:** Echarás de menos años de sabiduría

<br/><br/>

## ⚪ ️ 5.9 Build matrix: Run the same CI steps using multiple Node versions

:white_check_mark: **Haz:** Quality checking is about serendipity, the more ground you cover the luckier you get in detecting issues early. When developing reusable packages or running a multi-customer production with various configuration and Node versions, the CI must run the pipeline of tests over all the permutations of configurations. For example, assuming we use MySQL for some customers and Postgres for others — some CI vendors support a feature called ‘Matrix’ which allow running the suit of testing against all permutations of MySQL, Postgres and multiple Node version like 8, 9 and 10. This is done using configuration only without any additional effort (assuming you have testing or any other quality checks). Other CIs who doesn’t support Matrix might have extensions or tweaks to allow that
<br/>

❌ **De lo contrario:** So after doing all that hard work of writing testing are we going to let bugs sneak in only because of configuration issues?

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo: Using Travis (CI vendor) build definition to run the same test over multiple Node versions

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
    <td align="center"><a href="https://twitter.com/michalbiesiada"><img src="https://avatars0.githubusercontent.com/u/18367606?v=4" width="100px;" alt=""/><br /><sub><b>Michal</b></sub></a><br /><a href="#content-mbiesiad" title="Content">🖋</a></td>
    <td align="center"><a href="http://roywalker.me"><img src="https://avatars0.githubusercontent.com/u/611846?v=4" width="100px;" alt=""/><br /><sub><b>roywalker</b></sub></a><br /><a href="#content-roywalker" title="Content">🖋</a></td>
    <td align="center"><a href="https://dangen-effy.github.io/"><img src="https://avatars3.githubusercontent.com/u/23185799?v=4" width="100px;" alt=""/><br /><sub><b>dangen</b></sub></a><br /><a href="#content-dangen-effy" title="Content">🖋</a></td>
    <td align="center"><a href="https://dev.to/mbiesiad"><img src="https://avatars1.githubusercontent.com/u/60202305?v=4" width="100px;" alt=""/><br /><sub><b>biesiadamich</b></sub></a><br /><a href="#content-biesiadamich" title="Content">🖋</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->
