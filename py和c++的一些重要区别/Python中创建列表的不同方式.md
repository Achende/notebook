Python 中有多种创建列表的方法。先总结后详述：

**总结:**

| 方法                 | 描述                                                               | 优点                         | 缺点/注意事项                        |
| :------------------- | :----------------------------------------------------------------- | :--------------------------- | :----------------------------------- |
| `[]` (字面量)        | 最直接、基本的方式                                                   | 简单直观                     |                                      |
| `list(iterable)`     | 将其他可迭代对象转换为列表                                           | 灵活，易于类型转换           |                                      |
| 列表推导式           | 基于现有迭代对象创建新列表，可包含逻辑和转换                       | 简洁、高效、可读性好（常用） | 对于复杂逻辑可能变得难读             |
| `append()`           | 逐个添加元素到列表末尾                                             | 适合逐步构建列表             | 效率不如列表推导式（如果已知大小）   |
| `extend(iterable)`   | 将一个可迭代对象的所有元素添加到列表末尾                           | 方便合并序列               |                                      |
| `[element] * n`      | 创建包含 n 个重复元素的列表                                        | 简洁（用于重复）             | **对可变对象极不安全，易出错！**     |

选择哪种方法取决于你的具体需求：

*   如果只是简单列出元素，用 `[]`。
*   如果需要从其他序列转换，用 `list()`。
*   如果需要根据规则或现有序列生成新列表，优先考虑列表推导式。
*   如果需要在运行时动态添加元素，用 `append()` 或 `extend()`。
*   如果需要重复不可变元素，可以用 `*`，但对可变元素**绝对要避免**！



***1. 使用方括号 `[]` (列表字面量 - Literal)***

这是最基本、最直接的方法，直接用方括号将元素括起来，用逗号分隔。

```python
# 创建空列表
empty_list = []
print(empty_list)  # 输出: []

# 创建包含整数的列表
numbers = [1, 2, 3, 4, 5]
print(numbers)     # 输出: [1, 2, 3, 4, 5]

# 创建包含不同类型元素的列表
mixed_list = [1, "hello", 3.14, True, None, [10, 20]]
print(mixed_list)  # 输出: [1, 'hello', 3.14, True, None, [10, 20]]
```

***2. 使用 `list()` 构造函数***

`list()` 是一个内置函数，可以将其他可迭代对象 (iterable) 转换为列表。

```python
# 从字符串创建列表（每个字符是一个元素）
string_to_list = list("Python")
print(string_to_list)  # 输出: ['P', 'y', 't', 'h', 'o', 'n']

# 从元组 (tuple) 创建列表
tuple_to_list = list((10, 20, 30))
print(tuple_to_list)   # 输出: [10, 20, 30]

# 从 range 对象创建列表
range_to_list = list(range(5)) # range(5) 生成 0, 1, 2, 3, 4
print(range_to_list)   # 输出: [0, 1, 2, 3, 4]

# 从集合 (set) 创建列表（顺序可能不固定）
set_to_list = list({1, 3, 2})
print(set_to_list)     # 输出可能是: [1, 2, 3] 或其他顺序

# 从字典 (dict) 的键、值或项创建列表
my_dict = {'a': 1, 'b': 2}
keys_list = list(my_dict.keys())     # 或 list(my_dict)
values_list = list(my_dict.values())
items_list = list(my_dict.items()) # 列表中的元素是 (键, 值) 元组
print(keys_list)     # 输出: ['a', 'b']
print(values_list)   # 输出: [1, 2]
print(items_list)    # 输出: [('a', 1), ('b', 2)]

# 使用 list() 创建空列表（等同于 []）
empty_list_constructor = list()
print(empty_list_constructor) # 输出: []
```

***3. 列表推导式 (List Comprehension)***

正如你之前看到的，这是一种非常强大和简洁的方式，用于基于现有可迭代对象创建新列表。

```python
# 创建 0 到 9 的平方列表
squares = [x**2 for x in range(10)]
print(squares)  # 输出: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# 创建 0 到 9 中的偶数列表
evens = [x for x in range(10) if x % 2 == 0]
print(evens)    # 输出: [0, 2, 4, 6, 8]

# 对列表中的每个字符串执行操作
words = ["hello", "world", "python"]
upper_words = [word.upper() for word in words]
print(upper_words) # 输出: ['HELLO', 'WORLD', 'PYTHON']
```

***4. 使用 `append()` 方法逐步构建***

可以先创建一个空列表，然后使用 `append()` 方法逐个添加元素。

```python
my_list = []
my_list.append("apple")
my_list.append("banana")
my_list.append("cherry")
print(my_list) # 输出: ['apple', 'banana', 'cherry']

# 在循环中构建
numbers_built = []
for i in range(1, 6):
  numbers_built.append(i * 10)
print(numbers_built) # 输出: [10, 20, 30, 40, 50]
```

***5. 使用 `extend()` 方法合并列表***

`extend()` 方法可以将一个可迭代对象中的所有元素添加到列表末尾。

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
list1.extend(list2) # 将 list2 的元素添加到 list1
print(list1) # 输出: [1, 2, 3, 4, 5, 6]
print(list2) # 输出: [4, 5, 6] (list2 本身不变)

list3 = [7, 8]
list3.extend("abc") # 也可以扩展字符串等可迭代对象
print(list3) # 输出: [7, 8, 'a', 'b', 'c']
```

***6. 使用乘法 `*` (用于重复元素 - 需谨慎!)***

可以使用乘法运算符 `*` 来创建一个包含重复元素的列表。

*   **对于不可变对象 (如数字、字符串、元组) 通常是安全的：**

    ```python
    zeros = [0] * 5
    print(zeros) # 输出: [0, 0, 0, 0, 0]

    abcs = ["abc"] * 3
    print(abcs)  # 输出: ['abc', 'abc', 'abc']
    ```

*   **⚠️ 对于可变对象 (如列表、字典) 需要非常小心！** 这种方式会创建**指向同一个对象的多个引用**，修改一个会影响所有：

    ```python
    # ！！！不推荐的方式初始化嵌套列表！！！
    nested_bad = [[]] * 3
    print(nested_bad) # 输出: [[], [], []]
    nested_bad[0].append(1) # 修改第一个内部列表
    print(nested_bad) # 输出: [[1], [1], [1]] <-- 问题！所有内部列表都变了！

    # 正确的创建嵌套列表的方式是使用列表推导式
    nested_good = [[] for _ in range(3)]
    nested_good[0].append(1)
    print(nested_good) # 输出: [[1], [], []] <-- 正确！
    ```
