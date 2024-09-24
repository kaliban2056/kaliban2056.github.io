+++
title = 'Building a Simple Multi-Client Chat Application in Python'
date = 2024-09-23T15:41:49+02:00
draft = false
tags = ["programming", "python", "networking"]
+++

In this post, I'll walk through a basic chat application I built using Python's `socket` and `threading` modules.
This project allows multiple clients to connect to a server and communicate in real-time.
It's a great example of how socket programming and threading can be used to build networked applications in Python.

## Project Overview

The project consists of two main scripts:

-   `server.py`: Manages client connections and broadcast messages to all clients.
-   `client.py`: Connects to the server, sends messages, and receives messages from other clients.

### Key Featureswr

-   **Multi-client support**: The server can handle multiple clients simultaneously.
-   **Nicknames**: Each client is prompted to choose a nickname upon connection.
-   **Message broadcasting**: Messages from one client are shared with all others.
-   **Join/Leave notification**: Clients are notified when someone joins or leaves the chat.

## Server-Side Code

1. **Setting Up the Server Socket**

```python
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((host, port))
server.listen()
```

-   `socket.AF_INET`: This specifies that we are using an IPv4 address.
-   `socket.SOCK_STREAM`: We're using TCP, which is a connection-oriented protocol.
-   `bind((host, port))`: The server binds to the provided IP address and port.
-   `listen()`: Starts the server, making it listen for incoming connections.

This sets up a server that listen for incoming connections. When a client connects, the server will handle communication in a separate thread.

2. **Accepting Client Connections**

```python
client, address = server.accept()
```

-   `accept()`: Waits for an incoming connection. When a client connects, ti returns a new `client` socket and the client's `address`.

Once a connection is accepted, the server will assign the client to a separate thread for communication using the `handle()` function.

3. **Handling Client Messages**

```python
def handle(client):
    while True:
        try:
            message = client.recv(1024)
            broadcast(message)
        except:
            # Client disconnects
            index = clients.index(client)
            clients.remove(client)
            client.close()
            nickname = nicknames[index]
            broadcast(f"{nickname} left the chat.".encode('ascii'))
            nicknames.remove(nickname)
            break
```

-   `client.recv(1024)`: Reads up to 1024 bytes of data from the client, which represents a message.
-   `broadcast(message)`: sends the received message to all connected clients.
-   If the client disconnects or an error occurs, the server removes the client from the list and broadcast a notification to the other clients.

4. **Broadcasting Messages to All Clients**

```python
def broadcast(message):
    for client in clients:
        client.send(message)
```

-   This function iterates through all connected clients and sends them the given message. It's used whenever a client sends a message or when a user joins or leaves the chat.

5. **Listening for New Connections**

```python
def receive():
    while True:
        client, address = server.accept()
        client.send("NICK".encode('ascii'))
        nickname = client.recv(1024).decode('ascii')
        nicknames.append(nickname)
        clients.append(client)
        print(f"Nickname of the client is {nickname}")
        broadcast(f"{nickname} joined the chat".encode('ascii'))
        thread = threading.Thread(target=handle, args=(client,))
        thread.start()
```

-   `server.accept()`: Accepts new client connections.
-   `client.send("NICK")`: Request a nickname from the client.
-   `nickname = client.recv(1024).decode()`: Receives and decodes the nickname sent by the client.
-   `threading.Thread(target=handle)`: Starts a new thread for each connected client, allowing multiple clients to communicate without blocking one another.

The `receive()` function continuously waits for new clients and assigns each one to a new thread for indivisual handling.

## Client-Side Code

1. **Setting Up the Client Socket**

```python
clietn = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("127.0.0.1", 5555))
```

-   `socket.AF_INET`: Specifies that we are using IPv4.
-   `socket.SOCK_STREAM` Sets up the socket to use TCP.
-   `connect()`: Connects to the server at the specified IP and port.

Once connected, the client will interact with the server by sending and receiving messages.

2. **Receiving Messages from the Server**

```python
def receive():
    while True:
        try:
            message = client.recv(1024).decode('ascii')
            if message == "NICK":
                client.send(nickname.encode('ascii'))
            else:
                print(message)
        except:
            print("An error occurred!")
            client.close()
            break
```

-   `client.recv(1024)`: Listens for incoming messages from the server.
-   If the server sends "NICK", the client responds by sending its nickname.
-   Otherwise, the message is printed to the console.
-   If there is an error, the client closes the connection.

3. **Sending Messages to the Server**:

```python
def write():
    while True:
        message = f"{nickname}: {input('')}"
        client.send(message.encode('ascii'))
```

-   This function continuosly waits for user input and sends it to the server.
-   `input()`: Reads user input from the console.
-   The message is sent to the server, where it is broadcast to other connected clients.

## Running the Application

1. **Start the Server**

In one terminal, run the server:

```python
python3 server.py
```

The server will start listening for client connections.

2. **Connect Clients**

In other terminals, run multiple instances of the client:

```python
python3 client.py
```

Each client will be promoted to choose a nickname, and once connected, they can send and receive messages.

3. **Chat in Real-Time**

Messages typed in any client terminal will be broadcast to all connected clients. If a user disconnects, the other clients will be notified.

## Learning Points

1. **Socket Programming**

This project demonstrates the fundamentals of socket programming:

- Server-Client communication: You learned how to establish a connection between a server and multiple clients over TCP.
- Socket creation: Both server and client sockets were created to send and receive data.
- Handling multiple clients: With threading, the server can manage multiple clients simultaneously, making this a simple but powerful example of concurrent network programming.

2. **Threading in Python**

- Parallel handling of clients: The use of threads ensures that the server can handle multiple clients concurrently without blocking or slowing down due to one particular client.
- Thread safety: Although this example doesn’t cover it explicitly, dealing with shared resources across threads requires care, especially when working on larger or more complex applications.

3. **Message Broadcasting**

The server can broadcast any client’s message to all other connected clients. This is a critical pattern in applications like chat rooms, multiplayer games, and real-time collaborative platforms.

4. **Handling Client Disconnects**

The server not only handles client connections but also gracefully removes clients from the active list upon disconnection. This ensures that resources are cleaned up properly and other clients are notified.

## Final Thoughts

This project offers a solid foundation for understanding socket programming, multi-threading, and basic network communication in Python. From here, you can expand and improve the project by:

- Adding a GUI: A graphical interface would make the chat application more user-friendly.
- Implementing encryption: Add security to the chat by encrypting messages between the server and clients using SSL/TLS.
- Enhancing error handling: While this application handles basic errors like disconnections, more sophisticated error handling would make it more robust.
- Scaling: Modify the server to handle more significant traffic, or make it accessible over a public IP for use across networks.

Feel free to experiment with the code, build upon it, and explore more advanced topics like non-blocking sockets, socket.io for web applications, or even building your own messaging protocols.