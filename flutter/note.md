# Flutter
## Dart
### Hello World
```dart
void main(){
    print('Hello, World!');
}
```
### Variables
dart支持以下数据类型：数字(number) 字符串(string) 布尔值(boolean) 列表(list) 集合(set) 映射(map) 符文(rune) 符号(Symbol)
#### number
```dart
int a = 10;
int b = 0xDEADBEEF;
double c = 3.14;
double d = 1.42e5;
```
#### string
```dart
String str1 = 'hello';
String str2 = "hello";
String str = 'hello ' + 'world!'
String newStr = '这是${str}';
```
#### boolean
```dart
bool a = true;
bool b = false;
```
#### list
```dart
List<int> arr = [1,2,3];

var ls = new List();
print(ls);//[]

List<String> arr = const ["常量", "不可再运行时更改"];
```
#### set
```dart
Set <String> cls = {"小王", "小杨"}; 
```
#### map
不严格地说，可以看作 Object / JSON 。
```dart
Map<String, String> person = {
 // Key:    Value
   'name': '杨莹',
   'age': '18',
   'eat': 'true'
};

Map<int, String> nobleGases= {
// Key:    Value
    2: 'react',
    10: 'vue',
    18: 'spring boot'
}

print(person['name']); //杨莹
print(person['age']); //18

var obj = new Map();
obj['flag'] = true;
print(obj.length);//1

var obj = {'name':'杨莹'};
assert(obj['age'] == null);//null
```
#### 自动推断数据类型
dart支持自动推断数据类型，可以像JS一样使用 var 关键字来声明：
```dart
var name = 'Voyager I';
var year = 1977;
var antennaDiameter = 3.7;
```
但是容易导致以下错误
```dart
var x = 3; // x is inferred as an int.
x = 4.0;
```
因为 "x is inferred as an int."
可以改为
```dart
num y = 3; // A num can be double or int.
y = 4.0;
```
#### nullable type
```dart
double? x; // Declare instance variable x, initially null.
double? y; // Declare y, initially null.
double z = 0; // Declare z, initially 0.
```
#### `final` and `const`
const修饰的常量在编译时确定，不能在构造函数中初始化，是编译时常量。  
final修饰的常量必须在声明进初始化或者在构造函数中初始化，是运行时常量。  
共同点是两者赋值后就不能再修改(不能重新赋值，对于引用类型可以修改属性)。  
```dart
  const test1="hello";//正确，编译期常量
  final test2="hello";//正确，运行时常量

  const test3=DateTime.now();//编译报错,值不是编译期常量
  final test4=DateTime.now();//正确，运行时常量

  const test5=new List();//编译报错,值不是编译期常量
  final test6=new List();//正确，运行时常量
```
### Iteration
```dart
if (year >= 2001) {
  print('21st century');
} else if (year >= 1901) {
  print('20th century');
}

for (final object in flybyObjects) {
  print(object);
}

for (int month = 1; month <= 12; month++) {
  print(month);
}

while (year < 2016) {
  year += 1;
}
```

### Function
```dart
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```
#### optional parameters
Named parameters are optional unless they're explicitly marked as `required`.
If you don't provide a default value or mark a named parameter as required, their types must be nullable as their default value will be null:
```dart
void enableFlags({bool? bold, bool? hidden}) {...}

enableFlags(bold: true, hidden: false);
```
When calling a function, you can specify named arguments using paramName: value. For example:
```dart
void enableFlags({bool bold = false, bool hidden = false}) {...}
```
If you instead want a named parameter to be mandatory, requiring callers to provide a value for the parameter, annotate them with `required`:
```dart
const Scrollbar({super.key, required Widget child});
```
#### shorthand syntax
For functions that contain just one expression, you can use a shorthand syntax:
```dart
flybyObjects.where((name) => name.contains('turn')).forEach(print);

bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```
If someone tries to create a Scrollbar without specifying the child argument, then the analyzer reports an issue.
#### anonymous function
you can also create functions without names. These functions are called anonymous functions, lambdas, or closures.

```dart
const list = ['apples', 'bananas', 'oranges'];

var uppercaseList = list.map((item) {
  return item.toUpperCase();
}).toList();
// Convert to list after mapping

for (var item in uppercaseList) {
  print('$item: ${item.length}');
}
```
### `import`
使用 `import` 关键字来访问在其它库中定义的 API。
```dart
import 'dart:math';
```
### Class
Use ?. instead of . to avoid an exception when the leftmost operand is null:
```dart
var p = Point(2, 2);

// Get the value of y.
assert(p.y == 2);

// Invoke distanceTo() on p.
double distance = p.distanceTo(Point(4, 4));

// If p is non-null, set a variable equal to its y value.
var a = p?.y;
```
#### `getter` and `setter`
getter: the function implements when you get the value of the very variable
setter: the function implements when you set the value of the very variable
```dart
class Rectangle {
  double left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  double get right => left + width;
  set right(double value) => left = value - width;
  double get bottom => top + height;
  set bottom(double value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
```
#### Abstract methods
```dart
abstract class Doer {
  // Define instance variables and methods...

  void doSomething(); // Define an abstract method.
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // Provide an implementation, so the method is not abstract here...
  }
}
```
Initializing a non-late instance variable where it's declared sets the value when the instance is created, before the constructor and its initializer list execute. As a result, the initializing expression (after the =) of a non-late instance variable can't access this.
```dart
double initialX = 1.5;

class Point {
  // OK, can access declarations that do not depend on `this`:
  double? x = initialX;

  // ERROR, can't access `this` in non-`late` initializer:
  double? y = this.x;

  // OK, can access `this` in `late` initializer:
  late double? z = this.x;

  // OK, `this.x` and `this.y` are parameter declarations, not expressions:
  Point(this.x, this.y);
}
```