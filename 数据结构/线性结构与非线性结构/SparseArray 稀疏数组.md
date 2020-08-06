#### SparseArray 稀疏数组





> 当一个数组中，大部分元素相同时，可以使用 **稀疏数组** 来保存该数组

**处理方法：**

- 记录数组一共有多少行，多少列，有多少个不同的值
- 把具有不同值元素的行、列、值，记录在一个小规模的数组中，从而缩小数据的规模

**例如：**

有如下一个二维数组：

**6行 6列**，数组中相同的元素为**0**，<span style='color:green'>**绿色代表行**</span>，<span style='color:blue'>**蓝色代表列**</span> ，<span style='color:red'>**红色代表不同值**</span>

> 
>
> 这里为了方便理解和说明，并没有使用数组中的索引来画表格，实际编码中，注意切换
>
> 

| <span style='color:green'>行</span>  <span style='color:blue'>列</span> | <span style='color:blue'>1</span> | <span style='color:blue'>2</span> | <span style='color:blue'>3</span> | <span style='color:blue'>4</span> | <span style='color:blue'>5</span> | <span style='color:blue'>6</span> |
| :----------------------------------------------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: |
|              <span style='color:green'>1</span>              |                 0                 |                 0                 |                 0                 |                 0                 | <span style='color:red'>7</span>  |                 0                 |
|              <span style='color:green'>2</span>              |                 0                 |                 0                 | <span style='color:red'>-1</span> |                 0                 |                 0                 |                 0                 |
|              <span style='color:green'>3</span>              |                 0                 | <span style='color:red'>5</span>  |                 0                 |                 0                 |                 0                 |                 0                 |
|              <span style='color:green'>4</span>              |                 0                 |                 0                 |                 0                 | <span style='color:red'>-9</span> |                 0                 |                 0                 |
|              <span style='color:green'>5</span>              |                 0                 |                 0                 |                 0                 |                 0                 |                 0                 | <span style='color:red'>7</span>  |
|              <span style='color:green'>6</span>              |                 0                 | <span style='color:red'>54</span> |                 0                 | <span style='color:red'>5</span>  |                 0                 |                 0                 |

​	我们按照普通的数组来存储的话，会存储**36**个元素

​	转换成 **稀疏数组** 试试：

1. 记录数组一共有多少 <span style='color:green'>**行**</span>，<span style='color:blue'>**列**</span>, <span style='color:red'>**不同值**</span>

   给定数组一共有 <span style='color:green'>**6行**</span> ，<span style='color:blue'>**6列**</span>，<span style='color:red'>**7个不同值**</span>，那么 **稀疏数组** **第一行**就记录这些信息

   | <span style='color:green'>行</span>  <span style='color:blue'>列</span> |    <span style='color:blue'>1</span>     |    <span style='color:blue'>2</span>    |     <span style='color:blue'>3</span>      |
   | :----------------------------------------------------------: | :--------------------------------------: | :-------------------------------------: | :----------------------------------------: |
   |              <span style='color:green'>1</span>              | <span style='color:green'>6（行）</span> | <span style='color:blue'>6（列）</span> | <span style='color:red'>7（不同值）</span> |
   |              <span style='color:green'>2</span>              |                                          |                                         |                                            |
   |              <span style='color:green'>3</span>              |                                          |                                         |                                            |
   |              <span style='color:green'>4</span>              |                                          |                                         |                                            |
   |             <span style='color:green'>...</span>             |                                          |                                         |                                            |

2. 记录不同值的 <span style='color:green'>**行**</span>，<span style='color:blue'>**列**</span>, <span style='color:red'>**不同值**</span>。

   从第二行开始，记录这些不同值在原来数组中的 <span style='color:green'>**行**</span>，<span style='color:blue'>**列**</span>, <span style='color:red'>**值**</span> 。	

   | <span style='color:green'>行</span>  <span style='color:blue'>列</span> |       <span style='color:blue'>1</span>        |       <span style='color:blue'>2</span>       |        <span style='color:blue'>3</span>         |
   | :----------------------------------------------------------: | :--------------------------------------------: | :-------------------------------------------: | :----------------------------------------------: |
   |              <span style='color:green'>1</span>              | <span style='color:green'>（共）6（行）</span> | <span style='color:blue'>（共）6（列）</span> | <span style='color:red'>（共）7（不同值）</span> |
   |              <span style='color:green'>2</span>              | <span style='color:green'>（第）2（行）</span> | <span style='color:blue'>（第）3（列）</span> |    <span style='color:red'>（value）-1</span>    |
   |              <span style='color:green'>3</span>              | <span style='color:green'>（第）3（行）</span> | <span style='color:blue'>（第）2（列）</span> |    <span style='color:red'>（value）5</span>     |
   |              <span style='color:green'>4</span>              | <span style='color:green'>（第）4（行）</span> | <span style='color:blue'>（第）4（列）</span> |    <span style='color:red'>（value）-9</span>    |
   |              <span style='color:green'>5</span>              | <span style='color:green'>（第）5（行）</span> | <span style='color:blue'>（第）6（列）</span> |    <span style='color:red'>（value）7</span>     |
   |              <span style='color:green'>6</span>              | <span style='color:green'>（第）6（行）</span> | <span style='color:blue'>（第）2（列）</span> |    <span style='color:red'>（value）54</span>    |
   |              <span style='color:green'>7</span>              |      <span style='color:green'>...</span>      |      <span style='color:blue'>...</span>      |        <span style='color:red'>...</span>        |

   到此 **稀疏数组** 记录完毕，再一次阅读这个 **稀疏数组** ：

   **第一行** ：表示原来的数组一共有 <span style='color:green'>**6行**</span>、<span style='color:blue'>**6列**</span>,的数据，总共有 <span style='color:red'>**7个不同值**</span>

   从第二行开始，就表示这些不同值的具体位置(行列信息 和 值)

   **第二行** ：表示 <span style='color:green'>（第）2（行）</span> <span style='color:blue'>（第）3（列）</span> 有一个 <span style='color:red'>**不同值**</span>，<span style='color:red'>值为 -1</span>，这行其他数据全部是相同值 0

   以此类推.....

   **稀疏数组** 记录了 3*6 = 18个元素，相比于原来的 6\*6=36个元素 起到了一定了压缩作用。