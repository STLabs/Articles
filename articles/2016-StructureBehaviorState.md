# Structure Behavior State The Three Axis of Software
Amber Star - 2016

I like to think of software as having three axis: structure, behavior, and state. Thinking in these terms helps to reason about these different aspects of the system. An analogy would be a factory. A factory has a building,  equipment to produce a product, and products that it produces.

Structure is the building of the factory. The containers, the abstractions, the boxes on the whiteboard. 

Behavior is the process of a factory, the robots, the assembly line, the workers. Behavior in the system is the functions that take the current state and produce a new state.

State, is the product in the factory at all of its stages. The raw materials, components, and parts along the way to becoming the product. 

State flows through the structure like an assembly line in a factory, and is acted upon by the behavior or functions of the system.

Thinking about software as structure, behavior, and state is useful when trying to decide what is functional and what is imperative. Ask yourself, is this part of the structure, state, or the behavior.

In Swift I find that I want my structure to be classes, my state to be structs, and my behavior to be pure functions whenever possible. I pass state in to my components where they are acted upon by the behavior. 