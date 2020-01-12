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
