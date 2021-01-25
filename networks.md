# What is a computer network?
+ Built for GP hardware and are able to carry many different types of data, and support a range of varying applications

# Requirements for Network Design
## Connectivity
+ A network must provide connectivity between a set of computers

## Links, Nodes and Clouds
### Links
+ Physical medium by which two or more computers are directly connected by (coxial cable or fibre)

+ `Point-to-Point` links are links that are limited to a pair of nodes

+ `Multiple Access` links are links that can be shared by more than two nodes (single link)

  ![hello](https://lh4.googleusercontent.com/nspZRdY1VbTGIumEVKt7FySXH0FlaYxUX-W22xU5vCIRzxGqBSPKlTub1vroPLgGSDTdYWKnXciqNBRBZBl7=w1366-h568)

+ `multiple-access` links are often limited in size, ito geographical distance that they can cover and the number of nodes they can connect

+ Satellite links can however cover a wide geographical region

### Nodes
+ Computers connected via links are referred to as `Nodes`
+ Or devices such as routers, switches, gates etc.



### Indirect Connectivity between Nodes

+ Indirect connectivity can be achieved by using something called a `forwarding node`

+ A `forwarding node` is attached to atleast two links and runs software that forwards data received on one link out on another

+ Organized on a systematic way, these forwarding nodes form a `switched network`

  ![switched network](https://lh6.googleusercontent.com/lRagHzKyDYZ4dneOKUV4litFhBcKofTh4-klapyqkKw1GV-LQBYHcdF-YDcen6welAbBi7yIjIL5FJ9DLTC4=w1366-h625) 

+ Nodes inside the cloud are termed `switches` whose sole function is to store and forward packets

+ Nodes outside the cloud are termed `hosts` that support users and run application programs

+ The cloud itself denotes any type of network

### Packet Switched Networks

+ Nodes in a `packet switched` network send `discrete` blocks of data to each other 
+ Blocks of data corresponds to some piece of `application data` -> file, email, image etc
+ Each block of data is referred to as a `packet` or `message`

#### Store and Forward Strategy

+ Used by packet switched networks
+ Each node in a network using this strategy:
  + Receives a complete packet over some link
  + Stores the packet in its internal memory
  + Forward complete packet to next node

### Internetwork Networks

+ Internet

+ Indirect connection between a set of computers through the interconnections between a set of networks

  ![internet](https://lh3.googleusercontent.com/FcJWJ4Hy8DXOSU-EwN2h8Y4GlgJt6ZY5JjLdtfoSVLHuKm0sPYECiq10HPEO5vFPTxQwQwdASoc_tK4Q6zHB=w1366-h568)

+ A node that is connected to two or more networks is termed a `router` or `gateway`

+ Forwards messages from one network to another

+ An arbitrarily large network can be built by interconnecting smaller networks to form much larger networks

### Host - to - Host connectivity

+ Each node in a network must be able to say which of the other nodes on the network it wants to communicate with
+ An address is therefore assigned to each node
+ `Address` is a byte string used to ID a node
+ A network can use a node's address to distinguish it from other nodes connected to the network
+ If a sending and receiving node are not directly connected, then then the switches and routers of the network use the adresses to decide how to forward the message toward the destination
+ The process of determining systematically how to forward messages toward the destination node based on its address is  called `routing`

### Casting

+ Source node sends a message to a single destination node -> `unicast`
+ Source node sends a message to some subset of the other nodes, but not all -> `multicast`
+ A network bust support `multicast` and `broadcast`adresses



## Cost - Effective Resource Sharing

+ Standard: Given a collection of nodes indirectly connected by a nesting of networks, it is possible for any pair of hosts to send messages to each other across a sequence of links and nodes.
+ The goal is to provide all pairs of hosts with the ability to exchange messages

### Multiplexing

+ A system resource is shared among multiple users
+ Akin to a physical CPU shared among multiple jobs.
+ Data being sent by multiple users can be multiplexed over physical links that make up a network

![mutliplex](https://lh6.googleusercontent.com/-egBMym4NXXfg3EXYgWvf8x8j1tfnqu0vo1N818c-Juo7lIrV6VXEieP0B_sxB06PyK2n8gi65qlzfuHj25f=w1366-h625)

+ Consider the simple network above:
  + Three hosts on the left: L1, L2, L3
  + Three hosts on the right: R1, R2, R3
  + The three hosts on the left are sending data to the three hosts on the right by sharing a switched network containing only one physical link
  + Assume: L1 -> R1, L2 -> R2, L3 -> R3
  + In this situation:
    + Three flows of data - corresponding to the three airs of hosts
    + Are multiplexed onto a single physical link by Switch 1
    + Then demultiplexed back into seperate flows by Switch 2

## Methods of Multiplexing

### Synchronous Time - Division Multiplexing (STDM)

+ Divide time into equal sized quanta and in a round robin fashion, give each flow a chance to send its data over the physical link
+ Example:
  + During t_1, data from flow_1 is transmitted
  + During t_2, data from flow_2 is transmitted
  + During t_3, data from flow_3 is transmitted
+ This process continues until all the flows have had a turn, at which the first flow gets to go again, and the process repeats

### Frequency Division Multiplexing (FDM)

+ Transmit each flow over the physical link at a different frequency, similar to how different TV stations are transmitted at different frequencies on a physical cable TV link

### Statistical Multiplexing

+ Similar to STDM in that the physical link is shared over time
  + Data from one flow is transmitted over the physical link
  + Then data from another flow is transmitted, and so on
+ Unlike STDM, data is transmitted from each flow on demand rather than during a predetermined time slot
+ If only one flow has data to send, it gets to transmit that data without waiting for its TQ to come around and reduce idle time
+ However, Statistical Multiplexing (SM) has no mechanism to ensure that all the flows eventually get their turn to transmit over the physical link
  + Once a flow begins sending data, there needs to be some way other flows can have a turn
+ To account for this, SM defines an upper bound on the size of the block of data that each flow is permitted to transmit at a given time
+ Limited size block referred to as a packet
+ A host may not send a complete message in one packet
+ Source fragments message into several packets
+ Receiver reassembles the packets back into original message
+ Each flow sends a sequence of packets over the physical link, with a decision made on a packet by packet basis as  to which flow's packet to send next

![smm](https://lh5.googleusercontent.com/bFMOBktn06MSOMDarhB0AockIfEWBtjwBBTkRxyH315tDgWNPjiMYMo_j3u2MhPOkaZgmS6c7iapJSNmRSvY=w811-h625)

+ Should more than one of the flows have data to send, then their packets are interleaved on the link

### Limitations of STDM and FDM

+ If one of the flows (host pairs) does not have any data to send, its share of the physical link (TQ or Fq) remains idle, even if one of the other flows has data to transmit
+ Both multiplexing strategies are limited to situations in which the maximum number of flows is fixed and known ahead of time

### Packet Choice Decisions

+ In a network consisting of switches interconnected by links, the decision would be made by the switch that transmits packets onto the shared link as to which packet from a source flow gets to be sent first.
+ A switch could be designed to service packets on a FIFO basis.
+ Or the packets from different flows could be services in a RR manner
+ Since the switch has to multiplex many incoming packet streams onto one outgoing link, it is possible that the switch will recieve packets faster than the shared link can accomadate.
  + Thus the switch will be forced to buffer these packets in its memory
  + If the buffer space runs out some packets will have to be dropped
  + A switch operating in this state is said to be congested

## Channels

+ A network provides a logical channel over which application-level processes can communicate with each other
+ Think of a channel as connecting one process to another
+ A network provides a variety of different types of channels, with each application selecting the type that best meets its needs

## Common Communication Patterns

### File Access Programs

+ FTP and NFS (Network File System)
+ Processes:
  + Process 1: request that a file be read or written
  + Process 2: Honors the request of Process 1
+ Client: The process that requests access to a file
+ Server: The process that supports access to a file
+ Reading a files:
  + Client sends small request message to server
  + Server responds with a large message that contains the data in the file
+ Writing a file:
  + Client sends a large message that contains the data to be written to the server
  + Server responds with a small message confirming that the write to disk has taken place
+ A request/reply channel used by file transfer applications would guarentee that every message sent by one side is received by the other side and that only one copy of each message is delivered
+ A message stream channel used by video-on-demand  and video conferencing applications must be parameterized to support both one-way and two-way traffic and support different delay properties
  + Message stream channel might not need to guarantee that all the messages are delivered, since a video application can operate adequately even if all the frames are not received.
  + It would need to ensure that those messages that are delivered arrive in the same order in which they were sent, to avoid displaying frames out of sequence
  + Multicast might also need to be supported so that multiple parties can participate

## Network Architecture

+ Guide the design and implementation of networks

### Layering and Protocols

+ Abstraction of network services leads to layering
+ Start with services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service
+ Services provided at the higher layers are implemented in terms of the services provided by the lower layers

![arch](https://lh3.googleusercontent.com/WtQeroq50gdy7v5Kmv-hIToqGMhO0lpStZtMpQ23ebKgFAgD3wLXd2qHH7tH24ThDc91D40KV4E4UrK7iRbK=w811-h625)

+ Layering decomposes the problem of building a network into more manageable components.
+ Several layers, each of which can solve one part of a large problem
+ Layering provides a more modular design. When new services need to be added, one needs to modify the functionality at one layer and reuse the functions at other layers

![arch2](https://lh6.googleusercontent.com/HP2z9LLIte5wcG7rG1SLZSuZe3561aKpPlI8GDgAzGcDWJcCFygSHuVxCeTwHFTmfD_YBvygFlRY_O7G6hFZ=w811-h625)

+ Each layer might also have multiple abstractions each providing a different service to the higher layers but building on the same low-level abstractions
+ The abstract objects that make up the layers of a network system are called `protocols`
+ A protocol provides a **communication service** that higher level objects (application processes or higher level protocols) use to exchange messages
+ Objects within differing layers may communicate with each other using a `protocol`

+ Each protocol defines two different interfaces:
  + Service interface to other objects on the same computer that want to use its communication services
    + Defines the operations that local objects can perform on the protocol
    + A req/reply protocol would support operations by which an application can send and receive messages
    + So objects on the same PC can make use of the send/receive message service provided by the request/reply protocol
    + Other objects may be in different layers as well
  + Peer interface to a counterpart peer on another machine
    + Defines the form and meaning of messages exchanged between protocol peers to implement the communication service
+ A protocol defines a `communication service` that it exports locally **(service)**, along with a `set of rules` governing the messages that the protocol exchanges with its peers **(peer)** to implement the service

