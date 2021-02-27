# Java Learning


# Java Learning ( Data Structures, mostly )

... And the greatest reason I learn it, is that ~~I LOVE COFFEE :coffee:~~ its DS are fuxxing easy to use.

## 01. Basic Usage in Java

### Way to write

- A `.java` File can be compiled through `javac` into `.class` File. `.java` File is called Source Code, after Compling it can be deleted.

- In every `.java` File can multiple `Class` be written. In every `Class` can multiple `Methods` be written. 

- After Compiling, execute `java class_name` in Terminal to run Functions in a specific class.

- A .java File can contain multipule class, __but only 1 public class__. Besides, the name of the public class must be same as the `.java` file.

    ```java
    // C.java
    class A{
        public static void main(String[] args){
            //Codes here
        }
    }

    class B{
        public static void main(String[] args){
            // Codes here
        }
    }

    public class C{
        public static void main(String[] args){
            // Codes here
        }
    }
    ```

- In every class, there is only 1 main Method. The way to write it is always this:

    ```java
    public class C{
        public static void main(String[] args){
            // Codes here
            // Attribute(s)
            // Method(s)
        }
    }
    ```

- At the end, like old Style, say "Hello world!":)

    ```java
    // HelloWorld.java
    public class HelloWorld {
        public static void main(String[] args){
            System.out.println("Hello World!");
        }
    }
    ```
## 02. Transformation of DataTypes in Java

- Except `boolean`, other DataType can be transformed into another.

- Low Capacity Data to High Capacity Data is called __Auto Transformation__. Capacity from low to high:
  
    __`byte < short / char < int < long < float < double`__

- High Capacity Data to Low Capacity Data is called __Forced Transformation__. This can cause __The Loss of Accurity__.

- Miss-Calculation among `byte, short, char`, they transform into `int` firstly.

- __Mix-Calculation among mix-DataTypes, they transform into the DataType with largest Capacity among them firstly.__

## 03. Methods in Class

### What is Methods

- Methods are a Piece of Code, they can handle with specific Problems and are written in Class ( __Method in Method is not possible!__ ), and the Sequence of Methods have no Influence on Code.

### Format

![Methods](/methods-in-java.png)

```java
[Modifier List] return-Type Method-Name(Parameters){
    Codes that handle with Problems;
}
```

### `static` or NOT?

- `Methods` without `static` can be used only through an `Object`. They are called as __`Instance Methods`__.

- if a Move needs Object to take part in, DONOT use `static`.

- `Methods` with `static` donot need `Object` to take part in. To access, `Class_Name.Method()`

    ```java
    class Method{

        public static void doSome(){
            // Codes
        }

        public void doOther(){
            // Codes
        }

        public static void main(String[] args){
            Student s = new Student();
            Method.doSome();
            // doSome();
            Method m = new Method();
            m.doOther();
        }
    }
    ```

### Usage

- You can define Methods, but you must not use them.

- In Class, type: `Class-Name.Method-Name(Parameters)`

- If `static` is in `[Modifier List]`*[(Reference here)](https://www.runoob.com/java/java-modifier-types.html)* or __the Methods are with the Calling-Code in the same Class__, `Class-Name` can be ignored.

- Methods in other Class, must be `Class-Name.Method-Name(Parameters)`.

### Overload: Methods with same Names and finish similar Functions.

- See Code below:

    ```java
    public class OverloadTest(){
        public static void main(String[] args){
            
            int result1 = sumInt(1,2);
            System.out.println(result1);
            
            double result2 = sumDouble(1.0, 2.0);
            System.out.println(result2);

            long result3 = sunLong(1L, 2L);
            System.out.println(result3);
        }

        public static int sumInt(int a, int b){
            return a + b;
        }

        public static double sumDouble(double a, double b){
            return a + b;
        }

        public static long sumLong(long a, long b){
            return a + b;
        }
    }
    ```

Though Functions `sumInt(), sumDouble(), sumLong()` are different, but they are similar.

- Overload see below:

    ```java
    public class OverloadTest(){
        public static void main(String[] args){
            
            int result1 = mySum(1,2);
            System.out.println(result1);
            
            double result2 = mySum(1.0, 2.0);
            System.out.println(result2);

            long result3 = mySum(1L, 2L);
            System.out.println(result3);
        }

        public static int mySum(int a, int b){
            return a + b;
        }

        public static int mySum(double a, double b){
            return a + b;
        }

        public static int mySum(long a, long b){
            return a + b;
        }
    }
    ```

Code above will automatically select which `mySum` will be used.

- When will Overload occur, __it goes with Parameters only__...

|               Case               |                                     Examples                                     |
| :------------------------------: | :------------------------------------------------------------------------------: |
|         in same `Class`          |                                     Basic 1                                      |
|    with the same Method Name     |                                     Basic 2                                      |
|  Parameters in different amount  |             `public static void m1(); public static void m1(int a)`              |
| Parameters in different Sequence | `public static void m2(int a, double b); public static void m2(double a, int b)` |
|  Paramaters in different Types   |         `public static void m3(int a); public static void m3(double a)`          |


## 04. JVM

### 3 primary Memory Spaces in JVM [Ref here](https://www.baeldung.com/java-stack-heap)

1. __Method Areas: <u>Codes and static Variables ( `Instance Variables` )</u>__

2. __Heap: storage <u>Instance Variables</u>. This Memory are handeled by Trash cycle Programm.__

3. __Stacks: when Methods are used, assign Room here, Stack-push. when Methods are finished, Stack-pop. on Running-Phase <u>local Variables</u> are storaged here. This Memory are mostly used.__

![JVM](/jvm-3.jpg)

### where are the Variables?

- Variables / Attributes beyond Methods in Class are called __Member Variables ( It's accessble only through Object ).__

    ```java
    class Student{
        //Member Variables below
        int stu_No; 
        String name;
        int age;
        String address;
        ...
        // Member Variables without `static` are called Instance Variables;
        // instead, Member Variables with `static` are called static Variables.
    }    

    public class myClass{
        public static void main(String[] args){
            
            int i = 10;
            Student s = new Student();
            // s maps the Address of the Instance, 
            // Instance / Object is storaged in Heap in JVM
            // s and i are storaged in Stack in JVM
            // s have Member Variables.
        }
    }
    ```

In the Code above, __i and s called local Variable ( in Stack )__, s' Attributes like __stu_No, age, etc. are called Instant Variables ( in Heap ).__

- `Member Variables` contain `static Variables` and `Instance Variables`.

![Memory-Variables](/JVM-Memory.png)

| Modifier |          Function           |
| :------: | :-------------------------: |
| `public` |     accessible anywhere     |
| `static` | accessible without `Object` |

## 05. Object-oriented

### 3 Features

1. Encapsulation ( Attributions )

    - simplify, offer simple Interfaces for Users. ( i.e, Camera )

    - after Encapsulation there is Object

    - after Encapsulation the Programms becomes resuable

    - improve the Security

    - `private` Attributions $\rarr$ write Interfaces ( `set` and `get`. __These 2 Methods have no Modifier `static`__)

    ```java
    class Student{
        private String name;
        private int age;
        private String addr;

        public void setName(String myName){
            name = myName;
            // Code that determins the Legality
        }

        public String getName(){
            return name;
        }
    }
    ```

2. Inheritance

    - Ancestor: `java.lang.Object`
    
    - `[Modifiers] class subclass extands superclass{}`
    
    - Basic: Reusablility of Codes;
    
    - Advanced: Base Stone of the __Overload__ and __the Polymorphism__
    
    - `superclass` and `subclass`
    
    - __private, Constructors__ are not inheritance.

3. Polymorphism

    - upcasting: `subclass` $\rarr$ `superclass` ( automatic )
    
    - downcasting: `superclass` $\rarr$ `subclass` ( forced ) when specific `Methods` are only in `Subclass`
    
    - __There must be extend-Relationship by upcasting and downcasting__

    ```java
    public class Animal{
        public void move(){
            System.out.println("Animal Moving!");
        }

        public static void main(String[] args){
            Animal a = new Bird(); 
            a.move();
            //Bird to Animal, upcasting
            // a.move() -> Bird Flying!
            // a.sing() -> CANNOT compile. In Class Animal there's no Method called "sing()"
            // In other Word: Compile check a's Class, Animal. But Animal cannot sing.
            // Run: run Methods in Bird. Because we have a Bird() Object "newed".

            // when we want Animal a to sing, we can transform its' DataType
            Bird b = (Bird) a;//Animal to Bird, downcasting
            b.move(); //Bird Fying!
            b.sing(); // Bird Singing!
            
            Cat c = (Cat) a;
        }
    }

    class Bird extends Animal{
        public void move(){
            System.out.println("Bird Flying!");
        }

        public void sing(){
            System.out.println("Bird Singing!");
        }
    }

    class Cat extends Animal{
        public void move(){
            System.out.println("Cat Jumoing!");
        }

        public void catchMouse(){
            System.out.println("Cat catches Mouse!");
        }
    }
    ```

   - `java.lang.ClassCastException` It happens in `downcasting`.

    ```java
    /*
    Codes below can compile.
    */
    public class Animal{
        public void move(){
            System.out.println("Animal Moving!");
        }

        public static void main(String[] args){
            Animal a = new Bird(); // We created a Bird Object, store its' Address in a with Animal.
            Cat c = (Cat) a;
            // Bird and Cat have no Inheritance Relationship. It cannot run.
            // But in Compile, while a's Type is Animal, Animal and Cat have Inheritance Relationship, compile works.
        }
    }
    ```

    - how to avoid `java.lang.ClassCastException` $\rarr$ `instanceof`

        - `Reference instanceof Data-Type`
        
        - returns `boolean`

    ```java
    public class Animal{
        public void move(){
            System.out.println("Animal Moving!");
        }

        public static void main(String[] args){
            Animal a = new Bird(); 
            // We created a Bird Object, store its' Address in a with Animal.
            // a is an Instance of Bird, but Reference is Animal.
            if(a instanceof Cat){
                Cat c = (Cat) a;
                c.catchMouse();
            }
            else if(a instanceof Bird){
                Bird b = (Bird) a;
                b.sing();
            }
        }
    }
    ```

### In the Life Circle:

1. Object Oriented Analysis (OOA)

2. Object Oriented Design (OOD)

3. Object Oriented Programming (OOP)

### Class / Object ( Instance ) in Java

1. Class: 
   
   - A Template, a Concept, doesn't exist in the real World, an abstract Result after Thought.
   
   - describes mostly Status (__Attributes__) and Actions (__Methods__).

2. Object: Individual in the real World.

### Constructor

1. Differences between `Methods` and `Constructor` ( __has `return-Type` or not__ )

    ```java

    [Modifier List] Constructor-Name(parameters){
        //Codes
    }

    [Modifier List] return-Type Method-Name(Parameters){
        //Codes
    }
    ```

2. __Constructor-Name must be same as Class-Name.__

### `this` Key Word

- `this` points at the Object itself. It's saved in __Heap__.

- `this` appears in `Instance Methods` ( Methods without `static` )

- `this` can also appear in `Constructors`, using other `Constructors` at the meanwhile.

    ```java
    public class Customer{
        
        String name;

        public Customer(){
            // this.name = "NULL";
            this(name);
        }

        public Customer(String name){
            this.name = name;
        }

        public void shopping(){
            System.out.println(this.name + "is shopping!");
        }

    }

    ```

### `static`

- an Example:

    ```java
    public class Customer {
        public static void shopping() {
            System.out.println("In shopping!");
        }
        
        public void running() {
            System.out.println("On running!");
        }

        public static void main(String[] args){
            Customer c1 = new Customer();
            // Method "running()" is only through an Object accessible.
            c1.running();

            // The following Codes output without Nullpointer Error.
            // There's Warning. static Methods are accessible through object, too.
            // BUT, Advice is, use it through "Class.static_Method()".
            c1 = null;
            c1.shopping();
        }
    }

    ```

- when `static` Variables?

    - Same Attribute(s) in Objects

    - `static` Variables are storaged during the Load of Class in __"Method Area"__

    - `static` Variables have Nothing to do with Objects.

    - `static Code Block` will be executed during the Load of Class from up to down and only once.

    - `static Code Block` can be used to record when the Class are loaded. ( Log )

    - p.S. `Instance Code Block` can be used to record when the Object are created.
  
    ```java
    public class Chinese{
        private String name;
        private String id;
        // the Variable "country" here are same: China.
        // private String country;

        // So we write it in this Way
        static String country = "China";
        // By writing in this way the Variable "country" is saved in "Method Area" instead of in "Heap"
        
        // It's accessible by:
        // zhangsan.country;
        // Chinese.country;
    }
    ```

- In `static` there's no `this`. It cannot visit `Instance Variables` and `Instance Methods` directly ( must through an Object ).

### `Override`

- when `Override`?

    - `Methods` in `Superclass` cannot feed the Need of `Subclass`
    
    - __Override Methods have same Modifier, returnType and Parameters__
    
    - __The Access Right must be same or higher__
    
    - __The Number of Errors must be same or less__
    
    - Deals with only `Methods` ( except `static Methods` )
    
    - Override the Methods in the __closet Superclass__

    ```java
    public class Animal{
        protected void move(){
            System.out.println("Moving");
        }
    }

    public class Bird extends Animal{
        public void move(){
            System.out.println("Flying");
        }
    }

    ```

### `final`

- `final Class` cannot be inheritaged

- `final Methods` cannot be override

- `final Variables` cannot be changed after Value given

- `final Variable` must be Value given __manually__

- `final static Variable` is called `Constant` ( e.g., `final static double PI = 3.1415926`, `Constant` write in __UPPERCASE__ )

    ```java
    public class Test{
        final int age = 24;
        // Variable age here must be a Value given.
        // And it cannot be given Value again.
    }
    ```

    ```java
    public class Test{
        final int age;

        public Test(){
            this.age = 24;
        }
        // Variable age here must be a Value given.
        // And it cannot be given Value again.
    }
    ```


    ```java
    public class Test{
        public static void main(String[] args){
            
            User u = new User(100);
            // Variable u above watiting to be handeled by Trash Recycling.
            Usre u = new User(200);
        }
    }
    class User{
        int credit;
        public User(int credit){
            this.credit = credit;
        }
    }
    ```

    ```java
    public class Test{
        public static void main(String[] args){
            
            final User u = new User(100);
            // Variable u above CANNOT be handeled by Trash Recycling. 
            // And we are noot allowed to new a new User Object
            u.credit = 10000;
            // But Variables in u can be modified.
        }
    }
    class User{
        int credit;
        public User(int credit){
            this.credit = credit;
        }
    }
    ```
## 06. Data Structure

### Math & Nums

- __Short, Integer, Long, Float, Double, Boolean,__ Character, Byte.

- Methods of Classes above: [click here](https://www.runoob.com/java/java-number.html)

- P.S. __Nums.toString()__: transfer a Number to String


### String

- Mostly used Methods:

    - __char charAt(int index)__: returns the Character at the Index.
    - __int length()__: returns the Length of the String.
    - __int parseInt()__: transfer the String into an Integer.
    - __char[] toCharArray()__: transfer the String into an Character-Array.
    - __boolean isEmpty()__: if the String is empty.
    - __int hashCode()__: returns the HashCode of the String.
    - __int indexOf(char ch(,int fromIndex))__: returns the Index of the Character ch the first time it appears( after the fromIndex).

- Other Methods of String: [click here](https://www.runoob.com/java/java-string.html)

- The __DataType__ above is often used to initialize a DataStructure ( See below ).

### Queue & Stack & Bag

|       Initialization       |                           Queue                            |
| :------------------------: | :--------------------------------------------------------: |
|       Initialization       | Queue<__DataType__> queue_name = new Queue<__DataType__>() |
|         int size()         |               returns the size of the Queue                |
|     boolean isEmpty()      |                judge if the Queue is empty                 |
| enqueue(__DataType__ Item) |                enqueue an Item into a Queue                |
|   __DataType__ dequeue()   |                 dequeue the first-in Item                  |


|         Options         |                           Stack                            |
| :---------------------: | :--------------------------------------------------------: |
|     Initialization      | Stack<__DataType__> stack_name = new Stack<__DataType__>() |
|       int size()        |               returns the size of the Stack                |
|    boolean isEmpty()    |                judge if the Stack is empty                 |
| push(__DataType__ item) |              push a new element into a Stack               |
|   __DataType__ pop()    |                  returns the last-in Item                  |

|        Options         |                         Bag                          |
| :--------------------: | :--------------------------------------------------: |
|     Initialization     | Bag<__DataType__> bag_name = new Bag<__DataType__>() |
|       int size()       |             returns the size of the Bag              |
| add(__DataType__ Item) |               add an Item into the Bag               |

### ArrayList

|              Options               |                               ArrayList                                |
| :--------------------------------: | :--------------------------------------------------------------------: |
|           Initialization           | ArrayList<__DataType__> arraylist_name = new ArrayList<__DataType__>() |
|             int size()             |                   returns the Size of the ArrayList                    |
| add(int Index, ___DataType__ Item) |                         add an Item into index                         |
|    contains(__DataType__ Item)     |                   if the ArrayList contains the Item                   |
|           get(int index)           |                       get the Item through index                       |
|   int indexOf(__DataType__ Item)   |                     returns the Index of the Item                      |
|               sort()               |                           sort the ArrayList                           |
|             toArray()              |                  transfer the ArrayList into an Array                  |
|             toString()             |                  transfer the ArrayList into a String                  |

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/ArrayList.html).

### LinkedList

|               Options               |                           LinkedList                           |
| :---------------------------------: | :------------------------------------------------------------: |
|           Initialization            | LinkedList<__DataType__> list = new LinkedList<__DataType__>() |
|             int size()              |               returns the Size of the LinkedList               |
| add((int index, )__DataType__ Item) |        add an Item at the end of the LinkedList / index        |
|          remove(int index)          |           remove the index-th Item of the LinkedList           |
|           get(int index)            |            get the index-th Item of the LinkedList             |
|         Object[] toArray()          |      returns an Array composed by the Items of LinkedList      |

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/LinkedList.html).

### HashMap

|                  Options                   |                                                  HashMap                                                  |
| :----------------------------------------: | :-------------------------------------------------------------------------------------------------------: |
|               Initialization               | HashMap<__DataType__ Key, __DataType__ Value> sites = new HashMap<__DataType__ Key, __DataType__ Value>() |
|                 int size()                 |                                      returns the size of the HashMap                                      |
| __value's DataType__ get(__DataType__ Key) |                                         returns the value of Key                                          |
|   boolean containsKey(__DataType__ Key)    |                                   if the HashMap contains the Key-Value                                   |
|          remove(__DataType__ Key)          |                                      remove the Item of the HashMap                                       |

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/HashMap.html).

### HashSet

|               Options               |                          HashSet                          |
| :---------------------------------: | :-------------------------------------------------------: |
|           Initialization            | HashSet<__DataType__> sites = new HashSet<__DataType__>() |
|             int size()              |              returns the size of the HashSet              |
| boolean contains(__DataType__ Item) |             if the HashSet contains the Item              |
|      remove(__DataType__ Item)      |              remove the Item of the HashSet               |

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/HashSet.html).
