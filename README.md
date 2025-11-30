# Core Dart

## Introduction
Dart is a modern, open-source programming language developed by Google in 2011. It was designed for building fast, scalable, and cross-platform applications, particularly for the web, mobile, and desktop. Initially focused on replacing JavaScript for web development, Dart gained significant popularity after the introduction of Flutter, Google’s UI toolkit for creating natively compiled applications from a single codebase. Dart is object-oriented, class-based, and uses a C-style syntax, making it familiar to developers from Java or JavaScript backgrounds. Key features of Dart include sound typing, asynchronous programming with `async` and `await`, garbage collection, just-in-time and ahead-of-time compilation, and a rich standard library. Its ability to compile to native code and JavaScript makes it versatile and efficient for both frontend and backend development.

**Development & Deployment**
| Platform | Development | Deployment |
|---------|------------|-----------|
| Desktop & Mobile | JIT + DVM | AOT + runtime |
| Web | dartdevc | dart2js |
 
**JIT compilation:**  Compiles the program’s source code into machine code **at runtime** (while the program is running). It allows **faster development cycles** since changes can be tested immediately without full recompilation. JIT is mainly used during **development** for features like **hot reload** in Flutter. However, it can cause slightly slower startup times because compilation happens on the device.
  
**AOT compilation:** Converts the source code into **native machine code before execution**. This makes the app **run faster** and **start instantly**, since no compilation occurs at runtime. AOT is used for **production builds** in Flutter to deliver high performance and optimized executables. The trade-off is longer build times during compilation and larger binary sizes.

**Compile Time:** The phase when your code is translated from a high-level language (like Dart, C, or Java) into machine-readable code (binary or intermediate form). It happens before the program is executed. Tasks that happen here:
-   Syntax checking (missing semicolon, wrong keyword, etc.)
-   Type checking (e.g., assigning a _String_ to an _int_ variable in strongly typed languages)
-   Converting source code into executable code or bytecode
Errors found: Compile-time errors

Examples:
- ```int x = "hello"; // type mismatch```
- Missing semicolon ;
- Calling a function that doesn’t exist

**Run Time:** The phase when the program is actually running (executing instructions on the CPU). It happens after compilation (or interpretation, in some languages).

Tasks that happen here:
-   Memory allocation
-   Variable initialization 
-   Executing logic, loops, conditions, etc.

Errors found: Run-time errors
Examples:
- Dividing by zero (10 / 0)
- Accessing an invalid array index
- Null pointer exceptions
- Running out of memory

## Variables

-   Used to store data
-   Stores reference of an object
 
### Creating variables

Type annotation
``` dart
<type> <variable_name>;
int age;
double price;
List<String> values;
```
Using `var` keyword
``` dart
var <variable_name>;
var age;
var values;
```
Using `dynamic` keyword
``` dart
dynamic <variable_name>;
dynamic age;
dynamic values;
```
**var vs dynamic**
| var | dynamic |
| --- | --- |
| Type inference at compile-time. | Type inference at run-time. |
| var is not a stand-alone type. | dynamic is a stand-alone type. |
| Static type checking with Dart analyzer. Gives compile-time errors. | Stops analyzer & runtime type checking. Throws runtime exceptions. |
| Use when the type is clear and consistent. | Use when type is unknown, e.g., JSON parsing. |

``` dart
void main() {
  var name = "Arnab"; // inferred as String
  // name = 10; // Error: can't assign int to String
  name = "Sakib"; // allowed
}

void main() {
  dynamic data = "Arnab";
  data = 10;    // allowed
  data = true;  // allowed
}

```
``` dart
var test(){
} // not allowed

dynamic test(){
} // allowed
```
``` dart
var x = 10
print(x.toUpperCase()); // error

dynamic x=10;
print(x.toUpperCase()); // exception
```
**final**

Meaning: Can only be assigned once.

When value is set: At run time (when the program runs).

Flexibility: The value can be calculated dynamically (not known at compile time).
Example:
``` dart
final DateTime now = DateTime.now(); // valid
print(now);
```
Here now gets its value only when the program runs.

**const**

Meaning: A compile-time constant.

When value is set: At compile time (before the program runs).

Flexibility: Must be a fixed, immutable value known during compilation.
Example:
``` dart
const pi = 3.1416; // valid
const time = DateTime.now(); // ERROR (not known at compile time)
```
## Comments
``` dart
// Single line comment
/*
Multiline comment
*/
/// Documentation comment
// TODO: comment
```
## Data types

Single value type: Numbers (integers and doubles), Strings, Booleans

Multi value type: List, Set, Map, Enum
### int
Used to represent whole numbers
On native platforms, values can be from -263 to 263 – 1
On the web, it is represented as JavaScript numbers (64 bit floating point values with no fractional part)
``` dart
void main() {
  int x = 5;
  // Common properties
  print(x.isEven); // false
  print(x.isOdd); // true
  print(x.bitLength); // 3 (binary of 5 is 101)
  print(x.sign); // 1

  // Common methods
  print(x.abs()); // 5
  print(x.compareTo(8)); // -1 (less than 8)
  print(x.remainder(2)); // 1
  print(x.toDouble()); // 5.0
  print(x.toString()); // "5"
  print(x.toRadixString(2)); // "101" (binary)
  print(x.gcd(10)); // 5
  print((-1).toUnsigned(8)); // 255
  print((255).toSigned(8)); // -1
  print((7 ~/ 2)); // 3 (integer division)

  // Bitwise operations
  int a = 5; // 0101
  int b = 3; // 0011
  print(a & b); // 1 (AND)
  print(a | b); // 7 (OR)
  print(a ^ b); // 6 (XOR)
  print(~a); // -6 (NOT)
  print(a << 1); // 10 (shift left)
  print(a >> 1); // 2 (shift right)
}

```

### double

Used to represent fractional numbers
Supports 64 bit as specified by the IEEE 754 standard
``` dart
void main() {
  double y = 5.75;

  // Common properties
  print(y.isFinite); // true
  print(y.isInfinite); // false
  print(y.isNaN); // false
  print(y.sign); // 1

  // Common methods
  print(y.abs()); // 5.75
  print(y.ceil()); // 6
  print(y.floor()); // 5
  print(y.round()); // 6
  print(y.truncate()); // 5
  print(y.clamp(3.0, 5.0)); // 5.0 (restricts value between 3 and 5)
  print(y.remainder(2)); // 1.75
  print(y.toInt()); // 5
  print(y.toString()); // "5.75"
  print(y.toStringAsFixed(1)); // "5.8"
  print(y.toStringAsPrecision(3)); // "5.75"
  print(y.compareTo(6.0)); // -1 (less than 6)
  print(y + 2.25); // 8
  print(y * 2); // 11.5
  print(y / 2); // 2.875

  // Special values
  double nanValue = double.nan;
  double infValue = double.infinity;
  double negInf = double.negativeInfinity;
  print(nanValue.isNaN); // true
  print(infValue.isInfinite); // true
  print(negInf.isInfinite); // true
}

``` 

### String
An object of class ‘String’
Holds a sequence of UTF-16 code units
``` dart
void main() {
  String s = "Hello World";

  // Common properties
  print(s.length); // 11
  print(s.isEmpty); // false
  print(s.isNotEmpty); // true
  print(s.codeUnits); // [72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]
  print(s.runtimeType); // String

  // Common methods
  print(s.toUpperCase()); // "HELLO WORLD"
  print(s.toLowerCase()); // "hello world"
  print(s.contains("World")); // true
  print(s.startsWith("Hello")); // true
  print(s.endsWith("ld")); // trueprint(s.indexOf("o")); // 4
  print(s.lastIndexOf("o")); // 7
  print(s.substring(0, 5)); // "Hello"
  print(s.replaceAll("l", "*")); // "He**o Wor*d"
  print(s.replaceFirst("o", "0")); // "Hell0 World"
  print(s.split(" ")); // ["Hello", "World"]
  print(s.trim()); // "Hello World" (no extra spaces removed here)
  print(" Dart ".trim()); // "Dart" (spaces removed)
  print(s.padLeft(15, '*')); // "***Hello World"
  print(s.padRight(15, '*')); // "Hello World***"

  // String interpolation
  String name = "Arnab";
  int age = 22;
  print("My name is $name and I am $age years old.");
  // "My name is Arnab and I am 22 years old."

  // String to number conversion
  String numStr = "42";
  print(int.parse(numStr)); // 42
  print(double.parse("3.14")); // 3.14

  // Number to string
  int n = 100;
  print(n.toString()); // "100"
}

```

### List
Ordered collection of index based values
Index starts from zero
Duplicate elements are allowed
Supports generics. Allow same & different types of values
Can be growable  ```var values = []```, ```var values = List.empty(growable: true)``` or fixed length list ```var values = List.empty(_)```
Implements iterable
``` dart
void main() {
  // Creating Lists
  var values = [10, 20, 30];
  List<dynamic> fruits = ['Apple', 'Orange', 'Cherry', 10];
  List<int> nums = [10, 35, 55];

  // Fixed-length list
  var items = List.filled(5, 1, growable: false); // [1, 1, 1, 1, 1]

  // Immutable list
  const List<int> immutableNums = [10, 35, 55];

  // Generated list
  var generatedItems = List.generate(5, (int index) => index * index); // [0, 1, 4, 9, 16]

  // Creating list from another list
  List<int> originalItems = [1, 3, 5, 7, 9];

  // Using List.from (runtime type check)
  // Note: This will throw at runtime if type doesn't match
  List<String> itemsFrom = List<String>.from(
    ['A', 'B', 'C'],
  );

  // Using List.of (compile-time type check)
  // Uncommenting the below line would show compile-time error
  // List<String> itemsOf = List<String>.of(originalItems);

  // Accessing list elements
  print(originalItems[1]);        // 3
  print(originalItems.elementAt(1)); // 3

  // Iterating through a list
  List<String> animals = ['Tiger', 'Cat', 'Giraffe'];

  // Using traditional for loop
  for (int i = 0; i < animals.length; i++) {
    print(animals[i]);
  }

  // Using for-in loop
  for (var animal in animals) {
    print(animal);
  }

  // Using forEach with a lambda
  animals.forEach((animal) {
    print(animal);
  });
}
```

#### Features of Lists in Dart

- ```if``` and ```for``` in List Construction: You can use ```if``` and ```for``` inside a list literal to conditionally or dynamically build lists.
``` dart
void main() {
  bool addMore = true;
  List<int> numbers = [1, 2, if (addMore) 3, for (int i = 4; i <= 6; i++) i];
  print(numbers); // [1, 2, 3, 4, 5, 6]
}
```
- Spread Operator: Use ... to insert all elements from one list into another easily.
``` dart
void main() {
  List<int> a = [1, 2, 3];
  List<int> b = [0, ...a, 4, 5];
  print(b); // [0, 1, 2, 3, 4, 5]
}
```

- Range Error: Accessing an index outside the valid range causes a ```RangeError```.  
``` dart
void main() {
  List<String> fruits = ['apple', 'banana'];
  print(fruits[1]); // Works
  print(fruits[2]); // Throws RangeError
}
```

- Modification in ```for-in``` or ```forEach``` Loops: You cannot modify list elements directly using ```for-in``` or ```forEach```. Use a normal for loop instead.
``` dart
void main() {
  List<int> nums = [1, 2, 3];

  for (var n in nums) {
    n *= 2; // Doesn't modify original list
    print(nums); // [2, 3, 4]
  }
  print(nums); // [1, 2, 3]

  for (int i = 0; i < nums.length; i++) {
    nums[i] *= 2; // Modifies original list
  }
  print(nums); // [2, 4, 6]
}
```

- List is an Abstract Class: List is abstract; its constructors are factory constructors that return concrete implementations.
``` dart
void main() {
  List<int> list1 = List.empty(growable: true); // Creates a growable list
  list1.addAll([1, 2, 3]);
  print(list1); // [1, 2, 3]
}
```

- List of Lists (Matrix): You can store lists inside another list, creating a 2D structure. 
``` dart
void main() {
  List<List<int>> matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
  ];
  print(matrix[1][2]); // 6
}
```

- Default null values for uninitialized length: Increasing a fixed-length list’s size introduces null values in uninitialized positions.
``` dart
void main() {
  List<int?> list = List.filled(2, 10, growable: true);
  list.length = 4; // Expands list
  print(list); // [10, 10, null, null]
}
```

**List Properties**
``` dart
void main() {
  List<int> numbers = [10, 20, 30, 40];
  print(numbers.length); // 4
  print(numbers.first); // 10
  print(numbers.last); // 40
  print(numbers.isEmpty); // false
  print(numbers.isNotEmpty); // true
  var reversedList = numbers.reversed.toList();
  print(reversedList); // [40, 30, 20, 10]
}
```

**Methods for Adding Elements**
``` dart
void main() {
  List<int> list = [1, 2, 3];
  list.add(4); // [1, 2, 3, 4]
  list.insert(1, 10); // [1, 10, 2, 3, 4]
  list.addAll([5, 6]); // [1, 10, 2, 3, 4, 5, 6]
  list.insertAll(2, [7, 8]); // [1, 10, 7, 8, 2, 3, 4, 5, 6]
  print(list);
}
```

**Methods for Removing Elements**
``` dart
void main() {
  List<int> list = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  list.removeAt(2); // removes element at index 2 [1, 2, 4, 5, 6, 7, 8, 9]
  list.remove(6); // removes first occurrence of 6 [1, 2, 4, 5, 7, 8, 9]
  list.removeLast(); // removes last element [1, 2, 4, 5, 7, 8]
  list.removeRange(1, 3); // removes elements at indices 1 and 2 [1, 5, 7, 8]
  list.removeWhere((n) => n < 6); // removes elements < 6 [7, 8]
  list.retainWhere((n) => n == 7); // keeps only elements == 7 [7]
  list.clear(); // removes all elements []
  print(list);
}
```

**Utility and Searching Methods**
``` dart
void main() {
  List<int> list = [5, 2, 8, 2, 9, 5];

  print(list.indexOf(2)); // returns index of first occurrence of 2 is 1
  print(list.lastIndexOf(5)); // returns index of last occurrence of 5 is 5
  list.sort(); // [2, 2, 5, 5, 8, 9]
  list.shuffle(); // random order
  print(list.sublist(1, 4)); // returns portion of list (end index excluded)
  print(list.where((n) => n > 5).toList()); // elements > 5
  print(list.whereType<int>()); // only elements of int type
}
```

**Iteration and Transformation Methods**
``` dart
void main() {
  List<int> numbers = [1, 2, 3, 4];
  var squared = numbers.map((n) => n * n).toList();
  print(squared); // [1, 4, 9, 16]

  int sum = numbers.reduce(
    (a, b) => a + b,
  ); // combines all elements of a list into a single value
  print(sum); // 10
  int product = numbers.fold(
    1,
    (a, b) => a * b,
  ); // similar to reduce, but allows specifying an initial value
  print(product); // 24
  print(numbers.toSet()); // {1, 2, 3, 4}
  print(numbers.asMap()); // {0: 1, 1: 2, 2: 3, 3: 4}
}
```

**Condition Checking Methods**
``` dart
void main() {
  List<int> list = [10, 20, 30, 40];
  print(list.every((n) => n > 5)); // true (all > 5)
  print(list.any((n) => n == 20)); // true (at least one is 20)
}
```

### Set

A Set is an unordered collection of unique elements implemented as ```LinkedHashSet```.
``` dart
void main() {
  var numbers = {10, 20, 30, 20, 10};
  print(numbers); // {10, 20, 30} duplicates ignored
  print(numbers.runtimeType); // LinkedHashSet<int>
}
```

**Key limitations**
``` dart
void main() {
  var items = {10, 20, 30};

  // No index access
  print(items[0]); // Error: Set has no index operator

  // To modify, remove and re-add
  items.remove(20);
  items.add(50);
  print(items); // {10, 30, 50}
}
```

**Creating a Set**
| Method | Example Code |
| --- | --- |
| Empty Set | ```Set<int> emptySet = {}; // Without type, {} defaults to a Map``` |
| Set with Initial Values | ```var names = {'Mark', 'Alex', 'James'};``` |
| From another Set (no type check) | ```var set1 = Set.from([1, 2, 3, 3]); print(set1); // {1, 2, 3}``` |
| From another Set (type checked) | ```var set2 = Set.of([1, 2, 3]);``` |
| Unmodifiable Set | ```var fixed = Set.unmodifiable([1, 2, 3]); fixed.add(4); // Error``` |


**Special Features**
- `if` and `for` in Construction
``` dart
void main() {
  bool includeExtra = true;
  var values = {
    1,
    2,
    if (includeExtra) 3,
    for (var i in [4, 5]) i,
  };
  print(values); // {1, 2, 3, 4, 5}
}
``` 

- Spread Operator
``` dart
void main() {
  var base = {1, 2, 3};
  var extended = {...base, 4, 5};
  print(extended); // {1, 2, 3, 4, 5}
}
```

- Range Error
``` dart
void main() {
  var set = {10, 20, 30};
  print(set.elementAt(1)); // Works
  // print(set.elementAt(5)); // RangeError
}
```
- Constant (Immutable) Set
``` dart
void main() {
  const fixed = {1, 2, 3};
  // fixed.add(4); // Error: Cannot modify a const Set
  print(fixed); // {1, 2, 3}
}
```

- Iteration and Modification
``` dart
void main() {
  var colors = {'red', 'green', 'blue'};
  for (var c in colors) {
    print(c);
  }
  colors.forEach((c) => print(c.toUpperCase()));

  // Access using elementAt()
  for (int i = 0; i < colors.length; i++) {
    print(colors.elementAt(i));
  }
}

void main() {
  var nums = {1, 2, 3};
  for (var n in nums) {
    n *= 2; // No effect on original set
  }
  print(nums); // {1, 2, 3}
}
```

**Set Properties**
``` dart
void main() {
  var items = {'apple', 'banana', 'cherry'};

  print(items.length); // 3
  print(items.first); // apple
  print(items.last); // cherry
  print(items.isEmpty); // false
  print(items.isNotEmpty); // true
}
```

**Methods for Adding and Removing Elements**
``` dart
void main() {
  var setA = {1, 2, 3};

  setA.add(4); // Adds 4
  setA.add(2); // Duplicate ignored
  setA.addAll({5, 6}); // Adds multiple elements
  setA.remove(3); // Removes element 3
  setA.removeAll({1, 6}); // Removes all matching elements
  setA.clear(); // Empties the set
  print(setA); // {}
}
```

**Methods for Conditional Removal/Retention**
``` dart
void main() {
  var numbers = {10, 20, 30, 40, 50};
  numbers.removeWhere((n) => n < 30); // Removes values < 30
  print(numbers); // {30, 40, 50}

  numbers.retainWhere((n) => n >= 40); // Keeps only values >= 40
  print(numbers); // {40, 50}
  numbers.retainAll({50, 60, 70}); // Keeps only 50 (common element)
  print(numbers); // {50}
}
```

**Methods for Checking and Looking Up Elements**
``` dart
void main() {
  var fruits = {'apple', 'banana', 'orange'};

  print(fruits.elementAt(1)); // banana
  print(fruits.contains('apple')); // true
  print(fruits.containsAll({'apple', 'grape'})); // false
  print(fruits.lookup('banana')); // banana
  print(fruits.lookup('grape')); // null
}
```

**Methods for Filtering and Transformation**
``` dart
void main() {
  var words = {'dart', 'flutter', 'set', 'class'};

  var shortWords = words.where((w) => w.length <= 4).toSet();
  print(shortWords); // {dart, set}

  var onlyStrings = words.whereType<String>().toSet();
  print(onlyStrings); // {dart, flutter, set, class}

  var upperCase = words.map((w) => w.toUpperCase()).toSet();
  print(upperCase); // {DART, FLUTTER, SET, CLASS}
}
```

**Mathematical Set Operations**
``` dart
void main() {
  var set1 = {1, 2, 3, 4};
  var set2 = {3, 4, 5, 6};
  var unionSet = set1.union(set2);
  print(unionSet); // {1, 2, 3, 4, 5, 6}

  var intersectionSet = set1.intersection(set2);
  print(intersectionSet); // {3, 4}
  var differenceSet = set1.difference(set2);
  print(differenceSet); // {1, 2}
} 
```

**Methods for Reduction and Conversion**
``` dart
void main() {
  var numbers = {1, 2, 3, 4};

  var sum = numbers.reduce((a, b) => a + b);
  print(sum); // 10

  var product = numbers.fold(1, (a, b) => a * b);
  print(product); // 24

  var list = numbers.toList();
  print(list); // [1, 2, 3, 4]

  var setFromList = list.toSet();
  print(setFromList); // {1, 2, 3, 4}
}
```

**Methods for Condition Checking**
``` dart
void main() {
  var setA = {5, 10, 15};

  print(setA.every((n) => n > 0)); // true
  print(setA.any((n) => n == 10)); // true
}
```

**List vs Set**
| List | Set |
| --- | --- |
| Ordered collection. Original order preserved. | Unordered collection. Original order not preserved. |
| Allows duplicate elements. | Does not allow duplicate elements. |
| Allows index-based access (`list[index]`). | No index-based access. |
| Element value at a specific index can be modified. | Cannot modify an element once added. |
| `length` can be modified to add nulls or remove elements. | `length` cannot be modified. |
| Supports sorting, shuffling, reversing. | No default support for sorting, shuffling, reversing. |
| Can convert to Map using `asMap()`. | No built-in support to convert to Map. |
| Can hold multiple `null` values. | Can hold at most one `null` value. |

 

### Map
A Map is a collection of key-value pairs, where each key is unique.
``` dart
void main() {
  var student = {'name': 'Alice', 'age': 22, 'isPassed': true};

  print(student['name']); // Alice
  print(student); // {name: Alice, age: 22, isPassed: true}
}
```

Flavors of Map
-   **LinkedHashMap** Default, maintains insertion order.    
-   **HashMap** Fast lookup, no guaranteed order. 
-   **SplayTreeMap** Automatically sorted by key.
    
``` dart
import 'dart:collection';

void main() {
  var linkedMap = {'a': 1, 'b': 2, 'c': 3}; // LinkedHashMap (default)
  print(linkedMap); // Preserves insertion order

  var hashMap = HashMap(); // Order not guaranteed
  hashMap['x'] = 10;
  hashMap['y'] = 20;
  print(hashMap); // {x: 10, y: 20}

  var treeMap = SplayTreeMap(); // Sorted by key
  treeMap['banana'] = 2;
  treeMap['apple'] = 1;
  treeMap['cherry'] = 3;
  print(treeMap); // {apple: 1, banana: 2, cherry: 3}
}
```

**Importance in Flutter**
Maps are used widely for data storage and transfer:
- SQFLite DB: Query results often return `List<Map<String, dynamic>>`.
- Cloud Firestore: Documents are stored as Maps.
-  JSON (Web APIs): JSON data in Dart is represented as a `Map<String, dynamic>`.

``` dart 
void main() {
  Map<String, dynamic> user = {
    'id': 101,
    'name': 'John',
    'email': 'john@example.com',
  };

  print(user['email']); // john@example.com
}
```

**Key Map Methods**
``` dart
void main() {
  var data = {'a': 1, 'b': 2};

  // putIfAbsent
  data.putIfAbsent('c', () => 3);
  print(data); // {a: 1, b: 2, c: 3}

  // addAll
  data.addAll({'d': 4, 'e': 5});
  print(data); // {a: 1, b: 2, c: 3, d: 4, e: 5}

  // remove
  data.remove('b');
  print(data); // {a: 1, c: 3, d: 4, e: 5}

  // removeWhere
  data.removeWhere((key, value) => value > 3);
  print(data); // {a: 1, c: 3}

  // containsKey / containsValue
  print(data.containsKey('a')); // true
  print(data.containsValue(5)); // false

  // update
  data.update('a', (value) => value + 10);
  print(data); // {a: 11, c: 3}

  // updateAll
  data.updateAll((key, value) => value * 2);
  print(data); // {a: 22, c: 6}
}
```

### Enum
An enum (short for enumeration) is a special type used to define a fixed set of constant values. It helps make code more readable and type-safe.
Enums are implicitly ```const```.
Enum values are singletons.
Cannot be subclassed, mixed in, or instantiated manually.
Good for representing finite states like:
-   App theme (light, dark)   
-   Connection state (connected, disconnected) 
-   Order status (pending, shipped, delivered)
    
```enum Direction { north, south, east, west }```

Each value is a constant member of the enum.
Enum values are accessed using dot notation:
```print(Direction.north); // Output: Direction.north```
``` dart
enum Day { monday, tuesday, wednesday, thursday, friday, saturday, sunday }

void main() {
  var today = Day.friday;

  print(today); // Day.friday
  print(today.index); // 4
  print(
    Day.values,
  ); // [Day.monday, Day.tuesday, Day.wednesday, Day.thursday, Day.friday, Day.saturday, Day.sunday]
  print(today.name); // "friday"

  // Switch with enum
  switch (today) {
    case Day.monday:
      print("Start of the week");
      break;
    case Day.friday:
      print("Weekend is near");
      break;
    default:
      print("Regular day");
  }
}
```

**Enums with Associated Values (Enhanced Enums, Dart 2.17+)**
``` dart
enum Role {
  admin("Full Access"),
  user("Limited Access"),
  guest("Read Only");

  final String permission;
  const Role(this.permission);

  void describe() {
    print("Role: $name, Permission: $permission");
  }
}

void main() {
  Role.admin.describe(); // Role: admin, Permission: Full Access
}
```

## Operators in Dart
Operators are symbols that perform operations on values or variables. They can be unary (1 operand), binary (2 operands), or ternary (3 operands).

**Arithmetic Operators**
``` dart
void main() {
  var a = 10, b = 3;

  print(a + b); // 13
  print(a - b); // 7
  print(a * b); // 30
  print(a / b); // 3.333...
  print(a ~/ b); // 3
  print(a % b); // 1
}
```
  

**Relational Operators**
Used for comparison; result is always `bool`.
``` dart
void main() {
  var x = 5, y = 10;

  print(x < y); // true
  print(x >= y); // false
  print(x == y); // false
  print(x != y); // true
}
```

**Logical Operators**
``` dart
void main() {
  var a = true, b = false;

  print(a && b); // false
  print(a || b); // true
  print(!a); // false
}
```

**Assignment Operators**
``` dart
void main() {
  var x = 10;
  x += 5; // same as x = x + 5
  print(x); // 15

  x -= 3; // 12
  x *= 2; // 24
  x ~/= 4; // 6
  x %= 4; // 2
}
```

**Increment/Decrement Operators**
``` dart
void main() {
  var n = 5;

  print(n++); // 5 (post-increment: uses value first)
  print(n); // 6
  print(++n); // 7 (pre-increment: increments first)

  print(n--); // 7
  print(--n); // 5
}
```
  
  **Bitwise Operators**
``` dart
void main() {
  var a = 5; // 0101
  var b = 3; // 0011

  print(a & b); // 1 (AND)
  print(a | b); // 7 (OR)
  print(a ^ b); // 6 (XOR)
  print(~a); // -6 (NOT)
  print(a << 1); // 10 (Left shift)
  print(a >> 1); // 2 (Right shift)
}
```

**Conditional (Ternary) Operator**
``` dart
void main() {
  var age = 18;
  var result = (age >= 18) ? 'Adult' : 'Child';

  print(result); // Adult
}
```

**Type Test Operators**
``` dart
void main() {
  var value = 'Hello';

  print(value is String); // true
  print(value is! int); // true

  dynamic numValue = 42;
  var strValue = numValue as int; // as operator for typecasting
  print(strValue.runtimeType); // int
}
```

**Null Aware Operators**
``` dart
void main() {
  String? name;
  print(name ?? 'Guest'); // Guest

  name ??= 'Alice';

  print(name); // Alice
  print(name?.length); // 5

  var person = Person()
    ?..sayHello()
    ..sayBye();

  List<int>? numbers;
  print([
    ...?numbers ?? [1, 2, 3],
  ]); // [1, 2, 3]
}

class Person {
  void sayHello() => print('Hello');
  void sayBye() => print('Goodbye');
}
```  

**Cascade Notation Operators**

`..` Used to perform multiple method calls or property assignments on the same object.

`..?` Used to perform multiple operations on an object only if it is not null. Prevents null reference errors
``` dart
void main() {
  var list = [10, 20, 30];
  print(list[1]); // [] access 20

  var str = 'Dart';
  print(str.length); // . access 4
  greet('Arnab'); // () function call

  var p = Person()
    ..name = 'Alice'
    ..sayHello(); // .. cascade operator
}

void greet(String name) => print('Hello, $name');

class Person {
  String? name;
  void sayHello() => print('Hello, $name');
}
```

## Null safety in Dart

Null safety is a Dart 2.12+ feature (since July 2020) that prevents variables from holding `null` values by default , ensuring fewer runtime errors. Null safety only available for variable declared with type annotations. Variables declared with `var` and `dynamic` keywords can be `null`.
``` dart
void main() {
  String name = 'Arnab'; // Non-nullable
  name = null; //Error: can't assign null to a non-nullable variable
}
```
| Type | Declaration | Can Store Null? | Example |
| --- | --- | --- | --- |
| Non-Nullable | Must be initialized | No | `String name = 'John';` |
| Nullable | Optional initialization | Yes | `String? name; // or var name;` |

``` dart
void main() {
  String name = 'Dart'; // non-nullable
  String? nickname; // nullable

  print(name.length); // 4
  print(nickname?.length); // null (safe access)
}
```

The value of a non-nullable variable can be assigned to a nullable variable, but the value ofa  nullable variable can not be assigned to to non-nullable variable.
``` dart
void doSomething(int y) {
  // do something
}

void main() {
  int? x;

  doSomething(x); // Error
  if (x != null) {
    doSomething(x);
  }
  doSomething(x ?? 0);
}
```

### Advantages of Null Safety

-   **Saves Time and Effort:** No need for repetitive null checks - the compiler enforces safety.    
-   **Safer Code:** Prevents null reference exceptions both at **compile-time and run-time** (sound null safety).    
-   **Faster Performance:** Compiler optimizations lead to faster, smaller AOT (Ahead-of-Time) code.
    

### Handling Nullable Variables in Non-Nullable Contexts
Nullable variables cannot be directly assigned to non-nullable ones.

**Manual Null Check**
``` dart
void main() {
  String? name = 'Flutter';
  if (name != null) {
    String nonNullName = name;
    print(nonNullName.toUpperCase());
  }
}
```

**Default Value Operator (??)**
``` dart
void main() {
  String? name;
  String displayName = name ?? 'Guest';
  print(displayName); // Guest
}
```

**Null Assertion Operator (!)**

By using this I am telling the compiler that the variable absolutely going to have a value.
``` dart
void main() {
  String? name = 'Dart';
  String upperName = name!.toUpperCase();
  print(upperName); // DART
}
```
``` dart
void main() {
  String? name;
  String upperName = name!.toUpperCase();
  print(upperName); // Error: Unexpected null value.
}
```
If `name` were null, the code would throw a **runtime error**.

  
**Null Aware Access Operator (?)**

I am telling the compiler if the variable is not null then do your task either show null.
``` dart
void main() {
  String? name;
  print(name?.length); // null
  name = 'Dart';
  print(name?.length); // 4
}
```

**The `late` Keyword**

`late`  allows you to declare a **non-nullable variable** that is **initialized later**, before use. I am telling the compiler that at this time I do not know the value of the declared variable but it is up to me to initialize the variable before it can be used. Throws _LateInitializationError_ if the variable is not initialized.

***Late Initialization in a Class***
``` dart
class User {
  late String name; // declared but not initialized immediately

  void setName(String newName) {
    name = newName; // initialized later
  }

  void greet() {
    print('Hello, $name');
  }
}

void main() {
  var user = User();
  user.setName('Arnab');
  user.greet(); // Hello, Arnab
}
```

***Lazy Initialization***
``` dart
late String description = getDescription();

String getDescription() {
  print('Function called!');
  return 'Dart is powerful.';
}

void main() {
  print('Program started');
  print(description); // Function runs only when accessed
}
```

***Late with Asynchronous Initialization***
``` dart
late Future<String> data = fetchData();

Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return 'Data loaded';
}

void main() async {
  print(await data);
}
```

## Conditonal Statement
Decision-making statements `if else-if` control the flow of execution based on conditions that evaluate to **true** or **false**.
Simple if Statement
Executes a block only when the condition is true.
``` dart
if (condition) {
// code runs only if condition is true
}
```
``` dart
void main() {
  int age = 20;

  if (age >= 18) {
    print('You are an adult.'); // You are an adult.
  }
}
```

### if-else Statement
Executes one block when the condition is true, and another when false.
``` dart
if (condition) {
// true block
} else {
// false block
}
```
``` dart
void main() {
  int number = 5;

  if (number % 2 == 0) {
    print('Even number');
  } else {
    print('Odd number'); // Odd number
  }
}
```

### Nested if-else

Tests multiple conditions by placing one `if` or `if-else` inside another.
``` dart
if (condition1) {
if (condition2) {
// code if both are true
} else {
// code if condition1 true but condition2 false
}
} else {
// code if condition1 false
}
```
``` dart
void main() {
  int a = 20, b = 45, c = 30;

  if (a > b) {
    if (a > c) {
      print('a is largest');
    } else {
      print('c is largest');
    }
  } else {
    if (b > c) {
      print('b is largest');
    } else {
      print('c is largest');
    }
  }
}
```

### else-if Ladder
``` dart
if (condition1) {
// block 1
} else if (condition2) {
// block 2
} else if (condition3) {
// block 3
} else {
// default block
}
```
``` dart
void main() {
  int day = 3;

  if (day == 1) {
    print('Monday');
  } else if (day == 2) {
    print('Tuesday');
  } else if (day == 3) {
    print('Wednesday');
  } else if (day == 4) {
    print('Thursday');
  } else if (day == 5) {
    print('Friday');
  } else if (day == 6) {
    print('Saturday');
  } else if (day == 7) {
    print('Sunday');
  } else {
    print('Invalid day number');
  }
}
```

### Switch-Case Statement

A  switch-case statement is a multi-way decision-making structure that allows selection among multiple code blocks based on the value of a single expression.  
The **switch expression** can be of type **int, double, bool, String, enum, or class.**

**Key Rules and Requirements**
| Rule | Description |
| --- | --- |
| Unique Case Labels | Each case label must be unique within a switch block. |
| Type Matching | The data type of the switch expression must exactly match that of each case label. |
| Case Labels are Constants | Case labels must use constant values. |
| Break Requirement | A break statement is required only if the case contains executable code; it prevents fall-through. |
| Combining Cases (Fall-through) | Consecutive cases with no statements can be grouped by omitting break; control passes to the next non-empty case. |
| Default is Optional | The default block runs if no case matches. It is not mandatory. |
| Class Expressions | When switching on class objects, the class must override the `==` operator to allow comparison. |
``` dart
switch (day) {
  case 'Monday':
    print('Start of the week');
    break;

  case 'Friday':
    print('Weekend is near');
    break;

  case 'Saturday':
  case 'Sunday':
    print('Weekend');
    break;

  default:
    print('Midweek day');
}
```

## While & Do-While Loops

### while Loop (Entry Control Loop)

Type: Entry Control Loop - condition checked before the loop body.

Execution: The loop body executes only if the condition is initially true. If the condition is false from the start, the body does not run.

Condition: Must be a Boolean expression (true or false).
``` dart
int i = 1;

while (i <= 3) {
  print(i);
  i++;
}
```

### do-while Loop (Exit Control Loop)
Type: Exit Control Loop - condition checked after executing the loop body.

Execution: The loop body runs first, then the condition is checked.

Key Feature: Guaranteed to execute at least once, regardless of the condition.

Syntax Note: Must include a semicolon (;) at the end of the while condition.
``` dart
int i = 1;

do {
  print(i);
  i++;
} while (i <= 3);
```

**Summary of Differences**
| Feature | while Loop | do-while Loop |
| --- | --- | --- |
| Control | Entry Control Loop | Exit Control Loop |
| Condition Check | At the beginning | At the end |
| Guaranteed Execution | May execute 0 or more times | Executes at least once |


**In short:**
- Use  `while`  when you want the loop to run only if a condition is true from the start.  
- Use `do-while` when you need the loop to run at least once, regardless of the initial condition.

| while | do-while |
| --- | --- |
| Checks the condition **before** executing the loop body. If false initially, the loop body **never runs**. | Executes the loop body **first**, then checks the condition. The loop body **always runs at least once**, even if the condition is false initially. |
``` dart
int i = 5;

while (i < 5) {
  print(i); // This will not run because 5 < 5 is false
  i++;
}
```
``` dart
int i = 5;

do {
  print(i); // This runs once
  i++;
} while (i < 5);
```

## for, for-in, and forEach loops

### The `for` Loop
Used when the number of iterations is known in advance.
``` dart
for (initialization; condition; increment/decrement) {
// loop body
}
for (int i = 0; i < 5; i++) {
  print(i);
}
```

### The `for-in` Loop
Simplifies iteration over collections or other `Iterable` objects. Accesses each element directly, without using an index.
``` dart
for (var element in collection) {
// use element
}
```
Runs once per element; the loop variable holds the current value.
``` dart
var numbers = [1, 2, 3];

for (var n in numbers) {
  print(n);
}
```

### The `forEach` Loop
A higher-order function used to process every element in a collection. Executes a function for each element.
``` dart
collection.forEach((item) {
// operation
});
```
The function must return void. The parameter automatically receives each element. Runs until all elements are processed.
``` dart
var names = ['Alice', 'Bob', 'Charlie'];

names.forEach((name) {
  print(name);
});
```
| Loop Type | Use Case | Index Access | Syntax Style |
| --- | --- | --- | --- |
| for | Fixed number of iterations | Yes | Classic C-style |
| for-in | Iterating over collections | No | Cleaner syntax |
| forEach | Functional-style iteration | No | Uses callback function |
  
####  break  and Labelled break

**What is the `break` Statement?**

Used to  immediately terminate a loop (`for`, `while`, `do-while`) or a `switch` case.
-   **In switch:** Stops execution of the current case and exits the switch block.
-   **In loops:** Exits the loop even if the loop condition is still true. 
-   **Scope:** Valid only inside a loop or switch statement.
    

**Regular `break` in Loops**

-   **Function:** Exits the **innermost** loop that contains it.  
-   **Behavior:** When the `break` executes, control immediately moves outside that loop. 
-   **Limitation:** In **nested loops**, a regular `break` only exits the **inner loop**, not the outer one.
``` dart
for (int i = 1; i <= 5; i++) {
  if (i == 3) {
    break; // exits loop when i == 3
  }
  print(i);
}
// Output: 1, 2

for (int i = 1; i <= 3; i++) {
  for (int j = 1; j <= 3; j++) {
    if (j == 2) {
      break; // exits only inner loop
    }
    print('i: $i, j: $j');
  }
}
// Output:
// i: 1, j: 1
// i: 2, j: 1
// i: 3, j: 1
```

**Labeled `break` in Dart**

Used to exit a specific loop in a nested loop structure.
-   **How it works:**
    1.  Define a **label** before the target loop, ending with a colon (e.g., `outerLoop:`)
    2.  Use `break` followed by that label name (e.g., `break outerLoop;`).
        
-   **Result:** Control exits the **labeled loop**, skipping any remaining iterations.
    
``` dart
outerLoop: // label for the outer loop
for (int i = 1; i <= 3; i++) {
  for (int j = 1; j <= 3; j++) {
    if (j == 2) {
      break outerLoop; // exits both loops
    }
    print('i: $i, j: $j');
  }
}
// Output:
// i: 1, j: 1
```

| Feature | Regular break | Labeled break |
| --- | --- | --- |
| Scope | Innermost loop only | Any labeled outer loop |
| Use Case | Stop one loop | Exit multiple nested loops |
| Syntax Example | `break;` | `break outerLoop;` |
| Label Needed | No | Yes |
| Typical Use | Simple loops | Nested loops |

**In short:**
-   Use `break` for normal loop exits.
-   Use **labeled** `break` to exit **outer loops** directly in nested structures.
    

#### continue and Labeled continue

**What is the continue Statement?**
Used to skip the current iteration of a loop and move to the next one.
Behavior: When executed, all remaining statements in the current iteration are skipped.
Control Flow: Execution jumps to the start of the loop for the next iteration.
Scope: Valid only inside loops (for, while, or do-while).

**Regular continue in Loops**
- Scope: Affects the innermost loop where it appears.
- Effect: Skips the rest of the code in the current iteration and proceeds with the next.
- Use Case: Skipping over specific items in a sequence based on a condition (e.g., skip i = 4 or i = 7).
``` dart
for (int i = 1; i <= 7; i++) {
  if (i == 4 || i == 7) {
    continue; // skip printing 4 and 7
  }
  print(i);
}
// Output: 1, 2, 3, 5, 6
```

**Labeled continue in Dart**
Used to control which loop continues in nested loops.
Purpose: Skips the current iteration of an outer loop from inside an inner loop.

**How it works:**
- A label (a valid identifier followed by a colon) is placed before the outer loop.
- Use continue followed by the label name (e.g., `continue outerLoop;`).
- Effect: When executed, control jumps to the next iteration of the labeled loop.
``` dart
outerLoop:
for (int i = 1; i <= 3; i++) {
  for (int j = 1; j <= 3; j++) {
    if (j == 2) {
      continue outerLoop; // skips to next iteration of outer loop
    }
    print('i: $i, j: $j');
  }
}
// Output:
// i: 1, j: 1
// i: 2, j: 1
// i: 3, j: 1
```
| Feature | Regular continue | Labelled continue |
| --- | --- | --- |
| Scope | Innermost loop | Labelled (outer) loop |
| Effect | Skips current iteration | Skips current iteration of outer loop |
| Label Needed | No | Yes |
| Syntax Example | `continue;` | `continue outerLoop;` |
| Use Case | Skip an iteration | Skip outer loop iteration from inner loop |

**In short:**

-   Use `continue` to skip specific iterations in a single loop.
-   Use **labelled** `continue` to skip the current iteration of an **outer loop** in nested structures.
   

## Function
A function is a reusable block of code that performs a specific task.
Input/Output: Accepts input, processes it, and may return output.

**Benefits:**
- Divides large programs into smaller, manageable parts.
- Promotes code reusability.
- Improves readability and maintenance.
  
**Functions as Objects in Dart**
- Functions are first-class objects, meaning they can:
- Be stored in variables.
- Be passed as arguments to other functions.
- Be returned from other functions.
``` dart
void greet() => print("Hello!");

void main() {
  var sayHello = greet; // storing function in a variable
  sayHello(); // calling through variable
}
```

| Term | Definition | Example |
| --- | --- | --- |
| Function | Defined outside a class | `int add(int a, int b) => a + b;` |
| Method | Defined inside a class | `class Math { int add(int a, int b) => a + b; }` |


**Structure of a Dart Function**

**1. Function Header**
Return Type: Type of value returned (int, String, void, etc.).
Function Name: Identifier used to call the function.
Parameter List: Inputs passed to the function.
void: Used if the function returns nothing.

**2. Function Body**
Enclosed in {} - contains executable statements.
Ends with a return statement if a value is returned.
``` dart
int add(int a, int b) {
  return a + b;
}

void main() {
  print(add(3, 5)); // Output: 8
}
```

**Function Calling Mechanism (Caller vs. Called)**
- Calling Function: Initiates the call (e.g., main).
- Called Function: The function being invoked (e.g., factorial).

**Execution Flow:**
- The caller calls a function.
- Control transfers to the called function with its parameters.
- The called function executes and returns a result.
 - The caller resumes execution after receiving the return value.
``` dart
int factorial(int n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

void main() {
  int result = factorial(5);
  print(result); // Output: 120
}
```

| Concept | Description |
| --- | --- |
| Definition | Block of code for a specific task |
| First-Class Object | Can be stored, passed, or returned |
| Return Type | Data type of the output value |
| Parameters | Inputs provided to the function |
| void Keyword | Used for functions without return values |
| Function vs. Method | Outside class vs. Inside class |
| Execution Flow | Caller > Called > Return > Resume |
  

Positional parameters are assigned by order in the function call and are required unless explicitly made optional. Optional positional parameters are placed inside brackets`[]` and must be nullable if no value is provided. Only the right-most positional parameters can be optional. To avoid `null`, you can assign default values, but default values apply only to optional positional parameters. Named parameters, defined inside`{}`, let you pass arguments in any order using `name: value`. Named parameters are optional by default and get`null` if no value is passed unless a default value is assigned. You can force a named parameter to be required by using the`required` keyword. When combining both, positional parameters must come before named parameters.
``` dart
void calculate(int a, [int? b = 0], {required int c, int d = 1}) {
  // a = required positional
  // b = optional positional with default 0
  // c = required named
  // d = optional named with default 1
  print(a + b! + c + d);
}

void main() {
  calculate(5, 3, c: 2); // ok
  calculate(5, c: 2);    // ok, b defaults to 0
  // calculate(5);       // error: c is required
}
```
**Calling the Function**
When calling the function, you must follow the same strict order:
- Positional Arguments First: You must pass the values for all compulsory positional parameters first, in the correct sequence.
- Named Arguments Second: After all positional values, you can pass the named arguments using the name: value format. The order of the named arguments does not matter.

**Types of Functions**
Dart functions are divided into two main types:
- Predefined Functions (or Library Functions): These are built-in functions provided by the language, like `print()`
- User-Defined Functions: These are functions written and defined by the programmer, such as the `main()` function or any custom logic.

**Categories of Functions**
Functions are also categorized into four types based on their use of parameters (input) and return type (output)  
| Category | Parameter (Input) | Return Type (Output) | Example Use Case |
| --- | --- | --- | --- |
| No Parameter and No Return Type | No | No (void) | Prints a fixed message. |
| With Parameter and No Return Type | Yes | No (void) | Accepts data, processes it, prints result (e.g., cube). |
| No Parameter and With Return Type | No | Yes (e.g., int) | Performs internal calculation and returns value. |
| With Parameter and With Return Type | Yes | Yes (e.g., double) | Takes input, processes it, returns calculated result (e.g., area of a circle). |
  

**Callback function**

A callback function in Dart is a function passed as an argument to another function, which is invoked later when a certain event or operation completes. It allows asynchronous or event-driven programming by letting one piece of code execute after another finishes.
A callback is simply a function reference used as a parameter.
``` dart
void main() {
  printData(processData);
}

void printData(void Function(String) callback) {
  String data = "Hello Dart!";
  callback(data);
}

void processData(String data) {
  print("Processed: $data");
}
```

**Why Use Callbacks**
- To execute code after a task completes (e.g., async operations, UI updates).
- To customize the behavior of a function from outside (reusable APIs).
- Common in Flutter widgets, event handlers, and network requests.
``` dart
// Simulated DB query function
Future<void> getUserFromDB(
  Function(Map) onResult,
  Function(String) onError,
) async {
  try {
    await Future.delayed(Duration(seconds: 1)); // simulate DB latency
    Map user = {
      "id": 1,
      "name": "Arnab",
      "role": "user",
    };
    onResult(user); // success callback
  } catch (_) {
    onError("DB read failed"); // error callback
  }
}

void main() {
  print("Querying database...");

  getUserFromDB(
    (data) { // success handler
      print("User fetched: $data");
    },
    (err) { // error handler
      print(err);
    },
  );

  print("DB request sent.");
}
```

**Named callback**
``` dart
void greet() => print("Hello!");

void execute(void Function() callback) => callback();

void main() {
  execute(greet);
}
```
**Anonymous callback**
``` dart
execute(() => print("Hi there!"));
```

**Anonymous (Lambda) Functions**

An anonymous function is a function without a name. It is used for short, self-contained operations, often passed as an argument to another function.
``` dart
(parameterList) {
// function body
};
```
No name or return type is declared.
Parameters appear in parentheses.
Body enclosed in {}.
Ends with a semicolon (;).

**Execution Methods**
_Assign to a variable_
``` dart
void main() {
  var cube = (int n) {
    return n * n * n;
  };

  print(cube(3)); // Output: 27
}
```
The variable `cube` acts as a callable reference.

_Pass as a parameter_
``` dart
void main() {
  var numbers = [1, 2, 3];

  numbers.forEach((n) {
    print(n * n);
  });
}
```
Commonly used with higher-order functions like `.forEach()` or `.map()`.

**Lambda (Arrow) Function**

When the function body has a single expression:
``` dart
(int n) => n * n * n;
```
Equivalent to:
``` dart
(int n) { return n * n * n; };
```

**Use Cases**
- Compact event handlers or callbacks.
- Inline logic for iteration or filtering.
- Simplifies code where a named function is unnecessary.

**Arrow Function**

The Arrow Function (or Fat Arrow Notation (`=>`)) is a shorthand notation for defining functions in Dart that contain only a single statement or single expression.

_Rules and Syntax_
- Single Expression Only: This notation can only be used when the function body has one expression that can be evaluated. It cannot be used for functions containing multi-statement logic like if/else or loops.
``` dart
returnType functionName(parameters) => expression;
int add(int a, int b) => a + b; // valid
```
The Notation: The symbol is `=>` (equals sign followed by a greater-than sign).

- No Brackets or return: You remove the curly brackets ({}) and the return keyword. The `=>` implicitly handles the return of the expression's result.

**Usage:** It can be applied to both normal functions and anonymous (lambda) functions.

**Recursion**

Recursion is a process where a function calls itself repeatedly. A function that does this is known as a recursive function . Recursion is typically used when a problem can be naturally defined in terms of itself, such as calculating a factorial (e.g., 5! = 4! x 5).
``` dart
int factorial(int n) {
  if (n == 1) return 1; // Base case
  return n * factorial(n - 1); // Recursive call
}

void main() {
  print(factorial(5)); // Output: 120
}
```

| Component | Description |
| --- | --- |
| Recursive Call | The statement inside the function where it calls itself, usually with a modified input (e.g., `getFactorial(n-1)`). |
| Base Case | An `if` condition that defines the termination point. When met (e.g., `n == 1`), the function returns a simple value and stops the process. |
