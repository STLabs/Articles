# The Component Pattern

The Component Pattern is a pattern I have identified in well structured systems. Software systems are a combination of structure, behavior, and state. Components define the structure of software systems. They are objects that have Actions, and Events. Components of a system are composed together in the pattern shown below. 
The goals are: 

![](../resources/images/ComponentPattern.jpg)



 A system composed from components. Arrows pointing in represent action methods. Arrows pointing out represent events. Outer component reacts to events of inner components. This keeps dependencies pointing inward. With composition of calls made inward, and events outward, no inner component is dependent on an outer component. Because the dependencies flow in the direction of composition of the system , the dependencies are inherent in the system itself.


The pattern is for composing software from "Components". It is intentionally simple and abstract and doesn't require a library or a framework. It is just an idea.

There are two primary underlying principles: 
1. Software has three distinct axis: Structure, behavior, and state.
2. Programming is an art of organization. Good structure supports good organization.

The pattern asserts that an ideal system is composed as one hierarchy of components. 


## What is a component?
A component is any composable type that has inputs and outputs  

###Components vs. Objects

* a component does not have methods that return values.
* a component does not have public properties (because that is a method that returns a value.


### Components vs. Functions
A function is a component with 1 input and 1 output. A component has N inputs, and N outputs.

### Components vs. Value types
A mutable value type can be a component. Mutating functions can be considered inputs (if they do not return values). The output of a value type component is itself upon mutation. 

### Components vs. UI Components
A component is not specific to UI,  although some components can be UI components.

###02/11/2016 

I was describing some rules for a UI design pattern and it occurred to me that these rules apply universally to the component pattern.

A component's responsibilities are: 

- Connect it's sub-components (often done when component starts)
- Listen to it's own inputs
- Send to it's sub-components inputs
- Listen to it's sub-components outputs
- Send to it's own outputs


By definition, a component owns it's sub-component's inputs and outputs. That said, what a component **doesn't do** is :
- listen to outputs it does not own.
- Sent to inputs it does not own.


Data should flowing in the direction of the components composition.

As stated before : 
> Because the dependencies flow in the direction of composition of the system , the dependencies are inherent in the system itself.
