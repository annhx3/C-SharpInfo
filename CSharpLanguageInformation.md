
# C#
## Language purpose/genesis
### Why was the language created?
Microsoft created C# as a replacement for Java with syntax similar to C and C++.

### What problems was the language trying to address?
Hejlsberg is C#'s principal designer and lead architect at Microsoft, and was previously involved with the design of Turbo Pascal, Embarcadero Delphi (formerly CodeGear Delphi, Inprise Delphi and Borland Delphi), and Visual J++. In interviews and technical papers he has stated that flaws in most major programming languages (e.g. C++, Java, Delphi, and Smalltalk) drove the fundamentals of the Common Language Runtime (CLR), which, in turn, drove the design of the C# language itself.

Since the release of C# 2.0 in November 2005, the C# and Java languages have evolved on increasingly divergent trajectories, becoming two very different languages. One of the first major departures came with the addition of generics to both languages, with vastly different implementations.

Furthermore, C# has added several major features to accommodate functional-style programming, culminating in the LINQ extensions released with C# 3.0 and its supporting framework of lambda expressions, extension methods, and anonymous types.  These features enable C# programmers to use functional programming techniques, such as closures, when it is advantageous to their application.

### Is the language a reaction to a previous language or a replacement for another language?
C# is a replacement for Java.

## Unique features of C#
### Does the language have any particularly unique features?
Assemblies:  This is a level of encapsulation above the typical namespaces or modules in most languages. Assemblies are similar to the idea of static/dynamic libraries in C or JAR files in Java. Notably, you can mark members as internal, which makes them public within the same assembly, but private to everybody outside the assembly. This is quite useful.
- Cross-language compatibility is first-class (not just for C): C# runs in the Common Language Runtime, which was designed from the beginning to support interoperability between languages.
- Properties are first-class: No longer need to write explicit getter and (optional) setter methods.
- Listeners are first-class: Classes can declare an event Foo with addFooListener and removeFooListener functionality built in.
- Foreign Methods are first-class: C# calls these extension methods.
- Partial Classes: Allows a class’s members to be defined in multiple files. Useful to add functionality to a generated class (for example, from a parser generator) without those modifications getting lost when the class is next regenerated.

## Name spaces
### How are name spaces implemented?
.NET Framework uses namespaces to organize its many classes. The namespace keyword is used to declare a scope. The ability to create scopes within your project helps organize code and lets you create globally-unique types.

```` 
namespace  SampleNamespace  
{  
	class  SampleClass  
	{  
		public  void  SampleMethod()  
		{  
			System.Console.WriteLine(  
			"SampleMethod inside SampleNamespace");  
		}  
	}  
}
 ````

### How are name spaces used?
Declaring your own namespaces can help you control the scope of class and method names.

## Types
### What types does the language support?
C# is a strongly-typed language. Every variable and constant has a type, as does every expression that evaluates to a value. Every method signature specifies a type for each input parameter and for the return value. The .NET class library defines a set of built-in numeric types as well as more complex types that represent a wide variety of logical constructs, such as the file system, network connections, collections and arrays of objects, and dates. A typical C# program uses types from the class library as well as user-defined types that model the concepts that are specific to the program's problem domain.  
C# also supports generics.
### Are both reference and value types supported?  Can new value types be created?
Instances of value types do not have referential identity nor referential comparison semantics - equality and inequality comparisons for value types compare the actual data values within the instances, unless the corresponding operators are overloaded. Value types are derived from System.ValueType, always have a default value, and can always be created and copied. Some other limitations on value types are that they cannot derive from each other (but can implement interfaces) and cannot have an explicit default (parameterless) constructor. Examples of value types are all primitive types, such as int (a signed 32-bit integer), float (a 32-bit IEEE floating-point number), char (a 16-bit Unicode code unit), and System.DateTime (identifies a specific point in time with nanosecond precision). Other examples are enum (enumerations) and struct (user defined structures).  
  
In contrast, reference types have the notion of referential identity - each instance of a reference type is inherently distinct from every other instance, even if the data within both instances is the same. This is reflected in default equality and inequality comparisons for reference types, which test for referential rather than structural equality, unless the corresponding operators are overloaded (such as the case for System.String). In general, it is not always possible to create an instance of a reference type, nor to copy an existing instance, or perform a value comparison on two existing instances, though specific reference types can provide such services by exposing a public constructor or implementing a corresponding interface (such as ICloneable or IComparable). Examples of reference types are object (the ultimate base class for all other C# classes), System.String (a string of Unicode characters), and System.Array (a base class for all C# arrays).  
 
Both type categories are extensible with user-defined types.
## Classes
### Defining
Use class keyword.
```
public  class  Customer  
{  
// Fields, properties, methods and events go here...  
}
```
### Creating new instances
Use new keyword.
```
Customer object1 = new Customer();
```
### Constructing/initializing
In C#:
```
   // Constructor that takes no arguments.
    public Person()
    {
        name = "unknown";
    }

    // Constructor that takes one argument.
    public Person(string nm)
    {
        name = nm;
    }
```
### Destructing/de-initializing
When garbage collection detects that there are no remaining references to the component, the runtime calls your component's destructor (Finalize in Visual Basic) and frees the memory. You should override your base class's Finalize method (for Visual Basic) or implement a destructor (for Visual C#) to implement your own clean-up code, but always include a call to the destructor or Finalize method of the base class.
In C#, a destructor is used instead of a Finalize method.
```
~ThisClass()
{
   m_gadget = null;
   m_gear = null;
   // The base class finalizer is called automatically
}
```
## Instance reference name in data type (class)
### this? self?
C# uses 'this' keyword.
```
public Employee(string name, string alias)
{
    // Use this to qualify the fields, name and alias:
    this.name = name;
    this.alias = alias;
}
```

## Properties
### Getters and setters…write your own or built in?
Using 'getters' and 'setters' aren't typically used in Python but can be utilized. The typical way is just to use plain attributes to pass the information and then to dereference the attribute using the 'del' function.
However, getters and setters can be added to the code to make it consistent to other programming. These can be added using the 'property' decorator without altering the original code
Getters and Setters are built in to auto-implemented properties in C# 
```
public class Customer
{
    public int ID { get; set; }
    public string Name { get; set; }
}
 ```
 
 ### Backing variables?
Built in / hidden but can be managed manually if needed.

Pre .NET 3.5: 
```
private string _something; 
public string Something 
{ 
	get { 
		return _something; 
		} 
	set { 
		_something = value; 
		} 
}
```
Or more recent:
``` public string Something { get; set; } ```

### Computed properties?
Yes, C# allows computed properties.  An example:
```
class TimePeriod
{
   private double seconds;

   public double Hours
   {
       get { return seconds / 3600; }
       set { 
          if (value < 0 || value > 24)
             throw new ArgumentOutOfRangeException(
                   $"{nameof(value)} must be between 0 and 24.");

          seconds = value * 3600; 
       }
   }
}
```
## Interfaces / protocols
### What does the language support?
C# supports interfaces. 
### What abilities does it have?
By using interfaces, you can, for example, include behavior from multiple sources in a class.
 ### How is it used?
 As a workaround because C# doesn't support multiple inheritance of classes. It uses the interface keyword (also see below for how to use).
```
interface IEquatable<T>
{
    bool Equals(T obj);
}
```
## Inheritance / extension
C# and .NET support single inheritance only.  However, inheritance is transitive, which allows you to define an inheritance hierarchy for a set of types.
```
public class A 
{
   private int value = 10;

   public class B : A
   {
       public int GetValue()
       {
           return this.value;
       }     
   }
}
```

## Reflection
### What reflection abilities are supported?
You can use reflection to dynamically create an instance of a type, bind the type to an existing object, or get the type from an existing object and invoke its methods or access its fields and properties. If you are using attributes in your code, reflection enables you to access them.
### How is reflection used?
Reflection is useful in the following situations:
- When you have to access attributes in your program's metadata. 
- For examining and instantiating types in an assembly.
- For building new types at runtime. Use classes in System.Reflection.Emit.
- For performing late binding, accessing methods on types created at run time. 

## Memory Management
### How is it handled?
The Microsoft .NET common language runtime requires that all resources be allocated from the managed heap. Objects are automatically freed when they are no longer needed by the application.

### How does it work?

When a process is initialized, the runtime reserves a contiguous region of address space that initially has no storage allocated for it. This address space region is the managed heap. The heap also maintains a pointer. This pointer indicates where the next object is to be allocated within the heap. Initially, the pointer is set to the base address of the reserved address space region.

An application creates an object using the new operator. This operator first ensures that the bytes required by the new object fit in the reserved region (committing storage if necessary). If the object fits, then the pointer points to the object in the heap, this object's constructor is called, and the new operator returns the address of the object.

## Reference Counting 
Reference counting is the idea that an object needs to be maintained when the count of that object is greater than 0. 
### Garbage Collection
The garbage collector checks to see if there are any objects in the heap that are no longer being used by the application. If such objects exist, then the memory used by these objects can be reclaimed. (If no more memory is available for the heap, then the new operator throws an OutOfMemoryException.)

In the common language runtime, the managed heap always knows the actual type of an object, and the metadata information is used to determine which members of an object refer to other objects.
### Automatic reference counting?
Not used in C# - an e-mail from Brian Harry explains why: 
> “We initially started with the assumption that the solution would take the form of automatic ref counting (so the programmer couldn't forget) plus some other stuff to detect and handle cycles automatically. ...we ultimately concluded that this was not going to work in the general case. >
In summary:
> * We feel that it is very important to solve the cycle problem without forcing programmers to understand, track down and design around these complex data structure problems.
>* We want to make sure we have a high performance (both speed and working set) system and our analysis shows that using reference counting for every single object in the system will not allow us to achieve this goal.
>* For a variety of reasons, including composition and casting issues, there is no simple transparent solution to having just those objects that need it be ref counted.
>* We chose not to select a solution that provides deterministic finalization for a single language/context because it inhibits interop with other languages and causes bifurcation of class libraries by creating language specific versions.


## Comparisons of References and Values
### How are values compared? (i.e. comparing two strings)
Equals and == will compare by reference by default if they're not overriden / overloaded in a subclass. ReferenceEquals will always compare by reference.

Strings overload == to implement value equality; also, since they're immutable, C# will generally reuse the same instance for the same literal string. 

## Nul/Nil references
### Which does the language use? (null/nil/etc)
Null
### Does the language have features for handling null/nil references?
The null keyword is a literal that represents a null reference, one that does not refer to any object. null is the default value of reference-type variables. Ordinary value types cannot be null. However, C# 2.0 introduced nullable value types.
```
        string s = null;
```
### Errors and exception handling
A try block is used by C# programmers to partition code that might be affected by an exception. Associated catch blocks are used to handle any resulting exceptions. A finally block contains code that is run regardless of whether or not an exception is thrown in the try block, such as releasing resources that are allocated in the try block. A try block requires one or more associated catch blocks, or a finally block, or both.
```
try
{
    // Code to try goes here.
}
catch (SomeSpecificException ex)
{
    // Code to handle the exception goes here - like 
“throw new System.ArgumentOutOfRangeException("Parameter index is out of range.", e);”
}
finally
{
    // Code to execute after the try (and possibly catch) blocks 
    // goes here.
} 
```
### Lambda expressions, closures, or functions as types
C# uses lambda expressions: 
(input-parameters) => expression
and uses delegates instead of functions as types. 
```
public delegate void DoSomethingDelegate(Object param1, Object param2);


delegate int del(int i);  
static void Main(string[] args)  
{  
    del myDelegate = x => x * x;  
    int j = myDelegate(5); //j = 25  
}  


```

## Listeners or Event Handlers
### Implementation of listeners and event handlers
Delegates are essentially method pointers.  The concept of delegates exist because to call a pointer to an instance method you need a pointer to the method and the instance reference in order to call the correct method; delegates encapsulate that pair and provide polymorphism for class methods--which don't require the instance reference.

As a method pointer, invoking a delegate calls the method to which it points.

Events are implemented with multicast delegates, meaning a delegate can point to more than one method, so raising an event may call multiple methods.


## Singleton
### How is a singleton implemented?

Common, non-treadsafe way:

```
public sealed class Singleton
{
    private static Singleton instance=null;

    private Singleton()
    {
    }

    public static Singleton Instance
    {
        get
        {
            if (instance==null)
            {
                instance = new Singleton();
            }
            return instance;
        }
    }
}
```
### Can it be made thread-safe?
```
public sealed class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    Singleton()
    {
    }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```
### Can the singleton instance be lazily instantiated?
Yes, like this:
```
public sealed class Singleton
{
    private static readonly Lazy<Singleton> lazy =
        new Lazy<Singleton>(() => new Singleton());
    
    public static Singleton Instance { get { return lazy.Value; } }

    private Singleton()
    {
    }
}

or this:
public sealed class Singleton
{
    private Singleton()
    {
    }

    public static Singleton Instance { get { return Nested.instance; } }
        
    private class Nested
    {
        // Explicit static constructor to tell C# compiler
        // not to mark type as beforefieldinit
        static Nested()
        {
        }

        internal static readonly Singleton instance = new Singleton();
    }
}

```

## Procedural Programming
### Does the language support procedural programming?
Most mainstream languages, including object-oriented programming (OOP) languages such as C#, were designed to primarily support imperative (procedural) programming.

## Functional Programming
### Does the language support functional programming?

The functional programming paradigm was explicitly created to support a pure functional approach to problem solving.

A functional approach involves composing the problem as a set of functions to be executed. You define carefully the input to each function, and what each function returns. 

Most languages that contain function pointers can be used to credibly support functional programming. Furthermore, C# includes explicit language extensions to support functional programming, including lambda expressions and type inference. LINQ technology is a form of declarative, functional programming.


## Multithreading
### Threads or thread-like abilities
Yes using ```System.Threading```.

### How is multitasking accomplished?
The .NET Framework System.Threading namespace makes using threads easier and creates and controls a thread, sets its priority, and gets its status.  By default, a C# program has one thread. However, auxiliary threads can be created and used to execute code in parallel with the primary thread.
