#apuntes #js
___

Es una forma de coger solo los atributos que nos interesan de un objeto y guardarlos en variables para su posterior uso.

```js
const { clientX, clientY } = event;
```

This means:

> “Take the `clientX` and `clientY` properties **from the `event` object** and create **two new constants** named `clientX` and `clientY` that hold those values.”

If you wanted to give them different names, you can do:
```js
const { clientX: x, clientY: y } = event; 
console.log(x, y);
```