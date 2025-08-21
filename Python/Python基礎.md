# Python 基礎

## データ型

```
# 整数
x = 5
# 浮動小数点
y = 3.14
# 文字列
name = "Alice"
# ブール値
is_valid = True
```

## 演算子

```
# 算術演算
sum = 5 + 3       # 8
division = 10 / 2 # 5.0
integer_div = 10 // 3 # 3
exponent = 2 ** 3   # 8

# 比較演算
a = 5
b = 3
result = a > b    # True

# 論理演算
logical_result = (a > b) and (b > 0) # True
```

## リスト

```
# リストの作成
fruits = ['apple', 'banana', 'cherry']
# インデックスとスライス
first_fruit = fruits[0]     # 'apple'
sublist = fruits[1:3]       # ['banana', 'cherry']
# 操作
fruits.append('orange')
fruits.remove('banana')
```

## タプル

```
# タプルの作成
coordinates = (10, 20)
# タプルは変更不可
# coordinates[0] = 15  # これはエラーになる
```

## 辞書

```
# 辞書の作成
person = {'name': 'Alice', 'age': 30}
# 辞書の操作
name = person['name']      # 'Alice'
person['age'] = 31
# メソッド
keys = person.keys()       # dict_keys(['name', 'age'])
values = person.values()   # dict_values(['Alice', 31])
```

## 集合

```
# 集合の作成
unique_numbers = {1, 2, 3, 4, 5}
# 集合の操作
unique_numbers.add(6)
unique_numbers.discard(2)
```

if 文

```
x = 10
if x > 5:
    print("xは5より大きい")
elif x == 5:
    print("xは5と等しい")
else:
    print("xは5より小さい")
```

for 文と while 文

```
# forループ
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# whileループ
count = 0
while count < 5:
    print(count)
    count += 1
```

## break, continue, else

```
for i in range(10):
    if i == 5:
        break  # iが5になった時点でループを終了
    if i % 2 == 0:
        continue  # iが偶数の場合、この反復をスキップ
    print(i)
else:
    print("ループが正常に終了しました")
```

## 関数の定義

```
def greet(name):
    return f"Hello, {name}"

print(greet("Alice"))  # Hello, Alice
```

## デフォルト引数と可変長引数

```
def multiply(a, b=2):
    return a * b

print(multiply(5))      # 10
print(multiply(5, 3))   # 15

def print_args(*args):
    for arg in args:
        print(arg)

print_args(1, 2, 3, 4)  # 1 2 3 4
```

## lambda 関数

```
square = lambda x: x ** 2
print(square(4))  # 16
```

## モジュール

```
# モジュールのインポート
import math
print(math.sqrt(16))  # 4.0

from math import pi
print(pi)  # 3.141592653589793
```

## パッケージ

```
# パッケージ構造の例
# mypackage/
# ├── __init__.py
# └── module.py
# __init__.pyの中でmoduleをインポートしておくと便利
from .module import some_function
```

## 例外処理

```
try:
    x = 10 / 0
except ZeroDivisionError:
    print("ゼロ除算エラーです")
else:
    print("エラーが発生しませんでした")
finally:
    print("例外処理が終了しました")
```

## カスタム例外

```
class CustomError(Exception):
    pass

def risky_function(value):
    if value < 0:
        raise CustomError("負の値は許可されていません")

try:
    risky_function(-1)
except CustomError as e:
    print(e)  # 負の値は許可されていません
```

## クラスの定義

```
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hello, my name is {self.name}"

p = Person("Alice", 30)
print(p.greet())  # Hello, my name is Alice
```

## 継承

```
class Employee(Person):
    def __init__(self, name, age, position):
        super().__init__(name, age)
        self.position = position

    def greet(self):
        return f"Hello, my name is {self.name} and I work as a {self.position}"

e = Employee("Bob", 40, "Developer")
print(e.greet())  # Hello, my name is Bob and I work as a Developer
```

## ファイルの読み書き

```
# 書き込み
with open('file.txt', 'w') as f:
    f.write('Hello, world!')

# 読み込み
with open('file.txt', 'r') as f:
    content = f.read()
    print(content)  # Hello, world!
```

## 標準ライブラリ

```
import os
import sys

print(os.getcwd())  # 現在の作業ディレクトリ
print(sys.version)  # Pythonのバージョン
```

## 仮想環境

```
# 仮想環境の作成
python -m venv myenv
# 仮想環境のアクティベート
# Windows:
myenv\Scripts\activate
# macOS/Linux:
source myenv/bin/activate
```

## コードスタイル PEP 8

```
インデントは4スペース。
1行の最大長は79文字。
関数やクラスの定義前に2行の空行を入れる。
```

## 文字列の操作

```
name = "Alice"
greeting = "Hello, " + name  # "Hello, Alice"
repeat = "Hi! " * 3          # "Hi! Hi! Hi! "

# f-stringを使ったフォーマット
age = 30
formatted = f"Name: {name}, Age: {age}"  # "Name: Alice, Age: 30"
```

## リスト内包表記

```
squares = [x**2 for x in range(10)]           # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
even_squares = [x**2 for x in range(10) if x % 2 == 0]  # [0, 4, 16, 36, 64]

# 辞書の内包表記
square_dict = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## リストのループ処理

```
# インデックスを使う
for i in range(len(fruits)):
    print(fruits[i])

# 直接要素を扱う
for fruit in fruits:
    print(fruit)
```

## else ブロックの使い方

```
# whileやforループのelseブロックは、ループが正常に終了した場合に実行されます。
# ループがbreakで終了した場合は実行されません。

for i in range(5):
    print(i)
else:
    print("ループが正常に終了しました")
```

## デコレータ

```
def decorator_function(original_function):
    # デコレータ関数を定義。引数に元の関数を受け取る。
    def wrapper_function():
        # デコレータがラップする関数を実行する前にメッセージを表示
        print("Wrapper executed this before {}".format(original_function.__name__))
        # 元の関数を実行し、その結果を返す
        return original_function()
    # ラップされた関数を返す
    return wrapper_function

@decorator_function
def say_hello():
    # 元の関数
    return "Hello!"

print(say_hello())  # Wrapper executed this before say_hello \n Hello!
```

## クロージャ

```
# 内側の関数が外側の関数の変数にアクセスできる機能
def outer_function(msg):
    # 外側の関数
    def inner_function():
        # 内側の関数は外側の関数の変数にアクセスできる
        print(msg)
    # 内側の関数を返す
    return inner_function

my_greeting = outer_function("Hello")
my_greeting()  # Hello
```

## モジュールの再利用

```
# mymodule.py
def greet(name):
    # 名前に対して挨拶を返す関数
    return f"Hello, {name}"

# main.py
import mymodule

# モジュールの関数を使って挨拶を表示
print(mymodule.greet("Alice"))  # Hello, Alice
```

## **all**と**init**.py

```
# __init__.py
__all__ = ['module1', 'module2']
# __init__.pyにより、package内のmodule1とmodule2のみがimport *でインポートされる

# パッケージ内の初期化処理を行うこともできます。
```

## raise を使ったエラーの再スロー

```
def foo():
    try:
        # 故意にゼロ除算を発生させる
        x = 10 / 0
    except ZeroDivisionError:
        # エラーメッセージを表示し、エラーを再スロー
        print("ZeroDivisionErrorが発生しました")
        raise  # エラーを再スロー

try:
    foo()
except ZeroDivisionError:
    # 再スローされた例外を捕捉し、エラーメッセージを表示
    print("再スローされたZeroDivisionError")
```

## クラスメソッドと静的メソッド

`クラスメソッド`: クラス自体に関連するメソッドで、@classmethod デコレータを使います。
`静的メソッド`: クラスの状態に依存しないメソッドで、@staticmethod デコレータを使います。

```
class MyClass:
    @classmethod
    def class_method(cls):
        # クラスメソッドはクラスオブジェクトを受け取る
        return "class method called"

    @staticmethod
    def static_method():
        # 静的メソッドはクラスの状態に依存しない
        return "static method called"

print(MyClass.class_method())  # class method called
print(MyClass.static_method()) # static method called
```

## プロパティ

```
# クラスの属性に対するゲッターとセッターを定義
class Person:
    def __init__(self, name):
        # プライベート属性を初期化
        self._name = name

    @property
    def name(self):
        # ゲッター: 属性を取得する
        return self._name

    @name.setter
    def name(self, value):
        # セッター: 属性の値を設定する
        self._name = value

p = Person("Alice")
print(p.name)  # Alice: ゲッターによって属性が取得される
p.name = "Bob"
print(p.name)  # Bob: セッターによって属性が設定された
```
