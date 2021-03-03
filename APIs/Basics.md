src: https://www.youtube.com/watch?v=GZvSYJDk-us&feature=emb_title

# Application Programming Interface (API)

#### What is an API? (:0)
- What is an Interface?
	- Interface: allows you to control something more easily after abstracting the inner workings / implementation; like an ipod; in device, there can be multiple layers of abstractions
- Remote APIs
- REST (representational state transfer) 
	- an architecutral style for developers to write APIs


#### How the Web Works (:17)
- Web
	- Internet browser, which is a client, is used to connect to a server by putting a URL (universal resource locator) in the address bar.
	- URL (or URI) includes a scheme portion (for example, HTTP -- Hypertext Transfer Protocol).
		- protocol - finding the expectation of how to communicate
	- Browser creates an HTTP request for you by specifying the URI and a particular **HTTP verb** (GET, POST, PUT, PATCH, DELETE). Server sends back a response with a body (for a webpage, that contains the HTML) that is typically represented as JSON (Javascript Object Notation) these days
		- HTTP is originally designed as a stateless protocol, meaning once a request is recieves a response, it's all done.
		- Requests have headers which can have auth info, caching info, etc. Responses also contains headers, including the status code

#### How REST Works with the Web (:22)
- What makes an API RESTful?
1. Client-Server Architecture
2. Statelessness
3. Layered System
4. Cacheability
5. Uniform Design
6. Code on Demand

- Much like the web, for APIs, the client (your program) makes a stateless HTTP request to the server (to maintain a state, send info via header) 
- CRUD (Creating, Reading, Updating, & Deleting)
	- what we can do with resources, matching the HTTP verbs

#### Exploring an API Online: Spotify Search API
- Authorization Header

#### Using an API from the command line:Twilio API (:44)

#### Using Postman to explore APIs (:53)

#### Using Helper Libraries (JS, Python) (1:14)
- alot of API code we have to write is boilerplate; thus, many products and services created **helper libraries**, aka SDKs (Software Development Kits), to help with this.

#### Making Flask app (1:34)

#### Making JS single page app (1:54)
- Single Page Application (SPA)
	- once the page is rendered, the client will responsible for rendering parts of the page. We won't rely on full page reload from server.
	- 