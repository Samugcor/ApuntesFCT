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