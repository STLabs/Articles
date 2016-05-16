#Messaging

### Why components need outputs, not public methods and properties.

When asked about the meaning of Object Oriented Programming Alan Kay once said: 

>> *"OOP to me means only messaging, local retention and protection and
 hiding of state-process, and extreme late-binding of all things"*
 
What is wrong with messaging in common OOP is that objects communicate across their boundaries and only at the request of the receiver. 

So a receiver has to ask another object for it's state when it needs it. The source of facts sends the state back to caller at the time of request, not at the time of truth.

Software is a process so any recorded data in the system is potentially suspect. It's a slice in time. Therefore we are trying to make a process by time slicing back in time, hoping that facts are correct.

In OOP objects communicate on the basis of recorded facts. Messaging on the other hand is about communicating the facts as they are true. To that end what is important are the following:

1. The existence of an output in context of some structure. (components) delivered as facts occur.
2. The intention of the receiver to receive that output as facts occur.

Public methods and properties do not provide these, and is why components have outputs.


 
 