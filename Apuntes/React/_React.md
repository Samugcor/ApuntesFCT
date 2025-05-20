---
aliases:
  - React
  - Apuntes React
---
#apuntes #react 
___
# ¿Qué es React?

**React es una biblioteca front-end de JavaScript** de código abierto cuyo objetivo es simplificar la creación de interfaces de usuario basadas en componentes.

React puede utilizarse para desarrollar aplicaciones de página única, móviles o renderizadas en servidor con frameworks como [[Next.js]] y [[Remix]]. Dado que **React solo se ocupa de la interfaz de usuario y de renderizar componentes en el DOM**, las aplicaciones React suelen depender de bibliotecas para el enrutamiento y otras funciones del lado del cliente. Una ventaja clave es que **React solo renderiza las partes de la página que han cambiado, evitando la renderización innecesaria de elementos del DOM sin cambios.**

**React te permite construir interfaces de usuario a partir de piezas individuales llamadas componentes que luego puedes combinar para formar pantallas, páginas y aplicaciones.**


# ¿Cómo funciona?

**Los componentes de React son funciones de JavaScript,** por lo que puedes usar todas las herramientas del lenguaje, como sentencias `if` o funciones como `map()` en un array. Lo que devuelva la función serán los elementos HTML que forman ese componente.

**Ej1:**
```js
function Video({ video }) {  
	return (  
		<div>  
			<Thumbnail video={video} />  
			<a href={video.url}>  
				<h3>{video.title}</h3>  
				<p>{video.description}</p>  
			</a>  
			<LikeButton video={video} />  
		</div>  
	);  
}
```

**Ej2:**
```js
function VideoList({ videos, emptyHeading }) {  

	const count = videos.length;  
	let heading = emptyHeading;  
	
	if (count > 0) {  
		const noun = count > 1 ? 'Videos' : 'Video';  
		heading = count + ' ' + noun;  
	}  
	
	return (  
		<section>  
			<h2>{heading}</h2>  
			{videos.map(video =>  
				<Video key={video.id} video={video} />  
			)}  
		</section>  
	);  
}
```

# Inicio rápido

```cardlink
url: https://es.react.dev/learn
title: "Inicio rápido – React"
description: "The library for web and native user interfaces"
host: es.react.dev
favicon: https://es.react.dev/favicon-32x32.png
image: https://es.react.dev/images/og-learn.png
```
> **Contenido:**
>    - [[#Cómo crear y anidar componentes]]
>    - [[#Cómo añadir estilos]]
>    - [[#Cómo mostrar datos]]
>    - [[#Cómo renderizar condicionales y listas]]
>    - [[#Cómo responder a eventos y actualizar la pantalla]]
>    - [[#Cómo compartir datos entre componentes]]

## Cómo crear y anidar componentes

Las aplicaciones de React están hechas a partir de __componentes__. Un componente es una pieza de UI que tiene su propia lógica y apariencia. Un componente puede ser tan pequeño como un botón, o tan grande como toda una página.

Los componentes de React son funciones de JavaScript que devuelven __markup__ (marcado) en sintaxis [[JSX]]:
```js
function MyButton() {  
	return (  
		<button>Soy un botón</button>  
	);  
}
```

Estos componentes luego pueden ser utilizados dentro de otros componentes:
```js
export default function MyApp() {  
	return (  
		<div>  
			<h1>Bienvenido a mi aplicación</h1>  
			<MyButton />  
		</div>  
	);  
}
```

>[!tip] Los componentes creados empiezan por Mayúscula: `<MyButton />`. a diferencia de las etiquetas HTML `<div>`

## Cómo añadir estilos

En React, especificas una clase de CSS con `className`. Funciona de la misma forma que el atributo `class` de HTML:
```
<img className="avatar" />
```

Luego escribes las reglas CSS para esa clase en un archivo CSS aparte. React no prescribe como debes añadir tus archivos CSS. En el caso más simple, añades una etiqueta `<link>` a tu HTML. Si utilizas una herramienta de construcción o un framework, consulta su documentación para saber como añadir un archivo CSS a tu proyecto.

## Cómo mostrar datos

Mediante [[JSX]] puedes utilizar expresiones de Java, lo que te permite acceder a las variables desde el DOM.
```jsx
return (  
	<h1>  
		{'Nombre' + user.name}  
	</h1>  
);
```

## Cómo renderizar condicionales y listas
### Condicionales
En React, no hay una sintaxis especial para escribir condicionales. En cambio, usarás las mismas técnicas que usas al escribir código regular de JavaScript. 
```js
let content;
if (isLoggedIn) {
	content = <AdminPanel />;
} else { 
	content = <LoginForm />;
}
return (  
	<div>{content}</div>
);
```

### Listas
Dependerás de funcionalidades de JavaScript como los bucles `for`y la función map() de los _array_ para renderizar listas de componentes.

Por ejemplo, digamos que tienes un array de productos:
```js
const products = [  { title: 'Col', id: 1 },  { title: 'Ajo', id: 2 },  { title: 'Manzana', id: 3 },];
```

Dentro de tu componente, utiliza la función `map()` para transformar el array de productos en un array de elementos `<li>`:
```js
const listItems = products.map(product =>  
	<li key={product.id}>
	    {product.title}  
	</li>
);
return (  
	<ul>{listItems}</ul>
);
```

Nota que `<li>` tiene un atributo `key` (llave). Para cada elemento en una lista, debes pasar una cadena o un número que identifique ese elemento de forma única entre sus hermanos. Usualmente, una llave debe provenir de tus datos, como un ID de una base de datos. React dependerá de tus llaves para entender qué ha ocurrido si luego insertas, eliminas o reordenas los elementos.

## Cómo responder a eventos y actualizar la pantalla

Puedes responder a eventos declarando funciones _controladoras de eventos_ dentro de tus componentes:

```js
function MyButton() {  
	function handleClick() { 
	   alert('¡Me hiciste clic!');
	}  
	return (
		<button onClick={handleClick}>
		      Hazme clic    
		</button>  
	);
}
```

>[!tip] ¡Nota que `onClick={handleClick}` no tiene paréntesis al final! No _llames_ a la función controladora de evento: solamente necesitas _pasarla hacia abajo_. React llamará a tu controlador de evento cuando el usuario haga clic en el botón.

A menudo, querrás que tu componente “recuerde” alguna información y la muestre. Por ejemplo, quizá quieras contar el número de veces que hiciste clic en un botón. Para lograrlo, añade _estado_ a tu componente.

Primero, importa [`useState`](https://es.react.dev/reference/react/useState) de React:

```js
import { useState } from 'react';
```

Ahora puedes declarar una _variable de estado_ dentro de tu componente:

```js
function MyButton() {  const [count, setCount] = useState(0);  // ...
```

Obtendrás dos cosas de `useState`: el estado actual (`count`), y la función que te permite actualizarlo (`setCount`). Puedes nombrarlos de cualquier forma, pero la convención es llamarlos algo como `[something, setSomething]`.

```js
function MyButton() {  
	const [count, setCount] = useState(0);  
	
	function handleClick() {  
		setCount(count + 1);  
	}  
	
	return (  
		<button onClick={handleClick}>  
			Hiciste clic {count} veces  
		</button>  
	);  
}
```

