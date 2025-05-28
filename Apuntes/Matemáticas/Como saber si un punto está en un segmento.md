#apuntes #mates #howto 
___
Hay dos formas de saber si un punto (`p`) está en un segmento (entre `a` y `b`).

# 1. [[Colinealidad]] y Bounding Box

1. Primero miramos si `p` está en la línea que se traza entre `a` y `b`. Esto podemos hacerlo con la [[Colinealidad]].
2. Comprueba que `p.x` está entre `a.x` y `b.x`. 
3. Comprueba que `p.y` está entre `a.y` y `b.y`.

# 2. Comprobar las distancias

La premisa es: **Distance from A to P** + **Distance from P to B** = **Distance from A to B**
Para eso necesitamos:

1. Obtén la distancia entre `a` y `b`.
2. Obtén la distancia entre `a` y `p`.
3. Obtén la distancia entre `p` y `b`.
4. Comprueba que la premisa es cierta.

Para obtener las distancias mira los apuntes de [[Distancia entre dos coordenadas]].
