[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/_dHmXan8)
# Lección: Arrays, Objetos, Funciones y callbacks

En esta lección cubriremos:

- Introducción a los arrays
- Buscles `for` con arrays
- Introducción a los Objetos
- Métodos
- Bucles `for…in`
- Palabra clave `this`
- Objetos en Javascript
- Callbacks
- Más métodos de Arrays (**`filter`**, búsqueda, **`slice`/`splice`**, **`reverse`/`sort`**, flechas breves, **`Object.groupBy`** — ver secciones al final del capítulo posterior a **`.map`**)

## Herramientas de editor (ESLint / Prettier / VS Code)

En la raiz estan `.vscode/`, `.eslintrc.json`, `.prettierrc.js`, `.prettierignore` y `.env.example`. La carpeta `Configuration-Files/backend-nodejs/` conserva el kit original (incluye un `package.json` de ejemplo con Express/Mongo); **este repo solo usa Jest** para la consigna.

- `npm run lint` / `npm run lint:fix`
- `npm run format` / `npm run format:check`

## Mapa de práctica (`homework.js`)

Requisito de runtime: **Node.js 22+** (necesario para `Object.groupBy` en `agruparPorCampoObjectGroupBy`; ver `engines` en `package.json`). Ejecutá `npm install` y `npm test`.

| Bloque temático                                   | Funciones / constantes destacadas                                                                                                                         |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Objeto literal + `this`                           | `crearGato`, `invocarMetodo`, `agregarMetodoCalculoDescuento`, nuevos `objetoNombreMayuscConFlechaAnidada`, `establecerValorMismaReferencia`              |
| Mutabilidad objeto + borrados                     | `agregarPropiedad`, `eliminarPropiedad`, `establecerValorMismaReferencia`                                                                                 |
| Declaradas vs expresadas + hoisting (`typeof`)    | `resultadoTipoFuncionExpresadaVar`, `sumarMedianteExpresionNombrada`                                                                                      |
| Flechas (`=>`)                                    | `duplicarConFlecha`                                                                                                                                       |
| Callbacks / encadenamiento (sincrónico)           | `invocarCallback`, `sumarArray`, `encadenarOperacionesSinAnidar`                                                                                          |
| Arrays básicos + mutación puntual                 | Ejercicios iniciales; `invertirEnLugar`, `ordenarNumerosAsc`                                                                                              |
| `.push` / `.pop` / `.shift` / `.unshift`          | `agregarItemAlFinalDelArray`, `agregarItemAlComienzoDelArray`, `sacarUltimoConPop`, `sacarPrimeroConShift`                                                |
| Búsqueda / `join` / `slice` / `concat` / `splice` | `dePalabrasAFrase`, `unirConSeparador`, `indicePrimero`, `indiceUltimo`, `existeConIncludes`, `subArregloCopia`, `pegarDosArreglos`, `aplicarSpliceDesde` |
| `reverse` / `sort` mutantes                       | `invertirEnLugar`, `ordenarNumerosAsc`                                                                                                                    |
| `forEach` / `map` / `filter` (reimplementaciones) | `forEach`, `map`, `filter`                                                                                                                                |
| `reduce` / `Object.groupBy`                       | `sumatorioConReduce`, `agruparPorCampoReduce`, `agruparPorCampoObjectGroupBy`                                                                             |
| Arrays de objetos                                 | `pasarUsuarioAPremium`, `sumarLikesDeUsuario`                                                                                                             |

Consultá también **[MAPA_TEMARIO.md](MAPA_TEMARIO.md)** para el cierre de cobertura frente al temario oficial.

La teoría que complementa todas las APIs del **`homework.js`** aparece desarrollada **al final del capítulo _Más métodos de Arrays_** (bloques después de **`.map`**: búsqueda, `slice`/`splice`, `reverse`/`sort`, **`.filter`**, flechas/expresiones e **`Object.groupBy`**).

### Archivos del ejercicio y tests

- Trabajar en **`homework.js`** (raíz del repo) siguiendo los comentarios de cada función; no renombrar las funciones ni quitar líneas desde `module.exports` hacia abajo.
- Verificar soluciones con **`tests/pruebas.test.js`**: tras `npm install`, ejecutá `npm test` en esta carpeta.

### GitHub Classroom y Actions (autoevaluación)

- Este repositorio usa **GitHub Actions** para ejecutar `npm ci` + `npm test` automáticamente.
- La plantilla también incluye un workflow de **issues automáticas** (idempotente) para acompañar la entrega.
- En GitHub Classroom, el resultado de Actions da feedback rápido, pero no reemplaza la revisión docente.

## Introducción a los arrays (matrices/arreglos)

En la lección anterior discutimos los 3 tipos de datos básicos (cadenas/strings, números y booleanos) y cómo asignar esos tipos de datos a las variables. Discutimos cómo una variable solo puede apuntar a una sola cadena, número o booleano. Sin embargo, en muchos casos queremos poder apuntar a una colección de tipos de datos. Por ejemplo, ¿qué pasaría si quisiéramos hacer un seguimiento del nombre de cada estudiante en esta clase usando una sola variable, `nombresEstudiantes`. Podemos hacer eso usando Arrays. Podemos pensar en las matrices como contenedores de almacenamiento para colecciones de datos. Construir una matriz es simple, declarar una variable y establecerla en []. Luego podemos agregar al contenedor (separadas por coma) tantas cadenas, números o booleanos como queramos y acceder a esos elementos cuando lo deseemos.

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];
```

### .length

Al igual que el tipo de dato _String_ tiene un método incorporado `.length`, también lo hace la matriz. De hecho, la matriz tiene muchos métodos incorporados útiles (los discutiremos en lecciones posteriores). Al igual que la cadena `.length` cuenta los caracteres, la matriz` .length` devolverá el número de elementos en una matriz:

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

console.log(nombresEstudiantes.length); // 4
```

### Acceso a elementos en una matriz

Podemos acceder a un elemento de una matriza en cualquier momento, solo necesitamos llamar al elemento por su posición en la matriz. Los elementos reciben una posición numérica (índice) de acuerdo con su ubicación en la matriz, en orden. El orden numérico de una matriz SIEMPRE comienza en 0, por lo que el primer elemento está en el índice 0, el segundo en el índice 1, el tercero en el 2, y así sucesivamente (esto puede ser complicado al principio, pero solo recuerda que las matrices siempre comienzan en 0).

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];
                                0         1        2        3
```

Para acceder al elemento, escribiremos el nombre o la variable de matriz, seguidos de corchetes que contienen la asignación numérica.

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

console.log(nombresEstudiantes[1]); // 'Antonio'
```

Para acceder dinámicamente al último elemento de la matriz, utilizaremos el método `.length`. En nuestra matriz `nombresEstudiantes`, la longitud es 4. Sabemos que el primer elemento siempre será 0, y cada elemento posterior se desplaza sobre un número. Entonces, en nuestro ejemplo, el último elemento tiene un índice de 3. Usando nuestra propiedad de longitud mostraremos cómo se hace cuando no sabemos el número de elementos en una matriz:

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', ... ,'Samuel'];

console.log(nombresEstudiantes[nombresEstudiantes.length - 1]);  // 'Samuel'
```

### Asignación

Podemos asignar y reasignar cualquier índice en la matriz usando el paréntesis/índice y un "=".

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

nombresEstudiantes[0] = 'Jorge';

console.log(nombresEstudiantes); // ['Jorge', 'Antonio', 'Sara', 'Samuel']
```

### `.push` y `.pop`

Otros dos métodos de matriz incorporados muy útiles son `.push` y` .pop`. Estos métodos se refieren a la adición y eliminación de elementos de la matriz después de su declaración inicial.

`.push` agrega un elemento al final de la matriz, incrementando su longitud en 1. `.push` devuelve la nueva longitud.

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

nombresEstudiantes.push('Patricia');

console.log(nombresEstudiantes); // ['Martin', 'Antonio', 'Sara', 'Samuel', 'Patricia']
```

`.pop` elimina el último elemento de la matriz, disminuyendo la longitud en 1. `.pop` devuelve el elemento "reventado" (_popped_).

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

nombresEstudiantes.pop();

console.log(nombresEstudiantes); // ['Martin', 'Antonio', 'Sara']
```

### `.unshift` y `.shift`

`.unshift` y` .shift` son exactamente como `.push` y` .pop`, excepto que operan en el primer elemento de la matriz. `.unshift(item)` colocará un nuevo elemento en la primera posición de la matriz, y `.shift()` eliminará el primer elemento de la matriz.

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

nombresEstudiantes.unshift('Leo');

console.log(nombresEstudiantes); // ['Leo', 'Martin', 'Antonio', 'Sara', 'Samuel']

nombresEstudiantes.shift();

console.log(nombresEstudiantes); // ['Martin', 'Antonio', 'Sara', 'Samuel']
```

### Notas sobre las matrices

Debido a que Javascript no es un lenguaje fuertemente tipado, las matrices tampoco necesitan ser tipadas. Las matrices en Javascript pueden contener múltiples tipos de datos diferentes en la misma matriz.

## Bucles `for`

La mayoría de las veces, los bucles for se utilizan para iterar sobre todos los elementos de una matriz. Usando la técnica de acceso al índice ("index access technique") podemos acceder a cada elemento de la matriz. Para hacer esto, usamos el método `.length` como punto de parada para el ciclo.

```javascript
const nombresEstudiantes = ['Martin', 'Antonio', 'Sara', 'Samuel'];

for (let i = 0; i < nombresEstudiantes.length; i++) {
  console.log(nombresEstudiantes[i]);
}

// 'Martin'
// 'Antonio'
// 'Sara'
// 'Samuel'
```

## Objetos de argumento

Cuando pasamos argumentos a una función, están contenidos en una estructura de datos tipo matriz llamada 'argumentos'. `arguments` está disponible para nosotros en cualquier lugar dentro de la función y contiene todos los argumentos que se le pasan. Si bien es como una matriz, no tiene todas las propiedades de una matriz. Una propiedad que tiene es el método `.length`. Cuando se nos da una función con un número desconocido de argumentos, podemos usar `.length` y un bucle` for` para iterar sobre todos los argumentos:

```javascript
function sumarTodosLosNumeros() {
  let sum = 0;

  for (let i = 0; i < arguments.length; i++) {
    sum = sum + arguments[i];
  }

  return sum;
}

sumarTodosLosNumeros(2, 5, 3, 4, 7, 9, 1, 0, 7, 7, 7); // 52
```

## Introducción a los Objetos

En la anterior lección aprendimos sobre _arrays_ o matrices. Las matrices son contenedores que sostienen colecciones de datos. En esta lección, introduciremos otro contenedor de datos, el _Objeto_. Los objetos y las matrices son similares en ciertas cosas, y muy diferentes en otras. Mientras que los array pueden contener múltiples elementos relacionados unos con otros, los objetos contienen mucha información sobre una sola cosa. Los objetos se instancian usando llaves (`{}`).

```javascript
const nuevoObjeto = {};
```

### Pares Clave:Valor (`Key:Value`)

A diferencia de las matrices que tienen elementos valorados en índices, los objetos usan un concepto llamado pares de clave:valor. La clave (_key_) es el identificador y el valor (_value_) es el valor que queremos guardar en esa clave. La sintaxis es "clave: valor". Los objetos pueden contener muchos pares de clave-valor, deben estar separados por una coma (importante: sin punto y coma dentro de un objeto). Las claves son únicas en un objeto, solo puede haber una clave de ese nombre, aunque, varias claves pueden tener el mismo valor. Los valores pueden ser cualquier tipo de dato de Javascript; cadena, número, booleano, matriz, función o incluso otro objeto. En esta demostración crearemos un objeto `usuario`.

```javascript
const usuario = {
  username: 'juan.perez',
  password: 'loremipsumpwd123',
  lovesJavascript: true,
  favoriteNumber: 42,
};
```

### Acceder a los valores

Una vez que tengamos los pares clave-valor, podemos acceder a esos valores llamando al nombre del objeto y la clave. Hay dos formas diferentes de hacer esto, usando puntos o usando corchetes.

Con la notación de puntos podemos llamar al nombre del objeto, un punto y el nombre de la clave. Así como llamamos a la propiedad `.length` en una matriz. La propiedad de longitud es un par de clave-valor.

```javascript
user.lovesJavascript; // true
user.username; // juan.perez
```

La notación de corchetes es como llamar a un elemento en una matriz, aunque con corchetes debemos usar una cadena o número, o una variable que apunte a una cadena o número. Se puede llamar a cada clave envolviéndola con comillas:

```javascript
const passString = 'password';
user['lovesJavascript']; // true
user['username']; // juan.perez
user[passString]; // loremipsumpwd123
```

Generalmente, verás que los corchetes casi siempre se usan con variables.

### Asignación de valores

Asignar valores funciona igual que acceder a ellos. Podemos asignarlos, cuando creamos el objeto, con notación de puntos o con notación de corchetes:

```javascript
const nuevoUsuario = {
  esNuevo: true,
};

const loveJSString = 'lovesJavascript';

nuevoUsuario.username = 'otro.nombre.de.usuario';
nuevoUsuario['password'] = '12345';
nuevoUsuario[loveJSString] = true;
```

## Eliminando propiedades

Si queremos eliminar una propiedad, podemos hacerlo usando la palabra clave `delete`:

```javascript
const nuevoObjeto = {
  eliminarEstaPropiedad: true,
};

delete nuevoObjeto.eliminarEstaPropiedad;
```

Es raro que veamos el uso de la palabra clave `delete`, muchos consideran que la mejor práctica es establecer el valor de una palabra clave en` undefined`. Dependerá de ti cuando llegue el momento.

## Métodos

En los objetos, los valores se pueden establecer en funciones. Las funciones guardadas en un objeto se denominan métodos. Hemos utilizado muchos métodos hasta ahora a lo largo de este curso. `.length`,` .push`, `.pop`, etc., son todos métodos. Podemos establecer una clave para un nombre y el valor para una función. Al igual que otras veces que llamamos métodos, llamaremos a este método usando notación de puntos y paréntesis finales (Nota: podemos llamar a un método con argumentos como lo haríamos con una función normal):

```javascript
const nuevoObjeto = {
  decirHola: function () {
    console.log('Hola a todo el mundo!');
  },
};

nuevoObjeto.decirHola(); //Hola a todo el mundo!
```

## Bucles `for…in`

A veces queremos iterar sobre cada par clave-valor en nuestro objeto. Con las matrices, utilizamos un estándar para el bucle y una variable de número de índice. Los objetos no contienen índices numéricos, por lo que el bucle estándar no funcionará para los objetos. Javascript tiene un segundo tipo de bucle for integrado llamado "_for ... in loop_". Es una sintaxis ligeramente diferente, comienza igual pero entre paréntesis declararemos una variable, la palabra clave `in` y el nombre del objeto. Esto recorrerá cada clave del objeto y finalizará cuando se hayan iterado todas las claves. Podemos usar esta clave, y la notación de corchetes, en nuestro bucle for para acceder al valor asociado con esa clave.

```javascript
const usuario = {
  username: 'juan.perez',
  password: 'loremipsumpwd123',
  lovesJavascript: true,
  favoriteNumber: 42,
};

for (let clave in usuario) {
  console.log(clave);
  console.log(usuario[clave]);
}

// username
// 'juan.perez'
// password
// 'loremipsumpwd123'
// lovesJavascript
// true
// favoriteNumber
// 42
```

## La palabra clave 'this'

Los objetos tienen una palabra clave autorreferencial que se puede aplicar en cada objeto llamado `this`. Cuando se llama dentro de un objeto, se refiere a ese mismo objeto. `this` puede usarse para acceder a otras claves en el mismo objeto, y es especialmente útil en métodos:

```javascript
const usuario = {
  username: 'juan.perez',
  password: 'loremipsumpwd123',
  lovesJavascript: true,
  favoriteNumber: 42,
  decirHola: function () {
    console.log(this.username + ' manda saludos!');
  },
};

usuario.decirHola(); // 'juan.perez manda saludos!'
```

Nota: la palabra clave `this` a veces puede ser uno de los temas más difíciles en Javascript. Lo estamos usando muy básicamente aquí, pero el tema se vuelve mucho más complejo muy pronto.

## Objetos en Javascript

En esta lección aprendimos qué son los Objetos y las muchas formas que existen para acceder a los valores, llamar a los métodos y asignar valores. Muchas de estas técnicas parecían muy familiares, como si las hubiéramos usado en prácticamente todos los aspectos de nuestros aprendizajes hasta ahora. Aquí hay un patrón, eso es porque TODO en Javascript es un Objeto. Las matrices son solo objetos con teclas numéricas, las cadenas son objetos bajo el capó con métodos incorporados, las funciones son en realidad objetos con sus propias propiedades especiales, todo el tiempo de ejecución de Javascript es un objeto (`window` en un navegador o` global` en el Node.js). Cuanto más trabajes con Javascript, más comenzará a tener sentido para ti. Solo recuerda, todo es un objeto.

## Callbacks

Un concepto muy importante en Javascript es la capacidad de pasar una función como argumento a otra función. Estas funciones se denominan `callbacks`. Estas funciones pueden llamarse en cualquier momento y pasar argumentos dentro de la función. Pronto descubriremos por qué las devoluciones de llamada son tan importantes para Javascript. La convención es usar `cb` como argumento para la variable que se usará de callback.

```javascript
function decirHolaAlUsuario(usuario) {
  return 'Hola ' + usuario + '!';
}

function decirAdiosAlUsuario(usuario) {
  return 'Adiós ' + usuario + '!';
}

function crearSaludo(usuario, cb) {
  return cb(usuario);
}

crearSaludo('Dan', decirHolaAlUsuario); // 'Hello Dan!'
crearSaludo('Dan', decirAdiosAlUsuario); // 'Goodbye Dan!'
```

## Más métodos de Arrays

Ya conocemos y utilizamos métodos de matriz, `.push`,` .pop`, `.shift`,` .unshift` y `.length`. Pero hay muchos más métodos disponibles de forma nativa en un array. Los métodos de los que vamos a hablar aquí se denominan "métodos de orden superior", porque toman los callbacks como argumentos.

### `.forEach`

`.forEach` es un bucle for integrado en cada array. `.forEach` toma un callback como su único argumento, e itera sobre cada elemento de la matriz y llama al callback en él. El callback puede tomar dos argumentos, el primero es el elemento en sí, el segundo es el índice del elemento (este argumento es opcional).

```javascript
const autos = ['Ford', 'Chevrolet', 'Toyota', 'Tesla'];

// Podemos escribir el callback en los paréntesis como una función anónima
autos.forEach(function (elemento, indice) {
  console.log(elemento);
});

// O podemos crear una instancia de una función para usarla como callback.
// Además, no necesitamos usar el argumento de índice, si no lo necesitas, no dudes en omitirlo.
function mostrarNombres(elemento) {
  console.log(elemento);
}

// And call that function in the forEach parentheses
autos.forEach(mostrarNombres);
```

### `.reduce`

`.reduce` ejecutará un bucle en nuestra matriz con la intención de reducir cada elemento en un elemento que se devuelve. Como es el primer argumento, acepta un callback que toma dos argumentos, primero un 'acumulador' (el resultado del método de reducción hasta ahora), y el segundo es el elemento en el que se encuentra actualmente. El callback debe contener siempre una declaración de devolución ("return"). `.reduce` también toma un segundo argumento opcional, que sería el acumulador de arranque ("starting accumulator"). Si no se suministra el acumulador de arranque, la reducción comenzará en el primer elemento de la matriz. `.reduce` siempre devolverá el acumulador cuando termine de recorrer los elementos.

```javascript
const numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const palabras = ['Hola,', 'mi', 'nombre', 'es', 'Martin'];

// Podemos escribir la función anónima directamente en los paréntesis de .reduce
// Si omitimos el elemento inicial, siempre comenzará en el primer elemento.
const suma = numeros.reduce(function (acc, elemento) {
  return acc + elemento;
});

// Podemos escribir una función fuera de los parents de .reduce (para usar varias veces más tarde)
function multiplicarDosNumeros(a, b) {
  return a * b;
}

const productos = numeros.reduce(multiplicarDosNumeros);

// .reduce funciona en cualquier tipo de datos.
// En este ejemplo configuramos un acumulador de arranque
const frases = palabras.reduce(function (acc, elemento) {
  return acc + ' ' + elemento;
}, 'Frase completa:');

console.log(suma); // 45
console.log(productos); // 362880
console.log(frases); // "Frase completa: Hola, mi nombre es Martin"
```

### `.map`

`.map` se usa cuando queremos cambiar cada elemento de una matriz de la misma manera. `.map` toma una devolución de llamada como único argumento. Al igual que el método `.forEach`, el callback tiene el elemento y el índice de argumentos opcionales. A diferencia de `.reduce`,` .map` devolverá toda la matriz.

```javascript
const numeros = [2, 3, 4, 5];

function multiplicarPorTres(elemento) {
  return elemento * 3;
}

const doble = numeros.map(function (elemento) {
  return elemento * 2;
});

const triple = numeros.map(multiplicarPorTres);

console.log(doble); // [ 4, 6, 8, 10 ]
console.log(triple); // [ 6, 9, 12, 15 ]
```

### `.filter`

Como **`map`**, **`.filter`** recorre el array con un callback, pero sólo arma un **nuevo array** con los elementos para los cuales el callback devuelve un valor **truthy**. **`forEach`** no devuelve nada; **`filter`** sí devuelve otra colección sin modificar la original si no la tocas vos.

```javascript
const puntajes = [8, 3, 10, -1];

const aprueba = puntajes.filter(function (n) {
  return n >= 7;
}); // [8, 10]

const negativos = puntajes.filter((n) => n < 0); // [-1] — ejemplo con flecha abreviada
```

Si el callback devolviera la condición equivocada, podrías obtener un array vacío. Usá **`return`** dentro del callback (salvo función flecha con retorno implícito en una sola expresión, como **`(n) => n < 0`**).

### Búsqueda y formas de texto: `.includes`, `.indexOf`, `.lastIndexOf`, `.join`

- **`.includes(item)`**: devuelve **`true`** o **`false`** según exista ese valor por igualdad **`===`** (útil antes de hacer operaciones pesadas por índice).
- **`.indexOf(item)`**: primera posición del ítem o **`-1`** si no está.
- **`.lastIndexOf(item)`**: última ocurrencia o **`-1`**.
- **`.join(separador)`**: concatena cada elemento como string usando el separador (por ejemplo un espacio o **`|`**). No modifica el array.

```javascript
const cosas = ['a', 'b', 'c', 'a'];
cosas.includes('x'); // false
cosas.indexOf('a'); // 0
cosas.lastIndexOf('a'); // 3
['uno', 'dos'].join(' → '); // 'uno → dos'
```

### Copiar un tramo sin mutar: `.slice`; unir arrays: `.concat`

- **`.slice(inicio, fin)`**: devuelve un **array nuevo**. El segundo índice **no se incluye** (igual que con strings). Si omitís **`fin`,** va hasta el final. **El array original no se modifica.**

```javascript
const base = ['x', 'y', 'z', 'w'];
const trozo = base.slice(1, 3); // ['y', 'z'] — base intacto
```

- **`.concat(otroArray)`**: devuelve un **nuevo** array con los elementos de ambos concatenados sin mutar los originales (también acepta elementos sueltos separados por coma si hace falta).

```javascript
const a = [1, 2];
const b = [3];
a.concat(b); // [1, 2, 3]; a sigue siendo [1, 2]
```

### Mutar posiciones con `.splice`; invertir `.reverse`; orden `.sort`

- **`.splice(inicio, cantidadEliminar, ...elementosParaInsertar)`**: **transforma el mismo array** y devuelve un array con los elementos eliminados. Es útil para recortar o insertar al medio cuando la consigna pide ese método nativo.

```javascript
const nums = [1, 4, 5];
nums.splice(1, 2, 'nuevo'); // devuelve [4, 5]; nums === [1, 'nuevo']
```

- **`.reverse()`**: invierte **en lugar** la lista y devuelve la misma referencia.

- **`.sort(comparador)`**: sin función, Javascript ordena **como texto** (no sirve bien para números). Para orden numérico ascendente desde el menor al mayor usamos:

```javascript
const mezclados = [9, -2, 0, 300];
mezclados.sort(function (a, b) {
  return a - b;
});
// [-2, 0, 9, 300] — ¡ojo! mutaste mezclados
```

Versión corta (**flechas** más abajo): **`arr.sort((a, b) => a - b)`**.

### Funciones flecha (`=>`) y nombre interno en expresiones

Una **función flecha** es sintaxis corta cuando el cuerpo es una sola expresión o necesitamos heredar **`this`** del contexto léxico donde se declaró:

```javascript
const duplicar = (num) => num * 2; // retorno implícito si el cuerpo es una sola expresión

const mitad = (n) => {
  return n / 2; // con llaves necesitás `return` explícito
};
```

En **métodos** de objeto escritos como **`metodo() { … }`**, una flecha definida dentro puede usar **`this`** de ese método (no el `this` externo equivocado típico de una flecha puesta como propiedad literal suelta sobre el objeto — ahí **`this`** no apunta al objeto).

Una **función por expresión con nombre interno** asignás con **`const`** (no tiene “hoisting” de cuerpo completo igual que **`function`** al inicio):

```javascript
const sumar = function sumDos(a, b) {
  return a + b;
};
```

El nombre **`sumDos`** sirve sobre todo para stacks de errores y recursión; desde afuera se llama **`sumar`**.

Con **`var sumar = …` más arriba** un **`typeof sumar`** previo sí puede comportarse distinto (área temporal de **`let`**/**`const`** frente al hoist de **`var`**); ese es el punto del ejercicio de constante **`resultadoTipoFuncionExpresadaVar`** frente al comentario en **`homework.js`**.

### `Object.groupBy` (Node 22+)

**`Object.groupBy(listaArray, clasificadora)`** (ES2024) devuelve un **objeto** cuyas claves son valores retornados por la función clasificadora y cuyos valores son **arrays de elementos** del grupo:

```javascript
const ventas = [
  { ciudad: 'ros', valor: 10 },
  { ciudad: 'mdp', valor: 5 },
  { ciudad: 'ros', valor: 3 },
];

const porCiudad = Object.groupBy(ventas, function (item) {
  return item.ciudad;
});
// { ros: [{…}, {…}], mdp: [{…}] }

const porTipo = Object.groupBy(ventas, (item) => item.ciudad === 'ros'); // ejemplo clave Boolean
```

Este repo exige runtime **≥ Node 22** para esa API (véase **`package.json`**). Si algunos estudiantes usan Node más viejo, fallará sólo ese ejercicio hasta actualizar motor.

### Patrón: encadenamiento sin callbacks anidados

En lugar de **f(f(f(x)))`** escrito a mano, podés recolectar todas las funciones en un **`[]`** y en un **`for`** clásico acumular el resultado llamando **`siguiente(resultadoTemporal)`**. Así **`encadenarOperacionesSinAnidar`** muestra cómo evitar pisar código con niveles ilegibles cuando todo es síncrono (no reemplaza al patrón `async`/Promises cuando haya asíncronos reales).

## Recursos adicionales

- [Understanding Callback Functions and How to Use Them](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/)
- [Eloquent Javascript: Higher Order Functions](https://eloquentjavascript.net/05_higher_order.html)
- [MDN: Callback function](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)
- [MDN: Array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [MDN: this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [MDN: for...in Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
- [MDN: Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN: for Loops](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)
- [MDN (es): `.filter`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [MDN (es): `.join`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/join)
- [MDN (es): `.slice`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- [MDN (es): `.splice`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- [MDN (es): función flecha](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [MDN (es): `Object.groupBy`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Object/groupBy)
