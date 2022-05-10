---
created: 2022-05-09 19:06
updated: 2022-05-09 21:52
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

### Flaws in HTTP 1.1
- HOL - **Head of Line Blocking**
	- Suppose a request is send for index.html file of a website.
	- A single TCP connection is created. 	
	- *TCP Connection gets blocked till the response is received*.
	- Internally the index.html also requires some CSS and JS files.
	- Now since we have a single TCP connection it will wait for the response of index.html files before requesting the CSS and JS files.

- Repetition of Header Data
	- Header information is repeated with each request.

- More focus on gzip, minifying CSS/JS, caching etc.

## HTTP 2
- Header data is separate from request data.
- Compress HTTP Headers using HPACK
- Allows Server Push
	- PUSH: PUSH Frames enables us to send mandatory resources in advance along with an HTTP response.
	- PUSH frames should be used with care as this can lead to increase in size of the HTTP response.
- Enables Multiplexing: process multiple requests over the same connection.
- HTTPS is a mandatory requirement
- HTTP 2 is built upon HTTP 1.1 so even though the client doesn't support HTTP 2 it will served using HTTP 1.1.

## HTTP 3

## References
