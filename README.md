Swift classes and structures are much closer in functionality than in other languages. You define properties and methods to add functionality to your classes and structures by using exactly the same syntax as for constants, variables, and functions. 

Much of this chapter describes functionality that can apply to instances of either a class or a structure type. An instance of a class is traditionally known as an object.
<br />

**Classes and structs in Swift have many things in common. Both can:**
<br />
 - Define properties to store values (stored and computed properties)

 - Define methods to provide functionality
 
 - Define initializers to set up their initial state
 
 - Conform to protocols to provide standard functionality of a certain kind

 - Define subscripts to provide access to their values using subscript syntax

 - Be extended to expand their functionality beyond a default implementation

<br />

**Classes have additional capabilities that structs do not:**
<br />

 - **Inheritance:** enables a class to inherit the characteristics of another class. 
 The structure does not need to inherit properties or behavior from another existing type.

 - **Type casting:** enables you to check and interpret the type of an object at runtime.

 - **Deinitializers:** enable an object to free up any resources it has assigned.

 - **Reference counting:** allows more than one reference to an object.
 <br />


**There is one big difference between class and struct:**
<br />
Classes are **reference types** but structs are **value types**. A value type is a type whose value is copied when it is assigned to a variable or constant,
or when it is passed to a function. All of the basic types in Swift integers, floating-point numbers, Booleans, strings, arrays and dictionaries are value types,
and are implemented as structures behind the scenes. Enumerations are value type too. 
Unlike value types, reference types are not copied when they are assigned to a variable or constant, 
or when they are passed to a function. Rather than a copy, a reference to the same existing instance is used instead 
(in assignement two variables point to the same object in memory. It is kind of like sharing.) Structures copy values while classes share objects.
<br />

| **Structures**  | **Classs** |
| ------------- | ------------- |
| Value types  | Reference types  |
| Copy  | Share |
<br />


    struct EmployeeStruct {
      var firstName: String
      var lastName: String

      var fullName: String {
        return "\(firstName) \(lastName)"
      }

      mutating func uppercasename() {
        firstName = firstName.uppercased()
      }    
    }
    
    var employee1 = EmployeeStruct(firstName: "hasti", lastName: "ranjkesh")
    var employee2 = employee1
    employee1.firstName = "HASTI"
    //employee2's firstName is still "hasti"
    
<br />  
In this case employee1 and employee2 would both have their own copy of the structure.     
What would happen If we used a class instead?    
<br />

    class EmployeeClass {
      var firstName: String
      var lastName: String
    
      init(firstName: String, lastName: String) {
          self.firstName = firstName
          self.lastName = lastName
      }
    
      var fullName: String {
          return "\(firstName) \(lastName)"
      }
    
      func uppercasename() {
          firstName = firstName.uppercased()
      }
     }
     var employee3 = EmployeeClass(firstName: "hasti", lastName: "ranjkesh")
     var employee4 = employee3 
     employee3.firstName = "HASTI"
     //employee4's firstName is "HASTI" too.

<br />

The stored properties and computed property work the same way. There is one difference,
Classes will not create a default initializer for you like structures do. So you have to create one yourself. 
Both employee3 and employee4 point to the same object in memory.

Instances of classes are mutable objects and can change whereas instances of structures are immutable values and they can not change. 
If you are making a method inside a struct that modifies that struct you have to mark it as mutating.
When you call uppercase method, you are basically making a new copy of the structure and making sure the swift compiler 
knows that too.  

<br />

**NOTE:** When we create a reference type like a class, the system stores the actual instance of that class and a region of memory called the **heap**.
Instances of a value type like a struct are stored in a different region of memory called the **stack**.


- The system uses the stack to manage anything in the immediate thread of execution. 
It’s controlled and managed by the CPU. For example when a function creates a variable, that is created on the stack,
and removed once the function returns. Since the stack is so well-organized it’s very efficient and very fast. 

- In contrast the system uses the heap to store reference types like classes. The heap is a large pool of memory that 
the system can request a dynamically allocating memory from. The heap does not automatically destroy its data like the stack does.
Instead you have to do a little more work to make that happen. This makes allocating and removing memory from the heap slower process 
than the same thing on the stack. When you create an instance of a class you are creating some storage inside the heap 
to store the instance of the class itself. It stores the address of that memory and you are named variable on the stack.
When you create an instance of a structure _that is not part of a class_ it’s stored on the stack instead the heap is involved at all.

<br />

**Choosing Between Classes and Structures:**
<br />
 - The structure’s primary purpose is to encapsulate a few relatively simple data values. 
 Think of values versus objects. Structs are value types which it means they are considered equal if they contain the exact same values. 
 However objects are unique and as such they all have their own identities. So if you had two objects contain the same exact values they 
 would not be considered equivalent. For example we created a structure for a employee. If one employee has the same name as another employee
 well they are not necessarily the same employee are they. They each have their own unique identity so maybe it would better to use classes in that case instead. 
 A point in a 3D coordinate system _encapsulating x, y and z properties, each of type Double_ is a good candidate for defining a struct.
 
 - Structs rely on a faster stack while classes rely on the slower heap. If you are creating many objects in a short period of time like for example a tight loop, 
 you might want to consider using struct instead of classes. If your instance however will have a long life cycle in memory or you are only creating a few instances
 then you might want to lean toward classes. For example you might want to use to calculate the total distance of a running route using many GPS based waypoints, 
 not only will you be creating many waypoints but they will be created and destroyed very frequently making that a great choice for structures.
 Conversely you might want to use a class represent an object for route history because there would only be one route history for a user and it exists for the lifecycle of that user object.
 
 - Structs are preferable if they are relatively small and copiable because copying is way safer than having multiple references to the same instance as
 happens with classes. This is especially important when passing around a variable to many classes and/or in a multithreaded environment
 
 - With Structs, there is much less need to worry about memory leaks or multiple threads racing to access/modify a single instance of a variable.
  Structs are automatically threadsafe due to not being shareable.
  
 - If your data will never change or you just need a simple data store then use structures, but if you want to update your data or add methods to your data so that 
 it can update its own state then consider using classes. 
 
<br />
Often it’s best to start with struct and if you find out later you need the capabilities of a class then just change it to a class. 




