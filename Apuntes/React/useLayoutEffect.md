#apuntes #react 
___
>[!warning] Es similar a [[useEffect]], para ver cuando usar uno u otro consulta la nota [[useEffect vs useLayoutEffect]]

__`useLayoutEffect`__ es un [[Hook]] de React, una función que da la habilidad a un componente de acceder y leer el layout del DOM. Así podremos acceder a características de los componentes del mismo, por ejemplo: las dimensiones de un elemento, la posición de scroll... .

React llama automáticamente a `useLayoutEffect` después de actualizar el DOM, pero antes de que el navegador muestre nada en la pantalla. 
Los pasos serían:
1. React renderiza el componente (ejecuta JSX y prepara el DOM).
2. Actualiza el DOM real basándose en ese renderizado.
3. `useLayoutEffect` se ejecuta sincrónicamente.
4. Solo después de finalizar, el navegador muestra la pantalla.

Esta función se llama otra vez cuando se renderiza nuevamente el componente.
