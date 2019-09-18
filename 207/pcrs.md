# Java - PCRS

# Quest 1

## Running things
* In python we could run modules, that is code that exists in a file which executed from top to bottom.
* We no longer have this freedom in java; everything is organized around classes. 
  * When we execute a program in java, a class is actually executed, but which method does it call? A special one called main.

## Typing
* Every variable has a type, which must be declared
* `int i;` declares `i` to be of type `int` and space is reserved for it. Instead we could have also written `int i = 42;` which assigns the value immediately after declaring it, though we could have postponed that for later.

## Variables
Java keeps track of the following
* Name - Provided on declaration
* Type - ditto
* Memory Space - used to hold the value of the variable
* Value - Can be given in the assignment statement

Note `int i = 19.2` will cause an error, since java would try to convert 19.2 to an integer, though it would create a loss of information, so it doesn't, on the other hand we can write `double i = 19` as no information is lost

### Variable Questions
1. We must assign an integer value so only the first makes sense 

2. The first seems fine, assuming we can do multiple variable declaration. The second one should not work as you will get a duplicate variable error. Fourth seems ok, as a is declared then assigned later on. Last is bad, no typing we can't use a variable that we haven't declared.

<hr>

## Reference types and Primitive types

### Basic Types
* `int` - `int age = 19;` just like python
* `String` - `String name = "ring"` observe, we must use double quotes
* `boolean` - `boolean teacher = true;`
* `double` - `double pi = 3.14`, A double is like a float in python, though it has extra memory allocated so it's possible to have more precision.

Note: There are more real and integer values types that trade up memory vs precision

### Reference Types
* Begins with a upper case letter
* Just like in python a Java variable cannot hold a `String` value directly inside of itself; only a reference to an object of type string
  
### Primitive Types
* Begins with a lower case letter
* type `int` is an example of a primitive type, it can hold an int value directly inside of itself.

An Example
```java
public class Simple {
    public static void main(String[] args) {
        int age = 21;
        String name = "Jude";
        System.out.println("Ciao!");
    }
}
```
Firstly observe tat age is primitive type, so we know that the value will be stored directly inside itself, and that name is a reference type so it will be referencing an object of type string. Below is the given stack frame

![](https://i.imgur.com/hmCnm98.png)

## Strings
* declaration can be done in two different ways `String s = new String("cat");` or the shorthand `String x = "dog";`
* Recall that it is a reference type, it stores a reference to a string object.
* They are immutable, that is it can't be modified after it has been created, we can operate on strings, though instead of changing the string it simply will return a new one.
* Concatenation: `String cd = s + x;`
* Indexing: `char c = cd.charAt(2);`, this is equivalent to `cd[2]` in python.
* Slicing: `cd = cd.substring(2, 4);` ~ `cd[2: 4]` in pyth
* Stripping: `cd = "    x    ";` -> `cd.trim();` removes trailing whitespace. Same as strip in pyth

Note: There are other useful methods that can be found on the java docs

### StringBuilder
* A sequence of characters, that **is mutable** 
* A reference type
* We cannot use the same shorthand as for strings, the following results in an error `StringBuilder sb = "x"` as we cannot convert a string into a `StringBuilder`
  

Examples
* Declaration: `StringBuilder sb = new StringBuilder("xyz");`
* Mutation: `sb.append("abc");`, `sb.insert(3, "def");`, `sb.setCharAt(3, 'k')`, `sb.reverse();`, more on docs.

### char
* We can use a `String` to hold a single character, though we have a primitive type that fulfills this need.
* When declaring, we must use single quotes when providing a literal value of type `char` eg. `char c = 'x'`
* Observe that SB's method setCharAt requires it's second argument to be of type char, therefore we used single quotes in the above SB example.

### Why a StringBuilder?
* Consider the following
```java
String x = "dog";
String y = "mat";
x = x + y;
```
Here we construct a new `String` object
* And now we have
```java
StringBuilder a = new StringBuilder("rat");
StringBuilder b = new StringBuilder("hat");
a.append(b);
```
* The second method modifies an existing object rather than creating a new one, therefore the second method is quicker.

## String Questions
1. After a couple wrong attemps, I figured it out, when we use double quotes to create a string, it first searches for the same value in the string pool then returns the reference, when we use new, it creates a new string object in the java heap.
   ![](https://i.imgur.com/VwLQEtP.png)
2. The second one is missing the new operator, the sixth one isn't giving a type for the declaration, the last two will work, though the second last one searches the string pool first to save memory.

For the memory model, if we use the `String x = "k";` syntax, it gets a place in the memory pool, otherwise it creates a new object.

String Splitting, remember to intialize ret to empty string.
```java
      String ret = "";
      String[] words = tester.split(" ");
      for (int i = 0; i < words.length; i++){
          ret += words[i].charAt(0);
      }
      return ret;
```

Implement both methods then use them in the last part.

<hr>

## Classes

### Constructing
```java
StringBuilder name;
name = new StringBuilder("Viriyakattiyaporn");
```
* Memory is allocated for the new object
* Arguments are evaluted
* Appropriate constructor is called (by the number and of arguments)
* A reference is returned to the newly-constructed object, in the above code we assigned this refernce to the variable `name`, below we can use it directly
`new StringBuilder("Professor").append(" Horton")`
* To learn what operations we can peform on our new object reference the java documentation, where we can learn about the interface not the implementation details (API).

### Calling methods
```java
String band = "Arcade Fire";
// Call an instance method via an instance.
int size = band.length();
```
* Above we call the length method on a type of `String`
```java
// Call a class method via the class name.
double x = Math.cos(48);
```
* Above we have a method associated with not individual instances of a class, but the class as a whole, this is called a class method.

### Data Members
* If a class has an instance varible (known as a `static` variable) which can be accessd as an instance variable or through the class name
`System.out.println(Integer.BYTES);`

### Garbage Collection
* Java automatically de-allocates memory for an object when no variable refers to an object.
* We can do this by hand by setting the variable holding said reference to null.


## Arrays
* Has a fixed length, set on declaration which never changes
* All elements in the array are of the same type 
* Declaration: `type[] name`
* They are reference types, when we declare an int array numbers like this `int[] numbers;` we create a variable that refers to an array.
* Since it is a reference type it will be referencing to an object containing a sequence of ints. This object must be created by using new, usually it could look like this `x = new String("y");`, though with arrays we will use a different special syntax, we still use new though now we will use square braces with an argument to the constructor which is the size of the array, like this: `numbers = new int[5];`. At this point we have a new array object that is on the heap, has 5 spots that can hold an int with a default value of 0 (each type has it's own default value), numbers refers to the whole object. 
* Alternatively we can construct and intilize the array all at once, as follows `numbers = {1, 2, 3, 4, 5, 6, 7}`
* The length of the array is stored in it's length attribute and can be accessed as so `numbers.length`
* We can access elements the same was as in pyth, so we can also assign a value to the int `numbers[1] = 512;` observe that we are storing an int which is a primitive type, therefore the value is stored directly in the array. We count up from 0, as usual
  
Note: We can't do special indexing as in python where we can use negative numbers as it must be withing the correct range, namely {0, ..., len - 1}

### Why so restrictive?
* Java actually has more flexible arrays that act more like the lists we know from python, though implementing such an array takes up more space and time. So we get the choice of having a super efficient array , or a less efficient but more flexible ArrayList

### Different Types in the Array
* Inheritance helps us here, every java class is a descendent of the built in class `Object`, therefore if we declare our list to be of type `Object`, then we gain more freedom, observe
```java
Object[] miscellany = new Object[5];
miscellany[0] = new String("hi");
// for primitives we must wrap them in an object
miscellany[1] = new Integer(23);
// Since every class is a descendent we can use any class we define, say Computer
miscellany[2] = new Computer("thinkpad");
// Arrays are a type of object so we have
miscellany[3] = new int[50];
```

Even though we can now put different types in our arrays, there are drawbacks, all java knows is that the elements are of type `Object` observe
```java
// No complaints
Object ele = miscellany[0];
// java only knows that it's of type object, so it won't allow us to do this
String s = miscellany[0];
```

Though we know that that element is a string, so we can cast it to a string, which tells java that indeed it is a string, we do so like this. `String s = (String) miscellany[0];`. If you cast an object to the incorrect type, we will get a CastException.

### Two dimensional Arrays
```java 
int[][] longChess;
// Now has 20 elements that refer to an array of 5 elements
longChess = new int[20][5];
longChess[19][5] = 12;
```

TODO: Ask about this.

In this example the elements are referring to arrays, though, we can make the two levels to the array separately, like so 
```java
int[][] longChess;
longChess = new int[20][];
for (int i = 0; i < 20; i++) {
    table[i] = new int[5];
}
```
This allows us to make multi-dimensional arrays of varying size
```java
int[][] weirdChess;
weirdChess = new int[3][];
weirdChess[1] = new int[99];
weirdChess[2] = new int[10];
weirdChess[1][8] = 170;
```

### Indexing Questions
* Remember `dee[0]` is an array itself.
* `dee[x][y]` where x is in 1 5
* Indexing starts at 0!

 ## Aliasing
 * When an object is created it's possible to create multiple variables that refer to this object, for example we have
```java
String name = new String("Justin Trudeau");
String primeMinister = name;
```
and in memory we observe that name and pM are referencing the same obj, in this case we say these variables are aliases or aliasing.
![](https://i.imgur.com/9TVJje0.png)

### Primitives & Aliasing
* Recall that `int` is a primitive so, so no aliasing happens, we see in the following example
```java
int number = 42;
int answer = number;
```
![](https://i.imgur.com/stFLkzW.png)
See that the variables contain their own `int`.

### Side-Effects
* Consider the situation where we have two references to the same object and we are calling some method that may modify some property of it as below
```java
// Create a Monster of size 12.
Monster one = new Monster(12);
Monster two = one;
// Increase the size of Monster two.
two.grow();
// Monster two now has size 24.  How big is Monster one?
int n = one.size();
```
Since one and two are aliases, we know that when two modifies the object that one is also modified as the point to the same object.

#### Only if mutable
* If we have aliasing to an immutable type, say `String` object, then if we modify one of the variables, we know that only a new string could have been returned, therefore the aliasing is broken, observe the following example
```java
String name = new String("Justin Trudeau");
String primeMinister = name;
primeMinister = primeMinister.replace('u', 'U');
System.out.println(name);
System.out.println(primeMinister);

// The output from this code is:

Justin Trudeau
JUstin TrUdeaU
```

### Avoiding Side effects
* When we have aliasing to a mutable object, then we get side effects, to avoid this we make a copy
```java
String[] words = {"hello", "bonjour", "adieu", "tschuss", "ciao"};
// This tries to be a copy, but it's not; it's an alias.
String[] copy1 = words;
copy1[1] = "xox";
String[] copy2 = new String[words.length];
for(int i = 0; i < words.length; i++) {
    copy2[i] = words[i];
}
copy2[3] = "yoy";
```
TODO: Ask about id77 for our copy.
![](https://i.imgur.com/D48nRD0.png)

### Shallow/Deep Copy
* In the above example we see that even though words and copy2 are separate arrays, the actual items inside of it refer to the same string objects, therefore there is some level of aliasing deeper within the structure, since the only items are of the `String` type so we could never have side effects, though if these items were mutable we could run into side effects for example
```java
int[][] table = {
    {11, 22},
    {5, 10}
};
int[][] copy = new int[2][2];
for (int i = 0; i < table.length; i++) {
    copy[i] = table[i];
}
int[] row = {0, 0};
copy[0] = row;
// Changing copy[0] did not change table.  All is right with the world.
// What happens if we do this?
copy[1][1] = -99999;
```
in this case the last line of the above code changed it changes both copy and table. To avoid this we have have to make a copy of table at every level, this is known as a **deep copy**.

## Questions
1. Primitive types store their values inside of themselves, therefore we can never have aliasing as they don't reference to an object.
2. Primitive types are immutable, observe the String class is immutable but StringBuilder is not.
3. All arrays are mutable, Array list is also mutable, note that Double wraps the double type which changes it from a primitive to an object.

1. By it's name we assume it's Immutable, therefore we can't modify it

# Control Structures
### If Statements
* Usually we write like this 
```java 
 if (classSize > 100) {
            sections = 2;
            classSize = classSize / 2;
        }
```
* Though if the body is just one line we can have
```java 
if (classSize > 500)
            System.out.println("Wow, that's big!");
```
beware if we add more lines beneth this don't let the indentation fool you, it's outside of the if -block, so always use 
* We use `else if`, rather than `elif`

### While loop
```java
        int number = 37;
        int divisor = 7;
        while (number > divisor) {
            number = number - divisor;
        }
        // We know here that (n > divisor) is false.
        System.out.println("Leftover: " + number);
```
* Unlike the case for if statements even if the body is one line long it should still have curly braces

### For Loops
* The syntax is C-like, and is as follows
```java
    //   This is the general structure of a basic for-loop:
        for (initialization; termination; increment) {
            loop body
        }
```
* The initialization is executed once, before iteration, often sets a counter to 0, though it can be any statement
* Termination, is a boolean condition, if true the loop body executes then the increment executes
* The increment as suggested by it's name is a statement which increments a variable, though it could be any statement.
* Observe the `while` loop equivalent
```java
// You may have noticed that the for-loop template above is equivalent to this while loop:
    initialization
    while (termination) {
        loop body
        increment
}
```
* We note that in the following example, the declaration of `i` in the initialization limits it scope and after the loop completes it disappears
```java
// Here is a simple example, where we find the sum of the first n
        // numbers.
        int n = 15;
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            sum += i;
        }
        System.out.println("Sum of the first " + n + "numbers is " + sum);
```
* Looping over indicies is as follows
```java
for (int i = 0; i < powers.length; i++) {
            System.out.println(powers[i]);
        }
```
Note that if the two code blocks were concatenated together, then it would still be fine since the old `i` is gone. This iterates over 0 to length - 1.

## ++, +=
* `i++` is equivalent to `i = i + 1`, same for `-- `
* Also recall `x += y` is equivalent to `x = x + y`, and same for `-`
* `++i` TODO: Ask about this

## Enhanced For-Loops
* This is more similar to the for loop we used in python. It works for both arrays and collections.
```java
for (int p : powers) {
            System.out.println(p);
        }
        // This loop is much simpler, and therefore less error prone, than
        // the one above that uses a regular for-loop.  You should use
        // enhanced for-loops whenever possible.
```

### If-Statement Questions
* We cannot say `i > j > 3` as it is a binary operator in java, though python was leaniant, and the last one doesn't make sense, by the same reasoning
* Recall  if the body of an if statement is only one line we don't need to write in the curly braces.

### For-Loop Questions 
#### P1
* We can initialize i inside or outside the for loop, we can also move the increment to the inner part of the loop.

## Do-While (And while alternatives)
* Written as below
```java
do {

//your code inside

} while (condition);
```
this code checks the condition **after** the loop runs, this insures that the code runs at least once.
* Recall that `i++` increments the variable after the condition is checked, whereas `++i`increments before.
```java
int i = 0;

while (i++ < 10);
```
* This new type of while loop lets us increment or decrement indicies until the condition is met. For example
```java
int[] A = new int[] {2, 4, 6, 8, 10, 12};

int i = 0; 

while (A[i++] < 7); 
```

### LL
* Iteration Q from pcrs
```java
    Node curr = first;
      while (curr != null && curr.next != null) {
          curr = curr.next;
      }
      return (curr == null)? null : curr.value;
```

## Classes
### Variables defined at teh class level
* When we define variables outside of any method, they come in two types
  * Instance varaibles: Evern instance of the class contins their own instance of each of these variables. And are generated when the instance is constructed `new X()`
  * Class Variables: Every instance of the class shares a single instance of each class variable, this is useful if we want the instances to acculmulated a value together. For example if we had a class `Monster` with a class varaible called `population` this should be a class variable since we want the sum of each moster stored in one location, not the literal value `1` stored in each population associated with an instance of a new monster.
  * We indicated a variable to be a class variable by using `static` when we declare it, through unlike the english definition of static: these values can change.
```java
 // The number of Monsters created so far.
    private static int population = 0;

    // === Instance Variables ===

    // The size of this Monster.
    private int size;
    // The name of this Monster.
    private String name;
    // The contents of this Monster's belly.
    private Monster[] belly;
    // The number of items in this Monster's belly.
    private int fullness;
```

## Representation Invariants
* Any type of constraints between the values of the instance variables, and relationships between them. Methods must make sure of the following
  * At the start of themethod body, we assume that the constraints hold, as to help us accomplish whtat the method is to do
  * By the end of the method body, we ensuer that the constraints are in fact still true. This guides us with the development of the method body, and tells us a part of what we must accomplish
  * An example: Say we have an "eat" method, though our RI's state that the belly array is already sorted based on monster size, our eat method havs to make sure that the belly array is sorted by the end of the method, though we assume that the array was sorted at the beghinning therefore we only have to insert the new item into the right spot in the sorted array.

## Constructor
* Has the same name as the class, with no return type. It is called automatically when an insatnce of the class is created, when "new" is used.
* We can in fact have multiple constructors so long as their signatures are different. This is useful if we want to be able to provide different sorts or amounts of information on intiialization, for example, we could initialize a `Monster` with , name size and bellyCapacity, or we could not provide any information, in which case the defaults will be used note how we do this below. Java figures this out by the number and type of arguments we provide.
```java
    public Monster(String name, int size, int bellyCapacity) {

        this.size = size;
        this.name = name;
        this.belly = new Monster[bellyCapacity];
        this.fullness = 0;
        this.population += 1;
    }
    public Monster() {
        this("Monster" + String.valueOf(population), 10, 3);
    }
```
* No-contructor
  * If we don't define any constructor at all, then one is supplied by the complier with no parameters and no body (no-arg  constructor), it is only there so the `new` statement compliles and runs. If you define a constructor, then the no-arg constructor is no longer supplied so then if that constructor contained at least one parameter, then the following wouldn't compile `Monster m4 = new Monster();`

## Methods
* A return type must be declared in front of the method name, note if it returns nothing then we write `void` as it's type.
* Returning is identical to pyth, though in a void method we don't return anything, so it cannot have a return statement.
* If we reach the end of a method without encountering a return statement then, unlike pyth, we don't return anything

## Overloading
Method overloading is a feature that allows a class to have more than one method with the same name, if their argument list differ. Unlike overriding, they both still exist separately though the parameters you will input will be different.


They must differ in one of two ways
1. The number of parameters
`f(int)` then `f(int, int)`
2. Type of parameters
`f(int, int)` then `f(int, float)`
3. Sequence of parameters
`f(int, float)` then `f(float, int)`

* The reason we would use it is to provide the option of using default values for argument, in python we could do this in the signature but in java we don't not have this functionality
* Overloading is good style
```java
  /**
     * Grows this Monster.
     *
     * @param factor The factor by which this Monster is to grow.
     */
    public void grow(int factor) {
        this.size = this.size * factor;
    }



    /**
     * Grows this Monster by a default factor.
     */
    public void grow() {
        /*
           Again, we call the other "grow" method to do the work.  This method
           would be one line long either way, but it is still smart to not
           repeat the code here.
        */



        grow(2);
    }
```

## Accessibility Modifiers
* `public` - vizible and can be accessed from all classes everywhere and the methods are included in the API for the class
* `private` - Consdider a method `X` which uses `z` as a helper, if we want to prevent client code from calling it we can declare it as private, this means it can only be called by other methods in the same class. Even subclasses wouldn't be able to access it.
* You can also control these modifiers on instance and class variables
* The philosophy in java is to make everything private unless you have a good reason not to. Methods may be part of the API, in which case they are public, but variables rarely belong in the API since it ties you down to your current implementation.
  * If we client code wants to know the value of a private variable, instead of changing the accessibility modifier we can define a public method which will return that value. If we want client code to be able to change theses values then we do the same thing, these are called "getters" and "setters"
  * We use getters and setters for good reason, here is an example. Let's say the class monster had an instance variable that kept track of their population, if instead we removed this variable kept track of the monsters in a Queue and made a method that returns the population using the Queue implementation, then no code would have to change. If instead we just had an inststance variable that kept track of the literal number then if we do the same change as above then every piece of client code that uses that insace variable would have to change

## toString
* the `toString` method is like the `__str__` method from pyth and is called implictly if we print an object, since all classes are descendents of class Object, so if he toString is not defined then it inherits one from class Object which returns a unique identifier for the object whose toString was called.

## @Override
* This annotation tells the reader and java what we will be doing, that is overriding
* It has a use which is to help catch errors, so if we accidentally mistype the name of the method we are attempting to override it will throw an error instead of defining a completely new one.

## equals
* This is java's version of python's `__eq__` method, though note, when we use `==` that is identity equality, then the equals method is not used, if we want to use it, it must be called by name
* The default equals method from Object it checks for identity equality, and so we can override it if we want different functionality
* When we override it though there are details which must be followed that is 
    1. Symmetry: For non-null references a and b, a.equals(b) if and only if b.equals(a)
    2. Reflexivity:  a.equals(a)
    3. Transitivity: If a.equals(b) and b.equals(c), then a.equals(c)
    * In addition we must also override an inherited method by the name of hashCode, the hashCode of an object is an integervalue that obeys this property
      * If two objects are equal (according to the equals method), they have the same hashCode. Though note it's possible for two objects to have the same hashCode and them to be different

## Class Methods
* Like class variables we use `static` to declare them
* Recall this allows a method to be associated with the class and not the instance, by prefixing the method with the class name like so: 
` System.out.println("Monster population: " + Monster.population()); `
* A class method cannot access an instance variable or call an instance method directly and you cant use `this` inside this method, the only way we can access an instance variable or call an instance method is if a reference to an object is passed to the method.
```java
    public static int population() {
        /* Using a class variable

        Because population was declared "static", there is only one,
        shared by all instances of Monster.  It is not stored in every
        instance of Monster.  So it would not make sense to say:
              return this.population;
        and in fact, that line would not compile.  We can access the
        variable through the class name, as below.  If we omit the
        class name and say simply:
              return population;
        Java would still find the class variable and the code would
        work the same.  However, it's good practise to be explicit
        and say that you mean to refer to a class variable. XXX Agreed?
         */
        return Monster.population;
    }
```

## Parameters
* Recall the following process when we call a method
    1. A new stack frame is pushed onto the stack
    2. Each parameter is defined in that stack frame
    3. The value of each argument is assigned to it's corresponding parameter.
* When we hit a return statement or get to the end of the method, the stack frame for that method is popped off the stack and all variables defined in it, that is local variables and parameters dissappear.
* From part of 3 of the process when a method is called we know something like the following happens `p1 = a1, p2 = a2`, that is the parameters are assigned to their arguments, this leads to different implications based on if they are primitive types or if they are reference types.
```java
static void increase(int i) {
        i = i + 1000;
    }


    public static void main(String[] args) {
        int cost = 14;
        increase(cost);
        System.out.println(cost);
    }
```
In the above example, we can see that since cost is a primitive when we have `i = cost`, the reference to cost is not passed, but the number 14, is which is stored directly inside it. In python it would fail due to another reason though, it would fail since when we evaluate what is on the rhs of the equals sign it gets stored in a new memory addres and then i is assigned to that.
Back to java, in order to solve this problem we should instead define a new method that returns the changed value and in the calling code, assign it to the variable we wish to change, we could call this new function `increased`.

### Reference Types cause Aliasing
* If the argument to a method is a variable, the parameter is assigned to the value contained that is contained within the variable. If it is a reference type then a reference is stored within the parameter, causing aliasing.
* An example of passing in a mutable type
```java 

static void increase(StringBuilder sb) {
    sb.append(sb);
    sb.append("!");
}


public static void main(String[] args) {
    StringBuilder word = new StringBuilder("rah");
    increase(word);
    System.out.println(word);
}
```
See here that in fact the call to `increase` has side effects, that is it modifies a variable outside of it's local scope.

# Quest 2
### Interface
This is like abstract classes in python. An interface in java is like a class though all methods are abstract  and (final fields)? are constants. We can implement an interface by providing code for each method from the interface.
```java
public interface Playable
{
    void play();
}
```


### Questions
#### Part 1, overloading
1. No methods are being overloaded each method `func` for both class `A` and `B` are completely separate
2. class B is overriding, not overloading.
3. Yes, this involves overloading, we now have two methods that are named the same though their arguments differ.
4. I believe this involves overriding, class B extends A therefore it has inherits the original `func(int i)` and then we overload it by saying `func(String s)` now, we have two different methods with the same name, note it doesn't matter that it's calling the super class method, since any method could do that, I think they were trying to trick us into thinking this method extends the function that it inherited.
5. We have overloading here as we have two methods with the same name but different signatures

#### Part 2, overloading
1. We can differentiate between the two different functions
2. These are pretty much the same function, so this should probably error, and it only checks # of parameters and type not the name
3. Diff no of params, so should be fine
4. Same func, but with different return value, this is not enough information for the complier to figure out which is which, so error
5. Yes, order is diff
6. This does not result in an error but also it doesn't even involve overloading

#### Part 3, overloading
```java
public class MyHashing {
    private int seed = 100;
    public MyHashing() {
    }
    public MyHashing(int seed) {
        this.seed = seed;
    }
    public int hash(String s) {
        int total = 0;
        for (char ch: s.toCharArray()) {
            total += ch;
        }
        return total;
    }
    public int hash(int i) {
        int tseed = this.seed;
        this.seed = i;
        return tseed;
    }
    
}
```
#### Static Questions, pt1
* `static` types means that they all share the same variable, it's a class variable, so by the end, they all share 3, as for the other variable, it is not a class variable, each one has been increased so they are all equal to 1.

* In a static method we cannot access `this`
1. We can access a class variable in the class method
2. We canot access an instance variable in the class method
3. We can access a class variable in a instance method
4. We can access a instance variable in a instance method
5. It's fine to access a class method like class.method()
6. We can't do this with non-class methods

#### Static Questions, pt2
* Candy Mountain
```java
import java.util.Random;

public class CandyPlayer {

  private static int totalCandy = (new Random()).nextInt(100);
  private int candies;
    
    public CandyPlayer(int candies) {
        this.candies = candies;
    }
    public int getMyCandy() {
        return this.candies;
    }
    static int getMountainCandy() {
        return totalCandy;
    }
    public boolean play(int gcan) {
        if (gcan <= this.candies) {	
            this.candies -= gcan;
            totalCandy += gcan;
            if (totalCandy - 2*gcan >= 0) {
                this.candies += 2*gcan;
                totalCandy -= 2* gcan;
            }
            return true;
        } else {
            return false;
        }
    }
    
}
```
part 2
```java
import java.util.Random;

public class CandyPlayer {

  private static int totalCandy = (new Random()).nextInt(100);
    private int candies;
    
    // New variables
    private static int turn;
    private static int nop;
    
    private int uid;
    
    // Getters
    public static int getTurn() {
        return turn;
    }
    public static int getNumberOfPlayers() {
        return nop;
    }
   // Setters
    public static void setTurn(int nturn) {
        turn = nturn;
    }
    public static void setNumberOfPlayers(int nnop) {
        nop = nnop;
    }
    
    public CandyPlayer(int candies) {
        this.candies = candies;
    }
    public int getMyCandy() {
        return this.candies;
    }
    static int getMountainCandy() {
        return totalCandy;
    }
    public boolean play(int gcan) {
        // Not your turn!

        if (!(this.uid == turn)) {
            return false;
        }
        // Ok You can play, it is your turn
        
        turn += 1;
        if (turn == nop) {
            turn = 0;
        }
        if (gcan <= this.candies){	
            this.candies -= gcan;
            totalCandy += gcan;
            if (totalCandy - 2*gcan >= 0) {
                this.candies += 2*gcan;
                totalCandy -= 2* gcan;
            }

            return true;
        } else {

            return false;
        }
    }
    
    
}
```

#### toString and equals
* Remember that when overriding the equals method, you must specify the parameter to be object so we don't overload, and we must cast this object to the correct type.
* If two hashcodes are the same then we are not sure if the objects are the same, only the opposite implication holds, therefore when we put into the hashmap we don't know which ones go into which bucket.
##### Part 3 last Q
* coord, 1, 2, 4 will have the same hashcode

## Equality
* Recall that in java `==` checks if we have two reference to the very same object, the equals method is used to check if the two objects have equivalent content, for example if we do 
```java
X l = X(z);
X o = X(z);
```
* Then `l == o` is false, since they reference different instances of `X`, but `l.equals(o)` holds, as we can see that they were built using the same paramter, therefore their content should be the same.

```java
X k = o;
```
* And then `k == o` would hold as they reference the same object
* java's implementation for the String object is as follows 
>"the result is true if and only if the argument is not null and is a String object that represents the same sequence of characters as this object."
* So when we write our own versions we can define any type of behavior we want.
* Recall that if you don't define an equals method you inherit one from class Object, it checks for identity equality.

### Special Case with String shortcut
if we construct a string like `x = "cat"`, that is we don't use `new` like `x = new String("cat");` then java saves spaces by only using one object for each unique string we create (String Interning), this yields some different results
```java
String s1 = "ice cream";
// Since the RHS of this assignment evaluates to the same String, "ice cream",
// Java doesn't bother to make a new String object.  It lets s2 reference the
// same String object as s1.
String s2 = "ice " + "cream";
// This may seem risky, but since Strings are immutable, no side effects 
// can occur despite the aliasing that is created.
```
In this case the following is true `s1 == s2` , `s1.equals(s2);`, 

#### Equality Quesitons
* Remember the last comparsion is true due to the special case we just discussed.
* Second one in part two is false, remember that if you don't define the equals method that that reference equality is inherited from `Object`

## Comparables
* this allows for sorting, a default sort method is provided that allows for arrays of ints or other primities to sorted. This method is overloaded, and there are multiples methods, that handle one of the primitive types, these methods are defined in the Arrays class, as a static method.
* In order to sort objects of other types and new ones we define, the designers of java have made a general sort method that accepts in an array of Object
* This sort method requires that every element have the `Comparable` interface, that is they must define the `compareTo` method
```java
 int compareTo(T o)
    // Compares this object with the specified object for order.
    // Returns a negative integer, zero, or a positive integer
    // as this object is less than, equal to, or greater than
    // the specified object.
```
* Let's say there is a MonthDay class which implements the `compareTo` method, then we k
