---
created: 2022-05-09 19:06
updated: 2022-05-11 16:14
---
---
**Links**: [[300 home]]

---
## Websockets
- Websockets are created using `ws://somewebsite.com` or `wss://somewebsite.com`. wss is for websockets with TLS.

### Handshake
- Websockets are *upgraded [[HTTP Deep Dive#HTTP 1 1|HTTP 1.1]] Get requests*. 
	- ![[attachments/Pasted image 20220511153923.png]]
	- ![[attachments/Pasted image 20220511154325.png]]
- So for establishing a websocket connection you first establish a HTTP 1.1 connection. This HTTP 1.1 connection is then upgraded to a websocket connection by the webserver.
- Uses the same TCP connection that was used for establishing HTTP 1.1.
- Status code of **101** for *switching the protocols*.
- Websockets will never work with [[HTTP Deep Dive#HTTP 1 0|HTTP 1.0]] since there were no persistent connections in HTTP 1.0. 

---
- Websockets are **stateful** protocol whereas *HTTP is a stateless* protocol.
- HTTP is simplex (either the client sends a request or server sends a response but not at the same time) whereas websockets are **full duplex** (both the client and server can send messages to each other at the same time).
- Websockets are **not horizontally scalable** whereas HTTP is. This is because HTTP is a stateless protocol (sends whatever is needed by the server in every request) and websocket is a stateful protocol. 
- When we refresh the page the websocket connection is closed.

### Use cases
- Multiplayer gaming
- Chatting applications
- *Dynamic UI*: we can dynamically refresh the UI without reloading the page. This is particularly useful in trading platforms. You see the prices getting update without refreshing the page.
- Showing client progress/logging
- **real time bidirectional communication**.