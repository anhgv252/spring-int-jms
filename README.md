spring-int-poc
=====================

Spring Integration project depicting async request/reply with jms.  The main challenge that this project attempts to solve
is the implentation of request reply are disconnected by calling a TCP async service whereby the original jms request headers
would not be able to be passed into the message going over the TCP based network.  The Spring Integration examples depict JMS
centric request replies using Gateways but in this case I am trying to depict disconnected async request reply where a message
starts in the JMS world and traverses a TCP async request response whereby the original JMS client request needs to receive a response
on a particular named reply queue.

Props to Ganesh Rajuladevi for taking the xml based config and converting the Spring Integration usage to java based Spring Configuration.  Note that 
the client and server-mid have both xml and @Configuration based methods of instantiation.

There are 3 sub-projects within this application:

- client
   The client serves to generate business objects each with a unique id and push them to an ActiveMQ queue.  The client
   also creates a reply queue which is in turn created on ActiveMQ vs using temp queues for each request.  The
   jms replyTo and jms correlationID are used respectively to route the message back to the request client and or
   client thread. 

- server-mid 
  This tier serves as a server and consumer for the jms messages pushed to the request queue by the client tier.
  The mid tier pulls messsages from the request queue and puts the orginal header into a ConcurrentHashMap before
  the message is sent over TCP to the server-netty tier.  When the async reply comes back via Netty an application
  generated message id is used to retrieve the original headers from the request message to properly create
  the response using jms correlation id and jms replyTo. 

- server-netty
  This is simply a netty echo server pulled from the examples and is simply used to simulate a TCP endpoint.

See the respective mark down files within the 3 subprojects.
