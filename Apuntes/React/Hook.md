#apuntes #react 
___

A **hook** is just a **special function** provided by React that you use **inside functional components** to give them **capabilities they wouldn’t normally have** — like having **state**, responding to **lifecycle events**, or accessing the **DOM**.

Imagine your component is a plain function:

```jsx
function MyComponent() {   
	return <div>Hello</div>; 
}
```

Now you want it to:
- Remember some state (like a counter)
- Do something when it appears on the screen

```jsx
import { useState, useEffect } from 'react';  

function MyComponent() {   
	const [count, setCount] = useState(0); // adds state   
	
	useEffect(() => {     
		console.log('Component mounted or updated'); // adds lifecycle behavior   
	});
	
	return <button onClick={() => setCount(count + 1)}>
			Clicked {count} times
		</button>; 
}
```