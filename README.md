# Advanced Programming Module 10

## Asynchronous Programming - Broadcast Chat

### Reflection

#### Experiment 2.1: Running the Broadcast
Steps to run the broadcast chat:
1. Open 4 terminals in the root directory
2. Type `cargo run --bin server` to run the server in the first terminal
3. Type `cargo run --bin client` in the remaining terminals to run the client

![Server and Clients](images/experiment_21.jpg)

Type a message in a client terminal. Watch the message from the client get received by the server, which is then broadcasted to all the other clients.

#### Experiment 2.2: Changing Ports
![Changing Ports](images/experiment_22.jpg)

In `server.rs` I changed the port number to 8080 in the `TcpListener` function.
I also made the port number in `client.rs` match which is in the `
async fn main() -> Result<(), tokio_websockets` crate.

Compared to the client side, the websocket protocol is not declared explicitly but it is implemented in the `tokio-websockets` crate. Morevoer, port 8080 is binded to a TCPListener which assigns a process that listens for an TCP connection going through that port. The server creates a socket when a connection is established, which is then passed to the websocket handler.


#### Experiment 2.3: Small Changes
I only changed one line of code in both `client.rs` and `server.rs`.
In `client.rs`, I changed:
```
                            println!("From Server: {}", text);
```
To:
```
                            println!("From Broadcast Server: {}", text);
```
While in `server.rs` I changed:
```
        println!("New connection from: {addr:?}");
```
To:
```
        println!("New connection from Ameera's Laptop: {addr:?}");
```
The changes can be seen in the image below:
![Small Changes](images/experiment_23.jpg)
I changed those lines to make the sources of the connections and messages more obvious. The server already knows which address creates what messages because it spawns an asynchronous thread based on the order of the clients connecting. In addition, that thread also accepts a stream of messages from said client.
A thread and handler is assigned to every client's host which is stored in the `addr` parameter which is shown in the terminals.