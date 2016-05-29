# The Component Pattern

The Component Pattern is a pattern in well structured systems. Software systems are a combination of structure, behavior, and state. Components define the structure of software systems. Components have inputs and outputs. Components of a system are composed together in the pattern shown below. The pattern is for composing software from "Components". It is intentionally simple and abstract and doesn't require a library or a framework. It is simply a pattern. How it is implemented is not specified.


![](../resources/images/ComponentPattern.jpg)



 A system composed from components. Arrows pointing in represent inputs. Arrows pointing out represent outputs. Outer components called parents process output of inner child components. This keeps dependencies pointing inward. With composition of input made inward, and output outward, no inner component is dependent on an outer component until it is in the context of the system. Because the dependencies flow in the direction of composition of the system , the dependencies are inherent in the system itself.
 
 There are two primary underlying principles:

1. Software has three distinct axis: Structure, behavior, and state.
2. Programming is an art of organization. Good structure supports good organization.

The pattern asserts that an ideal system is composed as one hierarchy of components. 

## What is a component?
1. A component is any composable type that has inputs and outputs.
2. Child components are inherently dependent on facts provided by it's input.
3. Parent components are inherently interested in the facts provided by the output of it's children.
4. Whether or not a component has state is irrelevant to the rest of the system. What matters is the output. 



 ![](../resources/images/Composition2.png)


Components are composed of subcomponents as shown above. A component has input and output. In this sense a component is similar to a function. It takes input, some process happens, and it produces output.  For example, the entire application is a component that takes it's initial state, and produces new state. State -> State the result is new state.

If we reason about this, we can determine that any child component is inherently dependent on it's parents state or the component wouldn't be necessary in the system. All components in an application are a function of the same total state. Technically they are all functions of AppState -> NewAppState.

It would not make sense to write every component specific to the application it happens to be in. Therefore we make components that are concerned with only the specific state they require. We call this substate. 

Because we know that a particular subcomponent plays some role in input and/or output of the entire application state, we need some way of bridging from the parent component to it's subcomponents.

Every subcomponent's input is therefore a mapping of it's parent's state. And every subcomponent's output is a reduction of the previous state, with it's output.


Although not all components require input or have output. When they do, it is the parent context that is inherently interested them.



---



###Notes:
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

### 05/27/2016 [DRAFT]
### 3 Dimensional Data Flow in the X Y and Z axis.
We can think of the the component pattern in 3 dimensions. 

1. The Y axis represents composition and data flow from parent to child.
2. The X axis represents connection and processing on the primary thread. 
3. The Z axis represents asynchronous processing on a secondary thread, emanating from and back to the XY plane.


If a component needs to do asynchronous processing on another thread. The result comes back to the original plane, and output. For example fetching data:

1. Input comes in to request data.
2. The asynchronous process occurs in the Z axis, which is an output in that axis. ( a child component). Result or failure occurs in the Z axis. Result is output in the X axis.
