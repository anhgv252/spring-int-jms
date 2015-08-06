# Spring Integration Sample

This represents the receiving side of an async request/reply usage of Spring Integration
delegating to ActiveMQ.

The business logic (SwitchMessageHandler) uses Spring Integration annotations (@MessagingEndpoint and
@ServiceActivator).  The important consideration is that the remoting interface and
implementation (in this case JMS) are abstracted behind Spring Integration Channel and
Gateway semantics.

Note that the replyTo channel and or queue are not specified within configuration as Spring Integration
is able to understand and use the JMS replyTo field within the underlying
JMS message.

Run the application:

1) edit the src/main/resources/application.properties file and edit the:
   broker.url for your intance of ActiveMQ.

2) Run the main method within the com.companyx.harness.ServerXmlDriven class.

3) Start the client application and run it.  Stdout messages will appear within this application's
   stdout.
