### 读取文件每一行，并处理其中数据 Read a file line-by-line by iterating.
> 数据如下
> ```
> AA 100 32.20
> IBM 50 91.10
> ```
```python
# pcost.py

total_cost = 0.0

with open('Data/portfolio.dat', 'r') as f:
    for line in f:
        fields = line.split()
        nshares = int(fields[1])
        price = float(fields[2])
        total_cost = total_cost + nshares * price

print(total_cost)
```
### 读取文件一次性处理数据 Read an entire file all at once as a string.

```python
with open('foo.txt', 'rt') as file:
    data = file.read()
    # `data` is a string with all the text in `foo.txt`
```

### 定义函数， 错误处理
```python
def portfolio_cost(filename):
    total_cost = 0.0
    with open(filename) as f:
        for line in f:
            fields = line.split()
            try:
                nshares = int(fields[1])
                price = float(fields[2])
                total_cost = total_cost + nshares*price

            # This catches errors in int() and float() conversions above
            except ValueError as e:
                print("Couldn't parse:", repr(line))
                print("Reason:", e)
    return total_cost

print(portfolio_cost('Data/portfolio3.dat'))
```
### 条件语句 conditional with if statement
> if 后可以不用括号， 是elif 不是 elseif   
> Check for multi conditions by adding extra checks using elif    
```python
if a > b:
    print("A")
elif a == b:
    print("B")
else:
    print("C")
```

### 用户输入 user input
```python
name = input('What is your name? ')
print('Hello ' + name)
```

### list comprehension (expression) for (variable_name) in (sequence) if (condition)
  

```python
>>> a = [1, -5, 4, 2, -2, 10]
>>> b = [2*x for x in a if x > 0 ]
>>> b
[2, 8, 4, 20]
>>>
```


### Tuples vs. Lists

Tuples look like read-only lists. However, tuples are most often used for a single item consisting of multiple parts.    
Lists are usually a collection of distinct items, usually all of the same type.   
Tuple 像是数据库的一行， 由不同的数据类型组成， List 通常是同一种数据类型， ordered, 体现的是 sequence   
### 读取CSV文件
```
import pandas as pd
columns_to_be_added_as_features = ['Sex','Age','SibSp','Parch','Pclass','Fare','Embarked']
train_df = pd.read_csv('/kaggle/input/titanic-data/train.csv', usecols=columns_to_be_added_as_features + ['Survived'])
test_df_matcher = pd.read_csv('/kaggle/input/titanic-data/test.csv', usecols=columns_to_be_added_as_features + ['PassengerId'])
test_df = test_df_matcher[columns_to_be_added_as_features]
print(train_df.head())
print("Number of rows in training set: {}".format(len(train_df)))

# Convert string to float.
for column_title in columns_to_be_added_as_features:
    if column_title in ['Embarked', "Sex"]:
        continue
    train_df[column_title] = pd.to_numeric(train_df[column_title], downcast="float")
    test_df[column_title] = pd.to_numeric(test_df[column_title], downcast="float")

train_df["Survived"] = pd.to_numeric(train_df["Survived"], downcast="float")

```
### 字符串处理
```
Method	Description
capitalize()	Converts the first character to upper case
casefold()	Converts string into lower case
center()	Returns a centered string
count()	Returns the number of times a specified value occurs in a string
encode()	Returns an encoded version of the string
endswith()	Returns true if the string ends with the specified value
expandtabs()	Sets the tab size of the string
find()	Searches the string for a specified value and returns the position of where it was found
format()	Formats specified values in a string
format_map()	Formats specified values in a string
index()	Searches the string for a specified value and returns the position of where it was found
isalnum()	Returns True if all characters in the string are alphanumeric
isalpha()	Returns True if all characters in the string are in the alphabet
isascii()	Returns True if all characters in the string are ascii characters
isdecimal()	Returns True if all characters in the string are decimals
isdigit()	Returns True if all characters in the string are digits
isidentifier()	Returns True if the string is an identifier
islower()	Returns True if all characters in the string are lower case
isnumeric()	Returns True if all characters in the string are numeric
isprintable()	Returns True if all characters in the string are printable
isspace()	Returns True if all characters in the string are whitespaces
istitle()	Returns True if the string follows the rules of a title
isupper()	Returns True if all characters in the string are upper case
join()	Joins the elements of an iterable to the end of the string
ljust()	Returns a left justified version of the string
lower()	Converts a string into lower case
lstrip()	Returns a left trim version of the string
maketrans()	Returns a translation table to be used in translations
partition()	Returns a tuple where the string is parted into three parts
replace()	Returns a string where a specified value is replaced with a specified value
rfind()	Searches the string for a specified value and returns the last position of where it was found
rindex()	Searches the string for a specified value and returns the last position of where it was found
rjust()	Returns a right justified version of the string
rpartition()	Returns a tuple where the string is parted into three parts
rsplit()	Splits the string at the specified separator, and returns a list
rstrip()	Returns a right trim version of the string
split()	Splits the string at the specified separator, and returns a list
splitlines()	Splits the string at line breaks and returns a list
startswith()	Returns true if the string starts with the specified value
strip()	Returns a trimmed version of the string
swapcase()	Swaps cases, lower case becomes upper case and vice versa
title()	Converts the first character of each word to upper case
translate()	Returns a translated string
upper()	Converts a string into upper case
zfill()	Fills the string with a specified number of 0 values at the beginning
```
### JSON
```
import json

# some JSON:
x = '{ "name":"John", "age":30, "city":"New York"}'

# parse x:
y = json.loads(x)

# the result is a Python dictionary:
print(y["age"])
```
```
# a Python object (dict):
x = {
  "name": "John",
  "age": 30,
  "city": "New York"
}

# convert into JSON:
y = json.dumps(x)

# the result is a JSON string:
print(y)

```
```
import json

x = {
  "name": "John",
  "age": 30,
  "married": True,
  "divorced": False,
  "children": ("Ann","Billy"),
  "pets": None,
  "cars": [
    {"model": "BMW 230", "mpg": 27.5},
    {"model": "Ford Edge", "mpg": 24.1}
  ]
}

# use four indents to make it easier to read the result:
print(json.dumps(x, indent=4))

```
### SHUFFLE and RESTORE  洗牌和恢复
```
# Change to your offset, 6 digits, like 123456 234567 325***

hex_str = "12345678abcdefgh1234223432344234"
seed_str = "123456"

def shuffle_hex_string(hex_str, offset_str):
    # Split offset string into array of 6 numbers
    right_shift = [int(digit) for digit in offset_str]
    
    # Split hex string into 8-char groups
    chunks = [hex_str[i:i+8] for i in range(0, len(hex_str), 8)]
    new_chunks = []
    
    for idx, chunk in enumerate(chunks):
        # Apply circular shift to all chunks, shuffle only if >= 8
        shift = right_shift[idx % 6]
        if len(chunk) < 8:
            # Only circular right shift for leftovers
            shifted = chunk[-shift:] + chunk[:-shift]
            new_chunks.append(shifted)
        else:
            # Shuffle: 2,4,6,3,1,8,5,7 (0-based: 1,3,5,2,0,7,4,6)
            shuffled = chunk[1] + chunk[3] + chunk[5] + chunk[2] + chunk[0] + chunk[7] + chunk[4] + chunk[6]
            # Circular right shift
            shifted = shuffled[-shift:] + shuffled[:-shift]
            new_chunks.append(shifted)
    
    return ''.join(new_chunks)

def restore_hex_string(shuffled_hex_str, offset_str):
    # Split offset string into array of 6 numbers
    right_shift = [int(digit) for digit in offset_str]
    
    # Split shuffled string into 8-char groups
    chunks = [shuffled_hex_str[i:i+8] for i in range(0, len(shuffled_hex_str), 8)]
    original_chunks = []
    
    for idx, chunk in enumerate(chunks):
        # Undo circular shift for all chunks, unshuffle only if >= 8
        shift = right_shift[idx % 6]
        restored_shift = chunk[shift:] + chunk[:shift]  # Left shift to undo right shift
        if len(chunk) < 8:
            # No shuffle to undo, just keep the unshifted result
            original_chunks.append(restored_shift)
        else:
            # Undo shuffle: Inverse of [1,3,5,2,0,7,4,6] → [4,0,3,1,6,2,7,5]
            restored = restored_shift[4] + restored_shift[0] + restored_shift[3] + restored_shift[1] + restored_shift[6] + restored_shift[2] + restored_shift[7] + restored_shift[5]
            original_chunks.append(restored)
    
    return ''.join(original_chunks)

if __name__ == "__main__":
    # Test inputs
    shuffled = shuffle_hex_string(hex_str, seed_str)
    print("Original:", hex_str)
    print("Shuffled:", shuffled)
    
    restored = restore_hex_string(shuffled, seed_str)
    print("Restored:", restored)
```
### Restore
```
# Change to your offset, 6 digits, like 123456 234567 325***

shuffled = "12345678abcdefgh1234223432344234"
seed_str = "123456"

def shuffle_hex_string(hex_str, offset_str):
    # Split offset string into array of 6 numbers
    right_shift = [int(digit) for digit in offset_str]
    
    # Split hex string into 8-char groups
    chunks = [hex_str[i:i+8] for i in range(0, len(hex_str), 8)]
    new_chunks = []
    
    for idx, chunk in enumerate(chunks):
        # Apply circular shift to all chunks, shuffle only if >= 8
        shift = right_shift[idx % 6]
        if len(chunk) < 8:
            # Only circular right shift for leftovers
            shifted = chunk[-shift:] + chunk[:-shift]
            new_chunks.append(shifted)
        else:
            # Shuffle: 2,4,6,3,1,8,5,7 (0-based: 1,3,5,2,0,7,4,6)
            shuffled = chunk[1] + chunk[3] + chunk[5] + chunk[2] + chunk[0] + chunk[7] + chunk[4] + chunk[6]
            # Circular right shift
            shifted = shuffled[-shift:] + shuffled[:-shift]
            new_chunks.append(shifted)
    
    return ''.join(new_chunks)

def restore_hex_string(shuffled_hex_str, offset_str):
    # Split offset string into array of 6 numbers
    right_shift = [int(digit) for digit in offset_str]
    
    # Split shuffled string into 8-char groups
    chunks = [shuffled_hex_str[i:i+8] for i in range(0, len(shuffled_hex_str), 8)]
    original_chunks = []
    
    for idx, chunk in enumerate(chunks):
        # Undo circular shift for all chunks, unshuffle only if >= 8
        shift = right_shift[idx % 6]
        restored_shift = chunk[shift:] + chunk[:shift]  # Left shift to undo right shift
        if len(chunk) < 8:
            # No shuffle to undo, just keep the unshifted result
            original_chunks.append(restored_shift)
        else:
            # Undo shuffle: Inverse of [1,3,5,2,0,7,4,6] → [4,0,3,1,6,2,7,5]
            restored = restored_shift[4] + restored_shift[0] + restored_shift[3] + restored_shift[1] + restored_shift[6] + restored_shift[2] + restored_shift[7] + restored_shift[5]
            original_chunks.append(restored)
    
    return ''.join(original_chunks)

if __name__ == "__main__":
    # Test inputs
    restored = restore_hex_string(shuffled, seed_str)
    print("Restored:", restored)

```
