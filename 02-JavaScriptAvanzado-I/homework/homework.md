# Homework JavaScript Avanzado I

## Scope & Hoisting

Determiná que será impreso en la consola, sin ejecutar el código.

> Investiga cuál es la diferencia entre declarar una variable con `var` y directamente asignarle un valor.

```javascript
x = 1;
var a = 5;
var b = 10;
var c = function (a, b, c) {
  var x = 10;
  console.log(x); // 10
  console.log(a); // 8
  var f = function (a, b, c) {
    b = a;
    console.log(b); // 8
    b = c;
    var x = 5;
  };
  f(a, b, c);
  console.log(b); // 9
};
c(8, 9, 10);
console.log(b); // 10
console.log(x); // 1
```

```javascript
console.log(bar); // undefined
console.log(baz); // baz is not defined
foo();
function foo() {
  console.log("Hola!"); // 'Hola!' (aunque esta linea no llega a ejecutarse, por el error de la línea 33)
}
var bar = 1;
baz = 2;
```

```javascript
var instructor = "Tony";
if (true) {
  var instructor = "Franco";
}
console.log(instructor); // 'Franco'
```

```javascript
var instructor = "Tony";
console.log(instructor); // 'Tony'
(function () {
  if (true) {
    var instructor = "Franco";
    console.log(instructor); // 'Franco'
  }
})();
console.log(instructor); // 'Tony'
```

```javascript
var instructor = "Tony";
let pm = "Franco";
if (true) {
  var instructor = "The Flash";
  let pm = "Reverse Flash";
  console.log(instructor); // 'The Flash'
  console.log(pm); // 'Reverse Flash'
}
console.log(instructor); // 'The Flash'
console.log(pm); // 'Franco'
```

### Coerción de Datos

¿Cuál crees que será el resultado de la ejecución de estas operaciones?:

```javascript
6 / "3"; // 2
"2" * "3"; // 6
4 + 5 + "px"; // '9px'
"$" + 4 + 5; // '$45'
"4" - 2; // 2
"4px" - 2; // NaN
7 / 0; // Infinity
{
}
[0]; // [0]
parseInt("09"); // 9
5 && 2; // 2
2 && 5; // 5
5 || 0; // 5
0 ||
  (5)[3] + // 5
    [3] -
    [10]; // 23
3 >
  2 > // false
  [] ==
  ![]; // true
```

> Si te quedó alguna duda repasá con [este artículo](http://javascript.info/tutorial/object-conversion).

### Hoisting

¿Cuál es el output o salida en consola luego de ejecutar este código? Explicar por qué:

```javascript
function test() {
  console.log(a); // undefined | En la linea 106 tiene la ejecución del console.log(a), y 'a' existe por la linea 109 mediante Hoisting, pero no puede acceder al valor = 1, por lo tanto es 'undefined'.
  console.log(foo()); // 2 | ejecuta la funcion 'foo()', esta retorna el valor 2, por lo tanto la linea 107 hace un console.log(2).

  var a = 1;
  function foo() {
    return 2;
  }
}

test();
```

Y el de este código? :

```javascript
var snack = "Meow Mix";

function getFood(food) {
  if (food) {
    var snack = "Friskies";
    return snack;
  }
  return snack;
}

console.log(getFood(false)); // undefined | en la funcion getFood(), se reconoce a la variable snack mediante hoisting, por lo que ya tiene un valor undefined. Dado que la evaluacion del if da false, snack devuelve su valoren la línea 128, y sigue siendo undefined.
```

### This

¿Cuál es el output o salida en consola luego de ejecutar esté código? Explicar por qué:

```javascript
var fullname = "Juan Perez";
var obj = {
  fullname: "Natalia Nerea",
  prop: {
    fullname: "Aurelio De Rosa",
    getFullname: function () {
      return this.fullname;
    },
  },
};

console.log(obj.prop.getFullname()); // 'Aurelio de Rosa' | 'obj' aplica la propiedad 'prop', que a su vez prop es otro objeto que aplica el método 'getFullname' y lo invoca. Esto es la línea 145, que retorna 'this.fullname', y this hace referencia al contexto del objeto 'prop', por lo tanto fullname es 'Aurelio De Rosa'

var test = obj.prop.getFullname;

console.log(test()); // 'Juan Perez' | 'test()' hace el mismo recorrido que el console.log() anterior, pero como 'test' se encuentra en el contexto global, 'this hace referencia al objeto global, y el valor de 'fullname' del objeto global, es 'Juan Perez'
```

### Event loop

Considerando el siguiente código, ¿Cuál sería el orden en el que se muestra por consola? ¿Por qué?

```javascript
function printing() {
  console.log(1); // 1°
  setTimeout(function () {
    console.log(2); // 4°
  }, 1000);
  setTimeout(function () {
    console.log(3); // 3°
  }, 0);
  console.log(4); // 2°
}

printing(); // primero se imprime la línea 163, las líneas 165 y 167 se ponen en espera, segundo imprime la línea 170. Las líneas que no fueron impresas, han tenido demoras, y como JavaScript es sincrónico, espera que se resuelvan de manera externa para recibir el resultado. El setTimeout de la línea 167 tiene una demora de 0, por lo que se retornara y se imprime en 3er lugar, y por último cuando se cumpla la demora de 1000 de la línea 165, se imprime en 4to lugar.
```

</br >

---

## **✅ FEEDBACK**

### Usa este [**formulario**](https://docs.google.com/forms/d/e/1FAIpQLSe1MybH_Y-xcp1RP0jKPLndLdJYg8cwyHkSb9MwSrEjoxyzWg/viewform) para reportar tus observaciones de mejora o errores. Tu feedback es muy importante para seguir mejorando el modelo educativo.
