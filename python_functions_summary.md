# **Конспект по некоторым аспектам функций в Python**  

## **1. Выполнение кода из строки**  

### **1.1 `eval()`** — выполняет строку Python-кода, возвращая результат.  
```python
x = 10
result = eval("x + 5")
print(result)
```

### **1.2 `exec()`** — выполняет переданный строковый или кодовый объект Python, не возвращает значение, может изменять переданные пространства имен.  
```python
code = "x = 5\nprint(x)"
exec(code)
```

## **2. Проверка свойств объектов**  

### **2.1 `callable()`** — проверяет, является ли объект вызываемым.  
```python
print(callable(len))
```

### **2.2 `hasattr()`** — проверяет наличие атрибута у объекта.  
```python
class A: pass  
a = A()  
print(hasattr(a, 'attr'))
```

### **2.3 `help()`** — выводит справочную информацию по объекту.  
```python
help(print)
```

### **2.4 `repr()`** — возвращает строковое представление объекта.  
```python
print(repr("Hello"))
```

## **3. Хеширование и атрибуты объектов**  

### **3.1 `hash()`** — возвращает хеш-значение объекта.  
```python
print(hash("Hello"))
```

### **3.2 `__dict__`** — содержит атрибуты объекта в виде словаря.  
```python
def my_func(): pass  
my_func.attr = "test"  
print(my_func.__dict__)
```

## **4. Управление областью видимости**  

### **4.1 `nonlocal`** — используется внутри вложенной функции для изменения переменной из внешней области видимости.  
```python
def outer():
    x = 10
    def inner():
        nonlocal x
        x += 5
    inner()
    print(x)
```

## **5. Декораторы**  

### **5.1 Базовый декоратор**  
```python
def sandwich(func):
    def wrapper(*args, **kwargs):
        print("---- Верхний ломтик хлеба ----")
        result = func(*args, **kwargs)
        print("---- Нижний ломтик хлеба ----")
        return result
    return wrapper
```

### **5.2 `functools.wraps`** — сохраняет оригинальные метаданные функции (`__name__`, `__doc__`, `__annotations__`) при использовании декораторов.  
```python
from functools import wraps

def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Before function call")
        result = func(*args, **kwargs)
        print("After function call")
        return result
    return wrapper
```

### **5.3 Декораторы с аргументами**  
```python
from functools import wraps

def repeat(n):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet():
    print("Hello!")
```
