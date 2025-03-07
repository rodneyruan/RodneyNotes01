### Key Characteristics of Python
Interpreted, Dynamically Typed, Extensive Standard Library,Object-Oriented,Garbage Collection, Corss-Platform, portable.

### is and ==
```
x is y  id(x) == id(y)
x == y
```
### List Tuple and Set
```
Immutable: Once created, you can’t change it
Allows Duplicates

List   An ordered, mutable collection of items (can contain duplicates).
Tuple  An ordered, immutable collection of items (can contain duplicates)
Set    An unordered, mutable collection of unique items.
```
#### Dictionary
```
A  colleciton of key-value pairs.
Unordered, mutual, could be modified.
Curly brackets. 
Fast lookups based on unique keys.
Allows you to store and retrieve values efficiently using keys.

my_dict ={}
person = {'Name':"Alice", "age":25, "city":"New York"}
my_dict['key']
my_dict.get('key')
my_dict.keys()
my_dict.values()
my_dict.items()
len(my_dict)
Add and modify:  my_dict["Age"] = 23, dict.update({})
delete： del my_dict["job"]   my_dict.pop("job") my_dict.clear()
for i in my_dict:
for value in my_dict.values():
for key, value in my_dict.items():
my_dict.copy()
new_dict = dict(my_dict)
Nested Dictionary: nested_dict["Personal"]["age"] = 23
```
### Catch Except
try:
except SomeError: 
else:
finally:
```
try:
    num = int("123")  # No error here
    if(something):
        raise(some eror)
except ValueError:
    print("Invalid input!")
else:
    print("No errors occurred!")  # Runs if no exception occurs
finally:
    print("This runs no matter what!")  # Always executes

```

### Read a file
```
with open("file_name","r") as f:
    f.read()
### Deep Copy
浅拷贝之后仍然指向同一块地址
import copy
copy.deepcopy(a)
```
#### String  Slicing
```
s[-6:]  # last 6 chars
s[:-7] # everything except the last 7 characters
s[::-1] Reverses the string
s[-1：-6：-1]
s[5:]+s[:5] 
```
#### String  Comparison and Concatenation
```
print(s1.lower() == s2.lower())
s.startswith("hello") s.startswith(...)
a = ["Python", "is", "a", "popular", "language", "for", "programming"]
res = " ".join(a)
res = "{} is a popular language for {}".format(s1, s2)
res = f"{s1} is a popular language for {s2}"

```
### Generators
Generate values lazily (on-the-fly) rather than storing them all in memory at once,offering memory efficiency and flexibility
Values are produced one at a time, ***only when requested***
```
List: [x * 2 for x in range(3)] creates [0, 2, 4] in memory.
Generator: (x * 2 for x in range(3)) yields 0, 2, 4 one-by-one.
```
### List index overflow
You got a []

### Two Lists, Get the Diff
```
Change it to a set
set1= set(list1)
set2 = set(list2)
set1 & set2
set1 ^ set2
```

### Decorator （装饰器） 类似于C语言的函数指针传递方法

A decorator in Python is a design pattern that lets you ***modify or extend*** the behavior of a function or method without changing its source code.
It’s essentially a function that takes another function as an argument, wraps it with additional logic, and returns a new function.


```
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with args: {args}")
        result = func(*args, **kwargs)
        print("Finished")
        return result
    return wrapper

@my_decorator
def add(a, b):
    return a + b

print(add(3, 5))
```

### What Are *args and **kwargs?
Special syntax in Python for handling variable numbers of arguments in functions.  
Use when you don’t know how many arguments will be passed. 

*args (Positional Arguments) Collects extra positional arguments into a tuple.  
The * unpacks a sequence of arguments into the function 
You can iterate over args like any tuple.
```
def mixed_args(a, b, *args):
    print("a:", a, "b:", b, "args:", args)

mixed_args(1, 2, 3, 4, 5)
1```
**kwargs (Keyword Arguments) dictionary
The ** unpacks key-value pairs into the function.
```
def mixed_kwargs(a, b, **kwargs):
    print("a:", a, "b:", b, "kwargs:", kwargs)

mixed_kwargs(1, 2, name="Bob", score=95)
```
### 计算列表出现的次数
set-> count
### Generator with yield
Memory Efficiency
Lazy Evaluation
Processing Infinite or Large Sequences 即使死循环也不会有事
on-demand allocation of memory
```
def infinite_count():
    i = 0
    while True:
        yield i
        i += 1
```
```
def count_up():
    print("22")
    for i in range(3):
        print("In the loop")
        yield i
gen = count_up()  # 这个函数暂时不执行，没有打印输出 doesn’t run the function immediately—it creates a generator object and stops.
                  #execution is paused before the first line.
print(next(gen))  # 0 执行到第一个yield， 函数暂停 pauses execution after the yield
print(next(gen))  # 1
print(next(gen))  # 2
```
### 内存管理
私有堆，只有解释器可以访问。 内置垃圾收集器。
### Pythecker
静态分析。
### 获取主目录
os.path.expanduser('~')
### RE  
pattern matching and text manipulation
```
import re
# Regular expression for email validation
email_regex = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
bool(re.match(email_regex, email))
```
[^abc]: Matches anything not a, b, or c.
[a-zA-Z0-9]: Letters or digits (used in email regex).
^ $ * + ?
*: 0 or more
+: 1 or more
?: 0 or 1
. single character

### Closure 闭包
嵌套函数，内部函数，外部函数， 把内部函数作为对象返回。
def outer_function(msg):
    def inner_function():
        print(f"Message: {msg}")  # 'msg' is remembered even after outer_function finishes
    return inner_function  # Returning inner function without calling it

closure_func = outer_function("Hello, Closure!")
closure_func()  # Output: Message: Hello, Closure!


### Functions are Objects
```
In Python, functions are treated as first-class objects, meaning they can:
Be assigned to variables
Be passed as arguments to other functions
Be returned from functions
Be stored in data structures like lists or dictionaries
```
### Pass by reference and pass by value

Mutable objects (lists, dicts, sets, etc.) → Passed by reference (modifications affect the original object).  
Immutable objects (integers, strings, tuples, etc.) → Behave like passed by value (modifications inside the function do not affect the original).

```
def modify_list(lst):
    lst = [100, 200, 300]  # Creates a new list (does not modify original)

numbers = [1, 2, 3]
modify_list(numbers)
print(numbers)  # Output: [1, 2, 3] (unchanged)

```
```
def modify_list(lst):
    lst.append(4)  # Modifies the original list

numbers = [1, 2, 3]
modify_list(numbers)
print(numbers)  # Output: [1, 2, 3, 4]

```
