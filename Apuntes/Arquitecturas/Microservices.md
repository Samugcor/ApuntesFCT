#apuntes #arquitecturas
___
### What is Microservices Architecture?

**Microservices architecture** is an approach to designing software applications as a collection of small, independent services that communicate with each other, usually over a network. Each service is focused on a single business functionality or domain and can be developed, deployed, and scaled independently.

In contrast to a **[[monolithic architecture]]**, where the entire application is built as a single, tightly coupled unit, a **microservices architecture** divides the application into smaller, more manageable services. Each service is independent, modular, and designed to perform a specific task.

### Key Characteristics of Microservices

1. **Single Responsibility**: Each microservice is focused on a single business function, such as handling user authentication, managing orders, or processing payments. This approach follows the **[[Single Responsibility Principle]]**.

> [!note] 
>  Esto está relacionado con el caso de uso que Moises puso de ejemplo en cuanto al uso de [[1_Introduction|Docker]] consulta el ejemplo [[Ejemplo de Granular Scaling|aquí]]

3. **Independently Deployable**: Microservices can be developed, deployed, and scaled independently of one another. This makes it easier to update or modify one service without affecting the entire application.

4. **Communication Over Networks**: Microservices typically communicate with each other over **HTTP**, **REST APIs**, **gRPC**, **message queues**, or other network protocols.

5. **Decentralized Data Management**: Each microservice has its own database or data store, which ensures loose coupling. This avoids a situation where one service needs to wait for a centralized database to make changes or fetch data.

6. **Technology Agnostic**: Each microservice can be written in a different programming language or use different technologies, as long as the service exposes an API for communication. For example, one microservice might be written in **Java**, while another might use **Node.js** or **Python**.

7. **Fault Isolation**: If one microservice fails, it doesn't necessarily bring down the entire system. This isolation allows the system to continue functioning with reduced capabilities or with other services running normally.

8. **Scalability**: Each service can be scaled independently based on demand. For example, if you have a payment service that gets a lot of traffic, you can scale it up without scaling the entire application.

### Benefits of Microservices Architecture

1. **Flexibility in Development**:

	- Teams can work on different services in parallel. Each team is responsible for one or a few services, making development faster and more efficient.

2. **Faster Releases**:

    - Since microservices are independent, new features or bug fixes can be deployed without affecting the entire application. This speeds up the release cycle.

3. **Improved Fault Tolerance**:

    - Microservices are isolated from each other, so if one service fails, the rest of the application can continue to function. This leads to more robust and reliable systems.

4. **Technology Diversity**:

    - Different services can be written using different technologies that are best suited for the task. For example, a service dealing with heavy data processing might use a language or framework optimized for performance, while a simple web-facing service might use a more lightweight framework.

5. **Independent Scaling**:

    - You can scale only the microservices that require additional resources (e.g., a highly requested service) rather than scaling the entire application.


### Challenges of Microservices

1. **Complexity**:

    - Managing multiple services can be complex. It involves more infrastructure, communication between services, and service orchestration (i.e., ensuring that everything works together).

2. **Network Latency**:

    - Microservices communicate over a network, which can introduce latency and additional overhead compared to function calls within a monolithic application.

3. **Data Management**:

    - Each microservice usually has its own database, so managing data consistency, transactions, and handling failures becomes more complex.

4. **Distributed Systems Issues**:

    - Microservices often involve distributed systems, which can have issues like network failures, partial failures, and consistency problems that need to be carefully managed.

5. **Testing**:

    - Testing microservices can be more complex than testing monolithic applications, as you need to ensure that not only individual services work correctly but that they all integrate and communicate properly.

### Relationship with [[1_Introduction|Docker]] (or other alternatives for containerization)

In a **microservices architecture**, each service is developed and deployed independently. [[1_Introduction|Docker]] provides a way to containerize these services so they can be deployed and run consistently across various environments, such as development, staging, and production.