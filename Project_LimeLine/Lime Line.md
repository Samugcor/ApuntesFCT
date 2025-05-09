___
**Lime Line** es una aplicación web para crear líneas de tiempo y mostrarlas de forma gráfica.

El objetivo es facilitar la creación y visualización de esquemas del tipo línea temporal, donde se representa un espacio temporal en forma de línea y se marcan con puntos sobre la misma los eventos que han tenido lugar, mediante una interfaz gráfica sencilla.

## Funcionalidades:

- Crear una línea de tiempo
- Mostrar graficamente la línea temporal en un entorno Canvas que permita una visualización más detallada.
- Eliminar línea de tiempo 
- Añadir evento
- Modificar evento
- Eliminar evento
- Agregar notas
- Modificar notas
- Eliminar notas
- Descargar imagen
- Descargar datos de la línea de tiempo en JSON
- Descargar datos de la línea de tiempo en MD

## Desarrollo

En este apartado se irá documentando las distintas fases del desarrollo, cada entrada contará con su propia nota detallando: **tema (nombre), día, fase y que se ha hecho**.

```dataview
TABLE fechainicio AS "📆Fecha", horasdedicadas AS "🕑Horas", fase AS "Fase" 
FROM #desarrollo AND #limeline 
```
