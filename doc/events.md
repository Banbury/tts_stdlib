# events
A library for sending events between objects.
Events can be sent between objects, to and from Global and to the sender itself.

## Usage
Include the file ```eventhandler``` in the Global script.

```lua
#include !/events/eventhandler
```

Every object, that wants to send or receive events, has to include the file ```events```.

```lua
#include !/events/events
```

The event handler needs to be started in the Global script.

```lua
function onLoad()
    EventHandler.start()
end
```

The Global script will always receive all events. Objects have to subscribe to the event handler to receive events.

```lua
function onLoad()
    Event.subscribe()
end
```

In order to receive an event, a function needs to be registered with the event handler.

```lua
Event.register("onDoSomething", onDoSomething)
```

The Global script has to call the ```register``` function in ```EventHandler```.
```lua
EventHandler.register("onHelloWorld", onHelloWorld)
```

To send an event call the ```send``` function.
```lua
Event.send("onHelloWorld", { name="World" })
```

The Global script again has to use the equivalent function in ```EventHandler```.
```lua
EventHandler.send("onGlobalHelloWorld")
```

Events are identified by their name. So you cannot have two events with the same name.

Events can send a table of arguments to the receiver.

An event handling function has a single parameter, that contains:
* ```guid```: The id of the sending object. Contains 'Global' if the event is sent by the Global script.
* ```event```: The name of the event.
* ```args```: The table of arguments given with the ```send``` function.

```lua
function onHelloWorld(args)
    print("Hello " .. args.args.name .. "!")
end
```
