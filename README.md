spring-int-poc
=====================

Spring Integration project depicting async request/reply with jms.

There are 3 sub-projects within this application:

-client
   The client serves to generate business objects each with a unique id and push them to an ActiveMQ queue.  The client
   also creates a reply queue which is in turn created on ActiveMQ vs using temp queues for each request.  The
   jms replyTo and jms correlationID are used respectively to route the message back to the request client and or
   client thread.  There are 2 different


See the respective mark down files within the 3 subprojects.
