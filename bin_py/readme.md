## Python使用记录

自安装python软件包在该目录下：
```bash
python2.7/lib/python2.7/site-packages/
```

***

``` python code
# 对字典元素进行排序
dic = {'a':31, 'bc':5, 'c':3, 'asd':4, 'aa':74, 'd':0}
dict= sorted(dic.iteritems(), key=lambda d:d[1], reverse = True)
print dict
```

***

#### 常用工具
##### > tensorflow
###### 基本元素

```python
"""
tf中的数据被称为张量tensor，tensor在图间流动，先构造图在执行。
通过会话Sesson.run执行图流程
"""
import tensorflow as tf
a = tf.contant(2)  # 常量
a = tf.contant(2)  # 常量
s = tf.Session()  # 会话
c = tf.placeholder(tf.int16)  # 变量 使用的时候填充
with tf.Session() as sess:
    result = sess.run(a+b)
    print(result)
```

```python
import tensorflow as tf
tf.__version__  # 查看版本
tf.__path__  # 安装路径
```

***遇到的问题***

1. 引入seq2seq网络，不同版本的不同方法

```
# 老版本
from tensorflow.python.ops import seq2seq
tensorflow.unpack()
# v1.3.0版本
from tensorflow.contrib.legacy_seq2seq.python.ops import seq2seq
tensorflow.unstack()
```


##### > numpy

>以下仅为在工作中常用到的一些函数和用法

```python
# list类型转换为numpy
n = numpy.array(list([1, 2, 3, 4]))

# 初始化空数组
y = np.empty(data_tensor.shape, dtype=data_tensor.dtype)

# 得到矩阵的纬度信息，x y z ... 轴的纬度
n.shape
n.reshape(a, newshape, order='C')  # ?

# numpy.array保存到文件 和从文件中加载
n.save(file)
m = n.load(file)
m.size
m.sum() # 求和计算

# list转换为numpy二维数组
v = [1,2,3,4,5]
nv = numpy.array(v, dtype=numpy.float64)

vv = [[1,2,3], [2,3,4], [3,4,5]]
nv = numpy.array(vv, dtype=numpy.float64)
```


***
#### python内建类或函数
##### > re

``` python
# 对cont按""中的各个字符进行分割
re.split(",|.|!|?", cont)
```

##### > argparse

```python
def get_args():
    """
    参数处理类 示例用法
    """
    parser = argparse.ArgumentParser()
    parser.add_argument('--data_dir', type=str,
        default='preprocessed', 
        help="directory with processed data")
    args = parser.parse_args()
    return args
```

##### > enumerate

```python
# 第二个参数控制索引的下标起始地址
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1, 1):
    print index, item
>>>
1 这
2 是
3 一个
4 测试
```

##### > map

```python
# vocab字典，通过map得到字段的value值
map(vocab.get, ['y', 't'])
# 第一个参数为函数，第二个参数为依次传入第一个参数的数值，结果有map返回，为list类型
```

##### > collections

以下几个函数常被用到：
```python
deque # 双向队列，可以从头尾插入弹出元素
Counter # 对字符串或者list中的元素进行计数
OrderedDict # 对字典自动按key进行排序
defaultdict # 可以设置默认value值的字典
```

##### > pickle

```python
dump # 可以将对象序列化写入
loads # 序列化加载
```

```python
from six.moves import cPickle as pickle
import cPickle
with open(vocab_file, 'wb') as f:
    pickle.dump(vocab, f)
```

##### > codecs

读写文件时指定编码格式
```
with codecs.open(args.input_file, 'r', encoding='utf-8') as f:
    data = f.read()
```

***

#### >logging

``` 
import logging
logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
# 屏幕上打印:
# WARNING:root:This is warning message
```


```
import logging
logging.basicConfig(level=logging.DEBUG,
                format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                datefmt='%a, %d %b %Y %H:%M:%S',
                filename='myapp.log',
                filemode='w')
logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')

```

##### >re
```
import re
r = re.compile("^select ([a-zA-Z]*) from ([a-zA-Z]*) secom")
a = r.match("select name from table secom")
print a.group(0), a.group(1), a.group(2)
----
select name from table secom
name
tabe 
```

``` cpp
#include <boost/algorithm/string.hpp>
vector<string> vec_num;
boost::split(vec_num, number_text, boost::is_any_of(" "));    // 分割字符串放到vec中

boost::regex phone_reg = "(^|[^0-9])((\\(\\d{3,4}\\)|\\d{3,4}-|\\s)?\\d{7,8})([^0-9]|$)";
boost::smatch mat;
boost::regex_search(begin, end, mat, phone_reg)； // 从begin与end指向的字符串中匹配phone_reg，匹配结果到mat中
// mat[0]指向整个字符串，mat[i]知晓第i个匹配模式（每个括号为一个匹配模式）
```


##### >中文可视化输出到文件
```
# json中unicode编码，格式化输出中文可显写入文件
s = json.dumps(x, indent = 4, ensure_ascii=False)
s = s.encode('utf-8')
filename = 'data/%s_%s.json' %(pref, taskid)
with open(filename, 'w') as f:
    json.dump(x, f, indent=4, ensure_ascii=False)
```



