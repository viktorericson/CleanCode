# Clean Code


> The objective of this guideline is to ensure consistency, readability, and maintainability in our code. It is essential for all contributors, both current and future, to familiarize themselves with these standards and apply them. Before pushing any code to the repository, students should review their work to ensure it adheres to these guidelines.


### 1. Naming Conventions
- **Clear and Intentional**: Use names that reveal intention. For example, in C#, int elapsedTimeInDays; rather than int e;.
- **Avoid Misleading Names**: Ensure names do not mislead about the code's functionality. For example, avoid calling a collection of users as usersList if it is not a list.
- **Make meaningful distinctions**:The different things in a scope should have distinguishable meanings, which covers not misspelling words, adding numbers and noise words. For example, referring to two different age variables by int age and int ageVariable
- **Pronounceable names**: Use pronounceable words. For example, name a date date rather than ddmmyyyy.
- **Searchable names**: It is hard to locate single letter and number constants across a page. Therefore, name everything such as they are easy to locate and search. 
- **Class names**: The objects and classes should be nouns or noun phrases like Car. Avoid using verbs as class names.
- **Method names**: Methods should be verbs like savePage.
- **Wording consistency**: Be consistent with how things is worded. For example avoid using get and retrieve as equivalents, rather pick one of them.
- **Avoid same word for different purposes**: Expanding on wording consistency, avoid using the same word for different purposes. For example, don’t use a consequent word for a function like add for consistency when the function is not adding in the same way as previous instances of add functions.
- **Use solution domain names**: The ones who read the code are familiar with computer science terms, therefore these terms should be used. If there is no computer science term, use a problem domain term.
- **Add meaningful context**: Add context which makes it easier for the reader to understand which part of the structure variables, functions ect. belong to. However, avoid redundant prefixes of context. Keep the names short and precise and clear.

**Example of good naming:**

```Javascript
// Good naming and single responsibility
public class OrderProcessor
{
    public void ProcessOrder(Order order)
    {
        if (order.IsValid())
        {
            // Process the order
        }
    }
}
```

**Example of bad naming**
```Javascript
// Bad naming 
public class OP
{
    public void PO(O o)
    {
        if (o.IsValid())
        {
            // Process the order
        }
    }
}
```


### 2. Function Design
- **Single Responsibility**: Each function should do one thing only. For instance, in JavaScript, a function calculateTotalPrice() should only calculate and return the total price, not format it.
- **Small Size and Descriptive Names**: Functions should be small and have descriptive names. E.g., in C#, void ProcessCustomerOrder() rather than void Process().
- **Function arguments**: Limit the amount of function arguments. 
- **Avoid unexpecting behavior**: The function should not perform other tasks than what is expected of them. For example, unexpecting changes of variables.

### 3. Comments Usage

**Good comments:**
- “The best comment, is the comment you found a way not to write”
- Your comments should explain your code, often you should focus on the “why” and not what the code does. 
- Keep your comments clear and concise, and use them sparingly. 

**Bad comments:**
- Avoid comments that state the obvious.
- Remember that the comments are also used and read by others, so don't use them as a personal notepad. 
- If your comment is longer than your code, it’s probably redundant. 

Example of a **bad comment**:


```Javascript
// Calculates total price from given prices, returns total price calculated within the function
Function calculateTotalPrice(price: int[]) {
…
Return totalPrice;
};
```

### 4. Formatting and refactoring
 -A good rule of thumb is to clean your code as you go, so for every few lines you add, take a moment to reflect on your code and remove any redundant code. 
- Keep the same formatting principles throughout the project.
- Don’t leave it to the next person to re-format your code. 

### 5. Error handling
- **Use Exceptions**: Prefer using exceptions over return codes for error handling.
- **Context in Exceptions**: Provide context in exceptions to make troubleshooting easier.
  
Eg.
```C#
public void ReadFile(string filePath)
{
    try
    {
        string content = File.ReadAllText(filePath);
        // Process file content
    }
    catch (FileNotFoundException ex)
    {
        // Specific exception handling for file not found
        Console.WriteLine($"File not found: {ex.Message}");
    }
    catch (Exception ex)
    {
        // General exception handling
        Console.WriteLine($"An error occurred: {ex.Message}");
        // Optionally, rethrow to allow further handling up the call stack
        throw;
    }
}
```


### 6. Boundaries

- **Use Wrappers for External APIs**: Create wrappers around external libraries and APIs.

```C#
// External API call
ExternalLibrary.SomeMethod();

// Wrapper class
public class ExternalApiWrapper {
    public void SomeMethodWrapper() {
        ExternalLibrary.SomeMethod();
    }
}
```

- **Learn Through Tests**: Write learning tests to understand how the library works.
```C#
[Test]
public void TestExternalMethodBehavior() {
    var wrapper = new ExternalApiWrapper();
    Assert.AreEqual(expectedBehavior, wrapper.SomeMethodWrapper());
}
```


### 7. Unit Testing

**Test-Driven Development**: Write tests before implementing functionalities.

```C#
// First write this test
[Test]
public void ShouldCalculateSumCorrectly() {
    Assert.AreEqual(10, Calculator.Sum(7, 3));
}

// Then implement the method
public class Calculator {
    public static int Sum(int a, int b) {
        return a + b;
    }
}
```

**One Assert Per Test**: Ensure each test asserts only one condition.
```C#
// Instead of combining multiple asserts
[Test]
public void TestUserProfile() {
    var userProfile = new UserProfile("JohnDoe", "John", "Doe");
    Assert.AreEqual("JohnDoe", userProfile.Username);
    Assert.AreEqual("John", userProfile.FirstName);
    Assert.AreEqual("Doe", userProfile.LastName);
}

// Prefer separate tests for each condition
[Test]
public void UsernameShouldBeCorrect() {
    var userProfile = new UserProfile("JohnDoe", "John", "Doe");
    Assert.AreEqual("JohnDoe", userProfile.Username);
}

[Test]
public void FirstNameShouldBeCorrect() {
    var userProfile = new UserProfile("JohnDoe", "John", "Doe");
    Assert.AreEqual("John", userProfile.FirstName);
}

[Test]
public void LastNameShouldBeCorrect() {
    var userProfile = new UserProfile("JohnDoe", "John", "Doe");
    Assert.AreEqual("Doe", userProfile.LastName);
}
```

### 8. Objects and Data Structures

- **Encapsulation**: Hide internal data and expose necessary functionalities. For example, in C#, use properties instead of public fields.
Eg.
```C#
public class Box {
    private int length;
    public Box(int initialLength) {
        length = initialLength;
    }
    public void setLength(int newLength) {
        length = newLength;
    }
    public int getLength() {
        return length;
    }
}
```

- The **length** variable is private, so it cannot be accessed directly from outside the Box class.
- The constructor **Box(int initialLength)** allows setting the initial length of the box.
- Public methods **setLength(int newLength)** and **getLength()** are provided to modify and access the **length** respectively, adhering to the principles of encapsulation.

### 9. Classes

- **Single Responsibility Principle (SRP)**: Create classes with a single, well-defined purpose. Refactor if responsibilities multiply.
- **Encapsulation**: Hide internal complexities, expose necessary interfaces, and minimize dependencies.
- **Naming**: Use descriptive, clear names that accurately represent the class’s role and purpose.
- **Size and Cohesion**: Keep classes small, focused, and highly cohesive to avoid bloat and complexity.
- **Coupling**: Minimize interdependencies between classes for flexibility and maintainability.
- **Continuous Refactoring**: Regularly review and refactor classes to maintain cleanliness and address technical debt.

  **An example of these principles:**

```JavaScript
class Book {
    constructor(title, author) {
        this._title = title;
        this._author = author;
    }

    getTitle() {
        return this._title;
    }

    getAuthor() {
        return this._author;
    }
}

class Library {
    constructor() {
        this._books = [];
    }

    addBook(book) {
        this._books.push(book);
    }

    findBooksByAuthor(author) {
        return this._books.filter(book => book.getAuthor() === author);
    }
}

// Example usage
const book1 = new Book("1984", "George Orwell");
const book2 = new Book("Harry Potter and the Goblet Of Fire", "J. K. Rowling");

const library = new Library();
library.addBook(book1);
library.addBook(book2);

console.log(library.findBooksByAuthor("George Orwell"));
```

### 10. Systems

- **Separation of Concerns**: Partition systems into distinct sections, each addressing a separate concern or functionality.
- **Modularity**: Design systems with cohesive modules, keeping related functionalities together.
- **Abstraction**: Use abstraction to hide implementation details and expose necessary interfaces.
- **Decoupling**: Minimize interdependency between system components for flexibility and ease of change.
- **Layered Architecture**: Employ a layered architecture for clear separation of responsibilities and easier maintenance.
- **Dependency Management**: Manage dependencies carefully. Favorloosely  coupled components over tightly coupled ones.
- **Continuous Evaluation and Improvement**: Regularly assess and refine the system’s architecture to accommodate evolving requirements and technologies.

<details>
    <summary>
        See example here:
    </summary>
    <br>
    
    - Separation of Concerns:
        The system is divided into different sections such as User Interface (UI), Business Logic, and Data Storage.
        UI handles user interactions and display.
        Business Logic handles the core functionality like managing book inventories, processing orders, and user accounts.
        Data Storage is concerned with storing and retrieving data, like book details and user information.

    - Modularity:
        The system is broken down into modules such as a User Module (handling user accounts and profiles), a Catalog Module (managing book listings), and an Order Module (processing purchases and tracking orders).
        Each module is self-contained and focuses on a specific subset of the system's functionality.

    - Abstraction:
        The system uses abstract interfaces to interact between modules. For example, an OrderInterface might expose methods for placing and tracking orders without revealing the underlying logic.
        This allows changes to be made to the implementation of one module without affecting others that depend on it.

    - Decoupling:
        Modules interact with each other through interfaces or service contracts rather than direct implementation. This minimizes the dependencies between them.
        For example, the Order Module doesn't need to know the internal workings of the User Module, it just needs to know how to get the necessary user details through a defined interface.

    - Layered Architecture:
        The system uses a three-tier architecture: Presentation Layer (UI), Business Logic Layer, and Data Access Layer.
        Each layer has a specific role and communicates with the other layers in a controlled manner.
        This separation allows for easier maintenance and scalability of the system.

    - Dependency Management:
        The system is designed to minimize tight coupling between its components. For instance, if it uses a third-party payment gateway, it does so through an adapter that can be easily replaced if the payment service needs to change.
        Dependencies are injected into modules rather than being hardcoded, allowing for greater flexibility and easier testing.

    - Continuous Evaluation and Improvement:
        The system's architecture is regularly reviewed for potential improvements. This might include refactoring code for better efficiency, adopting new technologies for the UI, or updating the database system for better performance.
        Regular code reviews and performance monitoring help identify areas for improvement.

This example shows how each principle contributes to a well-structured and maintainable system. By adhering to these principles, the online bookstore system becomes flexible, scalable, and easier to maintain.
</details>
