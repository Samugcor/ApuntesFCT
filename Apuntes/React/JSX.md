#apuntes #react 
___
# ¿Qué es?

JSX (JavaScript XML), formalmente JavaScript Syntax eXtension, **es una extensión de JavaScript que permite la creación de árboles DOM** usando una sintaxis similar a XML. La mayoría de los proyectos de React usan JSX ya que fue diseñado para este y ofrece una mayor comodidad al permitir integrar expresiones de Js en medio. 

**Las expresiones de JavaScript (pero no las sentencias) pueden ser usadas dentro de JSX colocándolas dentro de llaves:**
```jsx
<h1>{10+1}</h1>
```

Las **expresiones condicionales** pueden usarse en su forma ternaria:
```jsx
const App = () => {
   const i = 1;
   
   return (
     <div>
       <h1>{ i === 1 ? 'true' : 'false' }</h1>
     </div>
   );
}
```