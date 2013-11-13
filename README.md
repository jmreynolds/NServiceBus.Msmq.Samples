# NServiceBus.Msmq.Samples #
----------

This repository contains the Samples for the MSMQ transport.
 
##Error Handling 

This sample demonstrates what happens when exceptions occur when messages are handled and how retries work. As a comparison, it also illustrates the behavior when the Second Level Retries (SLR) feature is turned off.

##Full Duplex

This sample illustrates the use of the request/response messaging pattern 
with NServiceBus. What you'll see is how to define messages, how to specify the
destination for a message, and how to send a message and how to handle the response. This sample also illustrates, configuration of custom logging using other log libraries such as NLog and setting up an unit of work pattern.

##Gateway

This sample demonstrates how logically different sites such as Headquarters, Stores communicate using the NServiceBus Gateway feature. This sample also demonstrates the use of the DataBus feature which enables in transferring large data. Data that needs to be transferred using the databus is defined using the DataBusProperty<T> as shown in Headquarter.Messages.PriceUpdated and the Headquarter endpoint has initialization code to setup the Databus.

##PubSub

This sample shows the use of publish subscribe messaging pattern using NServiceBus. This sample is also the "Getting Started" section of the documentation and shows polymorphic subscriptions
as well as durable subscriptions for publisher fault-tolerance.

##ScaleOut

This sample illustrates the Scale out scenario using the Distributor. It highlights how the same endpoint can be run using different feature profiles (using NServiceBus.Master and NServiceBus.Worker) to facilitate scaling out when necessary without having to change code. To scale out, all is needed is to deploy the endpoint to a different server and run using the worker profile.

##VideoStore

This sample implements the following worflow of a fictional video store. Users can order videos from the website. Once orders are submitted, there is a window of time allocated for handling cancellations due to buyer's remorse. Once the order has been accepted, they are provisioned and made available for download. In implementing the above workflow various aspects are highlighted:


- The Sales endpoint illustrates the use of the Saga pattern to handle the buyer's remorse scenario.  
The CustomerRelations endpoint illustrates how in-memory events (domain events pattern) can be defined and subscribed to.

- The request/response pattern is illustrated for the video provisioning between the ContentManagement endpoint and the Operations Endpoint.
The ECommerce endpoint is implemented as an ASP.NET MVC4 application which uses SignalR to show feedback to the user. 

- This sample also illustrates the use of Unobtrusive message conventions to let NServiceBus know in order to identify commands, events and messages defined as POCOs which avoids having to add a reference to the NServiceBus libraries in the message definition dlls.

- The use of message headers and message mutator is also illustrated when the user clicks on the Check box on the ECommerce web page, which conveniently stops at the predefined breakpoints in the message handler code on the endpoints.

- The use of encryption is illustrated by passing in the Credit Card number and the Expiration date from the ECommerce web site. The UnobtrusiveConventions defined in the ECommerce endpoint show how to treat certain properties as encrypted. Both the ECommerce and the Sales endpoint is setup for RijndaelEncryption and the encryption key is provided in the config file. If the messages are inspected in the queue, both the Credit Card number and the Expiration Date will show the encrypted values.  
