# Spring Integration Sample

This represent the client side of an async request/reply usage of Spring Integration
delegating to ActiveMQ.

The business logic (AppMessageService) is an interface that is proxied within Spring via the Gateway:

    <int:gateway id="appMessageService"
                 service-interface="com.companyx.service.AppMessageServiceSync"
                 default-request-channel="requestChannel"/>

The important consideration is that the remote interface and implementation (in this case JMS)
are abstracted behind Spring Integration Channel and Gateway semantics.

Note that the replyTo is not specified within configuration as Spring Integration
is able to understand and use the JMS replyTo field within the underlying
JMS message.

The reply queue is specified within the application.properties and is a long lived queue which will be created on the brokers.
the reply queue will be removed from ActiveMQ when the client application is shutdown.  This method differs from the
default behavior of using a temp queue per request.

Run the application via either the ClientAsyncConfigurationDriven or the ClientAsyncXmlDriven classes:

1) edit the src/main/resources/application.properties file and edit the:
   broker.url for your instance of ActiveMQ.

