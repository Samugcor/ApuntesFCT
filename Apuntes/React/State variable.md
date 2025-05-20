#apuntes #react 
___
# Índice

1. [[#¿Qué es?]]
2. [[#Escogiendo la estructura de la variable de Estado]]
	- [[#Agrupar estados relacionados.]]
	- 
___
# ¿Qué es?

En React, una variable de estado (state variable) son datos que un componente puede rastrear y a los que puede reaccionar cuando cambian. El concepto es parecido al de [[MutableLiveData]] en Android.

Para usarlo debemos primero importar `useState`:
```jsx
import { useState } from 'react';
```

Luego podemos usarlo dentro de nuestro componente como: `const [count, setCount] = useState(0);`

>[!tip] Ten en cuenta que puedes nombrarlos de cualquier forma, pero la convención es llamarlos algo como `[something, setSomething]`.

__Ej1:__ Guarda el numero de cliks sobre un botón
```jsx
function Counter() {
  const [count, setCount] = useState(0); // count starts at 0

  return (
    <button onClick={() => setCount(count + 1)}>
      You clicked {count} times
    </button>
  );
}
```

__La cosa se irá complicando cuando estado en un componente deba ser compartido con otro__, y quizás este otro pueda cambiar ese estado o cosas así. Por ejemplo, si en una aplicación de dibujo tenemos un componente App con un estado que guarda la herramienta seleccionada y un componente Menu donde se encuentran los botones que deberían cambiar dicho estado. 

Para facilitarnos las cosas a futuro es muy importante elegir una correcta estructura y el método adecuado para compartir la información.

# Escogiendo la estructura de la variable de Estado

```cardlink
url: https://react.dev/learn/choosing-the-state-structure
title: "Choosing the State Structure – React"
description: "The library for web and native user interfaces"
host: react.dev
favicon: https://react.dev/favicon-32x32.png
image: https://react.dev/images/og-learn.png
```

Al escribir un componente que contiene un estado, deberá decidir cuántas variables de estado usar y cuál debe ser la forma de sus datos:

- __Agrupar estados relacionados.__ Si siempre actualiza dos o más variables de estado al mismo tiempo, considere fusionarlas en una sola variable de estado.
- __Evite contradicciones en el estado.__ Cuando el estado está estructurado de tal manera que varias partes del mismo pueden contradecirse y discrepar entre sí, se deja margen para errores. Intente evitarlo.
- __Evite estados redundantes.__ Si puede calcular información a partir de las propiedades del componente o de sus variables de estado existentes durante la renderización, no debe incluir esa información en el estado de ese componente.
- __Evite la duplicación en el estado.__ Cuando los mismos datos se duplican entre múltiples variables de estado o dentro de objetos anidados, es difícil mantenerlos sincronizados. Reduzca la duplicación siempre que sea posible.
- __Evite estados muy anidados.__ Un estado muy jerárquico no es muy fácil de actualizar. Siempre que sea posible, es preferible estructurarlo de forma plana.


## Agrupar estados relacionados

```
const [x, setX] = useState(0);const [y, setY] = useState(0);
```

```
const [position, setPosition] = useState({ x: 0, y: 0 });
```

Técnicamente, se puede usar cualquiera de estos enfoques. Pero **si dos variables de estado siempre cambian juntas, podría ser buena idea unificarlas en una sola variable de estado.**

Otro caso en el que se agrupan los datos en un objeto o una matriz es cuando no se sabe cuántos fragmentos de estado se necesitarán. Por ejemplo, es útil cuando se tiene un formulario donde el usuario puede agregar campos personalizados.

>[!warning] 
>Si tu variable de estado es un objeto, recuerda que no puedes actualizar solo un campo sin copiar explícitamente los demás. Por ejemplo, no puedes usar `setPosition({ x: 100 })` en el ejemplo anterior porque no tendría la propiedad `y`. En cambio, si quisieras establecer solo `x`, usarías s`etPosition({ ...position, x: 100 })`.

## Evitar contradicciones

Ponemos por ejemplo un formulario de comentarios de un hotel con las variables de estado `isSending` e `isSent`, __esta combinación deja abierta la posibilidad de estados "imposibles".__ Por ejemplo, si se te olvida llamar a `setIsSent` y `setIsSending` juntos, podría terminar en una situación en la que `isSending` e `isSent` sean true al mismo tiempo. Cuanto más complejo sea el componente, más difícil será comprender qué sucedió.

Dado que `isSending` e `isSent` nunca deben ser `true` al mismo tiempo, es mejor reemplazarlas con una variable de estado `status` que puede tomar uno de _tres_ estados válidos: `'typing'` (inicial), `'sending'` y `'sent'.

## Evitar estados redundantes

Si puede calcular alguna información de las propiedades del componente, no  se debe colocar esa información en una variable de estado. Por ejemplo, si tenemos las variables de estado: `firstName`, `lastName` y `fullName`, esta última sería redundante. Siempre se puede calcular `fullName` a partir de `firstName` y `lastName`.

Aquí, `fullName` no es una variable de estado. Se calcula durante el renderizado:

```jsx
const fullName = firstName + ' ' + lastName;
```

Por lo tanto, los controladores de cambios no necesitan hacer nada especial para actualizarlo. Al llamar a `setFirstName` o `setLastName`, **se activa un nuevo renderizado** y, a continuación, se calcula el siguiente `fullName` a partir de los datos actualizados.

## Evitar duplicaciones en el estado

```jsx
import { useState } from 'react';

const initialItems = [
  { title: 'pretzels', id: 0 },
  { title: 'crispy seaweed', id: 1 },
  { title: 'granola bar', id: 2 },
];

export default function Menu() {
  const [items, setItems] = useState(initialItems);
  const [selectedItem, setSelectedItem] = useState(
    items[0]
  );

  function handleItemChange(id, e) {
    setItems(items.map(item => {
      if (item.id === id) {
        return {
          ...item,
          title: e.target.value,
        };
      } else {
        return item;
      }
    }));
  }

  return (
    <>
      <h2>What's your travel snack?</h2> 
      <ul>
        {items.map((item, index) => (
          <li key={item.id}>
            <input
              value={item.title}
              onChange={e => {
                handleItemChange(item.id, e)
              }}
            />
            {' '}
            <button onClick={() => {
              setSelectedItem(item);
            }}>Choose</button>
          </li>
        ))}
      </ul>
      <p>You picked {selectedItem.title}.</p>
    </>
  );
}
```

Actualmente, almacena el elemento seleccionado como un objeto en la variable de estado `selectedItem`. Sin embargo, esto no está bien: **el contenido de `selectedItem` es el mismo objeto que uno de los elementos de la lista de elementos. Esto significa que la información sobre el elemento se duplica en dos lugares.** **Si los datos del elemento cambian en la lista no cambiarán en `selectedItem`**. Por ello lo mejor es **guardar el id del objeto y realizar una búsqueda de coincidencia en la lista**.

El estado solía duplicarse así:

```jsx
items = [{ id: 0, title: 'pretzels'}, ...]
selectedItem = {id: 0, title: 'pretzels'}
```

Pero después del cambio, queda así:

```jsx
items = [{ id: 0, title: 'pretzels'}, ...]
selectedId = 0
```

**Ahora, si edita el elemento seleccionado, el mensaje a continuación se actualizará inmediatamente. Esto se debe a que `setItems` activa un nuevo renderizado, y `items.find(...) `encuentra el elemento con el título actualizado.**

## Evitar estados muy anidados

Los estados muy anidados son complicados de actualizar y generan problemas, como por ejemplo las [[Shallow copy]]. Para evitarlo lo más sencillo es normalizar los datos. Consulta más infrmación en este [enlace](https://react.dev/learn/choosing-the-state-structure#:~:text=calculated%20during%20render.-,Avoid%20deeply%20nested%20state,-Imagine%20a%20travel)