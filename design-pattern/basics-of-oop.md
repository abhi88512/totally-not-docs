**Summary of Object-Oriented Programming (OOP) Concepts**

**1. Core Concepts of OOP:**
- **Objects and Classes**: OOP revolves around objects, which are instances of classes. A class is a blueprint defining attributes (fields) and behaviors (methods) of objects. For example, a `Cat` class might have fields like name, sex, age, and methods like `meow()` or `eat()`. Objects like Oscar or Luna are instances of the `Cat` class with specific attribute values.
- **State and Behavior**: Fields store an object’s state (e.g., a cat’s age or color), while methods define its behavior (e.g., how it meows or runs).

**2. Class Hierarchies:**
- Classes can be organized into hierarchies. A superclass like `Animal` defines common attributes (e.g., name, age) and behaviors (e.g., `breathe()`, `sleep()`) for subclasses like `Cat` or `Dog`. Subclasses inherit from their superclass and can add or override specific behaviors (e.g., `Cat` has `meow()`, `Dog` has `bark()`).
- Hierarchies can extend further, e.g., an `Organism` superclass for `Animal` and `Plant` classes. Subclasses inherit all properties from their parent classes.

**3. Pillars of OOP:**
- **Abstraction**: Simplifies real-world objects by modeling only relevant attributes and behaviors in a specific context. For example, an `Airplane` class in a flight simulator focuses on flight details, while in a booking app, it focuses on seat availability.
- **Encapsulation**: Hides an object’s internal state and behaviors, exposing only a public interface (e.g., a car’s engine is hidden, but you interact via a key or pedal). Fields are made private or protected, accessible only within the class or its subclasses. Interfaces define interaction contracts without exposing internal details.
- **Inheritance**: Allows a subclass to extend a superclass, reusing its fields and methods while adding or overriding specific functionality. Subclasses inherit the superclass’s interface, and a class can implement multiple interfaces but typically extends only one superclass.
- **Polymorphism**: Enables objects to be treated as instances of their superclass or interface, with the program executing the correct subclass method at runtime. For example, calling `makeSound()` on an `Animal` object will invoke `meow()` for a `Cat` or `woof()` for a `Dog`.

**4. Relations Between Objects:**
- **Dependency**: A weak relationship where changes in one class (e.g., `Course`) may affect another (e.g., `Professor`). Using interfaces or abstract classes reduces dependency strength.
- **Association**: A stronger relationship where one object interacts with another, often via a field or method (e.g., a `Professor` has a `Student` field). It implies a persistent link.
- **Aggregation**: A “whole-part” relationship where one object contains others, but components can exist independently (e.g., a `Department` contains `Professors`). Shown in UML with an empty diamond.
- **Composition**: A stricter form of aggregation where components cannot exist without the container (e.g., a `University` consists of `Departments`). Shown in UML with a filled diamond.
- **Implementation**: A class implements an interface’s methods (e.g., `Airplane` implements `FlyingTransport`’s `fly()` method), allowing objects to be treated as the interface type.
- **Inheritance**: A subclass inherits and extends a superclass’s interface and implementation.

**5. UML Diagrams**:
- UML diagrams visualize classes, their attributes, methods, and relationships (e.g., inheritance, association). They may simplify details to focus on relationships or show quantities in aggregations/compositions.

**6. Key Takeaways**:
- OOP organizes code into objects and classes, promoting modularity and reuse.
- Class hierarchies and inheritance enable code reuse and specialization.
- The four pillars (abstraction, encapsulation, inheritance, polymorphism) distinguish OOP from other paradigms.
- Relationships like dependency, association, aggregation, and composition define how objects interact, with varying strengths and implications.

