# Transport layer

## segement
This is done by (possibly) breaking the application messages into smaller chunks and adding a transport-layer header to each chunk to create the transport-layer segment.


### Relationship Between Transport and Network Layers

a transport-layer protocol provides logical communication between processes running on different hosts, a network-layer protocol provides logical-communication between hosts.

- a computer network may make available multiple transport protocols, with each protocol offering a different service model to applications.
- the services that a transport protocol can provide are often constrained by the service model of the underlying network-layer protocol. If the network-layer protocol cannot provide delay or bandwidth guarantees for transport-layer segments sent between hosts, then the transport-layer protocol cannot provide delay or bandwidth guarantees for application messages sent between processes.
- certain services can be offered by a transport protocol even when the underlying network protocol doesn’t offer the corresponding service at the network layer.
	- reliable data transfer.
	- encryption

### Overview of the Transport Layer in the Internet

two protocol in transport layer: UDP and TCP  
Transport layer packet: segment  
network layer protocol: IP,  IP service model is a best-effort delivery service
	- it does not guarantee segment delivery
	- it does not guarantee orderly delivery of segments
	- it does not guarantee the integrity of the data in the segments
each host has an IP address

UDP and TCP is to extend IP’s delivery service between two end systems to a delivery service between two processes running on the end systems. Extending host-to-host delivery to process-to-process delivery is called transport-layer **multiplexing** and **demultiplexing**.

**UDP** process-to-process data delivery and error checking—are the only two services that UDP provides

**TCP** 
- reliable data transfer
- congestion control 

### Multiplexing and Demultiplexing

This job of delivering the data in a transport-layer segment to the correct socket is called **demultiplexing**
The job of gathering data chunks at the source host from different sockets, encapsulating each data chunk with header information (that will later be used in demultiplexing) to create segments, and passing the segments to the network layer is called **multiplexing**

transport-layer multiplexing requires (1) that sockets have unique identifiers, and (2) that each segment have special fields that indicate the socket to which the segment is to be delivered. These special fields, illustrated in Figure 3.3, are the **source port number field** and the **destination port number field**. Each port number is a 16-bit number, ranging from 0 to 65535. The port numbers ranging from 0 to 1023 are called **well-known port numbers** and are restricted, which means that they are reserved for use by well-known

#### Connectionless Multiplexing and Demultiplexing

It is important to note that a UDP socket is fully identified by a two-tuple consisting of a destination IP address and a destination port numbe

### Connection-Oriented Multiplexing and Demultiplexing

One subtle difference between a TCP socket and a UDP socket is that a TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number)

## Connectionless Transport: UDP

UDP takes messages from the application process, attaches source and destination port number fields for the multiplexing/demultiplexing service, adds two other small fields, and passes the resulting segment to the network layer.

- **Finer application-level control over what data is sent, and when**. UDP will package the data inside a UDP segment and immediately pass the segment to the network layer. TCP has a congestion-control mechanism that throttles the transport-layer TCP sender when one or more links between the source and destination hosts become excessively congested. TCP will also continue to resend a segment until the receipt of the segment has been acknowledged by the destination, regardless of how long reliable delivery takes. Since real-time applications often require a minimum sending rate, do not want to overly delay segment transmission, and can tolerate some data loss, TCP’s service model is not particularly well matched to these applications’ needs.
- **No connection establishment** UDP does not introduce any delay to establish a connection unlike the tcp that needs build connection before sending data. 
- **No connection state**.TCP maintains connection state in the end systems. This connection state includes receive and send buffers, congestion-control parameters, and sequence and acknowledgment number parameters. We will see in Section 3.5 that this state information is needed to implement TCP’s reliable data transfer service and to provide congestion control. UDP, on the other hand, does not maintain connection state and does not track any of these parameters. For this reason, a server devoted to a particular application can typically support many more active clients when the application runs over UDP rather than TCP.
- **Small packet header overhead** The TCP segment has 20 bytes of header overhead in every segment, whereas UDP has only 8 bytes of overhead.
### UDP Segment Structure
![image info](./fig3.7.png=250x)







