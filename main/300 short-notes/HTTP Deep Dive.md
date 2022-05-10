---
created: 2022-05-09 19:06
updated: 2022-05-10 15:47
---
---
**Links**: [[300 home]]

---
## History of HTTP
![[attachments/Pasted image 20220509192559.png]]

## HTTP 0.9
- Initial version of HTTP — a simple client-server, request-response, telenet-friendly protocol
- *Request nature: single-line* (method + path for requested document)
- Methods supported: `GET` only
- Response type: *hypertext only*
- Connection nature: terminated immediately after the response
- No HTTP headers (cannot transfer other content type files), No status/error codes, No URLs, No versioning

## HTTP 1.0
- *Provided header fields* including rich metadata about both request and response (*HTTP version number, status code, content type*)
- Response: *not limited to hypertext* (`Content-Type` header provided ability to transmit files other than plain HTML files — e.g. scripts, stylesheets, media)
- Methods supported: `GET` , `HEAD` , `POST`
- Connection nature: terminated immediately after the response i.e. establishing a **new TCP connection with each request**.
	- ![[attachments/Pasted image 20220509200607.png]]
- Establishing a *new connection for each request* — *major problem* in both HTTP/0.9 and HTTP/1.0. This meant these protocols were *very slow*.
- It was realised quickly by the devs and *within a year HTTP 1.1 was released*.

## HTTP 1.1
- Internet landscape was constantly changing with websites becoming more dynamic and heavy. HTTP 1.0 was very slow so a new and faster protocol was needed.
- Extra methods were added like `PUT`, `DELETE`
- Features like **CORS**, **Keep-alive**, **Caching** were introduced in this update.
- So in HTTP 1.1 we had **Persistent TCP Connection** using keep alive header.

### Keep alive
- The `Keep-Alive` *header* was first introduced in HTTP 1.1 
	- HTTP/1.1 changed the semantics of the HTTP protocol to use connection **keepalive by default**. Meaning, unless told otherwise (via `Connection: close` header), the server should keep the connection open by default.
	- However, this same functionality was also backported to HTTP/1.0 and enabled via the `Connection: Keep-Alive` header. Hence, if you are using HTTP/1.1, technically you don’t need the `Connection: Keep-Alive` header, but many clients choose to provide it nonetheless.

- Using Keep-alive option meant that the server won't close the TCP connection. 
- This enabled *re-using of the same TCP connection for multiple HTTP request*. 
	- ![[attachments/Pasted image 20220509212942.png]]

- Client, server, or any intermediary can provide information for `Keep-Alive` header independently. Also, a host can add `timeout` and `max` parameters in order to set a timeout or limit maximum request count per connection.

- Example
	- ![[attachments/Pasted image 20220510145407.png]]

### Flaws in HTTP 1.1
- HOL - **Head of Line Blocking**
	- Suppose a request is send for index.html file of a website.
	- A single TCP connection is created. 	
	- *TCP Connection gets blocked till the response is received*.
		- ![[attachments/Pasted image 20220510150129.png]]
	- Internally the index.html also requires some CSS and JS files.
	- Now since we have a single TCP connection it will wait for the response of index.html files before requesting the CSS and JS files.
	- One way of making it a bit better is by *establishing multiple TCP connections (6)*. But this is working around the problem instead of solving it. What if you have more than 6 things then we are back to the initial problem.
		- ![[attachments/Pasted image 20220510154008.png]]

- Repetition of Header Data
	- Header information is repeated with each request.

- More focus on gzip, minifying CSS/JS, caching etc.

## HTTP 2
- Header data is separate from request data.
- *Compress HTTP Headers* using **HPACK**
- Allows *Server Push*:
	- Push frames enables us to send mandatory resources in advance along with an HTTP response.
	- Server Push can be abused when configured incorrectly
- *HTTPS* is a mandatory requirement
- HTTP 2 is built upon HTTP 1.1 so even though the client doesn't support HTTP 2 it will served using HTTP 1.1.
- HTTP/2 encodes request and response messages into **binary**, instead of transmitting the normal plain-text messages you would see with HTTP/1.1.
- HOL Blocking problem in HTTP 1.1 is solved by **multiplexing**.

### Multiplexing
- HTTP/1.1 loads resources one after the other, so if one resource cannot be loaded, it *blocks all the other resources behind it*. 
- In contrast, *HTTP/2* is able to use a single TCP connection to send *multiple streams of data at once* so that no one resource blocks any other resource.
	- ![[attachments/Pasted image 20220510150259.png]]
- To achieve this parallel request over a single HTTP connection, **HTTP 2 uses the concept of streams**. 
- That is, each request being sent from the client has a *unique stream id* attached behind the scenes. This helps the client and server identify the calling and receiving endpoints. One can think of *each stream as an independent channel* for communication.
	- ![[attachments/Pasted image 20220510150310.png]]
	- ![[attachments/Pasted image 20220510154249.png]]

### Stream Prioritisation
- When downloading a website, the *order in which assets* (HTML, CSS, images, Javascript) *are downloaded is important* and can affect what you see in the browser. 
- If the assets are loaded in the wrong order your website may look incomplete or even lose functionality in some areas.
- *HTTP/1.1 eliminates this issue, as the head-of-line blocking makes it straightforward to load assets in the right order*. 
- HTTP/2 doesn’t have head-of-line blocking, therefore responses to the browser request might be received in any order.
- *HTTP/2 solves this issue by allowing the browser to indicate to the server what priorities should be given for downloading the specific files or objects*. 
- This means that web browsers will automatically download the most important assets first, therefore removing any potential for assets to be loaded in the wrong order.

## HTTP 3
- Perhaps the most obvious difference between HTTP/3 and the older versions is that HTTP/3 is fully based on **QUIC**, which utilises **UDP**.

## References
