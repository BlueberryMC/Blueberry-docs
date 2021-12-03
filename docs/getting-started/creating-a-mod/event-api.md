# Event API

## Using class (object) listener

```java title="SomeListener.java"
import net.blueberrymc.common.bml.event.EventHandler;
import net.blueberrymc.common.bml.event.Listener;
import net.blueberrymc.common.event.mod.ModReloadEvent;

public class SomeListener implements Listener {
  @EventHandler
  // the method can be static, or instance (non-static) method
  public static void onReload(ModReloadEvent e) {
    // do something when user has clicked "Reload" button on mod list screen
  }
}
```

```java title="ExampleMod.java"
import net.blueberrymc.common.Blueberry;
import net.blueberrymc.common.bml.BlueberryMod;

public class ExampleMod extends BlueberryMod {
  @Override
  public void onPreInit() {
    Blueberry.getEventManager().registerEvents(this, new SomeListener()); // don't forget to register listener!
  }
}
```

## Using functional-style listener

```java title="ExampleMod.java"
import net.blueberrymc.common.Blueberry;
import net.blueberrymc.common.bml.BlueberryMod;
import net.blueberrymc.common.bml.event.EventPriority;
import net.blueberrymc.common.event.mod.ModReloadEvent;

public class ExampleMod extends BlueberryMod {
  @Override
  public void onPreInit() {
    Blueberry.getEventManager().registerEvent(ModReloadEvent.class, this, EventPriority.NORMAL, e -> {
      // e: ModReloadEvent
    });
  }
}
```

## Event Priority
Every event listener has an `EventPriority` (defaults to `NORMAL`), which will control the order in which listeners are invoked when firing an event.
Listeners using `EventPriority.LOWEST` are called first, then VERY_LOW, LOW, NORMAL, etc.

When using an object listener, you can change the priority by providing a value to `@EventHandler`:
```java title="SomeListener.java"
@EventHandler(priority = EventPriority.LOW) // register a listener with low priority
public static void onReload(ModReloadEvent e) 
  // ...
}
```

When using a functional-style listener, you can change the priority easily:
```java title="ExampleMod.java"
@Override
public void onPreInit() {
  Blueberry.getEventManager().registerEvent(ModReloadEvent.class, this, EventPriority.LOW, e -> { // register a listener with low priority
    // ...
  });
}
```

## Implementing your own event

To create a event, you need to:

- create a class which extends `Event`
- define static `getHandlerList()` which returns HandlerList as a result

Simplest event implementation would be:
```java title="SomeEvent.java"
import net.blueberrymc.common.bml.event.Event;
import net.blueberrymc.common.bml.event.HandlerList;

public class SomeEvent extends Event {
    private static final HandlerList HANDLER_LIST = new HandlerList();

    public static HandlerList getHandlerList() {
        return HANDLER_LIST;
    }
}
```

By default, the event is called synchronously. This means you can only fire the event on main thread.

If any of these thread name conditions are met when the event is fired, the event would be considered synchronous:

=== "Client"
    - Render Thread*
    - Server Thread
    - main

=== "Server"
    - Server Thread*
    - main

<small>*Marked with `*` are matched by its reference (`Thread.currentThread() == thread`), not name*</small>

These thread are considered *asynchronous* (anything which does not meet the condition above):

- Netty Client IO
- Netty Server IO
- Netty Epoll IO
- Worker-Main-n
- Worker-Bootstrap-n

If defined type (asynchronous or synchronous) does not match the runtime thread, the event manager will throw exception.

To change the type, you can modify the constructor (in this example, the event is set to async):
```java title="AsyncXEvent.java"
import net.blueberrymc.common.bml.event.Event;
import net.blueberrymc.common.bml.event.HandlerList;

public class AsyncXEvent extends Event {
    private static final HandlerList HANDLER_LIST = new HandlerList();

    public AsyncXEvent() {
      super(true); // async: true
    }

    public static HandlerList getHandlerList() {
        return HANDLER_LIST;
    }
}
```

Or, you can do this to determine type at runtime (may be useful for events which may be called from both synchronous and asynchronous):
```java title="MysteryEvent.java"
import net.blueberrymc.common.bml.event.Event;
import net.blueberrymc.common.bml.event.HandlerList;

public class MysteryEvent extends Event {
    private static final HandlerList HANDLER_LIST = new HandlerList();

    public MysteryEvent() {
      super(!Blueberry.getUtil().isOnGameThread());
    }

    public static HandlerList getHandlerList() {
        return HANDLER_LIST;
    }
}
```
