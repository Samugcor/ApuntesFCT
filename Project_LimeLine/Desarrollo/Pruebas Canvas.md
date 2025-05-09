---
tags:
  - limeline
  - desarrollo
fechainicio: 2025-05-03
fechafin: 2025-05-05
fase: pruebas
horasdedicadas: "10"
dirproject:
  - D:\LimeLine\Pruebas_Canvas
---
___

>[!note] Summary:
> Simplemente hacemos pruebas para familiarizarnos un poco con los conceptos básicos
>
# Context:

**Queremos que el espacio** donde se renderizan nuestras líneas temporales **pueda ser modificado fácilmente por el usuario**, ya sea moviéndose por el espacio y haciendo zoom o añadiendo elementos como notas. Parece que la herramienta más apropiada para esto sería el **Canvas de HTML**

# Recursos:

```cardlink
url: https://youtube.com/playlist?list=PLpPnRKq7eNW3We9VdCfx9fprhqXHwTPXL&si=czN8tJ-at0-tk3g7
title: "HTML5 Canvas Tutorials for Beginners | Become a Canvas Pro 📋"
description: "Want to learn everything you need to know to become an HTML canvas pro? Hop on my back and I'll carry you through the canvas training pit all the way to gene..."
host: youtube.com
favicon: https://www.youtube.com/s/desktop/3747f4fc/img/logos/favicon_32x32.png
image: https://i.ytimg.com/vi/EO6OkltgudE/hqdefault.jpg?sqp=-oaymwEXCOADEI4CSFryq4qpAwkIARUAAIhCGAE=&rs=AOn4CLADvxe-2vWUGzjF2FSrtkdDnWs2XQ&days_since_epoch=20212
```
>**Contents:**
>- Creating and Resizing your Canvas
>- Drawing elements
>- Animating elements
>- Interacting with elements

```cardlink
url: https://www.youtube.com/watch?v=uCH1ta5OUHw&ab_channel=Frankslaboratory
title: "HTML Canvas DEEP DIVE"
description: "Creating beautiful interactive animations for the web can be easy. HTML canvas allows dynamic scriptable rendering of 2D shapes and bitmap images and we can ..."
host: www.youtube.com
favicon: https://www.youtube.com/s/desktop/3747f4fc/img/logos/favicon_32x32.png
image: https://i.ytimg.com/vi/uCH1ta5OUHw/maxresdefault.jpg
```

# Notas:
## Tamaño del Canvas

El tamaño del canvas es mejor ajustarlo mediante JS, ya que hacerlo mediante CSS nos va a estar dando problemas con las unidades de altura.

```js
let canvas = document.querySelector('canvas');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

## Círculos que se mueven y rebotan 
```js
let canvas = document.querySelector('canvas');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
  
let c = canvas.getContext('2d')

function Circulo(x,y,radious,color,dx,dy,velocity) {

    this.x = x;
    this.y = y;
    this.radious = radious;
    this.color = color;
    this.dx = dx;
    this.dy = dy;
    this.velocity = velocity;

    this.draw = function(){

        c.beginPath();
        c.arc(this.x, this.y, this.radious, 0, Math.PI * 2, false);
        c.strokeStyle = this.color;
        c.fillStyle = this.color;
        c.fill()
        c.stroke();

    }
  
    this.update = function(){

        if (this.x >window.innerWidth-this.radious || this.x-this.radious<0) {
            this.dx=-this.dx;
        }

        if (this.y>window.innerHeight-this.radious || this.y-this.radious<0) {
            this.dy=-this.dy;
        }

        this.x += this.dx * this.velocity;
        this.y += this.dy * this.velocity;

        this.draw();

    }
}

  

function animate(){

    requestAnimationFrame(animate);
    
    c.clearRect(0,0,canvas.width,canvas.height);

    for (let i = 0; i < circleArray.length; i++) {
        circleArray[i].update();
    }
}

let circleArray=[];

for (let i = 0; i < 50; i++) {

    //Queremos que el radio sea entre 10 y 50
    let radious = Math.floor((Math.random() * 40) + 10);
    
    //Queremos que la posición esté entre radio y canvas.width - radio
    let x = Math.floor((Math.random() * (canvas.width - radious * 2)) + radious) ;
    let y = Math.floor((Math.random() * (canvas.height - radious * 2)) + radious);

    //La dirección tiene que ser -1 o 1
    let dx = Math.round(Math.random()) * 2 - 1;
    let dy = Math.round(Math.random()) * 2 - 1;

    //La velocidad debería ser entre 0.5 y 1.5
    let velocity = Math.random() + 0.5;
    
    let color = '#'+(Math.random() * 0xFFFFFF << 0).toString(16).padStart(6, '0');

    circleArray.push(new Circulo(x,y,radious,color,dx,dy,velocity))
}

animate()
```

## Reaccionando a eventos

Para esto necesitamos [[Event listener]], cuando trabajamos con Canvas estos se crean con la sintaxis:
`window.addEventListener('eventname', function)`. Los eventos pueden devolver parámetros a la función, normalmente anónima.

### Posición del mouse

A través de escuchar (event listener) al movimiento del ratón podremos sacar las coordenadas del mismo y guardarlas en un objeto Js que nos servirá como vector.

```js
let mouse = {x:undefined,y:undefined}

window.addEventListener('mousemove',function (event) {

    mouse.x=event.x;
    mouse.y=event.y;

})
```
