# Intro
- Seperation of concerns
- Inject concrete implementations into interface spots
- Helps with TDD

Setting up Services:
```csharp
// SampleService.cs 
public class SampleService : ISampleService
{
    public string GetMessage(int id) 
    {
        switch(id) 
        {
            case 1:
                return "Hello World";
            case 2:
                return "What's up?";
            case 3:
                return "how's it going?"
        }
    }
}

// ISampleService.cs 
public interface ISampleService
{
    string GetMessage(int id);
}

```

Using DI:
```csharp

// HomeController.cs
public class HomeController : Controller
{
    private readonly ISampleService _service;

    public HomeController() : this(new SampleService()) {}

    public HomeController(ISampleService service) {
        _service = service;
    }

    .
    .
    .
    .

}

// From here it kinda depends on what framework you use...
// But use Ninject or similar to set up a dependency injection service.
// (Do this at the start of your program)
// Then, when you want to create a "HomeController" you would use that 
// dependency injection service to get an ISampleService to send to the
// constructor. 

```