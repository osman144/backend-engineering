# Request and Response Model
- **Overview**: The client sends a request, the server parses it, processes it, and sends a response back. The client then parses and consumes the response.
- **Serialization Formats**: Requests are often serialized in JSON or XML, facilitating efficient data storage, transmission, and interchange.
- **Usage**: Commonly used in web protocols such as HTTP, DNS, SSH, RPC, SQL, and various database protocols, as well as in APIs like REST, SOAP, and GraphQL.
- **Anatomy of a Request/Response**:
  - Defined by both client and server.
  - Contains Action (CRUD), Protocol (e.g., HTTP), headers.

# Synchronous vs Asynchronous
- **Synchronous I/O**:
  - The caller waits for a response and cannot proceed until it receives one.
  - The process is effectively frozen during the wait.
  - The caller and receiver are in sync.
- **Asynchronous I/O**:
  - Involves asynchronous programming (promises/futures).
  - The caller can continue working while waiting for a response.
  - Utilizes mechanisms like epoll or callbacks.
  - Example: Node.js spins a secondary thread to handle asynchronous operations.
  - Asynchronous processes are not in sync by nature.
  - Real-life example: Email.

# Push
- **Concept**: In some cases, clients need real-time notifications from the backend, making the standard request/response model less ideal.
- **Mechanism**:
  - Establish a connection using WebSockets, Server-Sent Events (SSE), or push services like Firebase Cloud Messages (FCM) or Apple Push Notification (APN).
  - Subscription and registration: Clients subscribe to receive push data.
  - Server initiates the push path.
  - Data transmission is immediate if the client is online. Offline clients receive data once they reconnect.
- **Push Model Use Cases**:
  - Often used by message brokers (e.g., RabbitMQ), though Kafka does not have a push model.
  - Pros: Real-time updates.
  - Cons: Requires clients to be online and connected.
- **WebSockets for Push Notifications**:
  - Provides a persistent, low-latency channel for real-time data exchange.
  - Maintains an open connection for continuous two-way communication, unlike traditional HTTP.

# Short Polling
- **Process**:
  - The client sends repeated requests to the server to check for new data.
  - If no new data is available, the server responds with a no-data message.
  - The client waits for a set interval before polling again.
- **Characteristics**:
  - Simple to implement but can be inefficient due to high network bandwidth usage and potential backend resource wastage.

# Long Polling
- **Description**: Simulates a push mechanism over HTTP. The server holds onto the request until new data or events occur.
- **Process**:
  - The client sends a request, and the server holds the request until it can respond with new data.
  - Used by Kafka: the server waits for new entries in a topic before responding.
- **Comparison with Short Polling**:
  - Offers near real-time updates.
  - More efficient than short polling but not as instant as WebSockets.

# Server-Sent Events (SSE)
- **Overview**: SSE allows servers to push real-time data updates to clients over a single HTTP connection.
- **Characteristics**:
  - Unidirectional: Only the server sends data to the client.
  - Persistent connection for continuous real-time updates.
- **Use Cases**: Real-time collaboration tools, stock tickers, live scores, live news, etc.
- **Pros and Cons**:
  - Pros: Real-time, compatible with the HTTP model.
  - Cons: Requires clients to be online; not ideal for lightweight clients.

# Pub/Sub
- **Concept**: A messaging pattern where publishers send messages without specifying the recipients.
- **Operation**:
  - Subscribers receive messages they are interested in, decoupling senders and receivers.
- **Advantages**:
  - Scalable, dynamic communication.
  - Useful for microservices and works even when the client isn't running.
- **Challenges**:
  - Handling message delivery issues and network saturation.

# Multiplexing vs Demultiplexing
- **Multiplexing**:
  - Combines multiple input signals into a single transmitted signal.
  - Maximizes the use of bandwidth.
- **Demultiplexing**:
  - Splits a single received signal into multiple output signals.
  - Directs data to the correct recipient or process.
- **Real-World Analogy**:
  - Multiplexing is like merging multiple lanes into a super-lane, while demultiplexing is splitting this super-lane back into separate lanes.

# Stateless vs Stateful
- **Stateful Backend**:
  - Stores state about clients in its memory.
  - Relies on the presence of this information.
- **Stateless Backend**:
  - Clients are responsible for transferring their state with every request.
  - Backend may store this state but it's not necessary.
  - Data can be stored elsewhere, like in a centralized system such as PostgreSQL.
  - A backend is stateless if it can be restarted while idle without disrupting ongoing workflows.
  - The backend application can be stateless while the overall system remains stateful due to the database.
  - If the database fails, all data could be lost.

## Protocols
- **Stateful Protocols**:
  - Example: TCP.
    - Stream-oriented, assigns sequence numbers to each byte.
    - Manages sequences and connection file descriptors.
    - Provides reliable and ordered data transfer.
- **Stateless Protocols**:
  - Example: UDP (User Datagram Protocol).
    - Treats each packet independently, without connection or state tracking.
    - Faster but less reliable, suitable for applications where data loss is preferable to delay.
- **Protocol Layers**:
  - Stateless protocols can be built on top of stateful ones, and vice versa.
  - Example: HTTP is stateless, built on top of stateful TCP.
  - Completely stateless systems are rare, with JWT as an example.

## Sidecar Pattern
- **Definition**:
  - A helper service or module running alongside the main application.
  - Adds functionality or handles tasks not the focus of the primary application, like logging, monitoring, networking, etc.
- **Examples**:
  - Service Mesh Proxies (Linkerd, Istio, Envoy).
  - Sidecar proxy container, ideally a layer 7 proxy.
- **Pros**:
  - Language agnostic (polyglot).
  - Facilitates protocol upgrades.
  - Enhances security.
  - Provides tracing, monitoring, and service discovery.
  - Can perform caching.
- **Cons**:
  - Adds complexity.
  - May introduce latency.

# Proxies
- **Forward Proxy**:
  - Acts as an intermediary between systems, typically client-facing.
- **Reverse Proxy**:
  - Sits in front of web servers, responding to client requests on their behalf.
  - Used for load balancing to distribute traffic among multiple servers.
  - Improves website performance and reliability.

![image](https://github.com/osman144/backend-engineering/assets/25594064/57063897-5204-47f2-a925-d56fbcfcfe44)
