#apuntes #conceptos
___

Una Shallow copy (Copia superficial) significa que solo se copian las propiedades de nivel superior, no los objetos ni arrays anidados que contenga. Por lo tanto, si el objeto tiene estructuras anidadas, estas se referencian, pero no se duplican por completo. **Por lo tanto, tanto el original como la copia apuntan al mismo objeto anidado y cualquier modificación sobre el mismo se reflejará en ambos**

Ej1:
```js
const user = {
  name: "Alice",
  age: 25,
  address: {
    city: "New York",
    zip: "10001"
  }
};

const copy = { ...user };

copy.name = "Bob";               // ✅ Changes only copy
copy.address.city = "Chicago";  // ⚠️ Also changes `user.address.city`!

```

Ej2:
```js
const users = [
  { name: "Alice" },
  { name: "Bob" }
];

const copy = [...users];

// Modify a nested object
copy[0].name = "Eve";

console.log(users[0].name); // 🔥 "Eve" — original is also changed!

```