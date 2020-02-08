# 结构化数据读写

## YAML `pyyaml`

<https://pyyaml.org/wiki/PyYAMLDocumentation>

```sh
pip install pyyaml
```

```python
import yaml

obj = yaml.load('An yaml document.') # 对不受信任的源使用yaml.safe_load()。
yaml.load_all(...) # 若yaml文档使用“---”分隔，此函数读取所有文档并装入一个list中。

yaml.dump({'a': 'apple', 'b': 'river'})
yaml.dump_all([1, 2, 3])
```

`safe_load()`只读取标准的YAML标记，而不会生成任意Python对象，从而不会有执行任意代码的风险。

## HTML `lxml`

### Element如list

```py
from lxml import etree

# Element构造方法
root = etree.Element("root")
print(root.tag)  # root

# Element的接口类似于list
# 同级关系
root.append(etree.Element("child1"))
child2 = etree.SubElement(root, "child2")
root.insert(2, etree.Element("child3"))

# 层级关系
child1 = root[0]
len(root)           # 3，可用于检测是否有子Element。
root.index(root[1]) # 1

root is root[1].getparent()
root[0] is root[1].getprevious()
root[2] is root[1].getnext()

# 与原始数组的不同在于使用“=”时，元素会被移动而不是被复制。
root[0] = root[-1] # 得到[child3, child2]而不是[child3, child2, child3]。
# 可以使用`from copy import deepcopy`来进行复制。

# 遍历
children = list(root)
for child in root:
    print(child.tag)

print(etree.tostring(root, pretty_print=True))
```

### Element上的属性如dict

```py
root = etree.Element("root", python="this")
root.set("java", "that")
root.get("java")
```

```py
>>> attributes = root.attrib

>>> print(attributes["interesting"])
totally
>>> print(attributes.get("no-such-attribute"))
None

>>> attributes["hello"] = "Guten Tag"
>>> print(attributes["hello"])
Guten Tag
>>> print(root.get("hello"))
Guten Tag
```

### Element包含Text

使用`text`和`tail`属性。

```py
>>> html = etree.Element("html")
>>> body = etree.SubElement(html, "body")
>>> body.text = "TEXT"

>>> etree.tostring(html)
b'<html><body>TEXT</body></html>'

>>> br = etree.SubElement(body, "br")
>>> etree.tostring(html)
b'<html><body>TEXT<br/></body></html>'

>>> br.tail = "TAIL"
>>> etree.tostring(html)
b'<html><body>TEXT<br/>TAIL</body></html>'
```
