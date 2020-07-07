# chapter 2 

## socket
a socket is the interface between the application layer and the transport layer within a host. It is also referred to as the Application Programming Interface(API) between the application and the network

## The Interface Between the Process and the Computer Network
The only control that the application developer has on the transport-layer side is (1) the choice of transport protocol and (2) perhaps the ability to fix a few transport-layer parameters such as maximum buffer and maximum
segment sizes.

## Addressing Processes
To identify the receiving process, two pieces of information need to be specified: (1) the address of the host and (2) an identifier that specifies the receiving process in the destination host.

- In the Internet, the host is identified by its IP address
- A destination port number is to identify receiving process

## overview of HTTP

- Each URL has two components: the hostname of the server that houses the object and the object’s path name
- stateless protocol: an HTTP server maintains no information about the clients. If a particular client asks for the same object twice in a period of a few seconds, the server does not respond by saying that it just served the object to the client; instead, the server resends the object, as it has completely forgotten what it did earlier

- Non-Persistent and Persistent Connections

- round-trip time (RTT): which is the time it takes for a small packet to travel from client to server and then back to the client.

	GET /somedir/page.html HTTP/1.1  
	Host: www.someschool.edu  
	Connection: close  
	User-agent: Mozilla/5.0 Accept-language: fr

- The first line of an HTTP request message is called the **request line**; the subsequent lines are called the **header lines**

- The request line has three fields: 
-- the method field: post, get, head, put, delete 
-- the URL field
-- the HTTP version field

	HTTP/1.1 200 OK  
	Connection: close  
	Date: Tue, 18 Aug 2015 15:44:04 GMT  
	Server: Apache/2.2.3 (CentOS) Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT Content-Length: 6821  
	Content-Type: text/html  
                            
	(data data data data data ...)  

- It has three sections: an initial status line, six header lines, and then the entity body。

