# Effective Java (Joshua Bloch)

Joshua Bloch, Effective Java, 2nd Edition. Copyright 2008 Sun Microsystems, Inc.

## Creating and Destroying Objects

### Consider static factory methods instead of constructors

**Advantages:**
- Unlike constructors, static factory methods have names.
- Unlike constructors, they are not required to create a new object each time they're invoked.
- Unlike constructors, they can return an object of any subtype of their return type.
- They reduce the verbosity of creating parameterized type instances.
    - ``` Map<String, List<String>> m = new HashMap<String, List<String>>();```  
        With static factories the compiler can figure out the type parameters for you (Type Inference).  
        - ``` Map<String, List<String>> m = HashMap.newInstance();```  
        Note: Java 7 introduced type inference through the use of the diamond operator.  
            - ``` Map<String, List<String>> m = new HashMap<>();```

**Disadvantages:**
- The main disadvantage of providing only static factory methods is that classes without public or protected constructors cannot be subclassed.
    - This can be a blessing in disguise, as it encourages to use composition instead of inheritance.
- They are not readily distinguishable from other static methods.
    - Common names for static factory methods:
        - valueOf - Returns an instance that has, loosely speaking, the same value as its parameters. Such static factories are effectively type-conversion methods.
        - of - A concise alternative to valueOf, popularized by EnumSet.
        - getInstance - Returns an instance that is described by the parameters but cannot be said to have same value. In the case of a singleton, getInstance takes no parameters and returns the sole instance.
        - newInstance - Like getInstance, except that newInstance guarantees that each instance returned is distinct from all others.
        - getType - Like getInstance, but used when the factory method is in a different class. Type indicates the type of object returned by the factory method.
        - newType - Like newInstance, but used when the factory method is in a different class. Type indicates the type of object returned by the factory method.
        
**Summary:**  
Static factory methods and public constructors both have their uses. Avoid the reflex to provide public constructors without first considering static factories.
 
### Consider a builder when faced with many constructor parameters

**Telescoping constructor pattern** = You provide a constructor with only the required parameters, another with a single optional parameter, a third with two optional parameters, and so on, culminating in a constructor with all the optional parameters.  
This works but it is hard to write client code when there are many parameters, and harder still to read it.

**JavaBeans pattern** = you call a parameterless constructor to create the object and then call setter methods to set each required parameter and each optional parameter of interest.  
Disadvantages:
- A JavaBean may be in an inconsistent state partway through its construction.
- Precludes the possibility of making a class immutable.
- Required added effort to ensure thread safety.

**Solution:**  
A form of the Builder pattern.

Example:

```java
// Builder Pattern
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;
    
    public static class Builder {
        // Required parameters
        private final int servingSize;
        private final int servings;
        
        // Optional parameters - initialized to default values
        private int calories = 0;
        private int fat = 0;
        private int carbohydrate = 0;
        private int sodium = 0;
        
        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings = servings;
        }
        
        public Builder calories(int val) { calories = val; return this; }
        public Builder fat(int val) { fat = val; return this; }
        public Builder carbohydrate(int val) { carbohydrate = val; return this; }
        public Builder sodium(int val) { sodium = val; return this; }
        
        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }
    
    private NutritionFacts(Builder builder) {
        servingSize = builder.servingSize;
        servings = builder.servings;
        calories = builder.calories;
        fat = builder.fat;
        sodium = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}
```

Client code:

```java
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8).calories(100).sodium(35).carbohydrate(27).build();
```

**Advantages:**
- Simulates named optional parameters.
- Class.newInstance breaks compile-time exception checking. The Builder interface corrects these deficiencies.

  ```java
  public interface Builder<T> {
    T build();
  }
  ```
  
**Disadvantages:**
- The cost of creating the builder is unlikely to be noticeable in practice, it could be a problem in some performance-critical situations.
- More verbose, so it should be used only if there are enough parameters, say, four or more. Keep in mind that you may want to add parameters in the future. It's often better to start with a builder in the first place.

**Summary:**  
The Builder pattern is a good choice when designing classes whose constructors or static factories would have more than a handful of parameters, especially if most of those parameters are optional.

### Enforce the singleton property with a private constructor or an enum type

*Singleton*  
A class that instantiated exactly once.  
Making a class a singleton can make it difficult to test its clients.

Before release 1.5, there were two ways to implement singletons.

```java
// Singleton with public final field
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    
    public void leaveTheBuilding() { ... }
```

Advantage:
- The declarations make it clear that the class is a singleton.
- Simpler

One caveat: a privileged client can invoke the private constructor reflectively with the aid of the AccessibleObject.setAccessible method.  
If you need to defend against this attack, modify the constructor to make it throw an exception if it's asked to create a second instance.

```java
// Singleton with static factory
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    public static Elvis getInstance() { return INSTANCE; }
    
    public void leaveTheBuilding() { ... }
}
```

Advantage:
- Gives you the flexibility to change your mind about whether the class should be a singleton without changing its API.

Has the same caveat mentioned above.

To make a singleton class serializable, it is not sufficient merely to add implements Serializable to its declaration.  
To maintain the singleton guarantee, you have to declare all instance fields *transient* and provide a *readResolve* method.  
Otherwise, each time a serialized instance is deserialized, a new instance will be created.

```java
// readResolve method to preserve singleton property
private Object readResolve() {
    return INSTANCE;
}
```

As of release 1.5, there is a third approach to implementing singletons. Simply make an enum type with one element:

```java
// Enum singleton - the preferred approach
public enum Elvis {
    INSTANCE;
    
    public void leaveTheBuilding() { ... }
}
```

Advantages:
- More concise
- Provides the serialization machinery for free
- Provides an ironclad guarantee against multiple instantiation

**Summary:**  
A single-element enum type is the best way to implement a singleton.

### Enforce noninstantiability with a private constructor

A class that is just a grouping of static methods and static fields do have valid uses.
Such *utility classes* were not designed to be instantiated: an instance would be nonsensical.

**Attempting to enforce noninstantiability by making a class abstract does not work.** The class can be subclassed and the subclass instantiated.
Furthermore, it misleads the user into thinking the class was designed for inheritance.

**A class can be made noninstantiable by including a private constructor**

```java
// Noninstantiable utility class
public class UtilityClass {
    // Suppress default constructor for noninstantiability
    private UtilityClass() {
        throw new AssertionError();
    }
    ... // Remainder omitted
}
```

The AssertionError isn't strictly required, but it provides insurance in case the constructor is accidentally invoked from within the class.  
It is wise to include a comment on the constructor.  
Side effect: this prevents the class from being subclassed.

### Avoid creating unnecessary objects

