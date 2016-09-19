# The Component Pattern [Beta 0.1]
 There are two primary underlying principles:

1. Software has three distinct axis: structure, behavior, and state.
2. Programming is an art of organization. Good structure supports good organization.

The component pattern is a pattern for creating well structured software. The pattern asserts that an ideal system is composed as one hierarchy of components, starting with the application component. It is intentionally abstract and doesn't require a library or a framework.

![](../resources/images/ComponentPattern.jpg)

 Components define the structure of software and are are composed together as shown in the diagram above. Arrows pointing in represent input. Arrows pointing out represent output. Outer components are parent components of inner components. This keeps dependencies pointing inward and output outward.  No inner component is dependent on an outer component until it is in the context of it's parent. Because the dependencies flow in the direction of composition of the system , the dependencies are inherent in the system itself.
 
## What is a component?
1. A component is any composable type  that has input, a process, and output. (note: while a component may have multiple inputs and outputs, for reasoning purposes we consider the entire set of inputs and outputs as a whole.)
2. Child components are inherently dependent on facts provided by input from it's parent.
3. Parent components are inherently interested in the facts provided by the output of it's child components.
4. In the component pattern everything is a component. It is not specific to UI. For example the application is a component.

 ![](../resources/images/Composition2.png)
 
## Composition
Components are composed of sub-components as shown above. The Y axis represents composition. A component receives input, some process happens, and it produces output at some point in time. This is represented by the X axis. Each child components input is a mapping of it's parent's input. Each child components output is reduced into the parents process and may produce output. 
 
  -  Input  = ParentInput -> ChildInput
 
  -  Output = ParentInput, ChildOutput -> ParentOutput? 

### State

Keep in mind, when we talk about state in components we are interested in the transient state. Whether or not a component has internal stored state does not matter.

An entire application is a component that takes it's initial state as input, and produces new state at some point in time. If we reason about this further, we can determine that any sub-component of the application is inherently dependent on the application state or the component wouldn't be necessary! In theory, all components in an application are a function of the same total state. AppState -> AppState.

It would not make sense to write every component specific to an application. Components do something specific and we want to re-use them. Therefore, we make components work with  specific state. But how do we bridge from the parent component's state to it's subcomponents specific state? This is what is most important about this pattern. Where truth comes from, and where resulting updates flow.

In theory every subcomponent's input is a mapping of it's parent's state. And every subcomponent's output causes an update to it's parent. In the diagram above this is shown in the yellow as Map, and Reduce. All child input is a mapping of parent input. Even if the component takes no input, in theory it is a map of ParentState -> (). All child output is a reduce or fold into it's parent's process and may cause the parent to output. So parent output is a function of (PreviousParentState, ChildOutput) -> NewParentState

Not all components require input or have output. But it's always in the context of it's parent  that makes their use interesting to the application. Maintaining these relationships are the constraints of this pattern.

Keep in mind, this is theory. How it is expressed and implemented is flexible.

###Messaging and The Significance of an "Output"

#### Why components have outputs, not public methods and properties. AKA, why return values are harmful to software structure.

When asked about the meaning of Object Oriented Programming Alan Kay once said: 

>> *"OOP to me means only messaging, local retention and protection and
 hiding of state-process, and extreme late-binding of all things"*
 
What is wrong with messaging in common OOP is that objects communicate across their boundaries and only at the request of the receiver. 

So a receiver has to ask another object for it's state when it needs it. The source of facts sends the state back to caller at the time of request, not at the time of truth.

Software is a process so any recorded data in the system is potentially suspect. It's a slice in time. Therefore we are trying to make a process by time slicing back in time often using past truths that may or may not be in sync, hoping that facts are correct.

In OOP objects communicate on the basis of recorded facts. Messaging in the component pattern on the other hand is about communicating the facts as they are true. To that end what is important are the following:

1. The existence of an output in context of some structure. (components) delivered as facts occur.
2. The intention of the receiver to receive that output as facts occur.

Public methods and properties do not provide these, and is why components have outputs.

---

## Notes

### May 29, 2016
This is a learning project for me.  These ideas were developed in my own work.  I then discovered others seemingly working on these ideas as well.  I have not seen this pattern spelled out, so I decided to take notes and share the ideas I have. Whether or not it is correct or perfect, I don't know. I iterate ideas by trying to prove them wrong. So far this has proven to be a useful pattern in my work, but it's still evolving.

[Elm](http://elm-lang.org) is a very close implementation of this pattern. [Cycle.js](http://cycle.js.org) is another. [React/Redux](https://facebook.github.io/react/index.html) is also. However in my implementation of this pattern components are not just UI specific. Recently React added higher order components too. Another interesting similar implementation of this pattern is [Flutter](https://flutter.io). 


## A thought experiment for fun.
Imagine we have a set of boxes, and in the one side of each box was a fitting labeled input, and on the other side of the box had a fitting labeled output.

We also have a set of hoses that can connect to the fittings.  Now if we connect all the boxes together with the hoses, so that when we add input into the outer box, new output comes out the other fitting of the same box. 

You can't stick a hose through the side of the box, reach in and get output, and thread the hose back out the same side! It's physically impossible. Yet that is what we do all the time in software. In the physical world you can't get it wrong, or you can at least easily tell when you do, but in the software world you can get it wrong and it is hard to tell.


### Feb 11, 2016

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

### 05/27/2016 [DRAFT]
### 3 Dimensional Data Flow in the X Y and Z axis.
We can think of the the component pattern in 3 dimensions. 

1. The Y axis represents composition and data flow from parent to child.
2. The X axis represents connection and processing on the primary thread. 
3. The Z axis represents asynchronous processing on a secondary thread, emanating from and back to the XY plane.

If a component needs to do asynchronous processing on another thread. The result comes back to the original plane, and output. For example fetching data:

1. Input comes in to request data.
2. The asynchronous process occurs in the Z axis, which is an output in that axis. ( a child component). Result or failure occurs in the Z axis. Result is output in the X axis.
