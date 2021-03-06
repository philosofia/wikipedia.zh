> 本文内容由[PL-SQL](https://zh.wikipedia.org/wiki/PL-SQL)转换而来。


**PL/SQL**（Procedural Language/SQL）是[甲骨文公司](../Page/甲骨文公司.md "wikilink")專有的[SQL](../Page/SQL.md "wikilink")擴展語言，應用在[甲骨文公司](../Page/甲骨文公司.md "wikilink")的[Oracle](https://zh.wikipedia.org/wiki/Oracle "wikilink")[数据库系統](https://zh.wikipedia.org/wiki/数据库系統 "wikilink")。一些的[SQL](../Page/SQL.md "wikilink")[数据库管理系統也提供了類似的](https://zh.wikipedia.org/wiki/数据库管理系統 "wikilink")[擴展SQL語言](https://zh.wikipedia.org/wiki/擴展SQL語言 "wikilink")。PL/SQL的的[語法非常類似於](https://zh.wikipedia.org/wiki/語法 "wikilink")[Ada](../Page/Ada.md "wikilink")，而且像1980年代的[Ada](../Page/Ada.md "wikilink")編譯器一樣，PL/SQL的運作系統使用[Diana作為](https://zh.wikipedia.org/wiki/Diana "wikilink")[中介語言](https://zh.wikipedia.org/wiki/中介語言 "wikilink")。

重要的是PL/SQL緊密的結合在[Oracle数据库裡面](https://zh.wikipedia.org/wiki/Oracle "wikilink")。

PL/SQL是[Oracle數據庫使用的三種語言的其中之一](https://zh.wikipedia.org/wiki/Oracle "wikilink")，另外兩個是[SQL](../Page/SQL.md "wikilink")和[Java](../Page/Java.md "wikilink")。

## 歷史

## 特性

### SQL连接操作

Oracle连接操作(left join ,right join,full join)的语法确与SQL标准完全不同，没有左连接与右连接的概念，也不支持全外连接。Oracle语法如下所示：

` select * from t1,t2 where t1.id=t2.id(+)`

采用(+)来表示外连接，在Oracle中它相当于左连接。Oracle9i中增加了标准外连接的语法支持，但使用不广。

### 物化视图

物化视图（materialized view）或译为实体化视图。与普通视图关系不同，物化视图更像是一个表，保存了实实在在的数据，并且可以与表一样定义存储参数，可以与表一样使用select,insert,update,delete。在其它数据库中也有和物化视图相似的解决方案，DB2叫物化查询表(materialized query table)，sqlserver有索引视图，但是索引视图仅是起优化作用，与oracle的物化视图还不太一样。

## 数据类型

### 数值类型

采用本地的number类型做指数或对数运算，与标准的浮点数性能可能会相差50倍。好在Oracle10g中增加了高效的浮点类型binary_float,binary_double，从而弥补了浮点数性能的问题。

``` PLSQL
variable_name number[([P][, S])] := 0;
```

  - NUMBER可选指定precision (P)与scale (S)。[精度表示十进制有效数字的个数](https://zh.wikipedia.org/wiki/精度 "wikilink")，最多不能超过38个有效数字（实际支持39-40位十进制数字）。Scale的范围为\[-84，127\]。Scale为正数时，表示从小数点到最不重要的十进制有效数字的个数；为负数时，其绝对值表示从最不重要的十进制有效数字到小数点的位数。如果没有指定精度，precision与scale默认为最大的取值区间。如果指定了精度，没有指定scale，scale默认为0。内部存储格式是变长阿拉伯数字的字节数组:
      - 首字节为长度值，最大22；如果为NULL，则该字节值为255(0xFF)
      - 第二字节是符号和指数字节(sign bit/exponent)，其最高比特为符号位，1表示正数，0表示负数；其余7比特构成基为100的指数值，取值范围\[-65，62\]，NUMBER数据类型的取值范围为\[10<sup>-130</sup>,10<sup>126</sup>)；
          - 第二字节值大于128，则：指数值=字节值 - 128 - 64= 字节值-192，即去除符号比特后偏移了64。字节值最大为254
          - 第二字节值等于128，则NUMBER数据类型表示值0
          - 第二字节值小于128，则：指数值=(255-字节值)-128-64=63-ZV，即取反后去除符号比特再偏移64
      - 其余字节保存了基数为100的数值00-99
          - 对于正数：实际值＝存储值－1
          - 对于负数：实际值＝存储值-101；字节值102 (0x66)标志字节数组的结束。\[1\]
          - 两个字节255与101表示正无穷
          - 单字节0表示负无穷
  - INTEGER是NUMBER的子类型，它等同于NUMBER（38,0），用来存储整数。若插入、更新的数值有小数，则会被四舍五入。
  - FLOAT类型也是NUMBER的子类型。Float(n),数 n 指示位的精度，可以存储的值的数目。n 值的范围可以从 1 到 126。若要从二进制转换为十进制的精度，请将 n 乘以 0.30103。要从十进制转换为二进制的精度，请用 3.32193 乘小数精度。126 位二进制精度的最大值是大约相当于 38 位小数精度。
  - BINARY_FLOAT 是 32 位、 单精度浮点数字数据类型。可以支持至少6位精度,每个 BINARY_FLOAT 的值需要 5 个字节，包括长度字节。
  - BINARY_DOUBLE 是为 64 位，双精度浮点数字数据类型。每个 BINARY_DOUBLE 的值需要 9 个字节，包括长度字节。

其它数值类型： dec, decimal, double precision, int, numeric, real, smallint, binary_integer.

### 字符类型

字符串数据类型依据存储空间分为两种：

  - 固定长度类型：CHAR/NCHAR，自动补足空格，最多可以存储2,000字节
  - 可变长度类型：VARCHAR2/NVARCHAR2，最大字节数都是4000，自动删除首尾的空格

串的开头存储了串的长度。如果串的长度小于或等于250（0x01\~0xFA）， Oracle 会使用1 个字节来表示长度。对于所有长度超过250 的串，都会在一个标志字节0xFE 后跟有两个字节来表示长度。

chr(0)表示的不可见字符，即我们通常所说的\\0

  - CHAR类型： CHAR(size \[BYTE | CHAR\]) 固定长度字符串；
  - NCHAR类型： 根据字符集而定的UNICODE格式固定长度字符串 最大长度2000 bytes。
  - VARCHAR类型: 不建议使用。虽然VARCHAR数据类型目前是VARCHAR2的同义词，VARCHAR数据类型将被重新定义为一个单独的数据类型用于可变长度的字符串相比，与VARCHAR2具有不同的比较语义
  - varchar2类型：变长字符串
  - nvarchar2()类型：包含UNICODE格式数据的变长字符串

<!-- end list -->

``` plpgsql
--  字段translated_name是NCHAR类型，则需要如下书写：
SELECT translated_description FROM product_descriptions
WHERE translated_name = N'LCD Monitor 11/PM';

variable_name varchar2(20) := 'Text';

-- e.g.:
address varchar2(20) := 'lake view road';
```

### 日期类型

``` PLSQL
variable_name date := to_date('01-01-2005 14:20:23', 'DD-MM-YYYY hh24:mi:ss');
```

  - Date类型可以表示日期与时间。精度到秒。日期范围可以是公元前4712年1月1日至公元9999年12月31日。占用7个字节的存储空间。第1字节：世纪+100；第2字节：年； 第3字节：月； 第4字节：天； 第5字节：小时+1； 第6字节：分+1；第7字节：秒+1。其中时间可以忽略。但无法只表示时间而忽略日期。[Oracle Datatypes](http://download.oracle.com/docs/cd/B19306_01/server.102/b14200/sql_elements001.htm)
  - TIMESTAMP类型：7字节或11字节的定宽日期/时间数据类型。可以包含小数秒，小数位数可以指定为0-9，默认为6位，所以最高精度可以到ns(纳秒).如果精度为0，则用7字节存储，与date类型功能相同，如果精度大于0则用11字节存储。
  - TIMESTAMP WITH TIME ZONE类型：TIMESTAMP类型的变种，它包含了时区偏移量的值
  - TIMESTAMP WITH LOCAL TIME ZONE类型：
  - INTERVAL YEAR TO MOTH：
  - INTERVAL DAY TO SECOND：

函数`TO_DATE`把字符串转换为日期值。

``` PLSQL
 to_date('31-12-2004', 'dd-mm-yyyy')

 to_date ('31-Dec-2004', 'dd-mon-yyyy', 'NLS_DATE_LANGUAGE = American')
```

函数`TO_CHAR (date_string, format_string)`把日期值转换为字符串。

PL/SQL支持使用ANSI日期与时间间隔值\[2\] The following clause gives an 18-month range:

示例：

``` PLSQL
WHERE dateField BETWEEN DATE '2004-12-30' - INTERVAL '1-6' YEAR TO MONTH
    AND DATE '2004-12-30'
```

``` PLSQL
create table T
(
   C1 DATE,
   C2 TIMESTAMP(9)
);

insert into t(c1,c2) values(date'2010-2-12',timestamp'2010-2-12 13:24:52.234123211');
insert into t(c1,c2) values(
        to_date('2010-2-12 10:20:30','YYYY-MM-DD HH24:MI:SS'),
        to_timestamp('2010-2-12 13:24:52.123456','YYYY-MM-DD HH24:MI:SS.FF6')
);

SQL> select c1,dump(c1) c1_d,c2,dump(c2) c2_d from t;
```

  - sysdate--返回当前系统日期和时间，精确到秒
  - systimestamp--返回当前系统日期和时间，精确到毫秒

日期型数据可以与数值加减得到新的日期，加减数值单位为天

  - sysdate+1--取明天的当前时间
  - sysdate-1/24--取当前时间的前一个小时

### LOB类型

内置的LOB数据类型包括BLOB、CLOB、NCLOB、BFILE（外部存储）的大型化和非结构化数据，如文本、图像、视屏、空间数据存储。

  - BLOB 数据类型：存储非结构化的二进制数据大对象，它可以被认为是没有字符集语义的比特流，一般是图像、声音、视频等文件。BLOB对象最多存储(4 gigabytes-1) \* (database block size)的二进制数据。
  - CLOB 数据类型：存储单字节和多字节字符数据。支持固定宽度和可变宽度的字符集。CLOB对象可以存储最多 (4 gigabytes-1) \* (database block size) 大小的字符
  - NCLOB 数据类型：存储UNICODE类型的字符数据，支持固定宽度和可变宽度的字符集，NCLOB对象可以存储最多(4 gigabytes-1) \* (database block size)大小的文本数据。
  - BFILE 数据类型：存储在数据库外的二进制文件，只读，最大长度4G

### LONG类型，RAW类型，LONG RAW类型

均为较老的数据类型，Oracle不建议使用。

  - LONG类型存储变长字符串，最多达2G的字节数据。存储在LONG 类型中的文本要进行字符集转换。支持LONG 列只是为了保证向后兼容性。LONG类型的限制如下：
      - 一个表中只有一列可以为LONG型。
      - LONG列不能定义为主键或唯一约束
      - 不能建立索引
      - LONG数据不能指定正则表达式。
      - 函数或存储过程不能接受LONG数据类型的参数。
      - LONG列不能出现在WHERE子句或完整性约束（除了可能会出现NULL和NOT NULL约束）
  - LONG RAW 类型，能存储2GB 的原始二进制数据（不用进行字符集转换的数据）
  - RAW类型用于存储二进制或字符类型数据，变长二进制数据类型，这说明采用这种数据类型存储的数据不会发生字符集转换。这种类型最多可以存储2,000字节的信息

### ROWID & UROWID类型

在数据库中的每一行都有一个地址。然而，一些表行的地址不是物理或永久的，或者不是ORACLE数据库生成的。例如，索引组织表行地址存储在索引的叶子，可以移动。例如,外部表的ROWID（如通过网关访问DB2表）不是​​标准的ORACLE的rowid。

ORACLE使用通用的ROWID（UROWIDs）的存储地址的索引组织表和外表。10个字节，格式为： \*\*\*\*\*\*\*\*.\*\*\*\*.\*\*\*\*，\*为0或1。NROWID类型为二进制数据表中记录的唯一行号，最大长度4000字节

索引组织表有逻辑urowids的，和外表的外urowids。UROWID这两种类型的存储在ROWID（堆组织的表的物理行id）。

创建基于逻辑的rowid在表中的主键。逻辑的rowid不会改变，只要主键不改变。索引组织表的ROWID伪UROWID数据类型。你可以访问这个伪列，你会堆组织表的ROWID伪（即使用一个SELECT ...ROWID语句）。如果你想存储的rowid索引组织表，那么你就可以定义一列的表型UROWID到列检索值的ROWID伪。

### 指定列的数据类型

定义一个变量，其类型是指定表的指定列的数据类型：

`Variable_name `<span style="color:#B8860B">`Table_name`</span><span style="color:#00f;">`.`</span>`Column_name`<span style="color:#00f;">`%type;`</span>

### 自定义类型

程序员自定义类型：

``` plpgsql
type data_type is record (field_1 type_1 := xyz, field_2 type_2 := xyz, ..., field_n type_n := xyz);
```

例如：

``` plpgsql
declare
    type t_address is record (
        name address.name%type,
        street address.street%type,
        street_number address.street_number%type,
        postcode address.postcode%type);
    v_address t_address;
begin
    select name, street, street_number, postcode into v_address from address where rownum = 1;
end;
```

可以使用点表示（dot-notation）获取结构中的域：

`v_address.street := 'High Street';"`

### 自增长数据类型

Oracle的数据类型里没有自增长（auto-incremental）字段类型，Oracle的官方解决方案是采用sequence实现。insert的时候需要用sequence.nextval。需要增加一张专用表来保存自增长字段的表和字段名，每次新增记录时都把这个记录值加1再取出使用。

## 基本程式

## 条件语句

以下的代码展示了IF-THEN-ELSIF结构。ELSIF和ELSE部分是可选的，从而可以创建更简单的IF-THEN或者IF-THEN-ELSE结构。

``` PLSQL
IF x = 1 THEN
   sequence_of_statements_1;
ELSIF x = 2 THEN
   sequence_of_statements_2;
ELSIF x = 3 THEN
   sequence_of_statements_3;
ELSIF x = 4 THEN
   sequence_of_statements_4;
ELSIF x = 5 THEN
   sequence_of_statements_5;
ELSE
   sequence_of_statements_N;
END IF;
```

CASE语句简化了一些大的IF-THEN-ELSE结构。

``` PLSQL
CASE
   WHEN x = 1 THEN sequence_of_statements_1;
   WHEN x = 2 THEN sequence_of_statements_2;
   WHEN x = 3 THEN sequence_of_statements_3;
   WHEN x = 4 THEN sequence_of_statements_4;
   WHEN x = 5 THEN sequence_of_statements_5;
   ELSE sequence_of_statements_N;
END CASE;
```

CASE语句可以使用预定义的选择符：

``` PLSQL
CASE x
   WHEN 1 THEN sequence_of_statements_1;
   WHEN 2 THEN sequence_of_statements_2;
   WHEN 3 THEN sequence_of_statements_3;
   WHEN 4 THEN sequence_of_statements_4;
   WHEN 5 THEN sequence_of_statements_5;
   ELSE sequence_of_statements_N;
END CASE;
```

## 陣列

## 迴圈

比较常用的有三种形式。

`For ... Loop`
`   ...`
`   End Loop;`

loop循环是最简单的循环语句，用于无限制的循环执行语句：

`Loop`
`   ...`
`   End Loop;`

`while...loop;`

如果退出循环，则必须使用exit语句终止循环。exit语句分两种格式：

`exit：该格式的语句用于无条件强迫终止循环。`
`exit...when：该格式用于有条件终止循环，首先检测when的条件是否满足。`

例1：

`loop`
`    if...then exit；`
`    end if；`
`end loop；`

例2：

`loop`
`   exit when；`
`end loop；`

while...loop循环在执行语句时，首先检测条件的值。例如：

`declare`
`  div_name varchar2(20);`
`  div_num integer:=1;`
`begin`
`  while div_num<10 loop`
`    select name into div_name from div_tab where div_author ='A000'||to_char(div_num);`
`    div_num:=div_num+1;`
`  end loop;`
`end;`

for...loop循环可以限定循环的次数例如：

`declare`
`  div_name varchar2(20);`
`  div_num integer:=1;`
`begin`
`  for div_num in 1..9 loop`
`      select name into div_name from div_tab where div_author='A000'||to_char(div_num);`
`  end loop;`
`end;`

例如：

`declare`
`   div_name varchar2(20);`
`   div_num integer:=1;`
`begin`
`   for div_num in 1..9 loop`
`        EXIT WHEN div_num >7;`
`        DBMS_OUTPUT.put_line(div_num);`
`   end loop;`
`end;`

## 類似的語言

功能近似PL/SQL的[程序語言和其他](https://zh.wikipedia.org/wiki/程序語言 "wikilink")[關係型資料庫](https://zh.wikipedia.org/wiki/關係型資料庫 "wikilink")：

  - [Sybase](../Page/Sybase.md "wikilink") [ASE](https://zh.wikipedia.org/wiki/ASE "wikilink")
  - [Microsoft SQL Server的](https://zh.wikipedia.org/wiki/Microsoft_SQL_Server "wikilink")[Transact-SQL](../Page/Transact-SQL.md "wikilink")
  - [PostgreSQL](../Page/PostgreSQL.md "wikilink")資料庫的[PL/pgSQL](https://zh.wikipedia.org/wiki/PL/pgSQL "wikilink")（模仿PL/SQL）
  - [IBM DB2的](../Page/IBM_DB2.md "wikilink")[SQL PL](https://zh.wikipedia.org/wiki/SQL_PL "wikilink")\[3\]
  - 符合[ISO](https://zh.wikipedia.org/wiki/ISO "wikilink") [SQL](../Page/SQL.md "wikilink")的[SQL/PSM標準](https://zh.wikipedia.org/wiki/SQL/PSM "wikilink")。

## 注释

## 參考文献

## 外部連結

## 参见

  - [Oracle数据库](../Page/Oracle数据库.md "wikilink")
  - [SQL](../Page/SQL.md "wikilink")
  - [Transact-SQL](../Page/Transact-SQL.md "wikilink")
  - [關聯式資料庫管理系統](https://zh.wikipedia.org/wiki/關聯式資料庫管理系統 "wikilink")

{{-}}

[Category:SQL](https://zh.wikipedia.org/wiki/Category:SQL "wikilink") [Category:甲骨文公司软件](https://zh.wikipedia.org/wiki/Category:甲骨文公司软件 "wikilink")

1.  [Oracle Ducuments about Data Type](https://docs.oracle.com/cd/B28359_01/server.111/b28318/datatype.htm#CNCPT713)
2.
3.  [SQL PL](http://publib.boulder.ibm.com/infocenter/db2help/index.jsp?topic=/com.ibm.db2.udb.doc/ad/c0011916.htm)