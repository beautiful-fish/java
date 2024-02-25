## java常用方法总结

#### 1.String类

- s.charAt(i);

- char[] chars = s.toCharArray();

- s.subString(left,right); //包含左边，不包含右边

- String str = s.join("xxx", a); //a可以是泛型为String的集合或者String数组或者多个字符串对象(之间用逗号隔开)，xxx经常是某个符号

  参数列表：
  　　1、表示连接的符号
  　　2、表示被连接的数组（也可以是集合），或者是要连接的多个字符串

- String[] str = s.split("xxx") //参数为传入字符类型的分隔符

- String str = new String(charArray,offset,count) //该方法为：public String(char value[], int offset, int count) 

  注：Integer.parseInt(String)方法，可以快捷的把String类型转为Integer类型

#### 2.StringBuffer

  StingBuffer ss = new StringBuffer();  

  StingBuffer ss = new StringBuffer(string);

- ss.append(); //增
- ss.chatAt(index);
- ss.deleteCharAt(i); //删
- ss.toString();
- ss.length() //求长度
- ss.reverse();
- ss.setChar(index,'char') //修改字符串中的index处的字符，并不影响其他字符
- ss.insert(index,"string") //插入
- ss.setLength(num) //重新设置StringBuffer的长度，也可设为0；

#### 3.List

- list.add(int index, E element) //增
- list.remove(int index) //删
- list.set(int index, E element) //改
- list.get(int index) //查
- String[] str = list.toArray(new String[0]) //list转为String数组
- Integer[] integers = list.toArray(new Integer[0]) //list转为int数组

**LinkedList 同时继承了List接口和Deque接口，所以它同时具有两个接口的方法**

**常见用法**

```java
List<List<Integer>> lists = new ArrayList<>(); 
for (int i = 0; i < num.length; i++) {
	lists.add(new ArrayList<>());
}
lists.get(index).add(xxx); //相当于在操作二维数组，但是要比操作数组要灵活


lists.add(new ArrayList<>(xxx)) //xxx可以为集合，例如deque
```

#### 4.Queue和Deque

###### Queue 单向队列

- queue.add() / queue.offer() // 1,2,3
- queue.remove() / queue.poll() // 2,3
- queue.elelment() / queue.peek() //返回队首元素的值    

###### Deque 双向队列

- deque.addFirst(value) / Deque.offerFirst(value)
- deque.addLast(value) / Deque.offerLast(value)
- deque.removeFirst() / Deque.pollFirst()
- deque.removeLast() / Deque.pollLast()
- deque.push(value)  // 模拟栈 push()相当于addFirst()
- deque.pop()   // 模拟栈 pop()相当于removeFirst()

#### 5.HashMap

- hashMap.get(key) //查
- hashMap.put(key, value) //可以用来增和改,强制改
- hashMap.putIfAbsent(key, value) //存在相应key则不改，不存在则加进去
- hashMap.put(key, hashMap.getOrDefault(key,默认值)+1) //适用于在value上+1的场景，getOrDefault(key,默认值)使用在返回value，但是不知道value是否是默认值还是之前保存过的其他值
- hashMap.remove() //删
- hashMap.containsKey()
- hashMap.containsValue()
- hashMap.keySet() 
- hashMap.entrySet() //推荐使用，常见格式为for(Map.Entry<x,x> entry: map.entryset()){}
- hashMap.size()
- hashMap.isEmpty()
- hashMap.clear() //清除所有元素

#### 6.Math

- Math.max()

- Math.max(Math.max(1,2),3) //用来比较三个数之间的最大值

- Math.min()

- Math.abs()

- Math.pow(10,i) //相当于10的i次方，i可以是具体的值，也可以当作变量

- Math.round()

  Case1：小数点后第一位 = 5
       正数：Math.round(11.5) = 12
       负数：Math.round(-11.5) = -11
  Case2：小数点后第一位 < 5
       正数：Math.round(11.49) = 11
       负数：Math.round(-11.49) = -11
  Case3：小数点后第一位 > 5
       正数：Math.round(11.69) = 12
       负数：Math.round(-11.69) = -12

#### 7.Arrays

- Arrays.fill(right, 1)  //给数组right的值都填充为1

- Arrays.sort(数组) //默认使数组升序排列

- Arrays.sort(数组，Comparator.reverseOrder()) //使数组降序排列

- Arrays.toString(数组)  //数组转字符串

- int[] newArray = Arrays.stream(array).filter(x -> x > 10).map(x -> x + 1).toArray() //流式操作比较灵活

  有distinct(), filter(), sort(), max(), min()等方法

- List<数组对应的类型> list = Arrays.asList(array) //数组转成list

#### 8.Scanner

Scanner in = new Scanner(System.in)

- in.nextInt()
- in.nextLine()
- in.next()
- in.hasNextInt()
- in.hasNextLine()
- in.hasNext()

#### 9.Set

- set.contains(obj)
- set.add(obj) //增
- set.remove(obj) //删
- set.isEmpty()
- set.size()
- set.clear() // 清空set
- 在set的构造器中可以直接传入list
- Integer[] nums = set.toArray(new Integer[0]) //set转换成对应类型的数组

#### 10.Integer

- int i = Integer.parseInt(string) // 字符串转数字
- Integer.MAX_VALUE
- Integer.MIN_VALUE

#### 11.iterator

java.util.iterator 接口 同时 Collection接口继承了java.lang.Iterable接口

增强for循环的原理是使用了iterator迭代器，并且使用增强for循环时不能修改集合元素的值。

因为next()中有一个checkForComodification()方法，这是实现迭代器中不能修改的关键。

```java
final void checkForComodification() {
	if (modCount != expectedModCount)
    	throw new ConcurrentModificationException();
}
```

- hasNext() 

- next() //从集合中取下一个值并返回

- remove() //从集合中删除相应的值

  

#### 12.CompletableFuture

- supplyAsync() // supplyAsync是创建带有返回值的异步任务

- runAsync() // runAsync是创建没有返回值的异步任务

- get() // 如果完成则返回结果，否则就抛出具体的异常

  

- thenApply() // 表示某个任务执行完成后执行的动作，即回调方法，会将该任务的执行结果即方法返回值作为入参传递到回调方法中，带有返回值，使用thenApply方法时子任务与父任务使用的是同一个线程

- thenApplyAsync() //thenApplyAsync在子任务中是另起一个线程执行任务，并且thenApplyAsync可以自定义线程池，默认的使用ForkJoinPool.commonPool()线程池。

- thenAccept() //thenAccep表示某个任务执行完成后执行的动作，即回调方法，会将该任务的执行结果即方法返回值作为入参传递到回调方法中，无返回值。

- thenAcceptAsync() //同上

- thenRun() // thenRun表示某个任务执行完成后执行的动作，即回调方法，无入参，无返回值

- thenRunAsync() //同上

- whenComplete() // whenComplete是当某个任务执行完成后执行的回调方法，会将执行结果或者执行期间抛出的异常传递给回调方法，如果是正常执行则异常为null，回调方法对应的CompletableFuture的result和该任务一致，如果该任务正常执行，则get方法返回执行结果，如果是执行异常，则get方法抛出异常。

- whenCompleteAsync() 

  

- thenCombine() //thenCombine会将两个任务的执行结果作为所提供函数的参数，且该方法有返回值

- thenCombineBoth() //thenAcceptBoth同样将两个任务的执行结果作为方法入参，但是无返回值

- runAfterBoth() //runAfterBoth没有入参，也没有返回值

- applyToEither() 

- accptEither() 

- runAfterEither()

  

- allOf()

- anyOf()

  

## Mysql常用方法     

- update 表名 **set** name='xxx',age='xxx' where name='xxx';

- insert **into** 表名 **values** ('liming','18'), ('danny','18');

- insert **into** 表名（name）**values** ('liming'),('danny');

- delete **from** 表名 where name = 'liming'; //删除表中指定数据

- select name, age from 表名 where name = 'xxx' //基础查询

- create table user (

  ​	id int not null auto_increment,

  ​	name varchar(255) not null,

  ​	money decimal default 0,

  ​	age int not null,

  ​	primary key('id'), //创建主键索引

  ​	unique uni_index_name(name), //创建唯一索引

  ​	index index_sex(sex)  //创建普通索引

  ​	index index_sex_name(sex,name) //创建组合索引

  ​	fulltext index_name(name) //创建全文索引

  ) 

- drop table user; //删除数据表

  

- alter table user **add** birthday varchar(20); //添加列

- alter table user **drop column** name; //删除列

- alter table user **modify column** age tinyint; //修改列

- create/drop database user; //创建或删除数据库

  **视图**

- **create view** top_10_user **as** select id ,name from user where id < 10;

- drop view top_10_user;

  **索引**

- create index(普通索引)/unique index(唯一索引)/fulltext index(全文索引) index_name on user(column name) //直接创建索引

- alter table user **add** index(普通索引)/unique(唯一索引)/fulltext(全文索引) index_name(column name) //修改表方式创建索引

- alter table user add primary key(id) //修改表方式创建**主键**索引

- show index/keys from 表名 //查看索引

  **注释**：全文索引fulltext，只能在char,varchar,text类型上创建并且一个表只能有一个全文索引
  
  **注释**：explain + select 查询语句 --> 可以查看该查询语句使用的索引和慢查询
  
  
  
  **慢查询**
  
  **使用慢查询日志，一般分为四步：**开启慢查询日志、设置慢查询阀值、确定慢查询日志路径、确定慢查询日志的文件名；
  
  set global slow_query_log = on;   # 开启慢查询日志
  set global long_query_time = 1;   # 设置慢查询阀值
  show global variables like "datadir";   # 确定慢查询日志路径
  show global variables like "slow_query_log_file";   # 确定慢查询日志的文件名

## ElasticSearch常用方法  

###### 创建索引

![image-20231031202852298](E:/typora/photo/image-20231031202852298.png)

![image-20231031171148655](E:/typora/photo/image-20231031171148655.png)

###### 1.查询所有的文档 query --> match_all

![image-20231031165643220](E:/typora/photo/image-20231031165643220.png)

###### 2.匹配查询 query --> match

###### 3.字段匹配查询 query --> multi_match

![image-20231031162604153](E:/typora/photo/image-20231031162604153.png)

###### 4.关键字精确查询 query --> term

![image-20231031162739778](E:/typora/photo/image-20231031162739778.png)

###### 5.多关键字精确查询 query --> terms

![image-20231031162839347](E:/typora/photo/image-20231031162839347.png)

###### 6.指定查询字段 _source

![image-20231031163032180](E:/typora/photo/image-20231031163032180.png)

###### 7.过滤字段

![image-20231031163116512](E:/typora/photo/image-20231031163116512.png)

###### 8.组合查询 query --> bool

![image-20231031163156737](E:/typora/photo/image-20231031163156737.png)

###### 9.范围查询 query --> range

![image-20231031163313970](E:/typora/photo/image-20231031163313970.png)

###### 10.模糊查询 query --> fuzzy

![image-20231031163417402](E:/typora/photo/image-20231031163417402.png)

###### 11.单字段排序 sort --> 字段名 --> order

![image-20231031163555134](E:/typora/photo/image-20231031163555134.png)

###### 12.多字段排序

![image-20231031163642556](E:/typora/photo/image-20231031163642556.png)

###### 13.高亮查询 highlight

###### ![image-20231031163745833](E:/typora/photo/image-20231031163745833.png)

###### 14.分页查询 from size

![image-20231031163845682](E:/typora/photo/image-20231031163845682.png)

###### 15.聚合查询 aggs

![image-20231031163950732](E:/typora/photo/image-20231031163950732.png)

对某个字段取最大值 max

![image-20231031164918547](E:/typora/photo/image-20231031164918547.png)

**注释：同理也可以求某个字段的 min, sum, avg**

 对某个字段的值**进行去重**之后再取总数

![image-20231031165105909](E:/typora/photo/image-20231031165105909.png)

state 聚合

![image-20231031165131777](E:/typora/photo/image-20231031165131777.png)

###### 16.桶聚合查询 aggs --> 别名 --> terms

在terms里面也可以写order排序

![image-20231031165254912](E:/typora/photo/image-20231031165254912.png)

 在 terms 分组下再进行聚合（ 多重aggs）

![image-20231031165426871](E:/typora/photo/image-20231031165426871.png)

## shell 

父shell和子shell

**系统全局变量**

$HOME 当前家目录

$PWD  当前的工作目录

$SHELL  当前使用的shell解析器

$USER  当前的用户

$PATH

等等。。。 可以用 env来查看全部的全局变量

**定义局部变量**

a=1 #注意等号两边不能有空格

word="hello"

echo $a

**定义全局变量**

export word #把word变量定义为全局变量 并且子shell对全局变量的更改对父shell是不可见的

**定义只读常量**

readonly b=5

**撤销变量**

unset word #不能unset只读变量

**特殊变量**

$n

```shell
用shell编程实现查找指定文本文件中出现频率最高的前10个单词

grep -oE/-n
grep [-acinv] '搜寻字符串' filename
1.-v 显示不被pattern匹配到的行
2.-i 忽略字符大小写
3.-n 显示行号
4.-c 统计匹配的行数
5.-o 仅显示匹配到的字符串
6.-E 使用ERE，相当于egrep 使用扩展正则

awk
格式
awk 'pattern + action' [FILE]
例如：awk -F ":" '{print $1"--"$2}' /etc/xxx   
常用参数
1.BEGIN 处理文本之前要执行的操作
2.END 处理文本之后要执行的操作
3.FS（field separator） 输入字段分隔符，默认空格，相当于-F
4.NF（number fields） 当前输入记录的字段数（列数）
5.NR（number records） 目前为止看到的记录总数（行数）
6.OFS 输出域分隔符（不常用）
7.ORS 输出记录分隔符（不常用）
8.RS（record separator） 输入记录分隔符，默认换行符
9.$0 整条记录
10.$1 表示当前行的第一个字段
练习1
1.搜索/etc/passwd有root关键字的所有行：awk -F: '/root/{print $0}' /etc/passwd
2.打印/etc/passwd的第2行信息：awk -F: 'NR==2{print $0}' /etc/passwd


sed
格式
sed [-hn..][-e<script>][-f<script FILE>][FILE]
命令解析
1.-h 显示帮助
2.-n 静默模式，仅显示script处理后的结果
3.-e<script> 以选项中指定的script来处理输入的文本文件
4.-f<script文件> 以选项中指定的script文件来处理输入的文本文件
常用命令
1.a：新增； sed -e '4a newline' ；在第4行后新增1行，内容为“newline”
2.c：取代；sed -e '2,5c number'；用“number”取代2到5行的内容
3.d：删除；sed -e '2,5d'；删除2到5行
4.i：插入；sed -e '2i newline'；在第2行前插入1行，内容为“newline”
5.p：打印；sed -n '/root/p'；打印与root匹配的行
6.s：取代；sed -e 's/old/new/g'；全局替换，若没有g则只替换每行的第一个
注：-e可省略

sort -nr
选项	说明
-b：忽略行首空格。
-d：按照字典序进行排序。
-f：忽略大小写。
-g：按照数值大小进行排序。
-i：忽略非打印字符。
-M：按照月份名称进行排序。
-n：按照数值大小进行排序。
-r：倒序排序。
-t：指定字段分隔符。
-k：指定排序字段。

uniq -c
选项	说明
-c：在每行前面显示该行在文件中出现的次数。
-d：仅显示重复的行。
-u：仅显示不重复的行。
-i：忽略大小写。
-f N：忽略前N个字段。
-s N：从第N个字符开始比较。
-w N：比较前N个字符

head
-q	隐藏文件名
-v	显示文件名
-c<字节>	显示字节数
-n<行数>	显示的行数

tail
-f	循环读取
-q	不显示处理信息
-v	显示详细的处理信息
-c<字节>	显示的字节数
-n<行数>	显示行数

find
语法：find [path...] [expression]
-name
-type
-size 
-time
 根据时间戳查找：
       以天为单位(time)：访问时间
           -atime [+|-]#
               +: 表示（#+1）天之外被访问过；
               -: 表示#天之内被访问过；
               无符号：表示短于（#+1）> x >=#天的时间段被访问过；    
           -mtime:修改时间
           -ctime:创建时间

       以分钟为单位(min)：
           -amin [+|-]#:访问时间
           -mmin:修改时间
           -cmin:创建时间


cut
cut -x xxx 文件名
截取文本和awk类似，但是awk更加灵活
-b 选择第几个字节并将其输出
-c 选择第几个字符并将其输出
-d 指定分隔符 例如 -d " "
-f 指定满足条件的第几个
例如：cut -d " " -f 1,2 xxx.txt  打印出前两个单词

#!/bin/bash

# 指定要查找的文本文件
text_file="example.txt"

# 使用grep命令过滤出所有单词，并统计每个单词的出现次数
word_counts=$(grep -oE '\w+' "$text_file" | sort | uniq -c)

# 找出出现次数最高的前10个单词
most_frequent_words=$(echo "$word_counts" | sort -nr | head -n10)

# 输出结果
echo "出现频率最高的前10个单词是："
echo "$most_frequent_words"
```



## 测试开发

**测试用例设计： 等价类，边界值** ...

1、场景法：用户可能执行的操作 每个点击按钮 

2、流程去考虑：登录、验证码登录、密码登录、登录成功、登录失败 

   按照用户输入内容的要求，测边界值，少做等价测试。

3、非功能测试的场景：

​	网络场景：没网，弱网，不同的网络场景4G/wifi的提示信息

​	兼容性: 不同手机的兼容性情况，每个手机的屏幕大小不一样，前端显示页面能够自适应

​	接口： 通过抓包（charles）查看返回是否正常，涉及手机号、钱、验证码接口是否加密等

​	数据校验：查看数据库是否按逻辑增加或减少，如何有事务的话，看数据库能否正常回滚（其中会用到sql语句）

​	UI：是否美观，是否和设计一致

​	权限：麦克风，摄像头权限等等

​	启动：热启动，冷启动，后台



​	压力测试：对某个接口进行压测 jmeter 

​			测试指标：RT(响应时间)，RPS(吞吐量和并发数有关)，TPS,QPS，错误率

​	安全测试：对输入框的SQL注入攻击，XSS跨站脚本攻击进行测试

4、业务上的（验证码有效时间、使用次数、一天内收验证码的次数）



**测试题目：1对1发红包**

功能测试： 点击红包按钮是否正常

​		 输入框 输入金额是否正常

​	     对方是否能正常接收红包

非功能测试：网络场景

​		  兼容性 

​		  接口 

​		  数据校验

​		  UI

​		  权限

​		  启动

测试用例自动化(pytest框架 用到python语言)

