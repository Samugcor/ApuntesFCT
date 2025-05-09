#apuntes #arquitecturas #fct
___
> [!warning]
> Esta entrada está hecha a partir de una pregunta a chatGPT sobre el ejemplo que Moises dio en la reunión de introducción. El lenguaje puede no ser el más adecuado ni representa las palabras textuales, porque no me acuerdo, pero da un feeling general.
### Prompt

> If implementing a web app for a marketplace working with a microservices architecture would we be able to relocate resources and sacale only the parts needed depending on the traffic of the page instead of needing to scale the whole in an event with a ton of pettitions for only one part (for example multiple petitions for the catalogue but none for the payment or delivery parts?

### Respuesta

> Yes, absolutely! One of the key advantages of a **microservices architecture** is the ability to **scale specific parts** of the application independently based on traffic and usage, rather than having to scale the entire application. This is known as **granular scaling**, and it's especially useful in scenarios like the one you described for a marketplace web app.
>
> **How Microservices Help with Granular Scaling**:
> In a **microservices architecture**, each part of the application (e.g., catalog, payment, delivery, user management) is a separate, independently deployable service. Each service is responsible for a specific domain, and they communicate with each other over APIs.
>
> When it comes to scaling, microservices allow you to focus your resources where they're needed most. For example, let’s say there’s a sudden surge in traffic for your marketplace **catalog** (perhaps users are browsing items), but the **payment** and **delivery** services are not experiencing much traffic. With microservices, you can **scale the catalog service** independently to handle the increased load without needing to scale the other services that aren’t under stress.