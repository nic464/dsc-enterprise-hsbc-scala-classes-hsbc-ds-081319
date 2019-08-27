
# Classes

## About `class`

* Classes are the templates or blueprints of a construct that encapsulates state and manages behavior.
* Classes have been around for a long time and in every object oriented language.
* Since Scala is a half object oriented language, half functional language, there are naturally classes.

## Our first `class`

* A `class` is `public` by default, so no need for a `public` modifier
* The `(firstName:String, lastName:String)` is the primary constructor!
* In Scala the primary constructor is "top-heavy" with a constructor that contains all the information
* Other constructors are smaller constructors that feed the top constructor
* The reason for the top heavy constructor is immutability


```scala
class Employee(firstName:String, lastName:String)
```




    defined class Employee
    



## Instantiating the `class`

Instantiating the class is fairly straightforward


```scala
val emp = new Employee("Dennis", "Ritchie")
```




    emp: Employee = Employee@1d79abe9
    



## Can’t access or modify member of a `class`?

* As it stands in our class above, we can neither access or modify our class
* Most of the time we don’t want to modify our class for immutability purposes
* To be able to access the members, we will predicate each of the values with `val`
* To be able to mutate the member variables, we predicate each of the values with `var` (Not recommended)

As it stands, running `javap -p Employee` from the shows the following Java code:
```
public class Employee {
  public Employee(java.lang.String, java.lang.String);
}
```

NOTE: `javap -p` shows the translated Java code from Scala.

## Accessing and Mutating

* `val` will create a Scala-style "getter"
* `var` will create a Scala-style "setter"


```scala
class Employee(val firstName:String, var lastName:String)
val emp = new Employee("Dennis", "Ritchie")
```




    defined class Employee
    emp: Employee = Employee@79034a3b
    




```scala
println(emp.firstName)           //Works because of val
```

    Dennis
    


```scala
println(emp.lastName)            //Works because of var
```

    Ritchie
    


```scala
emp.lastName = "Hopper" //Works because of var
```




    emp.lastName: String = Hopper
    




```scala
println(emp.lastName)
```

    Hopper
    

## Viewing bytecode with `val` and `var`

* The bytecode generated from javap -p Employee
  * Using `val` for firstName
  * Using `var` for lastName

```
public class Employee {
  private final java.lang.String firstName;
  private java.lang.String lastName;
  public java.lang.String firstName();
  public java.lang.String lastName();
  public void lastName_$eq(java.lang.String);
  public Employee(java.lang.String, java.lang.String);
}
```

## Classes Conclusion

* Classes are templates or blueprints
* `val` creates accessors, methods that will allow to access the inner state
* `var` create mutators and accessors, mutators allow us to change inner state.

**IMPORTANT:** We rarely use `var`, it would be best to avoid.
