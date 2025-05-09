#apuntes #react 
___

>[!tip] En resumen `useEffext` realiza acciones que no tienen que ver con la UI y `useLayoutEffect` realiza las que si tienen relación con la UI

|              | useEffect                                                                                                                     | useLayoutEffect                                                                                                                                                                                        |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| __Timing__   | Runs **asynchronously** _after_ the render is committed to the screen (after paint).                                          | Runs **synchronously** _after_ all DOM mutations but **before the browser repaints the screen**.                                                                                                       |
| __Use case__ | For most side effects like **data fetching, subscriptions, logging**, or **event listeners** that do not affect layout.       | When you need to **read layout from the DOM** and **synchronously re-render** (e.g., measure element dimensions, scroll position, or make DOM updates that must be visible before the browser paints). |
| __Behavior__ | Non-blocking. The browser paints the UI before running the effect, which is generally what you want for smoother performance. | Blocks the browser from painting until the effect runs and finishes. This can lead to performance issues if overused.                                                                                  |
