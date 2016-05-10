#Messaging

When asked about the meaning of Object Oriented Programming Alan Kay once said: 

>> *"OOP to me means only messaging, local retention and protection and
 hiding of state-process, and extreme late-binding of all things"*
 
What is wrong with messaging in common OOP is that objects communicate across their boundaries and only at the request of the reciever. 

So a receiver has to ask another object for it's state when it needs it. Then the source object sends the state back to caller.

Software is a process so any recorded data in the system is suspect. It's a slice in time. Therefore what is an objects method giving back to the caller? We are trying to make a process by time slicing back in time, hoping that facts are correct.

So OOP works on the basis of recorded facts. Messaging on the other hand is about communicating the facts as they are true.

You can't get facts as they are true by requesting them on demand.

This is why the "Reaction" is the least important part of FRP. What is significant and what is important is the following:

1. The existence of an output in context of some structure. (components) delivered as facts occur.
2. The intention of the receiver to revieve that output


For a while I have had a sense that return values on public methods breaks.it is do to public methods returning values, but could not pin down in clear terms why.

Functional Reactive Programming has seemed to provide what is missing. However signals just do not seem correct, and certainly observable is dis-honest. Signals lack context or structure.






 
 