The four pillars of Object-Oriented Programming (OOP) are fundamental concepts that distinguish OOP from other programming paradigms. Below, I’ll define each pillar clearly and concisely, building on the provided summary for consistency and adding deeper explanations where helpful.

### 1. Abstraction
**Definition**: Abstraction is the process of simplifying complex real-world objects or systems by modeling only the attributes and behaviors relevant to a specific context, while ignoring irrelevant details.

- **Explanation**: Abstraction allows programmers to focus on essential aspects of an object for a particular use case. For example, an `Airplane` class in a flight simulator might include attributes like `altitude` and `speed` and methods like `takeOff()`, but in a flight booking application, it might only include `seatMap` and `availableSeats()`. This selective modeling reduces complexity and improves focus.
- **Key Points**:
  - Abstraction is achieved through classes, interfaces, or abstract classes that define only necessary details.
  - It helps manage complexity by hiding unnecessary details from the user or other parts of the program.
  - Example: A `Car` class might abstract away engine mechanics, exposing only `start()` and `stop()` methods for a driving app.

### 2. Encapsulation
**Definition**: Encapsulation is the ability of an object to hide its internal state and behaviors from the outside world, exposing only a controlled, public interface for interaction.

- **Explanation**: Encapsulation protects an object’s data by making fields `private` or `protected`, allowing access only through methods (getters/setters or other operations). For example, a car’s internal engine workings are hidden, but you interact with it via a key or pedals. This ensures data integrity and restricts unauthorized access. In programming, interfaces and abstract classes further support encapsulation by defining strict interaction contracts.
- **Key Points**:
  - `Private` members are accessible only within the class; `protected` members are accessible within the class and its subclasses.
  - Encapsulation promotes modularity and reduces the risk of unintended interference between objects.
  - Example: A `BankAccount` class might have a private `balance` field, accessible only through `deposit()` and `withdraw()` methods.

### 3. Inheritance
**Definition**: Inheritance is the mechanism by which a subclass inherits attributes and methods from a superclass, allowing code reuse and the creation of specialized classes.

- **Explanation**: A subclass extends a superclass, inheriting its fields and methods while optionally adding new ones or overriding existing ones. For instance, a `Cat` class might inherit from an `Animal` superclass, reusing `name` and `breathe()` while adding a `meow()` method. Inheritance ensures that subclasses maintain the interface of the superclass, promoting consistency. However, a class typically extends only one superclass (single inheritance in most languages), though it can implement multiple interfaces.
- **Key Points**:
  - Enables code reuse and establishes a "is-a" relationship (e.g., a `Cat` is an `Animal`).
  - Subclasses must implement all abstract methods inherited from a superclass.
  - Example: A `Dog` class inherits `run()` from `Animal` but overrides `makeSound()` to implement `bark()`.

### 4. Polymorphism
**Definition**: Polymorphism is the ability of objects to be treated as instances of their superclass or interface, with the program dynamically executing the appropriate subclass-specific behavior at runtime.

- **Explanation**: Polymorphism allows a program to work with objects without knowing their exact type, as long as they share a common superclass or interface. For example, an `Animal` reference can point to a `Cat` or `Dog` object, and calling `makeSound()` will invoke `meow()` or `woof()` based on the actual object type. This is often achieved through method overriding (in subclasses) or interface implementation. Polymorphism enhances flexibility and extensibility in code design.
- **Key Points**:
  - Supports "one interface, multiple implementations" (e.g., different animals make different sounds).
  - Achieved through dynamic method dispatch or interface implementation.
  - Example: A `FlyingTransport` interface with a `fly()` method can be implemented by `Airplane` or `Helicopter`, and an `Airport` class can work with any `FlyingTransport` object without knowing its concrete type.

### Summary
The four pillars—**Abstraction**, **Encapsulation**, **Inheritance**, and **Polymorphism**—work together to make OOP modular, reusable, and flexible. Abstraction simplifies design, encapsulation ensures data security, inheritance promotes code reuse, and polymorphism enables dynamic behavior. These principles allow developers to model complex systems efficiently, as seen in examples like the `Cat` and `Animal` classes or real-world systems like cars and airplanes.

Below is the **Examples** section with simple ASP.NET Core Web API (.NET 8) examples for each of the four pillars of Object-Oriented Programming (OOP), along with explanations specific to each example. You can append this directly to your existing `.md` file.

```markdown
## Examples in ASP.NET Core Web API (.NET 8)

Below are simple examples demonstrating each OOP pillar using ASP.NET Core Web API in .NET 8. Each example is minimal, self-contained, and uses a university or transportation-related domain for consistency with the provided definitions.

### 1. Abstraction
**Example**: A `Car` class abstracts away complex engine details, exposing only `Start()` and `Stop()` methods for a driving API.

```csharp
// ICar.cs
public interface ICar
{
    string Start();
    string Stop();
}

// Car.cs
public class Car : ICar
{
    public string Start() => "Car engine started.";
    public string Stop() => "Car engine stopped.";
}

// CarController.cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class CarController : ControllerBase
{
    private readonly ICar _car;

    public CarController(ICar car)
    {
        _car = car; // Dependency injection
    }

    [HttpGet("start")]
    public IActionResult StartCar()
    {
        return Ok(_car.Start());
    }

    [HttpGet("stop")]
    public IActionResult StopCar()
    {
        return Ok(_car.Stop());
    }
}

// Program.cs (Dependency Injection Setup)
builder.Services.AddSingleton<ICar, Car>();
```

**Explanation**:
- The `ICar` interface abstracts the essential behaviors (`Start` and `Stop`) of a car, hiding complex details like engine mechanics.
- The `Car` class implements `ICar`, providing concrete behavior while keeping the interface simple.
- The `CarController` uses the abstracted `ICar` interface, allowing it to work with any car type (e.g., `ElectricCar`, `GasCar`) without needing internal details, demonstrating abstraction in a Web API context.

### 2. Encapsulation
**Example**: A `BankAccount` class hides its `balance` field, exposing it only through `Deposit` and `Withdraw` methods.

```csharp
// BankAccount.cs
public class BankAccount
{
    private decimal _balance; // Private field to encapsulate data

    public BankAccount(decimal initialBalance)
    {
        _balance = initialBalance;
    }

    public decimal GetBalance() => _balance; // Controlled access

    public string Deposit(decimal amount)
    {
        if (amount > 0)
        {
            _balance += amount;
            return $"Deposited {amount}. New balance: {_balance}";
        }
        return "Invalid deposit amount.";
    }

    public string Withdraw(decimal amount)
    {
        if (amount > 0 && _balance >= amount)
        {
            _balance -= amount;
            return $"Withdrew {amount}. New balance: {_balance}";
        }
        return "Invalid withdrawal amount or insufficient funds.";
    }
}

// BankAccountController.cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class BankAccountController : ControllerBase
{
    private readonly BankAccount _account;

    public BankAccountController()
    {
        _account = new BankAccount(1000); // Initial balance
    }

    [HttpGet("balance")]
    public IActionResult GetBalance()
    {
        return Ok(_account.GetBalance());
    }

    [HttpPost("deposit")]
    public IActionResult Deposit([FromBody] decimal amount)
    {
        return Ok(_account.Deposit(amount));
    }

    [HttpPost("withdraw")]
    public IActionResult Withdraw([FromBody] decimal amount)
    {
        return Ok(_account.Withdraw(amount));
    }
}
```

**Explanation**:
- The `BankAccount` class encapsulates the `_balance` field by making it `private`, preventing direct access.
- Public methods (`GetBalance`, `Deposit`, `Withdraw`) provide controlled access, ensuring data integrity (e.g., validating amounts).
- The `BankAccountController` exposes endpoints to interact with the `BankAccount`, demonstrating encapsulation by hiding internal state while allowing safe operations.

### 3. Inheritance
**Example**: A `Dog` class inherits from an `Animal` base class, reusing and overriding its behavior.

```csharp
// Animal.cs
public abstract class Animal
{
    public int Id { get; set; }
    public string Name { get; set; }
    public virtual string MakeSound() => "Some sound";
}

// Dog.cs
public class Dog : Animal
{
    public override string MakeSound() => "Bark";
}

// AnimalController.cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class AnimalController : ControllerBase
{
    [HttpGet("{id}")]
    public IActionResult GetAnimalSound(int id)
    {
        Animal animal = new Dog { Id = id, Name = "Buddy" };
        return Ok(animal.MakeSound());
    }
}
```

**Explanation**:
- `Dog` inherits from `Animal`, reusing the `Id` and `Name` properties and overriding the `MakeSound` method to return "Bark".
- This demonstrates an "is-a" relationship: a `Dog` is an `Animal`.
- The `AnimalController` treats the `Dog` as an `Animal`, showcasing how inheritance allows code reuse and specialization in a Web API.

### 4. Polymorphism
**Example**: A `FlyingTransport` interface is implemented by `Airplane` and used by an `AirportService` to handle different transport types.

```csharp
// IFlyingTransport.cs
public interface IFlyingTransport
{
    string Fly();
}

// Airplane.cs
public class Airplane : IFlyingTransport
{
    public string Fly() => "Airplane is flying.";
}

// AirportService.cs
public class AirportService
{
    private readonly IFlyingTransport _transport;

    public AirportService(IFlyingTransport transport)
    {
        _transport = transport; // Interface-based dependency
    }

    public string Operate() => _transport.Fly();
}

// AirportController.cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class AirportController : ControllerBase
{
    private readonly AirportService _airportService;

    public AirportController(AirportService airportService)
    {
        _airportService = airportService;
    }

    [HttpGet]
    public IActionResult OperateTransport()
    {
        return Ok(_airportService.Operate());
    }
}

// Program.cs (Dependency Injection Setup)
builder.Services.AddSingleton<IFlyingTransport, Airplane>();
builder.Services.AddSingleton<AirportService>();
```

**Explanation**:
- The `IFlyingTransport` interface defines a `Fly` method, implemented by `Airplane`.
- `AirportService` uses `IFlyingTransport`, allowing it to work with any implementation (e.g., `Airplane`, `Helicopter`) without knowing the concrete type.
- The `AirportController` calls `Operate`, which triggers the `Fly` method, demonstrating polymorphism through interface-based dynamic behavior.

### Notes
- These examples are designed to be minimal and run in a new ASP.NET Core Web API project (`dotnet new webapi -n ExampleApi`).
- Dependency injection is used where applicable to align with ASP.NET Core best practices.
- No external dependencies (e.g., databases) are included for simplicity.
- For production, add error handling, logging, and data persistence as needed.
