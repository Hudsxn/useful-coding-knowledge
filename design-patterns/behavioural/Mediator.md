## Mediator

The Mediator design pattern is a behavioral pattern that promotes loose coupling among a set of objects by centralizing their communication through a mediator object. In this pattern, objects do not directly communicate with each other but instead communicate through the mediator, which encapsulates the interaction logic.

The main idea behind the Mediator pattern is to reduce the complexity and dependencies between interacting objects by introducing a mediator that coordinates their interactions. This promotes better maintainability, scalability, and flexibility of the system as changes to one object or its interactions do not directly impact other objects.

Key components of the Mediator pattern include:
- Mediator: Defines an interface for communicating with colleague objects and manages their interactions.
- Colleague: Represents objects that interact with each other through the mediator. Colleague objects delegate their communication to the mediator instead of directly interacting with each other.

**Example in Java:**

Let's consider a simplified example of an air traffic control system, where multiple flights need to coordinate their landing and takeoff times to avoid collisions. In this scenario, we can use the Mediator pattern to manage the communication between the flights (colleagues) through the air traffic control mediator.

```java
import java.util.ArrayList;
import java.util.List;

// Mediator interface
interface ATCMediator {
    void registerFlight(Flight flight);
    void sendMessage(String message, Flight flight);
}

// Concrete mediator class
class ATCControlTower implements ATCMediator {
    private List<Flight> flights;

    public ATCControlTower() {
        this.flights = new ArrayList<>();
    }

    @Override
    public void registerFlight(Flight flight) {
        this.flights.add(flight);
    }

    @Override
    public void sendMessage(String message, Flight flight) {
        System.out.println("Message from ATC: " + message);
        for (Flight f : flights) {
            if (f != flight) {
                f.receiveMessage(message);
            }
        }
    }
}

// Colleague interface
abstract class Flight {
    protected ATCMediator mediator;

    public Flight(ATCMediator mediator) {
        this.mediator = mediator;
    }

    public abstract void send(String message);
    public abstract void receiveMessage(String message);
}

// Concrete colleague class
class BoeingFlight extends Flight {
    public BoeingFlight(ATCMediator mediator) {
        super(mediator);
    }

    @Override
    public void send(String message) {
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println("BoeingFlight received: " + message);
    }
}

// Concrete colleague class
class AirbusFlight extends Flight {
    public AirbusFlight(ATCMediator mediator) {
        super(mediator);
    }

    @Override
    public void send(String message) {
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println("AirbusFlight received: " + message);
    }
}

// Main class
public class MediatorPatternExample {
    public static void main(String[] args) {
        ATCMediator mediator = new ATCControlTower();
        Flight boeingFlight = new BoeingFlight(mediator);
        Flight airbusFlight = new AirbusFlight(mediator);

        mediator.registerFlight(boeingFlight);
        mediator.registerFlight(airbusFlight);

        boeingFlight.send("BoeingFlight requesting landing clearance.");
        airbusFlight.send("AirbusFlight requesting takeoff clearance.");
    }
}
```

In this example, the `ATCMediator` interface defines methods for registering flights and sending messages. The `ATCControlTower` class acts as the concrete mediator that coordinates communication between flights.

The `Flight` abstract class represents the colleague objects, which are the BoeingFlight and AirbusFlight classes in this example. Each flight delegates communication to the mediator through the `send` method.

When a flight sends a message, the mediator (ATCControlTower) relays the message to all other registered flights except the sender. This way, flights communicate indirectly through the mediator without having direct dependencies on each other.