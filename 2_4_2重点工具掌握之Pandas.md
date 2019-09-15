# 重点工具掌握之二：Pandas
Hi，朋友们，上周我们了解了Numpy的基本特性和用法，这周我们就来了解一下另外一个利器 —— Pandas。Pandas帮我们引入了更适应数据表的数据类型，而且它基于Numpy开发，运算速度也非常快，可以说它在Python数据分析中占据了C位，那我们快来一睹它的风采吧！

由于Pandas穿插应用在数据分析的各个流程中，所以在本文中，我们先介绍Pandas的基本知识，然后在梳理数据分析的流程中再讲解Pandas的函数应用。

## 本周内容
 
- **Pandas**简介
- **Pandas Series**
- **Pandas DataFrame**
- 数据分析流程及Pandas函数应用
- 延伸：Pandas数据融合

### Pandas简介
 
**Pandas** 是 Python 中的数据操纵和分析软件包，它是基于Numpy去开发的，所以Pandas的数据处理速度也很快，而且Numpy中的有些函数在Pandas中也能使用，方法也类似。
 
Pandas 为 Python 带来了两个新的数据结构，即 **Pandas Series**(可类比于表格中的某一列)和 **Pandas DataFrame**(可类比于表格)。借助这两个数据结构，我们能够轻松直观地处理*带标签*数据和*关系*数据。
 
> ⚠️Series中各个元素的数据类型可以不一致，DataFrame也是如此，这与numpy的ndarray不同。

> 其实还有一个三维的数据结构Panel，但用的很少，感兴趣的话可以了解一下～

### 创建Pandas Series
 
可以使用 `pd.Series(data, index)` 命令创建 Pandas Series，其中`data`表示输入数据， `index` 为对应数据的索引，除此之外，我们还可以添加参数`dtype`来设置该列的数据类型。
 
示例:
 
```python
import pandas as pd #约定俗成的简称
pd.Series(data = [30, 6, 7, 5], index = ['eggs', 'apples', 'milk', 'bread'],dtype=float)
 
out:
eggs      30.0
apples     6.0
milk       7.0
bread      5.0
dtype: float64
```
 
`data`除了可以输入列表之外，还可以输入字典，或者是直接一个标量。
 
```python
#data输入字典
pd.Series(data = {'eggs':30,'apples': 6,  'milk':7, 'bread':5},dtype=float)
 
out:
apples     6.0
bread      5.0
eggs      30.0
milk       7.0
dtype: float64
 
#data输入某一标量
pd.Series(data = 7, index = ['eggs', 'apples', 'milk', 'bread'])
 
out:
eggs      7
apples    7
milk      7
bread     7
dtype: int64
```
 
### 访问和删除Series中的元素
 
- **访问**
 
访问Series中的元素有两种方法：
 
一种类似于从列表中按照索引访问数据，一种类似于从字典中按照**key**来访问**value**。
 
下面看示例：
 
![FY9vQg.png](https://s1.ax1x.com/2018/12/11/FY9vQg.png)
 
从上面代码里也能发现，Pandas提供的`iloc`与`loc`分别对应着按索引访问和按key访问。
 
- **修改**
 
因为Series是可更改类型，若想更改其中某一项，只需访问它然后重新赋值即可。
 
- **删除**
 
可以使用 `.drop()` 方法删除 Pandas Series 中的条目。`Series.drop(label)` 方法会从给定 `Series` 中删除给定的 `label`。这个`label`可以是单个label或这是label组成的list。
 
![FYPWKe.png](https://s1.ax1x.com/2018/12/11/FYPWKe.png)
 
但需要注意的是，`.drop()`函数并不会修改原来的数据，如果你想要修改原数据的话，可以选择添加参数`inplace = True`或者是用原数据替换`s = s.drop(label)`
> `inplace`参数会经常出现在Pandas的函数中，所以，写代码时一定要细心，不要闹出诸如`s = s.drop(label,inplace=True)`这样的乌龙。
 
### Series运算
 
和ndarray一样，Series也可以进行**元素级**的算术运算，也可以使用np中提供的各种运算函数，如`sqrt()`等等。
 
这里可以想一下，如果Series中包含字符串，然后再进行乘法会是什么结果？
 
可以回想下字符串的知识`'*'*10`的结果是什么？
 
### 创建DataFrame
 
我们使用`pd.DataFrame(data, index, columns)`来创建一个DataFrame。
 
其中：
 
`data`是数据，可以输入ndarray，或者是字典（字典中可以包含Series或arrays或），或者是DataFrame；
 
`index`是索引，输入列表，如果没有设置该参数，会默认以0开始往下计数；
 
`columns`是列名，输入列表，如果没有设置该参数，会默认以0开始往右计数；
 
示例：
 
![FYkQDe.png](https://s1.ax1x.com/2018/12/11/FYkQDe.png)
 
从上述代码中可以看出，字典`d`中的`key`被当作列名，`value`被当作dataframe中的数据。
 
> 🤔 如果在上述代码中添加一个columns列，如`df = pd.DataFrame(data=d,index = ['a','b'],columns = ['col_1','col_2'])`，会返回什么结果呢？
 
### 访问DataFrame中的元素
 
与访问Series中的元素类似，我们可以通过列表式索引访问，也可以通过字典式Key值访问。
 
- 创建一个DataFrame
 
![FYfMh6.png](https://s1.ax1x.com/2018/12/12/FYfMh6.png)
 
 
 
- 访问某一行
 
![FYh15q.png](https://s1.ax1x.com/2018/12/12/FYh15q.png)
 
- 访问多行
 
![FY4lOe.png](https://s1.ax1x.com/2018/12/12/FY4lOe.png)
 
- 访问某一列
 
![FY4nW6.png](https://s1.ax1x.com/2018/12/12/FY4nW6.png)
 
- 访问多列
 
![FY4tYt.png](https://s1.ax1x.com/2018/12/12/FY4tYt.png)
 
> ⚠️使用df.iloc[:,0:2]这种方法只能筛选出连续的列，那如果想要筛选的列分别在1,3,5,10:17怎么办呢？可以搜一下`np.r_`的用法，试试看！
 
- 访问某一元素
 
![FY4aSf.png](https://s1.ax1x.com/2018/12/12/FY4aSf.png)
 
> 🤔 在第一种方法中，我们必须先访问列，再访问行，想想为什么？
### 删除、增加元素
 
- 删除元素
 
我们使用`.drop`函数删除元素，默认为删除行，添加参数`axis = 1`来删除列。
 
![FY5x2V.png](https://s1.ax1x.com/2018/12/12/FY5x2V.png)
 
值得注意的是，`drop`函数不会修改原数据，如果想直接对原数据进行修改的话，可以选择添加参数`inplace = True`或用原变量名重新赋值替换。
 
- 增加元素
 
这里先介绍两种方法，一种是`append()`，另外一种是`insert()`，这两种方法都比较简单，可类比于python list中的两种方法进行学习。
 
此外，Pandas还提供了其他更为复杂的做DataFrame融合的函数，比如说`concat()`、`merge()`、`join()`等等，相对难一些，会放在延伸内容Pandas数据融合中进行讲解。
 
### 更改行列标签
 
使用函数`rename()`即可。具体用法如下：
 
![FYIIiR.png](https://s1.ax1x.com/2018/12/12/FYIIiR.png)
 
除此之外，还可以使用隐匿函数lambda来对行列标签进行统一处理，比如：
 
![FYIoJ1.png](https://s1.ax1x.com/2018/12/12/FYIoJ1.png)
 
需要注意的是，`rename()`函数同样不会更改原数据，如果想直接对原数据进行修改的话，可以选择添加参数`inplace = True`或用原变量名重新赋值替换。
 
### 更改索引
 
可以使用函数`set_index(index_label)`，将数据集的index设置为`index_label`。
 
除此之外，还可以使用函数`reset_index()`重置数据集的index为0开始计数的数列。
 
### 缺失值(NaN)处理
 
`NaN`就是**Not a Number**的缩写，表示这里有数据缺失。 

> 如何处理缺失值呢？这就要根据确实数据的情况而定了，是直接删除？还是暴力平均值替换？还是分类之后再用平均值替换？还是用一些什么其他的方法，全靠你去把握了。可以看一看**Python Data Science**这本书中的[**Handling Missing Data**](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html)章节，你肯定会有所收获的。
 
- 查找NaN
 
我们可以使用`isnull()`和`notnull()`函数来查看数据集中是否存在缺失数据，在该函数后面添加`sum()`函数来对缺失数量进行统计。除此之外，还可以使用`count()`函数对非NaN数据进行统计计数。
 
![FYIzFA.png](https://s1.ax1x.com/2018/12/12/FYIzFA.png)
 
- 删除NaN
 
使用`dropna(axis)`函数可以删除包含NaN的行或列。
 
>  `dropna()`函数还有一个参数是`how`，当`how = all`时，只会删除全部数据都为NaN的列或行。
 
同样，该函数也不会修改原数据集。
 
- 替换NaN
 
使用`fillna()`函数可以替换NaN为某一值。其参数如下：
 
1. **value**：用来替换NaN的值
2. **method**：常用有两种，一种是`ffill`前向填充，一种是`backfill`后向填充
3. **axis**：0为行，1为列
4. **inplace**：是否替换原数据，默认为False
5. **limit**：接受int类型的输入，可以限定替换前多少个NaN
 
 
还可以使用`interpolate()`函数按照某一方法来替换NaN，如`linear`，它是忽略索引并将值视为相等间距，这是该函数的默认方法。更多method及解读请戳[pandas.DataFrame.interpolate](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.interpolate.html)
 
### 数据分析流程及Pandas应用
 
**数据分析不是从上至下一蹴而就的过程，而是需要你不断迭代、重复、完善，最终得到结论的过程。**
 
#### 提出问题
 
- 数据集中的各个变量之间的相关性如何？是否存在某些联系？
 
- 变量的统计结果会揭示什么？
 
- 根据现有掌握的数据，能否对未来走势进行预测？
 
- 根据你想了解的问题，去收集数据，再对问题进行修缮，如此**迭代**，获取更全面的数据，提出更一阵见血的问题。
 
  ...
 
#### 整理数据
整理数据是整个数据分析流程中最为耗时、最磨耐心的一部分，但也是对结果影响最大的一部分，所以，大家一定要踏下心来，结合实际业务，一定要把这部分做扎实～
 
- 收集
 
  数据库提取？直接下载？网络爬虫？
 
- 评估
 
  这个过程是对数据产生直观印象的过程，你要尝试了解数据集的大小，基本的统计结果，是否存在数据重复？缺失？数据类型是否正确？是否每个变量成一列&每个观察值成一行？数据是否有统计错误？(严重偏离正常值，比如说气温达到70℃等等)...
  - 打开文件
   ```python
  #打开csv文件
  pd.read_csv('filename')
  #打开excel文件
  pd.read_excel('filename')
  #处理中文字符的tsv文件
  pd.read_csv('filename',sep = '\t',encoding = 'utf-8')
  ```
  - 查看数据集数据
 
  ```python
  #查看前五行
  df.head()
  #查看尾五行
  df.tail()
  #查看随机一行
  df.sample()
  ```
 
    - 查看数据集信息
 
  ```python
  #查看数据集行数和列数
  df.shape
  #查看数据集信息（列名、数据类型、每列的数据量——可以看出数据缺失情况）
  df.info()
  #查看数据集基本统计信息
  df.describe()
  #查看数据集列名
  df.columns
  #查看数据集数据缺失情况 
  df.isnull().sum()
  #查看缺失列数据
  df[df['col_name'].isnull()]
  #查看数据集数据重复情况
  sum(df.duplicated())
  #查看重复数据
  df[df.duplicated()]
  #查看某列分类统计情况
  df['col_name'].value_counts()
  #查看某列唯一值
  df['col_name'].unique()
  #查看某列唯一值数量
  df['col_name'].nunique()
  #以某列对数据集进行排序
  df.sort_values(by = 'col_name',ascending = False)#False为由大至小
  ```
     - 数据筛选
 
  ```python
  #提取某行
  df.iloc[row_index]
  df.loc['row_name']
  #提取某几行
  df.iloc[row_index_1:row_index_2]
  #提取某列
  df['col_name']
  #提取某几列
  df[['col_name_1','col_name_2']]
  #提取某行某列的值
  df.iloc[row_index,col_index]
  df.loc['row_name','col_name']
  #筛选某列中满足某条件的数据
  df[df['col_name'] == value]#等于某值的数据，同理满足所有比较运算符
  df.query('col_name == value')#代码效果同上
  df[(df['col_name_1'] >= value_1) & (df['col_name_2'] != value_2)]#与&，或|
  df.query('(col_name_1 >= value_lower) & (col_name_2 <= value_upper)')
  df.groupby('col_name')#按col_name列进行分组，聚类
  ```
- 清理
 
  对评估出的问题进行逐项排查、清理，直至获取到干净的数据（推荐超级有用且经典的[Tidy Data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)，虽然代码用的是R语言，但代码不就只是工具而已嘛，关键的是**思维方法**）
 
  ```python
  #删除某行
  df.drop(['row_name'],inplace = True)#若添加inplace = True，修改后的数据会覆盖原始数据
  #删除某列
  df.drop(['col_name'],axis = 1)
  #缺失值的处理
  df.fillna(mean_value)#替换缺失值
  df.dropna()#删除包含缺失值的行
  df.dropna(axis = 1, how = 'all')#只删除所有数据缺失的列
  #删除重复值
  drop_duplicates(inplace = True)
  #更改某行/列/位置数据
  用iloc或者loc直接替换修改即可
  #更改数据类型
  df['datetime_col'] = pd.to_datetime(df['datetime_col'])
  df['col_name'].astype(str)#还可以是int/float...
  #更改列名
  df.rename(columns={'A':'a', 'C':'c'}, inplace = True)
  #apply函数
  #讲function应用在col_name列，此方法比用for循环快得多得多
  df['col_name'].apply(function)
  ```
  
#### 探索性数据分析
 
即Exploratory data analysis(EDA)，这是一种分析数据集——尤其是陌生数据集——的方法，具体实施的话可以采用定量、定性的数据分析或者是可视化分析。
 
这是一个强调**迭代**的过程，在这个阶段你要不断的对数据进行探索（提问、整理、分析、可视化等等），根据你得到的结果再去丰富你的数据或者完善你的问题，最终得出结论。
 
这是一个考验耐心和细心的繁琐过程，所以一定要**心平气和**，保持**工作的连贯性**。（~~不做完一套不能睡觉？~~）

在做EDA的过程中，一个很好的习惯就是备份！
```python
#导出csv文件
df.to_csv('filename.csv',index = False)
#导出中文字符的excel文件
df.to_excel('filename.xlsx',index = False,encoding = 'utf-8-sig')
```
 
> Tip:[utf-8与utf-8-sig 两种编码格式区别](https://blog.csdn.net/u012965373/article/details/52680787)
 
#### 得出结论
 
- 通过可视化展示结论
- 利用统计学指标，如假设检验的p-值等提供理论支撑
- 利用机器学习算法对数据进行预测、分类、关联度分析等
 
#### 传达结果
 
撰写报告，和别人分享你的研究结果。不管你报告的载体是PDF，PPT还是交互式的网页，都需要你凝练出最精简的点，一针见血。
> 所以，数据分析师们做的都是表面光鲜，背地里清理~~头发~~数据的工作。。。
 
 
### 延伸：数据融合
数据融合这部分，主要包括四个函数merge与join，concat与append，这里只展示基本用法与总结，更多实例可以戳(https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)
- merge
merge意为**合并**，当两个数据集需要按照某个共有列进行合并时，就需要用到merge了，它的关键参数为链接方式`how`，默认为内链接，大家可以类比SQL中的JOIN去学习
  > merge的连接方式与SQL对比
 
  > | 合并方式 | SQL JOIN           | 描述                    |
  > | -------- | ------------------ | ----------------------- |
  > | `left`   | `LEFT OUTER JOIN`  | 只用左表的key去匹配链接 |
  > | `right`  | `RIGHT OUTER JOIN` | 只用右表的key去匹配链接 |
  > | `outer`  | `FULL OUTER JOIN`  | 两表中key的并集         |
  > | `inner`  | `INNER JOIN`       | 两表中key的交集         |
  实例：
```
In [1]: left = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
   ....:                      'A': ['A0', 'A1', 'A2', 'A3'],
   ....:                      'B': ['B0', 'B1', 'B2', 'B3']})
   ....: 
 
In [2]: right = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
   ....:                       'C': ['C0', 'C1', 'C2', 'C3'],
   ....:                       'D': ['D0', 'D1', 'D2', 'D3']})
   ....: 
 
In [3]: result = pd.merge(left, right, on='key')
```
![_images/merging_merge_on_key.png](https://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key.png) 
- join
join是一种基于merge的快速合并方法，所需参数较少，默认以index作为链接键，进行左链接。
```
In [4]: left = pd.DataFrame({'A': ['A0', 'A1', 'A2'],
   ....:                      'B': ['B0', 'B1', 'B2']},
   ....:                      index=['K0', 'K1', 'K2'])
   ....: 
 
In [5]: right = pd.DataFrame({'C': ['C0', 'C2', 'C3'],
   ....:                       'D': ['D0', 'D2', 'D3']},
   ....:                       index=['K0', 'K2', 'K3'])
   ....: 
 
In [6]: result = left.join(right)
```
 
![_images/merging_join.png](https://pandas.pydata.org/pandas-docs/stable/_images/merging_join.png) 
- concat
concat是单词concatenate的简称，意为**拼接**，它是用来处理拼接多个具有相同列名或者索引的数据。
```
In [7]: df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
   ...:                     'B': ['B0', 'B1', 'B2', 'B3'],
   ...:                     'C': ['C0', 'C1', 'C2', 'C3'],
   ...:                     'D': ['D0', 'D1', 'D2', 'D3']},
   ...:                     index=[0, 1, 2, 3])
   ...: 

In [8]: df4 = pd.DataFrame({'B': ['B2', 'B3', 'B6', 'B7'],
   ...:                     'D': ['D2', 'D3', 'D6', 'D7'],
   ...:                     'F': ['F2', 'F3', 'F6', 'F7']},
   ...:                    index=[2, 3, 6, 7])
   ...: 

#关键参数axis，决定了拼接的方向，默认为拼接行（即向下拼接），axis=1时拼接列（即向右拼接）
In [9]: result = pd.concat([df1, df4], axis=1, sort=False)
```
![_images/merging_concat_axis1.png](https://pandas.pydata.org/pandas-docs/stable/_images/merging_concat_axis1.png)
- append
append时concat的简化函数，它只能拼接行，即向下拼接。
```
In [10]: df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
   ...:                     'B': ['B4', 'B5', 'B6', 'B7'],
   ...:                     'C': ['C4', 'C5', 'C6', 'C7'],
   ...:                     'D': ['D4', 'D5', 'D6', 'D7']},
   ...:                      index=[4, 5, 6, 7])
   ...: 
In [11]: result = df1.append(df2)
```
 
![_images/merging_append1.png](https://pandas.pydata.org/pandas-docs/stable/_images/merging_append1.png) 

- 总结
 
    - merge主要用来根据key列对数据集进行合并；
    - join相当于简化版的merge，key默认为index，所以你如果想按照index对数据集合并时，join就是你的首选；
    - 如果你想对数据集进行横向连接（axis = 1）或者纵向链接时，记得想起来用concat；
    - append相当于是简化版的concat，用得频次比concat要多得多。
    

 ## 最后
 本文依然只是Pandas的冰山一角，希望能引起你们的兴趣去积极探索，比如说更新数据时可以用到`update`或者`combine_first`函数，对数据进行reshape或者聚合的`stack`、`pivot`，对时间序列进行处理的`datetime`等等。大家也不要被这么多函数吓到，在学习或者工作的过程中，不断地去尝试新方法，多去翻Pandas的官方文档，多记笔记，相信你在数据科学的道路上肯定会越走越远哒！
