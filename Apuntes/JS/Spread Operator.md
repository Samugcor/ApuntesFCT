#apuntes #js 
___

Es un operador para los Array  y los Objetos que nos permite recuperar todo su contenido para usarlo de muchas maneras:

Ej1: Copiar Arrays o Objetos
```js
const nums = [1, 2, 3];
const copy = [...nums]; // [1, 2, 3]
```

```js
const user = { name: "Alice", age: 25 };
const copy = { ...user }; // Shallow copy
```

>[!warning] El Spread Operator tiene limitaciones al hacer copias de Objetos, dando lugar a lo que se denomina [[Shallow copy]],.

Ej2: Combinar Arrays o Objetos
```js
const a = [1, 2];
const b = [3, 4];
const combined = [...a, ...b]; // [1, 2, 3, 4]
```

```js
const a = { x: 1, y: 2 };
const b = { y: 3, z: 4 };
const merged = { ...a, ...b };// { x: 1, y: 3, z: 4 }
```

Ej3: Reemplazar o modificar items en un Array
```js
const arr = [1, 2, 3];
const updated = [...arr.slice(0, 1), 99, ...arr.slice(2)];// [1, 99, 3]
```

>[!tip] Este tipo de métodos se usa para algoritmos de ordenación como el [[Quicksort]]

