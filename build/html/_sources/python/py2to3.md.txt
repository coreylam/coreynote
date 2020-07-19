# python2 切换到 python3



## py3 中不支持的py2 用法

### Print Is A Function

- py2 中 `print` 为保留的关键字， 在 py3 中，改为普通的函数。

```bash
Old: print "The answer is", 2*2
New: print("The answer is", 2*2)

Old: print x,           # Trailing comma suppresses newline
New: print(x, end=" ")  # Appends a space instead of a newline

Old: print              # Prints a newline
New: print()            # You must call the function!

Old: print >>sys.stderr, "fatal error"
New: print("fatal error", file=sys.stderr)

Old: print (x, y)       # prints repr((x, y))
New: print((x, y))      # Not the same as print(x, y)!
```

- py2 中 `print` 支持 “softspace” 的特性，当前一个字符串换行结束时，下一个字符串不会自动添加空格， 在 py3 中，默认分隔符为空格，可通过 `sep` 参数指定

```python
# py2
>>> print "A\n", "B"
A
B
>>> print "A", "B"
A B

# py3
>>> print("A\n", "B")
A
 B
>>> print("A", "B")
A B
```



### Views And Iterators Instead Of Lists

- 字典 (`dict`) 的 `keys` 和 `values` 方法，在 py3 中返回类型为对应的视图,  而在 py2 中该返回值为 `List`

```bash
# python2
>>> d = {}
>>> type(d.keys())
<type 'list'>
>>> type(d.values())
<type 'list'>

# python3
>>> d = {}
>>> type(d.keys())
<class 'dict_keys'>
>>> type(d.values())
<class 'dict_values'>
```

- 因此，python3 中 `keys` 和  `values` 的返回值不能再使用 `sort` 等列表类的方法。

```python
# python2
k = d.keys()
k.sort()

# python3
k = sorted(d)
```



## py3 风格

> 这部分提供一些 python3 风格的写法，虽然对应的旧的写法依旧可以正常使用，但新的写法往往可以带来一些新的惊喜（虽然也有一些用法感觉还是旧的用着习惯），代码看起来也更有 python3 的风格， 而非用 python3 的解析器解析 python2 的代码。

### 字符串格式化 format

[**PEP 3101**](https://www.python.org/dev/peps/pep-3101): A New Approach To String Formatting

-  py3 使用 `format` 进行字符串格式化，代替 `%s` 的写法（虽然这种写法在 py3 中依旧支持）

### 函数参数类型

