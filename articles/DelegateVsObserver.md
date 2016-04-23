# Delegate vs. Observer, It's all messaging

Sometimes we tend to get caught up in the words we use. Observers, Delegates, Notifications, Reactive. Sometimes the only difference between these ideas are where the code ends up in the source files. Perhaps that is where we should start to reason about them. What will make the code clearer?


For example, let's look at how we can implement reactive notification in Swift without the baggage of any library.

```swift
protocol ModelDependent {
    var state: ModelState { get, set }
}

struct Model {
    var dependent: ModelDependent
    var state: ModelState {
        didSet {
            dependent.state = state
        }
    }
}

class ViewController : UIViewController, ModelDependent {
    var state: ModelState {
        didSet {
           updateViewWithState(state)
        }
    }

    func updateViewWithState(state: ModelState) {
        // configure view
    }
}
```


All we need is:
1. A protocol to abstract away the model dependent 
2. The local `didSet` observer on the `ViewController.state` property

When the model dispatches the state to the view it is updated accordingly. The update is triggered by the `didSet` observer on the `ViewController.state` property. No external observer pattern is necessary. No subscription, no KVO.

We should always try to channel state through a responsible actor in the system. For example, above the `updateViewWithState` method, may forward state to some of it's sub components. Letting a sub-component observe above it's parent is not necessary, and it entangles the structure of the software.


Figure out what makes the code clearer. Often you will find that Observer patterns tend to put code in bad places, such as in initialization of views defined in  closures. It may be boring, but there is nothing clearer than a good old type calling a function on another type. Don't give fancy words more meaning then they deserve, it's all just messaging. 