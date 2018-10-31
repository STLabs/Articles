# Views are controls
Amber Star - 2016

Ever wonder why the web seems to have such an elegant architecture? One reason is that the view layer is decoupled from everything else.

The way the web works, inherently enforces a clean separation of the presentation layer from the rest of the architecture. A web browser makes a request to the server, the server accesses the database, and returns a result which is rendered in the browser. 

It turns out this is exactly the right way to think about any application architecture. If you are able to get the view layer decoupled from the application logic, and data layers, you are on the path to a clean architecture.

We've all heard about or experienced the "Massive View Controller" problem in iOS. The problems stems from putting application logic in view controllers. View controllers become filled with this logic making it hard to test your logic, and also kind of makes it hard to pull that logic out later when you want to refactor your application.

So, what's the cleanest way to separate the view layer in your app from the rest of the logic and data layers? It's clearly a problem that a lot of thought is going into. There are all kinds of patterns and names being invented around this problem. But the reality is, it boils down to this simple principle. 

####Views are just controls
Treat everything visual in your app as a control. I refer to these as components. Think of the entire screen as a control. Just like any other control in Cocoa. What is unique about controls? They have properties that change their visual presentation, and they have actions. In other words, they have inputs and outputs, but other than that they are encapsulated. That's all a view really is. A thin layer that presents information in some visual way, and they have actions the user can invoke.

I'd like to see Cocoa allow us to define components like controls easier. If components, and events where first class citizens in Cocoa we could define a new component, give it properties and events, and wire them up to IBActions just like we can with Cocoa controls. This would eliminate the whole idea of ViewControllers entirely, allowing re-use of distinct UI.

But the idea goes further. Components should not be limited to just UI. Any element that has observable events I consider a component. More on that in a future article.
