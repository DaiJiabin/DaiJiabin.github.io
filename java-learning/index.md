# Java Learning


# Java Learning ( Data Structures, mostly )

... And the greatest reason I learn it, is that ~~I LOVE COFFEE :coffee:~~ its DS are soooooooooooo smoooooooth.

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

|  Modifier   |                  Function                   |
| :---------: | :-----------------------------------------: |
|  `public`   |             accessible anywhere             |
|  `static`   |         accessible without `Object`         |
| `protacted` | accesible in the same Package, and Subclass |
|    None     |       accessible in the same Package        |

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
    
    - _大家都知道花木兰替父从军的例子，花木兰替父亲花弧从军。那么这时候花木兰是子类，花弧是父类。花弧有自己的成员属性年龄，姓名，性别。花木兰也有这些属性，但是很明显二者的属性完全不一样。花弧有自己的非静态成员方法‘骑马杀敌’，同样花木兰也遗传了父亲一样的方法‘骑马杀敌’。花弧还有一个静态方法‘自我介绍’，每个人都可以问花弧姓甚名谁。同时花木兰还有一个自己特有的非静态成员方法‘涂脂抹粉’。但是，现在花木兰替父从军，女扮男装。这时候相当于父类的引用（花弧这个名字）指向了子类对象（花木兰这个人），那么在其他类（其他的人）中访问子类对象（花木兰这个人）的成员属性（姓名，年龄，性别）时，其实看到的都是花木兰她父亲的名字（花弧）、年龄（60岁）、性别（男）。当访问子类对象（花木兰这个人）的非静态成员方法（骑马打仗）时，其实都是看到花木兰自己运用十八般武艺在骑马打仗。当访问花木兰的静态方法时（自我介绍），花木兰自己都是用她父亲的名字信息在向别人作自我介绍。并且这时候花木兰不能使用自己特有的成员方法‘涂脂抹粉’。_
    
    - _那么终于一将功成万骨枯，打仗旗开得胜了，花木兰告别了战争生活。有一天，遇到了自己心爱的男人，这时候爱情的力量将父类对象的引用（花弧这个名字）强制转换为子类对象本来的引用（花木兰这个名字），那么花木兰又从新成为了她自己，这时候她完全是她自己了。名字是花木兰，年龄是28，性别是女，打仗依然那样生猛女汉子，自我介绍则堂堂正正地告诉别人我叫花木兰。OMG！终于，终于可以使用自己特有的成员方法‘涂脂抹粉’了。从此，花木兰完全回到了替父从军前的那个花木兰了。并且和自己心爱的男人幸福的过完了一生。_

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

    - classic Polymorphism Codes

        ```java
        public class Test{
            public static void main(String[] args){
                Master m = new Master(); // Parentclass oriented Programming
                Pet p = new Cat();
                m.feed(p); // Cat eating
            }
        }

        class Master{
            public void feed(Pet p){
                p.eat();
            }
        }

        class Pet{
            public void eat(){
                System.out.println("Pet eating");
            }
        }

        class Cat extends Pet{
            public void eat(){
                System.out.println("Cat eating");
            }
        }

        class Dog extends Pet{
            public void eat(){
                System.out.println("Dog eating");
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

3. Inner Class: 

    - Class in Class

    - `static`, `instance`, `local` inner Class

    ```java
    class Test{
        
        static class Inner1{

        } // static Class Inner1
        
        class Inner2{

        } // Instance Class Inner2

        public void doSome(){
            int i = 100;
            class Inner3{

            }// local Class Inner3, accessible only in doSome()
        }

    }
    ```

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

- Appears in `Constructor` and `Methods`, cannot appear in `static Method`

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

- `final static Variable` is called `Constant` ( e.g., `final static double PI = 3.1415926`, `Constant` should be written in __UPPERCASE__ )

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

### `super`

- __Father first, then Child.__

    ```java
    public class A{
        public A(){
            System.out.println("Constructor without Parameters in A!");
        }
        
        public static void main(String[] args) {
            A a = new A();
            System.out.println("------------------------------------");
            B b = new B();
        }
    }

    class B extends A{
        public B(){
            System.out.println("Constructor without Parameters in B!");
        }
    }

    // output

    Constructor without Parameters in A!
    ------------------------------------
    Constructor without Parameters in A!
    Constructor without Parameters in B!

    ```
    ```java
    public class A {
        public A() {
            System.out.println("Constructor without Parameters in A!"); // -> 1. Father First
        }

        public static void main(String[] args) {
            A a = new A();
            System.out.println("------------------------------------");
            B b = new B();
            b.getName();
        }
    }

    class B extends A {
        private String name;

        public B() {
            this("zhangsan"); // -> 2. Constructor with String
            System.out.println("Constructor without Parameters in B!"); // -> 3. syso
            System.out.println();
        }

        public B(String name) {
            this.name = name;
            System.out.println("Constructor with String in B!"); // -> 2. Constructor with String
        }
        
        public void getName() {
            System.out.println(this.name);
        }
    }

    // output

    Constructor without Parameters in A!
    ------------------------------------
    Constructor without Parameters in A! // -> 1. Father First
    Constructor with String in B! // -> 2. Constructor with String
    Constructor without Parameters in B! // -> 3. syso

    zhangsan
    ```

### `abstract class`

1. Definition

    - Class and Class have commen Features. These Features become `abstract class`. 

    - __`abstract class` cannot have Instance. But it can have Constructors -> used by `Subclass`__

    - __`abstract class` are used to be inherited.__

    - the `Subclas`s of `abstract class` can also be `abstract class`.

    - __`final` and `abstract` cannot be together.__

2. Howto

    ```java
    [modifier] abstract class class_Name{
        //Codes
    }
    ```

3. `abstract Methods` -> ( half abstract )

    ```java
    public abstract void doSome();
    // No Function Body ( no '{}' ), end  with ;
    ```

    __`abstract class` may not have `abstract Methods`, but `abstract Methods` must show up in `abstract class`.__

    __when there's a `Subclass` ( Non-abstract ), it must rewrite the `abstract Mehtods` in its' `Parent Class`.__

    ```java
    public abstract Animal{
        public abstract void move();
    }

    class Bird extends Animal{
        public void move(){

        }
        // if there's no rewirte of this Method, compile error.
    }
    ```

### `interface` -> ( total abstract )

1. Howto

    ```java
    [Modifier] interface interface_Name{
        //Codes
    }
    ```

2. `interface` supports `( multy ) Inheritage`

3. `interface` has only 2 Parts: __`( public static final ) Const` and `( public abstract ) Methods`.__

4. __Everthing in `interface` are `public`. `public abstract` before `Methods` can be ignored.__

    ```java
    interface A{

    }

    interface B{

    }

    interface myMath extends A, B{
        double PI = 3.1415926; 
        //public static final double PI = 3.1415926;
        int sum(int a, int b);
        //public abstract int sum(int a, int b);
    }
    ```

5. when an `unabstract class` __`implements`__ an `interface`, every `( public abstract ) Methods` in `interface` must be rewritten. `[Modifier]` must have `public`.

    ```java
    public class interface_Test {
        public static void main(String[] args) {
            myMath m1 = new myMathImpl();
            System.out.println(m1.sub(2,1));
            System.out.println(m1.sum(3,4));
        }
    }

    interface myMath{
        double PI = 3.1415926;
        int sum(int a, int b);
        int sub(int a, int b);
    }

    class myMathImpl implements myMath{
        public int sum(int a, int b){
            return a + b;
        }
        public int sub(int a, int b){
            return a - b;
        }
    }
    ```

6. one `class` can implement multiple `interface`. __`interface` can transform into other `interface` without Inheritage.__
 
    different from `class`, `upcasting` and `downcasting` in `class` must have Inheritage.

    ```java
    public class multi_implements {
        public static void main(String[] args) {
            A a = new D();
            B b = new D();
            C c = new D();
            B b1 = (B) a; //interface can transform into other interface

            // better way to write:

            if(a instanceof B)
                B b1 = (B) a;
            b1.m2();
        }
    }

    interface A{
        void m1();
    }

    interface B{
        void m2();
    }

    interface C{
        void m3();
    }

    class D implements A, B, C{
        @Override
        public void m1(){
            System.out.println("m1...");
        }

        @Override
        public void m2() {
            System.out.println("m2...");
        }

        @Override
        public void m3() {
            System.out.println("m3...");
        }
    }
    ```
    __This completes, that in Java `class` can extend only one single `class`.__
 
7. when `implements` and `extends` exist together: `class_Name extends parent_Class_Name implements interface_Name`

    ```java
    public class test04 {
        public static void main(String[] args) {
            flyable f = new Cat();
            f.Fly();

            flyable f1 = new Pig();
            f1.Fly(); //Polymorphism
        }
    }

    interface flyable{
        void Fly();
    }

    class Animal{

    }

    class Cat extends Animal implements flyable{
        public void Fly(){
            System.out.println("Cat! Fly me to the Moon!");
        }
    }

    class Pig extends Animal implements flyable{
        public void Fly(){
            System.out.println("Flying Pig! FFFFFFFF!");
        }
    }

    // output
    // Cat! Fly me to the Moon!
    // Flying Pig! FFFFFFFF!
    ```

### In a Word..

- `is a` -> `extends`

    ```java
    class Cat extends Animal{
        //Codes
    }
    ```

- `has a` -> `Attributes`

    ```java
    class Cat extends Animal{
        private boolean Tail;
    }
    ```

- `is like a` -> `implements`

    ```java
    interface Menu{
        void Steak();
    }

    class Cooker implements Menu{
        public void Steak(){
            System.out.println("cooking Steak...");
        }
    }
    ```

### An Example of `interface`

```java
// Menu.java
public interface Menu {
    void Steak();
    void Pasta();
}
```

```java
// Customer.java
public class Customer {

    private Menu foodmenu;

    public Customer() {

    }

    public Customer(Menu foodmenu) {
        this.foodmenu = foodmenu;
    }

    public Menu getFoodmenu() {
        return this.foodmenu;
    }

    public void order() {
        foodmenu.Pasta();
        foodmenu.Steak();
    }
}
```

```java
// AmericanCooker.java
public class AmericanCooker implements Menu {
    @Override
    public void Pasta() {
        System.out.println("Pasta with Pfeffer Minz!");
    }

    @Override
    public void Steak() {
        System.out.println("Steak with Butter!");
    }
}
```

```java
// ChineseCooker.java
public class ChineseCooker implements Menu{
    @Override
    public void Steak() {
        System.out.println("Steak with chinese Oil!");
    }

    @Override
    public void Pasta() {
        System.out.println("Pasta with chinese Tomatoes!");
    }
}
```

```java
// menu_Test.java
public class menu_Test {
    public static void main(String[] args) {
        Menu cooker1 = new ChineseCooker();
        Customer customer = new Customer(cooker1);
        customer.order();
    }
}
```

### Differences between `interface` and `abstract class`

|             `interface`             |                                 `abstract class`                                  |
| :---------------------------------: | :-------------------------------------------------------------------------------: |
|           total abstract            |                                   half abstract                                   |
|        without `Constructor`        |                                with `Constructor`                                 |
|        multiple Inheritance         |                                single Inheritance                                 |
| only `Const` and `abstract Methods` | a `class` can `implements` multiple `interface`, but only 1 `class` to inheritage |


## 06. `package` and `import`

1. `package <Package_Name>;`

2. Template of Package Name
   
   - `Reverse of the Company's Host + Project_Name + Module_Name + Function_Name`

   - Write in Lowercase ( i.e., `package org.apache.tomcat.core'` )

   - a `package` maps a Directory
   
   - after using `package`, `Class` has changed into `package_Name + Class_Name`

3. how to compile

    - `javac -d . XXX.java`

    - the Command above creates multiple Directories, that splits `package_Name` into Direstories.

4. how to run `.class`

    - run Command `java package_Name.XXX` under the same Directory of `XXX.java` File.

    - that is to say, the `class_Name` of `xxx.java` becomes `package_Name.XXX`

### an Example

```java
// HelloWorld.java
package self.study;

public class HelloWorld{
    public static void main(String[] args){
        System.out.println("package test!");
    }
}
```

```java
// Test.java
package self;

public class Test{
    public static void main(String[] args){
        self.study.HelloWorld hw = new self.study.HelloWorld();
        System.out.println("In Test!");
    }
}
```
- `HelloWorld.java` and `Test.java` locate at the same Dirtectory. `HelloWorld.class` locates in `./self/study`, `Test.class` locates in `./self`. when we `new` an Object of `HelloWorld.class`, we have to write it in `self.study.HelloWorld hw = new self.study.HelloWorld()` without `import`.

- with `import`, we rewrite `Test.java`, and import the `class` we need.

    ```java
    // Test.java
    package self;
    import self.study.HelloWorld
    public class Test{
        public static void main(String[] args){
            HelloWorld hw = new HelloWorld();
            System.out.println("In Test!");
        }
    }
    ```

### when `import`

- `class A` and `class B` locate in same `package`, we donot need to `import`

- `class A` and `class B` locate in different `package`, we need to `import`

- `import` locates under `package <package_Name>;` above `[Modifiers] class <class_Name>`

- an often-used Case: `import java.util.Scanner` Here `java.util` is a package_Name.

- `java.lang` package will be automatically imported.

## 07. Access Control ( `[Modifiers]` )

|  private   |               protected               |  public  |           -            |
| :--------: | :-----------------------------------: | :------: | :--------------------: |
| same Class | same Class, same Package and Subclass | Anywhere | same Class and Package |

- `public` > `protected` > `-` > `private`

## 08. typical Methods in Class `Object`

1. `toString()`

- __It's recommanded, that `toString()` should be rewritten.__

- when a Ref / Instance is output, `toString()` will be aumomatically used.

    ```java
    class Customer{
        private String Name;
        private int Age;
        private String IDnumber;

        public Customer(){

        }

        public Customer(String Name, int Age, String IDnumber){
            this.Name = Name;
            this.Age = Age;
            this.IDnumber = IDnumber;
        }

        public String toString(){
            return "Name: " + this.Name + " Age: " + this.Name.toString() + " IDnumber: " + this.IDnumber;
        }
    }
    ```

2. `equals()`

    ```java
    public boolean equals(Object obj){
        return this == obj;
    }
    ```

- to decide, wether 2 `Objects` are same - comparing their __Memory Addresses__. ( fast can be simplified as `==` )

- __It's recommanded, that `equals()` should be rewritten.__

    ```java
    class Customer{
        private String Name;
        private String IDnumber;

        public static boolean equals(Object obj){
            if(obj == null)
                return false;
            Customer objtemp = (Customer) obj;
            return objtemp.Name == this.Name && objtemp.IDnumber == this.IDnumber;
        }
    }
    // when 2 Customer Objects with same Name and IDnumber, they should be same. 
    // if we dont't rewrite equals(), their Memory Addresses are not same.
    ```

3. `hashCode()`

- `public native int hashCode();`

- This Method transforms the Memory Address into an unique HashCode.

## 08. Data Structure

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

### Array

- `<DataType>[] <Array_Name> = new <DataType>[<Array_Size>];`
  
  ( dynamic Initialization, `for( ; ; ) Array[i] = ...;` )

- `<DataType>[] <Array_Name> = {<DataType>obj1, ...};` ( static Initialization )

- storaged in __Heap-Memory__ ( `Object` )

- `length` Attribute is contained in every `Array`

- the Elements in `Array` are storaged continuely in Space ( Memory Address, one by one )

- __the Address of the first Element is the Memory Address of the whole `Array`__

- how to use `Array` as Parameter in a Method

    - `Method_Name(Array_Name)`

    - `Method_Name(new <DataType>[] {<DataType>obj1, ...})`

    - Elements in `String[] args` in `public static void main(String[] args)` are prepared for Users. Users provide Parameters, split by `Space`, when they run Command `java xxx <Parameters>` 

- copy an `Array`

    - `System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`

        ```java
        int[] src = {1,2,3,4,5};
        int[] dest = new int[100];
        System.arraycopy(src, 1, dest, 0, 2);
        // cioy start from the index with 1 in src
        // the copy Length is 2
        // we can find the Elements that're copied start from the index with 0 in dest
        // dest = {2, 3, 0, 0, ..., 0}
        ```


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
