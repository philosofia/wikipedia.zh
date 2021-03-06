> 本文内容由[Float.h](https://zh.wikipedia.org/wiki/Float.h)转换而来。


**`float.h`**是[C標準函数庫中的](https://zh.wikipedia.org/wiki/C標準函数庫 "wikilink")[头文件](../Page/头文件.md "wikilink")，定义了浮点类型的一些极限值。

## 宏

### 双精度浮点类型

  - DBL_DIG 十进制的精度位数：15
  - DBL_EPSILON 保持运算的最小值：2.2204460492503131e-016
  - DBL_MANT_DIG 尾数的位数：53
  - DBL_MAX 最大值：1.7976931348623158e+308
  - DBL_MAX_10_EXP 10进制最大指数值：308
  - DBL_MAX_EXP 2进制最大指数值：1024 （即可以表示到2<sup>1024</sup>这个数量级的值）
  - DBL_MIN 最小的正值：2.2250738585072014e-308
  - DBL_MIN_10_EXP10进制最小指数值： (-307)
  - DBL_MIN_EXP 2进制最小指数值： (-1021)
  - _DBL_RADIX 指数的进制基数： 2
  - _DBL_ROUNDS 额外的舍入方法： 1

### 单精度浮点类型

  - FLT_DIG 10进制的精度位数 6
  - FLT_EPSILON 保持加法运算的最小值 1.192092896e-07F
  - FLT_GUARD 0
  - FLT_MANT_DIG 尾数的位数： 24
  - FLT_MAX 最大值：3.402823466e+38F
  - FLT_MAX_10_EXP 十进制的最大指数值： 38
  - FLT_MAX_EXP 二进制的最大指数值： 128
  - FLT_MIN 最小正值：1.175494351e-38F
  - FLT_MIN_10_EXP 最小10进制指数值： (-37)
  - FLT_MIN_EXP 最小二进制指数值： (-125)
  - FLT_NORMALIZE 0
  - FLT_RADIX 指数的进制基数： 2
  - FLT_ROUNDS 额外的舍入方法： 1

### 长双精度浮点类型

均规定为双精度浮点类型的极限值：

  - LDBL_DIG 即DBL_DIG
  - LDBL_EPSILON 即DBL_EPSILON
  - LDBL_MANT_DIG 即DBL_MANT_DIG
  - LDBL_MAX 即DBL_MAX
  - LDBL_MAX_10_EXP 即DBL_MAX_10_EXP
  - LDBL_MAX_EXP 即DBL_MAX_EXP
  - LDBL_MIN 即DBL_MIN
  - LDBL_MIN_10_EXP 即DBL_MIN_10_EXP
  - LDBL_MIN_EXP 即DBL_MIN_EXP
  - _LDBL_RADIX 即DBL_RADIX
  - _LDBL_ROUNDS 即DBL_ROUNDS

## 参考文献

[Category:C標準函式庫](https://zh.wikipedia.org/wiki/Category:C標準函式庫 "wikilink")