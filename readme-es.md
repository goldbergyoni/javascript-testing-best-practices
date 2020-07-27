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

:white_check_mark: **Haz:** Testear las partes internas suele traer un gasto extra enorme para muy poco beneficio. Si tu código/API comprueba todo los resultado correctamente, ¿deberias perder las proximas 3 horas en comprobar como esta funcionando internamente y despues mantener esos test tan fragiles? Cada vez que se comprueba un comportamiento publico, la implementacion privada es implicitamente testeada y tus test se romperan solo si hay un problema concreto (por ejemplo una salida incorrecta). Este enfoque tambien es conocido como `behavioral testing` (testing de comportamiento). Por otro lado, si se testean las partes internas (caja blanca) tu enfoque cambia de planificar la salida del componente a detalles minusculos, y tus test pueden romperse debido a refactors de código menores sin que se rompan los test de salida, por lo que aumenta tremendamente el mantenimiento de los mismos.<br/>

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

:white_check_mark: **Haz:** A menudo, los errores de producción se revelan bajo una entrada muy específica y sorprendente: cuanto más realista sea la entrada de un test, mayores serán las posibilidades de detectar errores temprano. Utiliza bibliotecas dedicadas como [Faker] (https://www.npmjs.com/package/faker) para generar datos pseudo-reales que se asemejan en variedad y forma a los datos de prodcucción. Por ejemplo, dichas bibliotecas pueden generar números de teléfono realistas, nombres de usuario, tarjetas de crédito, nombres de empresas e incluso texto "lorem ipsum". También puedes crear algunos test (además de los test unitarios, no como un reemplazo) que aleatorizan los datos falsos para estirar la unidad que estamos testeando o incluso importar datos reales de su entorno de producción. ¿Quieres llevarlo al siguiente nivel? Vea la próxima sección (test basados en propiedades).
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
  //!Hemos descubierto un error muy pronto!
});
```

</details>

<br/><br/>

## ⚪ ️ 1.7 Testea muchas combinaciones de entrada utilizando test basados en propiedades

:white_check_mark: **Haz:** Por lo general elegimos pocos datos de entrada por cada test. Incluso cuando el formato de entrada se parece a datos reales (ver sección "no uses foo"), cubrimos solo unas pocas combinaciones de datos de entrada (method(‘’, true, 1), method(“string” , false” , 0)), Sin embargo, en producción, un API que es llamada con 5 parametros puede ser invocada por miles de permutaciones diferentes, una sola puede hacer que nuestro poceso falle ([ver Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)). ¿Qué tal si pudieras escribir un solo test que envíe 1000 permutaciones de diferentes entradas automáticamente y capture qué entrada hace que código no devuelva la respuesta correcta? Los test basados en propiedades son una técnica que hace exactamente eso: al enviar todas las combinaciones de entrada posibles a la unidad que está siendo testada, aumenta la probabilidad de encontrar un error. Por ejemplo, dado un metodo — addNewProduct(id, name, isDiscount) — las librerias compatibles llamaran a ese metodo con muchas combinaciones (numeros, textos y boleanos) como (1, “iPhone”, false), (2, “Galaxy”, true). Puedes ejecutar test basados en propiedades usando nuestra libreria de esta favorita (Mocha, Jest, etc) como [js-verify](https://github.com/jsverify/jsverify) o [testcheck](https://github.com/leebyron/testcheck-js) (mucho mejor documentada). Actualizado: Nicolas Dubien sugiere en los comentarios [checkout fast-check](https://github.com/dubzzz/fast-check#readme) que parece ofecer caracteristicas adicionales y es activamente mantenida.
<br/>

❌ **De lo contrario:** Inconscientemente, eliges los datos de entradas para tus test que cubren solo las ramas de código que funcionan bien. Desafortunadamente, esto disminuye la eficiencia de los test como vehículo para detectar errores.

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

:white_check_mark: **Haz:** Siguiendo la regla de oro (sección 0), cada test debe añadir y actuar en su propio conjunto de filas DB para evitar el acoplamiento y poder razonar fácilmente sobre el flujo del test. En realidad esto es a menudo ignorado por los desarroladores de test que siembran la DB con datos antes de ejecutar las pruebas ([tambien conocido como ‘test fixture’](https://en.wikipedia.org/wiki/Test_fixture)) a favor de mejorar el rendimiento. Si bien el rendimiento es una preocupación válida — puede mitigarse de otras formas (consulte la sección "test de componentes"), sin embargo, la complegidad del test es más dolorosa que otras consideraciones la mayoria de las veces. De manera practica, haga que cada test añada explicitamente los registros que necesitas y actua sobre ellos. Si el rendimiento se convierte en algo critico — se puede llegar al compromiso de utilizar los mismos datos en un conjunto de test siempre que no se muten los datos (por ejemplo en queries).

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

❌ **De lo contrario:** Sería muy dificil deducir a partir de los informes de test (por ejemplo, informe de CI) que es lo que ha salido mal

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

❌ **De lo contrario:** Cuando nos enfrentamos a un reporte con una lista plana de test, tendremos que leer rápidamente textos largos para determinar los escenarios principales y relacionar los test fallidos. Considera el siguiente caso: Cuando 7/100 test fallan, revisar una lista plana te exige leer el tesxto de las pruebas que fallan para ver como se relacionan entre ellas y que tienen en común. Sin embargo, en un informe jerarquizado, si los 7 estan bajo un mismo flujo o categoria, puedes saber rápidamente cual o donde puede estar la causa raiz del fallo

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

:white_check_mark: **Haz:** Each unit test covers a tiny portion of the application and it’s expensive to cover the whole, whereas end-to-end testing easily covers a lot of ground but is flaky and slower, why not apply a balanced approach and write tests that are bigger than unit tests but smaller than end-to-end testing? Component testing is the unsung song of the testing world — they provide the best from both worlds: reasonable performance and a possibility to apply TDD patterns + realistic and great coverage.

Component tests focus on the Microservice ‘unit’, they work against the API, don’t mock anything which belongs to the Microservice itself (e.g. real DB, or at least the in-memory version of that DB) but stub anything that is external like calls to other Microservices. By doing so, we test what we deploy, approach the app from outwards to inwards and gain great confidence in a reasonable amount of time.
<br/>

❌ **De lo contrario:** You may spend long days on writing unit tests to find out that you got only 20% system coverage

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Supertest allows approaching Express API in-process (fast and cover many layers)

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 Ensure new releases don’t break the API using

:white_check_mark: **Haz:** So your Microservice has multiple clients, and you run multiple versions of the service for compatibility reasons (keeping everyone happy). Then you change some field and ‘boom!’, some important client who relies on this field is angry. This is the Catch-22 of the integration world: It’s very challenging for the server side to consider all the multiple client expectations — On the other hand, the clients can’t perform any testing because the server controls the release dates. [Consumer-driven contracts and the framework PACT](https://docs.pact.io/) were born to formalize this process with a very disruptive approach — not the server defines the test plan of itself rather the client defines the tests of the… server! PACT can record the client expectation and put in a shared location, “broker”, so the server can pull the expectations and run on every build using PACT library to detect broken contracts — a client expectation that is not met. By doing so, all the server-client API mismatches are caught early during build/CI and might save you a great deal of frustration
<br/>

❌ **De lo contrario:** The alternatives are exhausting manual testing or deployment fear

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente:

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "Ejemplos con PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪ ️ 2.4 Test your middlewares in isolation

:white_check_mark: **Haz:** Many avoid Middleware testing because they represent a small portion of the system and require a live Express server. Both reasons are wrong — Middlewares are small but affect all or most of the requests and can be tested easily as pure functions that get {req,res} JS objects. To test a middleware function one should just invoke it and spy ([using Sinon for example](https://www.npmjs.com/package/sinon)) on the interaction with the {req,res} objects to ensure the function performed the right action. The library [node-mock-http](https://www.npmjs.com/package/node-mocks-http) takes it even further and factors the {req,res} objects along with spying on their behavior. For example, it can assert whether the http status that was set on the res object matches the expectation (See example below)
<br/>

❌ **De lo contrario:** A bug in Express middleware === a bug in all or most requests

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap:Ejemplo de cómo hacerlo correctamente: Testing middleware in isolation without issuing network calls and waking-up the entire Express machine

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Ejemplos con Jest")

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

## ⚪ ️2.5 Measure and refactor using static analysis tools

:white_check_mark: **Haz:** Using static analysis tools helps by giving objective ways to improve code quality and keep your code maintainable. You can add static analysis tools to your CI build to abort when it finds code smells. Its main selling points over plain linting are the ability to inspect quality in the context of multiple files (e.g. detect duplications), perform advanced analysis (e.g. code complexity) and follow the history and progress of code issues. Two examples of tools you can use are [Sonarqube](https://www.sonarqube.org/) (2,600+ [stars](https://github.com/SonarSource/sonarqube)) and [Code Climate](https://codeclimate.com/) (1,500+ [stars](https://github.com/codeclimate/codeclimate))

Credit: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **De lo contrario:** With poor code quality, bugs and performance will always be an issue that no shiny new library or state of the art features can fix

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: CodeClimate, a commercial tool that can identify complex methods:

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Ejemplos con CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimat, a commercial tool that can identify complex methods:")

</details>

<br/><br/>

## ⚪ ️ 2.6 Check your readiness for Node-related chaos

:white_check_mark: **Haz:** Weirdly, most software testings are about logic & data only, but some of the worst things that happen (and are really hard to mitigate) are infrastructural issues. For example, did you ever test what happens when your process memory is overloaded, or when the server/process dies, or does your monitoring system realizes when the API becomes 50% slower?. To test and mitigate these type of bad things — [Chaos engineering](https://principlesofchaos.org/) was born by Netflix. It aims to provide awareness, frameworks and tools for testing our app resiliency for chaotic issues. For example, one of its famous tools, [the chaos monkey](https://github.com/Netflix/chaosmonkey), randomly kills servers to ensure that our service can still serve users and not relying on a single server (there is also a Kubernetes version, [kube-monkey](https://github.com/asobti/kube-monkey), that kills pods). All these tools work on the hosting/platform level, but what if you wish to test and generate pure Node chaos like check how your Node process copes with uncaught errors, unhandled promise rejection, v8 memory overloaded with the max allowed of 1.7GB or whether your UX stays satisfactory when the event loop gets blocked often? to address this I’ve written, [node-chaos](https://github.com/i0natan/node-chaos-monkey) (alpha) which provides all sort of Node-related chaotic acts
<br/>

❌ **De lo contrario:** No escape here, Murphy’s law will hit your production without mercy

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: : Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/>

## ⚪ ️2.7 Avoid global test fixtures and seeds, add data per-test

:white_check_mark: **Haz:** Going by the golden rule (bullet 0), each test should add and act on its own set of DB rows to prevent coupling and easily reason about the test flow. In reality, this is often violated by testers who seed the DB with data before running the tests (also known as ‘test fixture’) for the sake of performance improvement. While performance is indeed a valid concern — it can be mitigated (see “Component testing” bullet), however, test complexity is a much painful sorrow that should govern other considerations most of the time. Practically, make each test case explicitly add the DB records it needs and act only on those records. If performance becomes a critical concern — a balanced compromise might come in the form of seeding the only suite of tests that are not mutating data (e.g. queries)
<br/>

❌ **De lo contrario:** Few tests fail, a deployment is aborted, our team is going to spend precious time now, do we have a bug? let’s investigate, oh no — it seems that two tests were mutating the same seed data

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: tests are not independent and rely on some global hook to feed global DB data

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Ejemplos con Mocha")

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

### :clap: Ejemplo de cómo hacerlo correctamente: We can stay within the test, each test acts on its own set of data

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

# Section 3️⃣: Frontend Testing

## ⚪ ️ 3.1 Separate UI from functionality

:white_check_mark: **Haz:** When focusing on testing component logic, UI details become a noise that should be extracted, so your tests can focus on pure data. Practically, extract the desired data from the markup in an abstract way that is not too coupled to the graphic implementation, assert only on pure data (vs HTML/CSS graphic details) and disable animations that slow down. You might get tempted to avoid rendering and test only the back part of the UI (e.g. services, actions, store) but this will result in fictional tests that don't resemble the reality and won't reveal cases where the right data doesn't even arrive in the UI

<br/>

❌ **De lo contrario:** The pure calculated data of your test might be ready in 10ms, but then the whole test will last 500ms (100 tests = 1 min) due to some fancy and irrelevant animation

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Separating out the UI details

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Ejemplos con React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Ejemplos con react-testing-library")

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

### :thumbsdown: Ejemplo Anti Patrón: Assertion mix UI details and data

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

## ⚪ ️ 3.2 Query HTML elements based on attributes that are unlikely to change

:white_check_mark: **Haz:** Query HTML elements based on attributes that are likely to survive graphic changes unlike CSS selectors and like form labels. If the designated element doesn't have such attributes, create a dedicated test attribute like 'test-id-submit-button'. Going this route not only ensures that your functional/logic tests never break because of look & feel changes but also it becomes clear to the entire team that this element and attribute are utilized by tests and shouldn't get removed

<br/>

❌ **De lo contrario:** You want to test the login functionality that spans many components, logic and services, everything is set up perfectly - stubs, spies, Ajax calls are isolated. All seems perfect. Then the test fails because the designer changed the div CSS class from 'thick-border' to 'thin-border'

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Querying an element using a dedicated attrbiute for testing

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

### :thumbsdown: Ejemplo Anti Patrón: Relying on CSS attributes

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

:white_check_mark: **Haz:** Whenever reasonably sized, test your component from outside like your users do, fully render the UI, act on it and assert that the rendered UI behaves as expected. Avoid all sort of mocking, partial and shallow rendering - this approach might result in untrapped bugs due to lack of details and harden the maintenance as the tests mess with the internals (see bullet 'Favour blackbox testing'). If one of the child components is significantly slowing down (e.g. animation) or complicating the setup - consider explicitly replacing it with a fake

With all that said, a word of caution is in order: this technique works for small/medium components that pack a reasonable size of child components. Fully rendering a component with too many children will make it hard to reason about test failures (root cause analysis) and might get too slow. In such cases, write only a few tests against that fat parent component and more tests against its children

<br/>

❌ **De lo contrario:** When poking into a component's internal by invoking its private methods, and checking the inner state - you would have to refactor all tests when refactoring the components implementation. Do you really have a capacity for this level of maintenance?

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Working realstically with a fully rendered component

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
  // Arrange
  const wrapper = mount(<Calendar showFilters={false} />);

  // Act
  wrapper.find("button").simulate("click");

  // Assert
  expect(wrapper.text().includes("Choose Filter"));
  // This is how the user will approach this element: by text
});
```

### :thumbsdown: Ejemplo Anti Patrón: Mocking the reality with shallow rendering

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

:white_check_mark: **Haz:** In many cases, the unit under test completion time is just unknown (e.g. animation suspends element appearance) - in that case, avoid sleeping (e.g. setTimeOut) and prefer more deterministic methods that most platforms provide. Some libraries allows awaiting on operations (e.g. [Cypress cy.request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)), other provide API for waiting like [@testing-library/dom method wait(expect(element))](https://testing-library.com/docs/guide-disappearance). Sometimes a more elegant way is to stub the slow resource, like API for example, and then once the response moment becomes deterministic the component can be explicitly re-rendered. When depending upon some external component that sleeps, it might turn useful to [hurry-up the clock](https://jestjs.io/docs/en/timer-mocks). Sleeping is a pattern to avoid because it forces your test to be slow or risky (when waiting for a too short period). Whenever sleeping and polling is inevitable and there's no support from the testing framework, some npm libraries like [wait-for-expect](https://www.npmjs.com/package/wait-for-expect) can help with a semi-deterministic solution
<br/>

❌ **De lo contrario:** When sleeping for a long time, tests will be an order of magnitude slower. When trying to sleep for small numbers, test will fail when the unit under test didn't respond in a timely fashion. So it boils down to a trade-off between flakiness and bad performance

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: E2E API that resolves only when the async operations is done (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Ejemplos con react-testing-library")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: Ejemplo de cómo hacerlo correctamente: Testing library that waits for DOM elements

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

### :thumbsdown: Ejemplo Anti Patrón: custom sleep code

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

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Ejemplos con Lighthouse")

✅ **Haz:** Apply some active monitor that ensures the page load under real network is optimized - this includes any UX concern like slow page load or un-minified bundle. The inspection tools market is no short: basic tools like [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) can be easily configured to watch whether the server is alive and response under a reasonable SLA. This only scratches the surface of what might get wrong, hence it's preferable to opt for tools that specialize in frontend (e.g. [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) and perform richer analysis. The focus should be on symptoms, metrics that directly affect the UX, like page load time, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [time until the page gets interactive (TTI)](https://calibreapp.com/blog/time-to-interactive/). On top of that, one may also watch for technical causes like ensuring the content is compressed, time to the first byte, optimize images, ensuring reasonable DOM size, SSL and many others. It's advisable to have these rich monitors both during development, as part of the CI and most important - 24x7 over the production's servers/CDN

<br/>

❌ **De lo contrario:** It must be disappointing to realize that after such great care for crafting a UI, 100% functional tests passing and sophisticated bundling - the UX is horrible and slow due to CDN misconfiguration

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

### :clap: Ejemplo de cómo hacerlo correctamente: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

</details>

<br/>

## ⚪ ️ 3.6 Stub flaky and slow resources like backend APIs

:white_check_mark: **Haz:** When coding your mainstream tests (not E2E tests), avoid involving any resource that is beyond your responsibility and control like backend API and use stubs instead (i.e. test double). Practically, instead of real network calls to APIs, use some test double library (like [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) for stubbing the API response. The main benefit is preventing flakiness - testing or staging APIs by definition are not highly stable and from time to time will fail your tests although YOUR component behaves just fine (production env was not meant for testing and it usually throttles requests). Doing this will allow simulating various API behavior that should drive your component behavior as when no data was found or the case when API throws an error. Last but not least, network calls will greatly slow down the tests

<br/>

❌ **De lo contrario:** The average test runs no longer than few ms, a typical API call last 100ms>, this makes each test ~20x slower

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Stubbing or intercepting API calls

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Ejemplos con React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Ejemplos con react-testing-library")

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

:white_check_mark: **Haz:** Although E2E (end-to-end) usually means UI-only testing with a real browser (See bullet 3.6), for other they mean tests that stretch the entire system including the real backend. The latter type of tests is highly valuable as they cover integration bugs between frontend and backend that might happen due to a wrong understanding of the exchange schema. They are also an efficient method to discover backend-to-backend integration issues (e.g. Microservice A sends the wrong message to Microservice B) and even to detect deployment failures - there are no backend frameworks for E2E testing that are as friendly and mature as UI frameworks like [Cypress](https://www.cypress.io/) and [Pupeteer](https://github.com/GoogleChrome/puppeteer). The downside of such tests is the high cost of configuring an environment with so many components, and mostly their brittleness - given 50 microservices, even if one fails then the entire E2E just failed. For that reason, we should use this technique sparingly and probably have 1-10 of those and no more. That said, even a small number of E2E tests are likely to catch the type of issues they are targeted for - deployment & integration faults. It's advisable to run those over a production-like staging environment

<br/>

❌ **De lo contrario:** UI might invest much in testing its functionality only to realizes very late that the backend returned payload (the data schema the UI has to work with) is very different than expected

<br/>

## ⚪ ️ 3.8 Speed-up E2E tests by reusing login credentials

:white_check_mark: **Haz:** In E2E tests that involve a real backend and rely on a valid user token for API calls, it doesn't payoff to isolate the test to a level where a user is created and logged-in in every request. Instead, login only once before the tests execution start (i.e. before-all hook), save the token in some local storage and reuse it across requests. This seem to violate one of the core testing principle - keep the test autonomous without resources coupling. While this is a valid worry, in E2E tests performance is a key concern and creating 1-3 API requests before starting each individial tests might lead to horrible execution time. Reusing credentials doesn't mean the tests have to act on the same user records - if relying on user records (e.g. test user payments history) than make sure to generate those records as part of the test and avoid sharing their existence with other tests. Also remember that the backend can be faked - if your tests are focused on the frontend it might be better to isolate it and stub the backend API (see bullet 3.6).

<br/>

❌ **De lo contrario:** Given 200 test cases and assuming login=100ms = 20 seconds only for logging-in again and again

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Logging-in before-all and not before-each

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

:white_check_mark: **Haz:** For production monitoring and development-time sanity check, run a single E2E test that visits all/most of the site pages and ensures no one breaks. This type of test brings a great return on investment as it's very easy to write and maintain, but it can detect any kind of failure including functional, network and deployment issues. Other styles of smoke and sanity checking are not as reliable and exhaustive - some ops teams just ping the home page (production) or developers who run many integration tests which don't discover packaging and browser issues. Goes without saying that the smoke test doesn't replace functional tests rather just aim to serve as a quick smoke detector

<br/>

❌ **De lo contrario:** Everything might seem perfect, all tests pass, production health-check is also positive but the Payment component had some packaging issue and only the /Payment route is not rendering

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Smoke travelling across all pages

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

:white_check_mark: **Haz:** Besides increasing app reliability, tests bring another attractive opportunity to the table - serve as live app documentation. Since tests inherently speak at a less-technical and product/UX language, using the right tools they can serve as a communication artifact that greatly aligns all the peers - developers and their customers. For example, some frameworks allow expressing the flow and expectations (i.e. tests plan) using a human-readable language so any stakeholder, including product managers, can read, approve and collaborate on the tests which just became the live requirements document. This technique is also being referred to as 'acceptance test' as it allows the customer to define his acceptance criteria in plain language. This is [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) at its purest form. One of the popular frameworks that enable this is [Cucumber which has a JavaScript flavor](https://github.com/cucumber/cucumber-js), see example below. Another similar yet different opportunity, [StoryBook](https://storybook.js.org/), allows exposing UI components as a graphic catalog where one can walk through the various states of each component (e.g. render a grid w/o filters, render that grid with multiple rows or with none, etc), see how it looks like, and how to trigger that state - this can appeal also to product folks but mostly serves as live doc for developers who consume those components.

❌ **De lo contrario:** After investing top resources on testing, it's just a pity not to leverage this investment and win great value

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Describing tests in human-language using cucumber-js

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

### :clap: Ejemplo de cómo hacerlo correctamente: Visualizing our components, their various states and inputs using Storybook

![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Detect visual issues with automated tools

:white_check_mark: **Haz:** Setup automated tools to capture UI screenshots when changes are presented and detect visual issues like content overlapping or breaking. This ensures that not only the right data is prepared but also the user can conveniently see it. This technique is not widely adopted, our testing mindset leans toward functional tests but it's the visuals what the user experience and with so many device types it's very easy to overlook some nasty UI bug. Some free tools can provide the basics - generate and save screenshots for the inspection of human eyes. While this approach might be sufficient for small apps, it's flawed as any other manual testing that demands human labor anytime something changes. On the other hand, it's quite challenging to detect UI issues automatically due to the lack of clear definition - this is where the field of 'Visual Regression' chime in and solve this puzzle by comparing old UI with the latest changes and detect differences. Some OSS/free tools can provide some of this functionality (e.g. [wraith](https://github.com/BBC-News/wraith), [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>) but might charge signficant setup time. The commercial line of tools (e.g. [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) takes is a step further by smoothing the installation and packing advanced features like management UI, alerting, smart capturing by elemeinating 'visual noise' (e.g. ads, animations) and even root cause analysis of the DOM/css changes that led to the issue

<br/>

❌ **De lo contrario:** How good is a content page that display great content (100% tests passed), loads instantly but half of the content area is hidden?

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: A typical visual regression - right content that is served badly

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Configuring wraith to capture and compare UI snapshots

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

### :clap: Ejemplo de cómo hacerlo correctamente: Using Applitools to get snapshot comaprison and other advanced features

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

# Section 4️⃣: Measuring Test Effectiveness

<br/><br/>

## ⚪ ️ 4.1 Get enough coverage for being confident, ~80% seems to be the lucky number

:white_check_mark: **Haz:** The purpose of testing is to get enough confidence for moving fast, obviously the more code is tested the more confident the team can be. Coverage is a measure of how many code lines (and branches, statements, etc) are being reached by the tests. So how much is enough? 10–30% is obviously too low to get any sense about the build correctness, on the other side 100% is very expensive and might shift your focus from the critical paths to the exotic corners of the code. The long answer is that it depends on many factors like the type of application — if you’re building the next generation of Airbus A380 than 100% is a must, for a cartoon pictures website 50% might be too much. Although most of the testing enthusiasts claim that the right coverage threshold is contextual, most of them also mention the number 80% as a thumb of a rule ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) that presumably should satisfy most of the applications.

Implementation tips: You may want to configure your continuous integration (CI) to have a coverage threshold ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) and stop a build that doesn’t stand to this standard (it’s also possible to configure threshold per component, see code example below). On top of this, consider detecting build coverage decrease (when a newly committed code has less coverage) — this will push developers raising or at least preserving the amount of tested code. All that said, coverage is only one measure, a quantitative based one, that is not enough to tell the robustness of your testing. And it can also be fooled as illustrated in the next bullets

<br/>

❌ **De lo contrario:** Confidence and numbers go hand in hand, without really knowing that you tested most of the system — there will also be some fear and fear will slow you down

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Example: A typical coverage report

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Setting up coverage per component (using Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Using Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Inspect coverage reports to detect untested areas and other oddities

:white_check_mark: **Haz:** Some issues sneak just under the radar and are really hard to find using traditional tools. These are not really bugs but more of surprising application behavior that might have a severe impact. For example, often some code areas are never or rarely being invoked — you thought that the ‘PricingCalculator’ class is always setting the product price but it turns out it is actually never invoked although we have 10000 products in DB and many sales… Code coverage reports help you realize whether the application behaves the way you believe it does. Other than that, it can also highlight which types of code is not tested — being informed that 80% of the code is tested doesn’t tell whether the critical parts are covered. Generating reports is easy — just run your app in production or during testing with coverage tracking and then see colorful reports that highlight how frequent each code area is invoked. If you take your time to glimpse into this data — you might find some gotchas
<br/>

❌ **De lo contrario:** If you don’t know which parts of your code are left un-tested, you don’t know where the issues might come from

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: What’s wrong with this coverage report?

Based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Measure logical coverage using mutation testing

:white_check_mark: **Haz:** The Traditional Coverage metric often lies: It may show you 100% code coverage, but none of your functions, even not one, return the right response. How come? it simply measures over which lines of code the test visited, but it doesn’t check if the tests actually tested anything — asserted for the right response. Like someone who’s traveling for business and showing his passport stamps — this doesn’t prove any work done, only that he visited few airports and hotels.

Mutation-based testing is here to help by measuring the amount of code that was actually TESTED not just VISITED. [Stryker](https://stryker-mutator.io/) is a JavaScript library for mutation testing and the implementation is really neat:

(1) it intentionally changes the code and “plants bugs”. For example the code newOrder.price===0 becomes newOrder.price!=0. This “bugs” are called mutations

(2) it runs the tests, if all succeed then we have a problem — the tests didn’t serve their purpose of discovering bugs, the mutations are so-called survived. If the tests failed, then great, the mutations were killed.

Knowing that all or most of the mutations were killed gives much higher confidence than traditional coverage and the setup time is similar
<br/>

❌ **De lo contrario:** You’ll be fooled to believe that 85% coverage means your test will detect bugs in 85% of your code

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: 100% coverage, 0% testing

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

### :clap: Ejemplo de cómo hacerlo correctamente: Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>

<br/><br/>

## ⚪ ️4.4 Preventing test code issues with Test linters

:white_check_mark: **Haz:** A set of ESLint plugins were built specifically for inspecting the tests code patterns and discover issues. For example, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) will warn when a test is written at the global level (not a son of a describe() statement) or when tests are [skipped](https://mochajs.org/#inclusive-tests) which might lead to a false belief that all tests are passing. Similarly, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) can, for example, warn when a test has no assertions at all (not checking anything)

<br/>

❌ **De lo contrario:** Seeing 90% code coverage and 100% green tests will make your face wear a big smile only until you realize that many tests aren’t asserting for anything and many test suites were just skipped. Hopefully, you didn’t deploy anything based on this false observation

<br/>
<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: A test case full of errors, luckily all are caught by Linters

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

:white_check_mark: **Haz:** Linters are a free lunch, with 5 min setup you get for free an auto-pilot guarding your code and catching significant issue as you type. Gone are the days where linting was about cosmetics (no semi-colons!). Nowadays, Linters can catch severe issues like errors that are not thrown correctly and losing information. On top of your basic set of rules (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), consider including some specializing Linters like [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) that can discover tests without assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) can discover promises with no resolve (your code will never continue), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) which can discover eager regex expressions that might get used for DOS attacks, and [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) is capable of alarming when the code uses utility library methods that are part of the V8 core methods like Lodash.\_map(…)
<br/>

❌ **De lo contrario:** Consider a rainy day where your production keeps crashing but the logs don’t display the error stack trace. What happened? Your code mistakenly threw a non-error object and the stack trace was lost, a good reason for banging your head against a brick wall. A 5min linter setup could detect this TYPO and save your day

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :thumbsdown: Ejemplo Anti Patrón: The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>

<br/><br/>

## ⚪ ️ 5.2 Shorten the feedback loop with local developer-CI

:white_check_mark: **Haz:** Using a CI with shiny quality inspections like testing, linting, vulnerabilities check, etc? Help developers run this pipeline also locally to solicit instant feedback and shorten the [feedback loop](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Why? an efficient testing process constitutes many and iterative loops: (1) try-outs -> (2) feedback -> (3) refactor. The faster the feedback is, the more improvement iterations a developer can perform per-module and perfect the results. On the flip, when the feedback is late to come fewer improvement iterations could be packed into a single day, the team might already move forward to another topic/task/module and might not be up for refining that module.

Practically, some CI vendors (Example: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/)) allow running the pipeline locally. Some commercial tools like [wallaby provide highly-valuable & testing insights](https://wallabyjs.com/) as a developer prototype (no affiliation). Alternatively, you may just add npm script to package.json that runs all the quality commands (e.g. test, lint, vulnerabilities) — use tools like [concurrently](https://www.npmjs.com/package/concurrently) for parallelization and non-zero exit code if one of the tools failed. Now the developer should just invoke one command — e.g. ‘npm run quality’ — to get instant feedback. Consider also aborting a commit if the quality check failed using a githook ([husky can help](https://github.com/typicode/husky))
<br/>

❌ **De lo contrario:** When the quality results arrive the day after the code, testing doesn’t become a fluent part of development rather an after the fact formal artifact

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: npm scripts that perform code quality inspection, all are run in parallel on demand or when a developer is trying to push new code

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

:white_check_mark: **Haz:** End to end (e2e) testing are the main challenge of every CI pipeline — creating an identical ephemeral production mirror on the fly with all the related cloud services can be tedious and expensive. Finding the best compromise is your game: [Docker-compose](https://serverless.com/) allows crafting isolated dockerized environment with identical containers using a single plain text file but the backing technology (e.g. networking, deployment model) is different from real-world productions. You may combine it with [‘AWS Local’](https://github.com/localstack/localstack) to work with a stub of the real AWS services. If you went [serverless](https://serverless.com/) multiple frameworks like serverless and [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) allows the local invocation of Faas code.

The huge Kubernetes eco-system is yet to formalize a standard convenient tool for local and CI-mirroring though many new tools are launched frequently. One approach is running a ‘minimized-Kubernetes’ using tools like [Minikube](https://kubernetes.io/docs/setup/minikube/) and [MicroK8s](https://microk8s.io/) which resemble the real thing only come with less overhead. Another approach is testing over a remote ‘real-Kubernetes’, some CI providers (e.g. [Codefresh](https://codefresh.io/)) has native integration with Kubernetes environment and make it easy to run the CI pipeline over the real thing, others allow custom scripting against a remote Kubernetes.
<br/>

❌ **De lo contrario:** Using different technologies for production and testing demands maintaining two deployment models and keeps the developers and the ops team separated

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Example: a CI pipeline that generates Kubernetes cluster on the fly <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Parallelize test execution

:white_check_mark: **Haz:** When done right, testing is your 24/7 friend providing almost instant feedback. In practice, executing 500 CPU-bounded unit test on a single thread can take too long. Luckily, modern test runners and CI platforms (like [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) and [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) can parallelize the test into multiple processes and achieve significant improvement in feedback time. Some CI vendors do also parallelize tests across containers (!) which shortens the feedback loop even further. Whether locally over multiple processes, or over some cloud CLI using multiple machines — parallelizing demand keeping the tests autonomous as each might run on different processes

❌ **De lo contrario:** Getting test results 1 hour long after pushing new code, as you already code the next features, is a great recipe for making testing less relevant

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente: Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Stay away from legal issues using license and plagiarism check

:white_check_mark: **Haz:** Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like [license check](https://www.npmjs.com/package/license-checker) and [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stackoverflow and apparently violates some copyrights

❌ **De lo contrario:** Unintentionally, developers might use packages with inappropriate licenses or copy paste commercial code and run into legal issues

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Ejemplo de cómo hacerlo correctamente:

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

:white_check_mark: **Haz:** Even the most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community tools such as [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), or commercial tools like [snyk](https://snyk.io/) (offer also a free community version). Both can be invoked from your CI on every build

❌ **De lo contrario:** Keeping your code clean from vulnerabilities without dedicated tools will require to constantly follow online publications about new threats. Quite tedious

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Example: NPM Audit result

![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>

<br/><br/>

## ⚪ ️5.7 Automate dependency updates

:white_check_mark: **Haz:** Yarn and npm latest introduction of package-lock.json introduced a serious challenge (the road to hell is paved with good intentions) — by default now, packages are no longer getting updates. Even a team running many fresh deployments with ‘npm install’ & ‘npm update’ won’t get any new updates. This leads to subpar dependent packages versions at best or to vulnerable code at worst. Teams now rely on developers goodwill and memory to manually update the package.json or use tools [like ncu](https://www.npmjs.com/package/npm-check-updates) manually. A more reliable way could be to automate the process of getting the most reliable dependency versions, though there are no silver bullet solutions yet there are two possible automation roads:

(1) CI can fail builds that have obsolete dependencies — using tools like [‘npm outdated’](https://docs.npmjs.com/cli/outdated) or ‘npm-check-updates (ncu)’ . Doing so will enforce developers to update dependencies.

(2) Use commercial tools that scan the code and automatically send pull requests with updated dependencies. One interesting question remaining is what should be the dependency update policy — updating on every patch generates too many overhead, updating right when a major is released might point to an unstable version (many packages found vulnerable on the very first days after being released, [see the](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope incident).

An efficient update policy may allow some ‘vesting period’ — let the code lag behind the @latest for some time and versions before considering the local copy as obsolete (e.g. local version is 1.3.1 and repository version is 1.3.8)
<br/>

❌ **De lo contrario:** Your production will run packages that have been explicitly tagged by their author as risky

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

<br/>

### :clap: Example: [ncu](https://www.npmjs.com/package/npm-check-updates) can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")

</details>

<br/><br/>

## ⚪ ️ 5.8 Other, non-Node related, CI tips

:white_check_mark: **Haz:** This post is focused on testing advice that is related to, or at least can be exemplified with Node JS. This bullet, however, groups few non-Node related tips that are well-known

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use a declarative syntax. This is the only option for most vendors but older versions of Jenkins allows using code or UI</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opt for a vendor that has native Docker support</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Fail early, run your fastest tests first. Create a ‘Smoke testing’ step/milestone that groups multiple fast inspections (e.g. linting, unit tests) and provide snappy feedback to the code committer</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Make it easy to skim-through all build artifacts including test reports, coverage reports, mutation reports, logs, etc</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Create multiple pipelines/jobs for each event, reuse steps between them. For example, configure a job for feature branch commits and a different one for master PR. Let each reuse logic using shared steps (most vendors provide some mechanism for code reuse)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Never embed secrets in a job declaration, grab them from a secret store or from the job’s configuration</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Explicitly bump version in a release build or at least ensure the developer did so</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Build only once and perform all the inspections over the single build artifact (e.g. Docker image)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Test in an ephemeral environment that doesn’t drift state between builds. Caching node_modules might be the only exception</li></ol>
<br/>

❌ **De lo contrario:** You‘ll miss years of wisdom

<br/><br/>

## ⚪ ️ 5.9 Build matrix: Run the same CI steps using multiple Node versions

:white_check_mark: **Haz:** Quality checking is about serendipity, the more ground you cover the luckier you get in detecting issues early. When developing reusable packages or running a multi-customer production with various configuration and Node versions, the CI must run the pipeline of tests over all the permutations of configurations. For example, assuming we use MySQL for some customers and Postgres for others — some CI vendors support a feature called ‘Matrix’ which allow running the suit of testing against all permutations of MySQL, Postgres and multiple Node version like 8, 9 and 10. This is done using configuration only without any additional effort (assuming you have testing or any other quality checks). Other CIs who doesn’t support Matrix might have extensions or tweaks to allow that
<br/>

❌ **De lo contrario:** So after doing all that hard work of writing testing are we going to let bugs sneak in only because of configuration issues?

<br/>

<details><summary>✏ <b>Código de Ejemplo</b></summary>

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