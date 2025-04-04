
The idea of the project is to create a tool that generates key points and summaries for Google Meet Meetings using as a base [this](https://github.com/dhruvldrp9/Google-Meet-Bot) repository. We want to prioritize User experience by making it's implementation and use simple.

We also want the rpojevt 
```css

┌──────────────────────────────┐
│         Contenedor Docker         │
│                                  │
│  ┌────────────┐                  │
│  │  Xvfb      │◄─── DISPLAY ─────┼─┐
│  └────────────┘                  │ │
│                                  │ │
│  ┌────────────┐                  │ │
│  │  Chrome    │ ──► Reproduce ───┘ │
│  │ (con Meet) │     audio           │
│  └────────────┘                    │
│                                   │
│  ┌──────────────┐     Captura     │
│  │  PulseAudio  │◄────────────────┘
│  └──────────────┘
│         ▲
│         │ socket
│  ┌──────────────┐
│  │  ffmpeg /    │
│  │  parec       │
│  └──────────────┘
│                                  │
│  ┌──────────────┐                │
│  │  Selenium    │─► controla ───►│
│  └──────────────┘                │
└──────────────────────────────┘
```
## 🔄 FLUJO DE FUNCIONAMIENTO

### 1. 🖥️ **Xvfb: pantalla virtual**

- Actúa como un “monitor ficticio”.
    
- Le dice a Chrome: “Aquí tienes una pantalla donde dibujar cosas”.
    

### 2. 🌐 **Chrome (navegador real con Google Meet)**

- Reproduce el audio de la reunión.
    
- Se lanza con Selenium, usando la pantalla virtual (`DISPLAY=:99`).
    
- Usa PulseAudio para reproducir el sonido dentro del contenedor (no hay parlantes reales).
    

### 3. 🎙️ **PulseAudio: servidor de audio**

- Chrome envía audio hacia PulseAudio (como si lo estuviera reproduciendo en altavoces).
    
- Funge como una “sala de mezcla” virtual.
    
- Permite a otras apps (como ffmpeg) **capturar** ese audio.
    

### 4. 📹 **ffmpeg o parec: capturador**

- Se conecta al servidor PulseAudio.
    
- Escucha lo que Chrome reproduce.
    
- Graba ese audio en `.wav` o `.mp3`.
    

Ejemplo con `ffmpeg`:

bash

CopiarEditar

`ffmpeg -f pulse -i default grabacion.wav`

O con `parec` (herramienta de Pulse):

bash

CopiarEditar

`parec --format=s16le --rate=44100 --channels=2 | sox -t raw -r 44100 -e signed -b 16 -c 2 - grabacion.wav`

### 5. 🧠 **Selenium (Python)**

- Controla Chrome: inicia sesión, acepta permisos, entra a la reunión.
    
- Puede incluso detectar cuándo hay usuarios y cuándo salir.
    
- Ejecuta todo en paralelo con `ffmpeg` para grabar.

> en caso de querer acceder ademas a la API de Google Calendar, para que ese bot se lance las veces que se necesite cada vez que haya una reunión, se necesitaría algo mas?

###### ChatGPT Plus

¡Excelente pregunta! Sí, si quieres que **el bot se ejecute automáticamente cada vez que haya una reunión en Google Calendar**, necesitas agregar un componente de **integración con la API de Google Calendar**. Vamos a verlo paso a paso.

---

## 🎯 OBJETIVO:

Que el bot:

1. Consulte Google Calendar.
    
2. Detecte cuándo hay reuniones de Google Meet programadas.
    
3. Se lance automáticamente antes de cada reunión para unirse y grabar.
    

---

## 🧱 ¿Qué necesitas además del contenedor?

### ✅ 1. **Acceso a la API de Google Calendar**

- Crear un **proyecto en Google Cloud Console**.
    
- Habilitar la API de Calendar.
    
- Crear un **OAuth 2.0 Client ID** o una **clave de servicio**.
    
- Compartir el calendario con el bot (si usas una clave de servicio).
    

> Te puedo ayudar con esto si no lo has hecho antes.

---

### ✅ 2. **Script externo que monitoree las reuniones**

Este script:

- Se ejecuta cada X minutos.
    
- Usa la API de Calendar para buscar eventos próximos con enlaces de Google Meet.
    
- Si detecta uno próximo, lanza un contenedor Docker con el bot grabador.
    

> Ejemplo en pseudocódigo Python:

python

CopiarEditar

`from googleapiclient.discovery import build from datetime import datetime, timedelta import subprocess  def obtener_eventos_proximos(service):     ahora = datetime.utcnow().isoformat() + 'Z'     en_15_min = (datetime.utcnow() + timedelta(minutes=15)).isoformat() + 'Z'      eventos = service.events().list(         calendarId='primary',         timeMin=ahora,         timeMax=en_15_min,         singleEvents=True,         orderBy='startTime'     ).execute().get('items', [])      return [e for e in eventos if 'hangoutLink' in e]  def lanzar_bot(hangout_link):     subprocess.Popen(["docker", "run", "--rm", "bot-grabador", hangout_link])  # Loop de ejemplo for evento in obtener_eventos_proximos(service):     lanzar_bot(evento['hangoutLink'])`

---

### ✅ 3. **Mecanismo de ejecución programada**

Tienes dos opciones para esto:

#### Opción A: Script externo (host Linux)

- Ejecutas un script cada 5 min con `cron` o un `systemd timer`.
    

#### Opción B: Contenedor adicional tipo "scheduler"

- Un contenedor Docker que corre continuamente o con cron internamente.
    
- Consulta Calendar y lanza otros contenedores del bot cuando hay reuniones.
    

> Esto permite tener un **sistema completo 100% en contenedores.**

---

## 🧩 Estructura final del sistema

less

CopiarEditar

`[Contenedor Scheduler]  ← Consulta Google Calendar cada 5 min        │        ├── Si hay reunión:        ▼ [Lanza Contenedor Bot Grabador]        ├── Selenium + Chrome        ├── Xvfb        ├── PulseAudio        ├── ffmpeg        └── Graba audio y guarda .wav`

---

## 🚨 Consideraciones importantes

- El bot debe tener **acceso a Google Calendar** (OAuth o clave de servicio).
    
- La cuenta bot debe tener permisos para unirse a la reunión.
    
- Asegúrate de que el bot **no intente unirse muy temprano** (ideal: 1-2 min antes).
    
- Puedes guardar los `.wav` en un volumen compartido o subirlos automáticamente a Drive/Cloud.