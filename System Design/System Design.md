src: https://www.freecodecamp.org/news/systems-design-for-interviews/#section-1-networks-and-protocols

1. Networks and Protocols
	- IP (Internet Protocol)
	- TCP (Transmission Control Protocol)
	- HTTP (Hyper Text Transfer Protocol)
2. Storage, Latency, and Throughput
	- Storage 
			- **Memory** -  more temporary. When device or server restarts, the data usually will be lost. Faster and less expensive.
			- **Disk** - more robust and persistent. Even with the power off and server restarted, the data will be stored.
	- Latency
		- = duration of an operation. For example, how long a "round trip" network request take (client sends a query and server sends back reseponse).
		- When loading a website, you want low latency.
	- Throughput
		- maximum capacity of a machine system.
3. System Availability
	- Quantifying Availability
4. [[Caching]]
	- helps reduce latency in a system by providing a temporary storage.
5. Proxy
	- a subsistute. Typically a server that acts as a middleman between client and another server.
	- a **forward proxy** acts on behalf of client; a **reverse proxy** acts on behalf of server.
	> "So, in a forward proxy, the server won't know that the client's request and its response are traveling through a proxy, and in a reverse proxy the client won't know that the request and response are routed through a proxy."
	- Your reverse proxy can be delegated a lot of tasks (gatekeeping, screening, loadbalancing, etc), assisting your main server.
6. Load Balancing
	- balancing and allocating the request load to maintain availability and throughput