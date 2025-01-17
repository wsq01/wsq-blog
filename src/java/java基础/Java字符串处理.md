



# 定义字符串
Java 没有内置的字符串类型，而是在标准 Java 类库中提供了一个`String`类来创建和操作字符串。

定义一个字符串最简单的方法是用双引号把它包围起来。这种用双引号括起来的一串字符实际上都是`String`对象，如字符串`“Hello”`在编译后即成为`String`对象。因此也可以通过创建`String`类的实例来定义字符串。

不论使用哪种形式创建字符串，字符串对象一旦被创建，其值是不能改变的，但可以使用其他变量重新赋值的方式进行更改。
## 直接定义字符串
直接定义字符串是指使用双引号表示字符串中的内容。
```java
String str = "Hello Java";
```
注意：字符串变量必须经过初始化才能使用。
## 使用 String 类定义
在 Java 中每个双引号定义的字符串都是一个`String`类的对象。因此，可以通过使用`String`类的构造方法来创建字符串，该类位于`java.lang`包中。

`String`类的构造方法有多种重载形式，每种形式都可以定义字符串。
1. `String()`
	 初始化一个新创建的`String`对象，表示一个空字符序列。
2. `String(String original)`
	 初始化一个新创建的`String`对象，使其表示一个与参数相同的字符序列。换句话说，新创建的字符串是该参数字符串的副本。
```java
String str1 = new String("Hello Java");
String str2 = new String(str1);
```
这里`str1`和`str2`的值是相等的。
3. `String(char[] value)`
	 分配一个新的字符串，将参数中的字符数组元素全部变为字符串。该字符数组的内容已被复制，后续对字符数组的修改不会影响新创建的字符串。
```java
char a[] = {'H','e','l','l','0'};
String sChar = new String(a);
a[1] = 's';
```
上述`sChar`变量的值是字符串`"Hello"`。 即使在创建字符串之后，对`a`数组中的第 2 个元素进行了修改，但未影响`sChar`的值。
4. `String(char[] value,int offset,int count)`
	 分配一个新的`String`，它包含来自该字符数组参数一个子数组的字符。`offset`参数是子数组第一个字符的索引，`count`参数指定子数组的长度。该子数组的内容已被赋值，后续对字符数组的修改不会影响新创建的字符串。
```java
char a[]={'H','e','l','l','o'};
String sChar=new String(a,1,4);
a[1]='s';
```
上述`sChar`变量的值是字符串`"ello"`。该构造方法使用字符数组中的部分连续元素来创建字符串对象。

# String和int的相互转换
## String转换为int
`String`字符串转整型`int`有两种方式：
* `Integer.parseInt(str)`
* `Integer.valueOf(str).intValue()`

```java
public static void main(String[] args) {
  String str = "123";
  int n = 0;
  // 第一种转换方法：Integer.parseInt(str)
  n = Integer.parseInt(str);
  System.out.println("Integer.parseInt(str) : " + n);
  // 第二种转换方法：Integer.valueOf(str).intValue()
  n = 0;
  n = Integer.valueOf(str).intValue();
  System.out.println("Integer.parseInt(str) : " + n);
}
//输出结果为：
//Integer.parseInt(str) : 123
//Integer.parseInt(str) : 123
```
在`String`转换`int`时，`String`的值一定是整数，否则会报数字转换异常（`java.lang.NumberFormatException`）。
## int转换为String
整型`int`转`String`字符串类型有 3 种方法：
* `String s = String.valueOf(i);`
* `String s = Integer.toString(i);`
* `String s = "" + i;`

使用第三种方法相对第一第二种耗时比较大。在使用第一种`valueOf()`方法时，注意`valueOf`括号中的值不能为空，否则会报空指针异常（`NullPointerException`）。
## valueOf() 、parse()和toString()
### valueOf()
`valueOf()`方法将数据的内部格式转换为可读的形式。它是一种静态方法，对于所有 Java 内置的类型，在字符串内被重载，以便每一种类型都能被转换成字符串。`valueOf()`方法还被类型`Object`重载，所以创建的任何形式类的对象也可被用作一个参数。这里是它的几种形式：
```java
static String valueOf(double num)
static String valueOf(long num)
static String valueOf(Object ob)
static String valueOf(char chars[])
```
调用`valueOf()`方法可以得到其他类型数据的字符串形式——例如在进行连接操作时。对各种数据类型，可以直接调用这种方法得到合理的字符串形式。所有的简单类型数据转换成相应于它们的普通字符串形式。任何传递给`valueOf()`方法的对象都将返回对象的`toString()`方法调用的结果。事实上，也可以通过直接调用`toString()`方法而得到相同的结果。

对大多数数组，`valueOf()`方法返回一个相当晦涩的字符串，这说明它是一个某种类型的数组。然而对于字符数组，它创建一个包含了字符数组中的字符的字符串对象。`valueOf()`方法有一种特定形式允许指定字符数组的一个子集。

它具有如下的一般形式：
```java
static String valueOf(char chars[], int startIndex, int numChars)
```
这里`chars`是存放字符的数组，`startIndex`是字符数组中期望得到的子字符串的首字符下标，`numChars`指定子字符串的长度。
### parse()
`parseXxx(String)`这种形式，是指把字符串转换为数值型，其中`Xxx`对应不同的数据类型，然后转换为`Xxx`指定的类型。
### toString()
`toString()`可以把一个引用类型转换为`String`字符串类型，是 sun 公司开发 Java 的时候为了方便所有类的字符串操作而特意加入的一个方法。
# 字符串拼接
`String`字符串虽然是不可变字符串，但也可以进行拼接只是会产生一个新的对象。`String`字符串拼接可以使用“+”运算符或`String`的`concat(String str)`方法。“+”运算符优势是可以连接任何类型数据拼接成为字符串，而`concat`方法只能拼接`String`类型字符串。
## 使用连接运算符“+”
Java 语言允许使用“+”号连接（拼接）两个字符串。在使用“+”运算符连接字符串和`int`型（或`double`型）数据时，“+”将`int`（或`double`）型数据自动转换成`String`类型。

只要“+”运算符的一个操作数是字符串，编译器就会将另一个操作数转换成字符串形式，所以应该谨慎地将其他数据类型与字符串相连，以免出现意想不到的结果。
## 使用 concat() 方法
`String`类的`concat()`方法实现了将一个字符串连接到另一个字符串的后面。
```
字符串 1.concat(字符串 2);
```
执行结果是字符串 2 被连接到字符串 1 后面，形成新的字符串。

`concat()`方法一次只能连接两个字符串，如果需要连接多个字符串，需要调用多次`concat()`方法。
# 获取字符串长度
要获取字符串的长度，可以使用`String`类的`length()`方法。
```
字符串名.length();
```
# 字符串大小写转换
`String`类的`toLowerCase()`方法可以将字符串中的所有字符全部转换成小写，而非字母的字符不受影响。
```
字符串名.toLowerCase()    // 将字符串中的字母全部转换为小写，非字母不受影响
```
`toUpperCase()`则将字符串中的所有字符全部转换成大写，而非字母的字符不受影响。
```
字符串名.toUpperCase()    // 将字符串中的字母全部转换为大写，非字母不受影响
```
```java
String str="abcdef 我 ghijklmn";
System.out.println(str.toLowerCase());    // 输出：abcdef 我 ghijklmn
System.out.println(str.toUpperCase());    // 输出：ABCDEF 我 GHIJKLMN
```
# 去除字符串中的空格
`String`类的`trim()`方法能去掉字符串中的首尾空格。
```
字符串名.trim()
```
```java
String str = " hello ";
System.out.println(str.length());    // 输出 7
System.out.println(str.trim().length());    // 输出 5
```
从该示例中可以看出，字符串中的每个空格占一个位置，直接影响了计算字符串的长度。

如果不确定要操作的字符串首尾是否有空格，最好在操作之前调用该字符串的`trim()`方法去除首尾空格，然后再对其进行操作。

注意：`trim()`只能去掉字符串中前后的半角空格（英文空格），而无法去掉全角空格（中文空格）。可用以下代码将全角空格替换为半角空格再进行操作。
```java
str = str.replace((char) 12288, ' ');    // 将中文空格替换为英文空格
str = str.trim();
```
其中，12288 是中文全角空格的`unicode`编码。
# 截取（提取）子字符串
在`String`中提供了两个截取字符串的方法，一个是从指定位置截取到字符串结尾，另一个是截取指定范围的内容。
## 1. substring(int beginIndex) 形式
此方式用于提取从索引位置开始至结尾处的字符串部分。调用时，括号中是需要提取字符串的开始位置，方法的返回值是提取的字符串。
```java
String str = "我爱 Java 编程";
String result = str.substring(3);
System.out.println(result);    // 输出：Java 编程
```
## 2. substring(int beginIndex，int endIndex) 形式
`beginIndex`表示截取的起始索引，截取的字符串中包括起始索引对应的字符；`endIndex`表示结束索引，截取的字符串中不包括结束索引对应的字符，如果不指定`endIndex`，则表示截取到目标字符串末尾。该方法用于提取位置`beginIndex`和位置`endIndex`位置之间的字符串部分。

注意：`substring()`方法是按字符截取，而不是按字节截取。
# 分割字符串
`String`类的`split()`方法可以按指定的分割符对目标字符串进行分割，分割后的内容存放在字符串数组中。该方法主要有如下两种重载形式：
```java
str.split(String sign)
str.split(String sign,int limit)
```
其中它们的含义如下：
* `str`为需要分割的目标字符串。
* `sign`为指定的分割符，可以是任意字符串。
* `limit`表示分割后生成的字符串的限制个数，如果不指定，则表示不限制，直到将整个目标字符串完全分割为止。

使用分隔符注意如下：

1）“.”和“|”都是转义字符，必须得加“\\\\”。
如果用“.”作为分隔的话，必须写成`String.split("\\.")`，这样才能正确的分隔开，不能用`String.split(".")`。
如果用“|”作为分隔的话，必须写成`String.split("\\|")`，这样才能正确的分隔开，不能用`String.split("|")`。

2）如果在一个字符串中有多个分隔符，可以用“|”作为连字符，比如：`“acount=? and uu =? or n=?”`，把三个都分隔出来，可以用`String.split("and|or")`。
# 字符串的替换
`String`类提供了 3 种字符串替换方法，分别是`replace()、replaceFirst()`和`replaceAll()`。
## replace() 方法
`replace()`方法用于将目标字符串中的指定字符（串）替换成新的字符（串）。
```
字符串.replace(String oldChar, String newChar)
```
其中，`oldChar`表示被替换的字符串；`newChar`表示用于替换的字符串。`replace()`方法会将字符串中所有`oldChar`替换成`newChar`。
## replaceFirst() 方法
`replaceFirst()`方法用于将目标字符串中匹配某正则表达式的第一个子字符串替换成新的字符串。
```
字符串.replaceFirst(String regex, String replacement)
```
其中，`regex`表示正则表达式；`replacement`表示用于替换的字符串。
```java
String words = "hello java，hello php";
String newStr = words.replaceFirst("hello","你好 ");
System.out.println(newStr);    // 输出：你好 java,hello php
```
## replaceAll() 方法
`replaceAll()`方法用于将目标字符串中匹配某正则表达式的所有子字符串替换成新的字符串。
```
字符串.replaceAll(String regex, String replacement)
```
其中，`regex`表示正则表达式，`replacement`表示用于替换的字符串。
```java
String words = "hello java，hello php";
String newStr = words.replaceAll("hello","你好 ");
System.out.println(newStr);    // 输出：你好 java,你好 php

public static void main(String[] args) {
    // 定义原始字符串
    String intro = "今天时星其天，外面时下雨天。妈米去买菜了，漏网在家写作业。" + "语文作业时”其”写 5 行，数学使第 10 页。";
    // 将文本中的所有"时"和"使"都替换为"是"
    String newStrFirst = intro.replaceAll("[时使]", "是");
    // 将文本中的所有"妈米"改为"妈妈"
    String newStrSecond = newStrFirst.replaceAll("妈米", "妈妈");
    // 将文本中的所有"漏网"改为"留我"
    String newStrThird = newStrSecond.replaceAll("漏网", "留我");
    // 将文本中第一次出现的"其"改为"期"
    String newStrFourth = newStrThird.replaceFirst("[其]", "期");
    // 输出最终字符串
    System.out.println(newStrFourth);
}
```
运行该程序，输出的正确字符串内容如下：
```
今天是星期天，外面是下雨天。妈妈去买菜了，留我在家写作业。语文作业是”其”写 5 行，数学是第 10 页。
```
# 字符串比较
比较字符串的常用方法有 3 个：`equals()`、`equalsIgnoreCase()`、`compareTo()`。
## equals() 方法
`equals()`方法将逐个地比较两个字符串的每个字符是否相同。如果两个字符串具有相同的字符和长度，它返回`true`，否则返回`false`。对于字符的大小写，也在检查的范围之内。
```java
str1.equals(str2);
```
`str1`和`str2`可以是字符串变量，也可以是字符串字面量。例如，下列表达式是合法的：
```java
"Hello".equals(greeting)
```
```java
String str1 = "abc";
String str2 = new String("abc");
String str3 = "ABC";
System.out.println(str1.equals(str2)); // 输出 true
System.out.println(str1.equals(str3)); // 输出 false
```
## equalsIgnoreCase() 方法
`equalsIgnoreCase()`方法的作用和语法与`equals()`方法完全相同，唯一不同的是`equalsIgnoreCase()`比较时不区分大小写。当比较两个字符串时，它会认为`A-Z`和`a-z`是一样的。
```java
String str1 = "abc";
String str2 = "ABC";
System.out.println(str1.equalsIgnoreCase(str2));    // 输出 true
```
## equals()与==的比较
`equals()`方法比较字符串对象中的字符。而==运算符比较两个对象引用看它们是否引用相同的实例。
```java
String s1 = "Hello";
String s2 = new String(s1);
System.out.println(s1.equals(s2)); // 输出true
System.out.println(s1 == s2); // 输出false
```
变量`s1`指向由`Hello`创建的字符串实例。`s2`所指的的对象是以`s1`作为初始化而创建的。因此这两个字符串对象的内容是一样的。但它们是不同的对象，这就意味着`s1`和`s2`没有指向同一的对象，因此它们是不`==`的。

因此，千万不要使用`==`运算符测试字符串的相等性，以免在程序中出现糟糕的 bug。从表面上看，这种 bug 很像随机产生的间歇性错误。
## compareTo() 方法
通常，仅仅知道两个字符串是否相同是不够的。对于排序应用来说，必须知道一个字符串是大于、等于还是小于另一个。一个字符串小于另一个指的是它在字典中先出现。而一个字符串大于另一个指的是它在字典中后出现。字符串（`String`）的`compareTo()`方法实现了这种功能。

`compareTo()`方法用于按字典顺序比较两个字符串的大小，该比较是基于字符串各个字符的 Unicode 值。
```java
str.compareTo(String otherstr);
```
它会按字典顺序将`str`表示的字符序列与`otherstr`参数表示的字符序列进行比较。如果按字典顺序`str`位于`otherster`参数之前，比较结果为一个负整数；如果`str`位于`otherstr`之后，比较结果为一个正整数；如果两个字符串相等，则结果为 0。

提示：如果两个字符串调用`equals()`方法返回`true`，那么调用`compareTo()`方法会返回 0。
```java
public static void main(String[] args) {
    String str = "A";
    String str1 = "a";
    System.out.println("str=" + str);
    System.out.println("str1=" + str1);
    System.out.println("str.compareTo(str1)的结果是：" + str.compareTo(str1));
    System.out.println("str1.compareTo(str)的结果是：" + str1.compareTo(str));
    System.out.println("str1.compareTo('a')的结果是：" + str1.compareTo("a"));
}
```
运行后的输出结果如下：
```
str = A
str1 = a
str.compareTo(str1)的结果是：-32
str1.compareTo(str)的结果是：32
str1.compareTo('a')的结果是：0
```
# 字符串查找
在给定的字符串中查找字符或字符串是比较常见的操作。字符串查找分为两种形式：一种是在字符串中获取匹配字符（串）的索引值，另一种是在字符串中获取指定索引位置的字符。
## 根据字符查找
`String`类的`indexOf()`方法和`lastlndexOf()`方法用于在字符串中获取匹配字符（串）的索引值。
### 1. indexOf() 方法
`indexOf()`方法用于返回字符（串）在指定字符串中首次出现的索引位置，如果能找到，则返回索引值，否则返回 -1。该方法主要有两种重载形式：
```java
str.indexOf(value)
str.indexOf(value,int fromIndex)
```
其中，`str`表示指定字符串；`value`表示待查找的字符（串）；`fromIndex`表示查找时的起始索引，如果不指定`fromIndex`，则默认从指定字符串中的开始位置（即`fromIndex`默认为 0）开始查找。
```java
String s = "Hello Java";
int size = s.indexOf('v');    // size的结果为8
```
### 2. lastlndexOf() 方法
`lastIndexOf()`方法用于返回字符（串）在指定字符串中最后一次出现的索引位置，如果能找到则返回索引值，否则返回 -1。该方法也有两种重载形式：
```java
str.lastIndexOf(value)
str.lastlndexOf(value, int fromIndex)
```
注意：`lastIndexOf()`方法的查找策略是从右往左查找，如果不指定起始索引，则默认从字符串的末尾开始查找。
## 根据索引查找
`String`类的`charAt()`方法可以在字符串内根据指定的索引查找字符。
```
字符串名.charAt(索引值)
```
提示：字符串本质上是字符数组，因此它也有索引，索引从零开始。
```java
String words = "today,monday,sunday";
System.out.println(words.charAt(0));    // 结果：t
System.out.println(words.charAt(1));    // 结果：o
System.out.println(words.charAt(8));    // 结果：n
```
# StringBuffer类
在 Java 中，除了通过`String`类创建和处理字符串之外，还可以使用`StringBuffer`类来处理字符串。`StringBuffer`类可以比`String`类更高效地处理字符串。

因为`StringBuffer`类是可变字符串类，创建`StringBuffer`类的对象后可以随意修改字符串的内容。每个`StringBuffer`类的对象都能够存储指定容量的字符串，如果字符串的长度超过了`StringBuffer`类对象的容量，则该对象的容量会自动扩大。
## 创建 StringBuffer 类
`StringBuffer`类提供了 3 个构造方法来创建一个字符串：
* `StringBuffer()`构造一个空的字符串缓冲区，并且初始化为 16 个字符的容量。
* `StringBuffer(int length)`创建一个空的字符串缓冲区，并且初始化为指定长度`length`的容量。
* `StringBuffer(String str)`创建一个字符串缓冲区，并将其内容初始化为指定的字符串内容`str`，字符串缓冲区的初始容量为 16 加上字符串`str`的长度。

```java
// 定义一个空的字符串缓冲区，含有16个字符的容量
StringBuffer str1 = new StringBuffer();
// 定义一个含有10个字符容量的字符串缓冲区
StringBuffer str2 = new StringBuffer(10);
// 定义一个含有(16+4)的字符串缓冲区，"青春无悔"为4个字符
StringBuffer str3 = new StringBuffer("青春无悔");
/*
*输出字符串的容量大小
*capacity()方法返回字符串的容量大小
*/
System.out.println(str1.capacity());    // 输出 16
System.out.println(str2.capacity());    // 输出 10
System.out.println(str3.capacity());    // 输出 20
```
## 追加字符串
`StringBuffer`类的`append()`方法用于向原有`StringBuffer`对象中追加字符串。
```
对象.append(String str)
```
该方法的作用是追加内容到当前`StringBuffer`对象的末尾，类似于字符串的连接。调用该方法以后，`StringBuffer`对象的内容也发生了改变。
```java
StringBuffer buffer = new StringBuffer("hello,");    // 创建一个 StringBuffer 对象
String str = "World!";
buffer.append(str);    // 向 StringBuffer 对象追加 str 字符串
System.out.println(buffer.substring(0));    // 输出：Hello,World!
```
## 替换字符
`StringBuffer`类的`setCharAt()`方法用于在字符串的指定索引位置替换一个字符。
```
StringBuffer 对象.setCharAt(int index, char ch);
```
该方法的作用是修改对象中索引值为`index`位置的字符为新的字符`ch`：
```java
StringBuffer sb = new StringBuffer("hello");
sb.setCharAt(1,'E');
System.out.println(sb);    // 输出：hEllo
sb.setCharAt(0,'H');
System.out.println(sb);    // 输出：HEllo
sb.setCharAt(2,'p');
System.out.println(sb);    // 输出：HEplo
```
## 反转字符串
`StringBuffer`类中的`reverse()`方法用于将字符串序列用其反转的形式取代。
```
StringBuffer 对象.reverse();
```
```java
StringBuffer sb = new StringBuffer("java");
sb.reverse();
System.out.println(sb);    // 输出：avaj
```
## 删除字符串
`StringBuffer`类提供了`deleteCharAt()`和`delete()`两个删除字符串的方法。
1. `deleteCharAt()`方法
	 `deleteCharAt()`方法用于移除序列中指定位置的字符。
```
StringBuffer 对象.deleteCharAt(int index);
```
`deleteCharAt()`方法的作用是删除指定位置的字符，然后将剩余的内容形成一个新的字符串。
```java
StringBuffer sb = new StringBuffer("She");
sb.deleteCharAt(2);
System.out.println(sb);    // 输出：Sh
```
2. `delete()`方法
	 `delete()`方法用于移除序列中子字符串的字符。
```
StringBuffer 对象.delete(int start,int end);
```
其中，`start`表示要删除字符的起始索引值（包括索引值所对应的字符），`end`表示要删除字符串的结束索引值（不包括索引值所对应的字符）。该方法的作用是删除指定区域以内的所有字符。
```java
StringBuffer sb = new StringBuffer("hello jack");
sb.delete(2,5);
System.out.println(sb);    // 输出：he jack
sb.delete(2,5);
System.out.println(sb);    // 输出：heck
```

# String、StringBuffer和StringBuilder类的区别
在 Java 中字符串属于对象，Java 提供了`String`类来创建和操作字符串。`String`类是不可变类，即一旦一个`String`对象被创建以后，包含在这个对象中的字符序列是不可改变的，直至这个对象被销毁。

Java 提供了两个可变字符串类`StringBuffer`和`StringBuilder`，中文翻译为“字符串缓冲区”。

`StringBuilder`类也代表可变字符串对象。实际上，`StringBuilder`和`StringBuffer`功能基本相似，方法也差不多。不同的是，`StringBuffer`是线程安全的，而`StringBuilder`则没有实现线程安全功能，所以性能略高。因此在通常情况下，如果需要创建一个内容可变的字符串对象，则应该优先考虑使用`StringBuilder`类。

`StringBuffer、StringBuilder、String`中都实现了`CharSequence`接口。`CharSequence`是一个定义字符串操作的接口，它只包括`length()、charAt(int index)、subSequence(int start, int end)`这几个 API。

`StringBuffer、StringBuilder、String`对`CharSequence`接口的实现过程不一样：

![对CharSequence接口的实现](Java字符串处理/1.png)

## 总结
`String`是 Java 中基础且重要的类，被声明为`final class`，是不可变字符串。因为它的不可变性，所以拼接字符串时候会产生很多无用的中间对象，如果频繁的进行这样的操作对性能有所影响。

`StringBuffer`就是为了解决大量拼接字符串时产生很多中间对象问题而提供的一个类。它提供了`append`和`add`方法，可以将字符串添加到已有序列的末尾或指定位置，它的本质是一个线程安全的可修改的字符序列。

在很多情况下我们的字符串拼接操作不需要线程安全，所以`StringBuilder`登场了。`StringBuilder`和`StringBuffer`本质上没什么区别，就是去掉了保证线程安全的那部分，减少了开销。

线程安全：
* `StringBuffer`：线程安全
* `StringBuilder`：线程不安全

速度：
一般情况下，速度从快到慢为`StringBuilder > StringBuffer > String`，当然这是相对的，不是绝对的。

使用环境：
* 操作少量的数据使用`String`。
* 单线程操作大量数据使用`StringBuilder`。
* 多线程操作大量数据使用`StringBuffer`。
