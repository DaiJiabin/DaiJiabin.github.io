# Java Learning


# Java Learning ( Data Structures, mostly )

... And the greatest reason I learn it, is that ~~I LOVE COFFEE :coffee:~~ its DS are fuxxing easy to use.

## Classes in Java

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

## Data Structures

### Queue & Stack & Bag

|Initialization|Queue|
|:-----:|:---:|
|Initialization|Queue<__DataType__> queue_name = new Queue<__DataType__>()|
|int size()|returns the size of the Queue|
|boolean isEmpty()|judge if the Queue is empty|
|enqueue(__DataType__ Item)|enqueue an Item into a Queue|
|__DataType__ dequeue()|dequeue the first-in Item|


|Options|Stack|
|:-----:|:---:|
|Initialization|Stack<__DataType__> stack_name = new Stack<__DataType__>()|
|int size()|returns the size of the Stack|
|boolean isEmpty()|judge if the Stack is empty|
|push(__DataType__ item)|push a new element into a Stack|
|__DataType__ pop()|returns the last-in Item|

|Options|Bag|
|:-----:|:---:|
|Initialization|Bag<__DataType__> bag_name = new Bag<__DataType__>()|
|int size()|returns the size of the Bag|
|add(__DataType__ Item)|add an Item into the Bag|

### ArrayList

|Options|ArrayList|
|:-----:|:-------:|
|Initialization|ArrayList<__DataType__> arraylist_name = new ArrayList<__DataType__>()|
|int size()|returns the Size of the ArrayList|
|add(int Index, ___DataType__ Item)|add an Item into index|
|contains(__DataType__ Item)|if the ArrayList contains the Item|
|get(int index)|get the Item through index|
|int indexOf(__DataType__ Item)|returns the Index of the Item|
|sort()|sort the ArrayList|
|toArray()|transfer the ArrayList into an Array|
|toString()|transfer the ArrayList into a String|

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/ArrayList.html).

### LinkedList

|Options|LinkedList|
|:-----:|:--------:|
|Initialization|LinkedList<__DataType__> list = new LinkedList<__DataType__>()|
|int size()|returns the Size of the LinkedList|
|add((int index, )__DataType__ Item)|add an Item at the end of the LinkedList / index|
|remove(int index)|remove the index-th Item of the LinkedList|
|get(int index)|get the index-th Item of the LinkedList|
|Object[] toArray()|returns an Array composed by the Items of LinkedList|

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/LinkedList.html).

### HashMap

|Options|HashMap|
|:-----:|:-----:|
|Initialization|HashMap<__DataType__ Key, __DataType__ Value> sites = new HashMap<__DataType__ Key, __DataType__ Value>()|
|int size()|returns the size of the HashMap|
|__value's DataType__ get(__DataType__ Key)|returns the value of Key|
|boolean containsKey(__DataType__ Key)|if the HashMap contains the Key-Value|
|remove(__DataType__ Key)|remove the Item of the HashMap|

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/HashMap.html).

### HashSet

|Options|HashSet|
|:-----:|:-----:|
|Initialization|HashSet<__DataType__> sites = new HashSet<__DataType__>()|
|int size()|returns the size of the HashSet|
|boolean contains(__DataType__ Item)|if the HashSet contains the Item|
|remove(__DataType__ Item)|remove the Item of the HashSet|

P.S. For more Options, [click here](https://www.runoob.com/manual/jdk11api/java.base/java/util/HashSet.html).
