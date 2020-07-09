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

### Request message

	GET /somedir/page.html HTTP/1.1  
	Host: www.someschool.edu  
	Connection: close  
	User-agent: Mozilla/5.0 Accept-language: fr

- The first line of an HTTP request message is called the **request line**; the subsequent lines are called the **header lines**

- The request line has three fields: 
	- the method field: post, get, head, put, delete 
	- the URL field
	- the HTTP version field

### Response message

	HTTP/1.1 200 OK  
	Connection: close  
	Date: Tue, 18 Aug 2015 15:44:04 GMT  
	Server: Apache/2.2.3 (CentOS) Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT Content-Length: 6821  
	Content-Type: text/html  
                            
	(data data data data data ...)  

- It has three sections: an initial **status line**, six **header lines**, and then the **entity body**.

#### Status code 
- **200 OK **: Request succeeded and the information is returned in the response.
- **301 Moved Permanently**: Requested object has been permanently moved; the new URL is specified in Location: header of the response message. The client software will automatically retrieve the new URL.
- **400 Bad Request**: This is a generic error code indicating that the request could not be understood by the server.
- **404 Not Found**: The requested document does not exist on this server.
- **505 HTTP Version Not Supported**: The requested HTTP protocol version is not supported by the server


### Cookies

- cookie technology has four components
	(1) a cookie header line in the HTTP response message;  
	(2) a cookie header line in the HTTP request message;   
	(3) a cookie file kept on the user’s end system and managed by the user’s browser;  
	(4) a back-end database at the Web site.

### web Caching

A **Web cache**—also called a **proxy server**—is a network entity that satisfies HTTP requests on the behalf of an origin Web server. The Web cache has its own disk storage and keeps copies of recently requested objects in this storage.

As an example, suppose a browser is requesting the object http://www.someschool.edu/campus.gif. Here is what happens
	- The browser establishes a TCP connection to the Web cache and sends an HTTP request for the object to the Web cache.
	- The Web cache checks to see if it has a copy of the object stored locally. If it does, the Web cache returns the object within an HTTP response message to the client browser.
	- If the Web cache does not have the object, the Web cache opens a TCP connection to the origin server, that is, to www.someschool.edu. The Web cache then sends an HTTP request for the object into the cache-to-server TCP connection. After receiving this request, the origin server sends the object within an HTTP response to the Web cache.
	- When the Web cache receives the object, it stores a copy in its local storage and sends a copy, within an HTTP response message, to the client browser (over the existing TCP connection between the client browser and the Web cache).

Typically a Web cache is purchased and installed by an ISP. For example, a university might install a cache on its campus network and configure all of the campus browsers to point to the cache

why web Cache
	- reduce reponse time.
	- Web caches can substantially reduce traffic on an institution’s access link to the Internet.
	- Web caches can substantially reduce Web traffic in the Internet as a whole, thereby improving performance for all applications

## DNS 

	Root DNS servers  
	com DNS servers org DNS servers edu DNS servers  
	facebook.com DNS servers  amazon.com DNS servers 

suppose a DNS client wants to determine the IPaddress for the hostname www.amazon.com. To a first approximation, the following events will take place. The client first contacts one of the root servers,which returns IP addresses for (top level domain)TLD servers for the top-level domain com. The client then contacts one of these TLD servers, which returns the IP address of an authoritative server for amazon.com. Finally,the client contacts one of the authoritative servers for amazon.com, which returns the IP address for the hostname www.amazon.com.



**Root DNS servers**. There are over 400 root name servers scattered all over the world. Figure 2.18 shows the countries that have root names servers, with countries having more than ten darkly shaded. These root name servers are managed by 13 different organizations. The full list of root name servers, along with the organizations that manage them and their IP addresses can be found at [Root Servers 2016]. Root name servers provide the IP addresses of the TLD servers.


**Top-level domain (TLD) servers**. For each of the top-level domains — top-level domains such as com, org, net, edu, and gov, and all of the country top-level domains such as uk, fr, ca, and jp — there is TLD server (or server cluster). The company Verisign Global Registry Services maintains the TLD servers for the com top-level domain, and the company Educause maintains the TLD servers for the edu top-level domain. The network infrastructure supporting a TLD can be large and complex; see [Osterweil 2012] for a nice overview of the Verisign network. See [TLD list 2016] for a list of all top-level domains. TLD servers provide the IP addresses for authoritative DNS servers.

**Authoritative DNS servers**. Every organization with publicly accessible hosts (such as Web servers and mail servers) on the Internet must provide publicly accessible DNS records that map the names of those hosts to IP addresses. An organization’s authoritative DNS server houses these DNS records. An organization can choose to implement its own authoritative DNS server to hold these records; alternatively, the organization can pay to have these records stored in an authoritative DNS server of some service provider. Most universities and large companies implement and maintain their own primary and secondary (backup) authoritative DNS server.














