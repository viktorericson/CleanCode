# Clean Code

#### 1. Naming Conventions
Clear and Intentional: Use names that reveal intention. For example, in C#, int elapsedTimeInDays; rather than int e;.
Avoid Misleading Names: Ensure names do not mislead about the code's functionality. For example, avoid calling a collection of users as usersList if it is not a list.
Make meaningful distinctions:The different things in a scope should have distinguishable meanings, which covers not misspelling words, adding numbers and noise words. For example, referring to two different age variables by int age and int ageVariable
Pronounceable names: Use pronounceable words. For example, name a date date rather than ddmmyyyy.
Searchable names: It is hard to locate single letter and number constants across a page. Therefore, name everything such as they are easy to locate and search. 
Class names: The objects and classes should be nouns or noun phrases like Car. Avoid using verbs as class names.
Method names: Methods should be verbs like savePage.
Wording consistency: Be consistent with how things is worded. For example avoid using get and retrieve as equivalents, rather pick one of them.
Avoid same word for different purposes: Expanding on wording consistency, avoid using the same word for different purposes. For example, don’t use a consequent word for a function like add for consistency when the function is not adding in the same way as previous instances of add functions.
Use solution domain names: The ones who read the code are familiar with computer science terms, therefore these terms should be used. If there is no computer science term, use a problem domain term.
Add meaningful context: Add context which makes it easier for the reader to understand which part of the structure variables, functions ect. belong to. However, avoid redundant prefixes of context. Keep the names short and precise and clear.

Example of good naming:
// Good naming and single responsibility
'''Javascript
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
'''


#### 2. Function Design
Single Responsibility: Each function should do one thing only. For instance, in JavaScript, a function calculateTotalPrice() should only calculate and return the total price, not format it.
Small Size and Descriptive Names: Functions should be small and have descriptive names. E.g., in C#, void ProcessCustomerOrder() rather than void Process().
Function arguments: Limit the amount of function arguments. 
Avoid unexpecting behavior: The function should not perform other tasks than what is expected of them. For example, unexpecting changes of variables.

#### 3. Comments Usage
Good comments:
“The best comment, is the comment you found a way not to write”
Your comments should explain your code, often you should focus on the “why” and not what the code does. 
Keep your comments clear and concise, and use them sparingly. 
Bad comments: 
Avoid comments that state the obvious.
Remember that the comments are also used and read by others, so don't use them as a personal notepad. 
If your comment is longer than your code, it’s probably redundant. 

Example of a bad comment:
// Calculates total price from given prices, returns total price calculated within the function
Function calculateTotalPrice(price: int[]) {
…
Return totalPrice;
};

#### 4. Formatting and refactoring
A good rule of thumb is to clean your code as you go, so for every few lines you add, take a moment to reflect on your code and remove any redundant code. 
Keep the same formatting principles throughout the project.
Don’t leave it to the next person to re-format your code. 

#### 5. Error handling
Use Exceptions: Prefer using exceptions over return codes for error handling.
Context in Exceptions: Provide context in exceptions to make troubleshooting easier.
Eg.
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



#### 6. Boundaries
Use Wrappers for External APIs: Create wrappers around external libraries and APIs.

// External API call
ExternalLibrary.SomeMethod();

// Wrapper class
public class ExternalApiWrapper {
    public void SomeMethodWrapper() {
        ExternalLibrary.SomeMethod();
    }
}

Learn Through Tests: Write learning tests to understand how the library works.

[Test]
public void TestExternalMethodBehavior() {
    var wrapper = new ExternalApiWrapper();
    Assert.AreEqual(expectedBehavior, wrapper.SomeMethodWrapper());
}



#### 7. Unit Testing
Test-Driven Development: Write tests before implementing functionalities.
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


One Assert Per Test: Ensure each test asserts only one condition.
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


#### 8. Objects and Data Structures
Encapsulation: Hide internal data and expose necessary functionalities. For example, in C#, use properties instead of public fields.
Eg.
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

The length variable is private, so it cannot be accessed directly from outside the Box class.
The constructor Box(int initialLength) allows setting the initial length of the box.
Public methods setLength (int newLength) and getLength() are provided to modify and access the length respectively, adhering to the principles of encapsulation.

#### 9. Classes
Single Responsibility Principle (SRP): Create classes with a single, well-defined purpose. Refactor if responsibilities multiply.
Encapsulation: Hide internal complexities, expose necessary interfaces, and minimize dependencies.
Naming: Use descriptive, clear names that accurately represent the class’s role and purpose.
Size and Cohesion: Keep classes small, focused, and highly cohesive to avoid bloat and complexity.
Coupling: Minimize interdependencies between classes for flexibility and maintainability.
Continuous Refactoring: Regularly review and refactor classes to maintain cleanliness and address technical debt.

#### 10. Systems
Separation of Concerns: Partition systems into distinct sections, each addressing a separate concern or functionality.
Modularity: Design systems with cohesive modules, keeping related functionalities together.
Abstraction: Use abstraction to hide implementation details and expose necessary interfaces.
Decoupling: Minimize interdependency between system components for flexibility and ease of change.
Layered Architecture: Employ a layered architecture for clear separation of responsibilities and easier maintenance.
Dependency Management: Manage dependencies carefully. Favorloosely  coupled components over tightly coupled ones.
Continuous Evaluation and Improvement: Regularly assess and refine the system’s architecture to accommodate evolving requirements and technologies.
