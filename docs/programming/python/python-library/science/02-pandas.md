# Pandas 常用操作

``` py
import pandas as pd
```

## 创建数据结构

pandas 中的主要数据结构被实现为以下两类：

- DataFrame，您可以将它想象成一个关系型数据表格，其中包含多个行和已命名的列。
- Series，它是单一列。DataFrame 中包含一个或多个 Series，每个 Series 均有一个名称。

``` py
city_names = pd.Series(['San Francisco', 'San Jose', 'Sacramento'])
population = pd.Series([852469, 1015785, 485199])

pd.DataFrame({ 'City name': city_names, 'Population': population })
```

``` py
# Create and populate a 5x2 NumPy array.
my_data = np.array([[0, 3], [10, 7], [20, 9], [30, 14], [40, 15]])

# Create a Python list that holds the names of the two columns.
my_column_names = ['temperature', 'activity']

# Create a DataFrame.
my_dataframe = pd.DataFrame(data=my_data, columns=my_column_names)
```

``` py
california_housing_dataframe = pd.read_csv("https://download.mlcc.google.cn/mledu-datasets/california_housing_train.csv", sep=",")
california_housing_dataframe.describe()

california_housing_dataframe.head() # 头几项信息

california_housing_dataframe.hist('housing_median_age') # 获取中值分布信息（图像）
```

## 访问数据

可以使用 Python dict/list 指令访问 `DataFrame` 数据。

``` py
cities = pd.DataFrame({ 'City name': city_names, 'Population': population })
print(type(cities['City name']))
cities['City name']
```

``` py
print("Rows #0, #1, and #2:")
print(my_dataframe.head(3), '\n')

print("Row #2:")
print(my_dataframe.iloc[[2]], '\n')

print("Rows #1, #2, and #3:")
print(my_dataframe[1:4], '\n')

print("Column 'temperature':")
print(my_dataframe['temperature'])
```

## 操作数据

可以向 Series 应用 Python 的基本运算指令，Series 也可用作大多数 NumPy 的函数的输入。

布尔值 Series 是使用“按位”而非传统布尔值“运算符”组合的。例如，执行逻辑与时，应使用 &，而不是 and。

``` py
population / 1000
np.log(population)
```

对于更复杂的单列转换，您可以使用 Series.apply。像 Python 映射函数一样，Series.apply 将以参数形式接受 lambda 函数，而该函数会应用于每个值。

``` py
population.apply(lambda val: val > 1000000)
```

## 复制

使用 DataFrame 的 `copy` 方法进行深复制

``` py
copy_of_my_dataframe = my_dataframe.copy()
```

## 索引

`Series` 和 `DataFrame` 对象也定义了 `index` 属性，该属性会向每个 `Series` 项或 `DataFrame` 行赋一个标识符值。

默认情况下，在构造时，*pandas* 会赋可反映源数据顺序的索引值。索引值在创建后是稳定的；也就是说，它们不会因为数据重新排序而发生改变。

``` py
cities.index
cities.reindex([2, 0, 1])
```
