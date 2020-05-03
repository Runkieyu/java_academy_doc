## JavaSE - Module 1 - Task 3 - 运算符

### 算数运算符

#### 1. 算数运算符的概念

* `+` 加法运算符
* `-` 减法运算符
* `*` 乘法运算符
* `/` 除法运算符
* `%` 取余运算符

**注意**

**1. 当两个整数相除时，只保留整数部分，丢弃小数部分(言外之意，两个不都是整数的数相除时可以保留小数部分)**

例： `5 / 2 = 2`

保留小数部分的处理方式一：使用强制类型转换其中一个操作数转换为 double 类型再运算即可(不推荐，因为强制转换类型会造成数据溢出)。

例：`(double)5 / 2` 或 `5 / (double)2` 

保留小数部分的处理方式二：另其中一个操作数乘以 1.0 即可。(推荐)

例：`5 * 1.0 / 2`

**2. 0不能做除数**

例：`5 / 0`

算数运算符的实现请参考代码 `ArithmeticTest.java`

```java
/*
    编程实现算术运算符的使用
 */
public class ArithmeticTest {
	
	public static void main(String[] args) {
		
		// 1.声明两个int类型的变量并初始化
		//int ia = 6, ib = 2;       // 表示声明两个int类型的变量ia和ib，不推荐使用
		int ia = 6;                 // 推荐该方式，提高了代码的可读性
		int ib = 2;
		System.out.println("ia = " + ia); // ia = 6
		System.out.println("ib = " + ib); // ib = 2
		
		System.out.println("----------------------------------------");
		// 2.使用上述变量实现算术运算符的使用   +  -  *  /  %
		// 表示声明变量ic来记录ia与ib的和
		int ic = ia + ib;
		System.out.println("ic = " + ic); // ic = 8
		// 其中ia+ib这个整体叫做表达式  ia、ib叫做操作数   +叫做操作符/运算符
		System.out.println(ia + ib);  // 8
		System.out.println(ia - ib);  // 4
		System.out.println(ia * ib);  // 12
		System.out.println(ia / ib);  // 3
		System.out.println(ia % ib);  // 0
		
		System.out.println("----------------------------------------");
		// 3.注意事项
		// 3.1 当两个整数相除时结果只保留整数部分，丢弃小数部分
		System.out.println(5 / 2); // 2
		
		System.out.println("----------------------------------------");
		// 3.2 若希望保留小数部分该如何处理？
		// 处理方式一：使用强制类型转换将其中一个操作数转换为double类型再运算即可
		System.out.println((double)5 / 2);   // 2.5
		System.out.println(5 / (double)2);   // 2.5
		System.out.println((double)5 / (double)2); // 2.5
		System.out.println((double)(5 / 2)); // 2.0
		// 处理方式二：让其中一个操作数乘以1.0即可（推荐）
		System.out.println(5*1.0 / 2); // 2.5
		System.out.println(5.0 / 2);   // 2.5   ia.0 错误的表示
		
		System.out.println("----------------------------------------");
		// 3.3 0不能作除数
		//System.out.println(5 / 0); // 编译ok，运行发生java.lang.ArithmeticException(算术异常 记住): / by zero
		System.out.println(5 / 0.0); // Infinity 无穷
 		System.out.println(0 / 0.0); // NaN Not a Number 
	}
}
```

对算数运算符的活用，如下例题：

**提示用户输入正整数类型的秒数，拆分后输出时秒分**

代码请参照 `ArithmeticTimeTest.java`

```java
/*
    编程使用算术运算符实现秒数的拆分
 */

import java.util.Scanner; 
 
public class ArithmeticTimeTest {
	
	public static void main(String[] args) {
		
		// 1.提示用户输入一个正整数的秒数并使用变量记录
		System.out.println("请输入一个正整数的秒数：");
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		
		// 2.将正整数的秒数拆分为时分秒后并使用变量记录
		// 3666秒 => 1小时1分钟6秒钟
		// 3666 / 3600 = 1 小时     3666 % 3600 = 66 / 60 = 1 分钟     3666 % 60 = 6 秒钟 
		int hour = num / 3600;      // 拆分小时数
		int min = num % 3600 / 60;  // 拆分分钟数
		int sec = num % 60;         // 拆分秒数
		
		// 3.打印最终的拆分结果
		System.out.println(num + "秒转换为" + hour + "小时" + min + "分钟" + sec + "秒钟");
	}
}
```

**注意**

**关于 `+` 何时作为字符串连接字符，何时作为加法运算符**

只要+两边的操作数中有一个操作数是字符串类型，则该+就被当做字符串连接符处理，否则当做加法运算符处理

```java
System.out.println(hour + min + sec);       // 整数8 
System.out.println(hour + min + sec + "");  // 字符串8
System.out.println(hour + min + "" + sec);  // 字符串26
System.out.println(hour + "" + min + sec);  // 字符串116
System.out.println("" + hour + min + sec);  // 字符串116
System.out.println("" + (hour + min + sec));// 字符串8
```

### 逻辑运算符

### 条件(三目)运算符

形式为 `条件表达式?表达式1:表达式2`。

流程为：判断表达式是否成立，若成立则执行表达式1，若不成立则执行表达式2。
    
例1：使用逻辑运算符和条件运算符判断输入的数字是否为三位数。

请参考代码 `LogicJudgeTest.java`

```java
/*
    编程使用逻辑运算符判断三位数
 */

import java.util.Scanner; 
 
public class LogicJudgeTest {
	
	public static void main(String[] args) {
		
		// 1.提示用户输入一个正整数并使用变量记录
		System.out.println("请输入一个正整数：");
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		
		// 2.使用逻辑运算符判断是否为三位数并打印    >= 100   <= 999   &&
		//System.out.println(100 <= num <= 999); // 错误: 二元运算符 '<=' 的操作数类型错误
		// 逻辑运算符主要用于连接多个关系运算符作为最终运算的表达式，用于实现多条件的连接
		System.out.println(100 <= num && num <= 999);
		// 使用三目运算符来判断是否为三位数
		System.out.println(num + ((100 <= num && num <= 999)? "是三位数": "不是三位数"));
	}
}
```

例2:使用三目运算符查找输入的两个数字的最大值。

请参考代码 `ThreeEyeTest.java`

```java
/*
    编程使用三目运算符查找最大值
 */

import java.util.Scanner; 
 
public class ThreeEyeTest {
	
	public static void main(String[] args) {
		
		// 1.提示用户输入两个整数并使用变量记录
		System.out.println("请输入两个整数：");
		Scanner sc = new Scanner(System.in);
		int ia = sc.nextInt();
		int ib = sc.nextInt();
		
		// 2.使用三目运算符找到最大值并打印
		int max = ia > ib? ia: ib;
		System.out.println("最大值是：" + max);
		System.out.println("最大值是：" + (ia > ib? ia: ib));
	}
}
```

### 赋值运算符

`=` 表示赋值运算符，用于将右边的数据赋值给左边的变量，并覆盖变量原来的数值。

* 赋值表达式本身也有值，其本身的值就是所赋的值

例： `System.out.println(i = 5)` 输出这个表达式的本身，结果为5。

* 复合赋值运算符： `+=`, `-=`, `*=`, `/=`。

**应注意的是，在结果上来看 `ia += 2` 和 `ia = ia + 2` 等价，但实际上并不是如此，比如：**

```java
byte ia = 10;
ia = ia + 2; 
```

在运行上述代码时会报错：`不兼容的类型: 从int转换到byte可能会有损失`，也就是说在做加法运算时，即使是 byte 之间的运算，也会由于编译器优化原理将结果转化为 Int 类型，所以如果想在这种情况下得到结果，则应当执行 `ia = (byte)(ia + 2)`，但同等情况下 `ia += 2`则不会报错，因此实际上两者并不等价。

**`==`判断时的注意点： `ia == 2` 和 `2 == ia` 在结果上相同，但推荐后者，因为如果少写了一个 `=` 时可以及时发现，理由是 `2 = ia` 会报错：错误: 意外的类型。**

复合运算符的实现请参考代码 `AssignTest.java`

```java
/*
    赋值运算符的使用
 */
public class AssignTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个int类型的变量并初始化
		int ia = 3;
		// 2.打印变量的数值
		System.out.println("ia = " + ia); // ia = 3
		
		System.out.println("-----------------------------------");
		// 3.简单赋值运算符的使用
		// 表示将数据5赋值给变量ia并且覆盖变量ia原来的数值
		ia = 5;
		System.out.println("ia = " + ia); // ia = 5
		// 下面的代码是在打印表达式的结果
		System.out.println( ia = 5 ); // 5
		System.out.println("ia = " + ia); // ia = 5
		int ib = ia = 6;
		System.out.println("ia = " + ia); // ia = 6
		System.out.println("ib = " + ib); // ib = 6
		int ic;
		ic = ib = ia = 8;
		System.out.println("ia = " + ia); // ia = 8
		System.out.println("ib = " + ib); // ib = 8
		System.out.println("ic = " + ic); // ic = 8
		
		System.out.println("-----------------------------------");
		// 4.复合赋值运算符的使用
		//ia = ia + 2;  目前推荐使用该方式
		ia += 2;        // 简化写法，从结果上来看是等价的
		System.out.println("ia = " + ia); // ia = 10
		
		System.out.println("-----------------------------------");
		// 5.笔试考点1
		byte b1 = 10;
		System.out.println("b1 = " + b1); // b1 = 10
		//b1 = b1 + 2; // 错误: 不兼容的类型: 从int转换到byte可能会有损失         byte + int 相加结果还是int类型
		//b1 = b1 + (byte)2; // 错误: 不兼容的类型: 从int转换到byte可能会有损失   byte + byte 相加结果还是int类型  编译器优化
		//b1 = (byte)(b1 + 2); // 强制类型转换，将int类型转换为byte
		b1 += 2; // 真正等价于b1 = (byte)(b1 + 2);
		System.out.println("b1 = " + b1); // b1 = 12
		
		System.out.println("-----------------------------------");
		// 6.笔试考点2
		//ia == 2; - 表示判断变量ia的数值是否等于2
		//2 == ia; - 表示判断2是否等于变量ia的数值，从结果上来说等价，推荐该方式
		//ia = 2;  - 表示将2赋值给变量ia，覆盖变量ia原来的数值
		//2 = ia;  //- 编译报错  错误: 意外的类型
	}
}
```

### 移位运算符

* 左移运算符 `<<` 

用于将数据的二进制位向左移动，右边用 0 补充。

* 右移运算符  `>>`

用于将数据的二进制位向右移动，左边用符号位填充，这意味着，如果左边符号位是 1 则用 1 填充，如果左边符号位是 0 ，则用 0 填充。

* 逻辑右移运算符 `>>>`

用于将数据的二进制位向右移动，**左边使用 0 补充。**

移位运算符的运用请参考 `MoveBitTest.java`

```java
/*
    编程实现移位运算符的使用
 */
public class MoveBitTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个byte类型的变量并初始化
		byte b1 = 13;
		// 2.打印变量的数值
		System.out.println("b1 = " + b1); // b1 = 13
		
		System.out.println("---------------------------------------------------");
		// 3.移位运算符的使用
		// 13的二进制是：... 0000 1101  => 左移1位的结果是：... 0001 1010 => 换算为十进制整数是：26
		//byte b2 = b1 << 1; // 错误: 不兼容的类型: 从int转换到byte可能会有损失   自动提升为int类型，也就是32位二进制
		byte b2 = (byte)(b1 << 1); 
		System.out.println("b2 = " + b2); // 26
		System.out.println(b1 << 1); // 26    左移1位相当于当前整数的数值*2
		System.out.println(b1 << 2); // 52    左移2位相当于当前整数的数值*4
		
		System.out.println("---------------------------------------------------");
		// 13的二进制是：... 0000 1101 => 右移1位的结果是：... 0000 0110 => 换算为十进制整数是：6
		System.out.println(b1 >> 1); // 6     右移1位相当于当前整数的数值/2
		System.out.println(b1 >> 2); // 3     右移2位相当于当前整数的数值/4
		
		System.out.println("---------------------------------------------------");
		// 逻辑右移   对于非负数来说，逻辑右移和右移的效果一致
		System.out.println(b1 >>> 2); // 3  
	}
}
```

**注意，在移位时，数据类型也会变为 Int 类型， 因此如果赋值给 byte 类型时会报错，需要强制转型。另外有一个小规律，向左移动一位，相当于当前数值 `* 2`，向右移动一位相当于当前数值 `/ 2`。**

### 位运算符

* 表示按位与运算 & ，按照二进制位进行与运算，同 1 为 1 ，一 0 为 0。

* 按位或运算 | ，按照二进制位进行或运算，一 1 为 1，同 0 为 0。

* 按位取反运算 ～ ，按照二进制位进行取反运算，1 为 0，0 为 1。

* 按异或运算符 ^ ，按照二进制位进行异或运算，同为 0 ，不同为 1。

位运算符的代码实现请参考`BitTest.java`

```java
/*
    编程实现位运算符的使用
 */
public class BitTest {
	
	public static void main(String[] args) {
		
		// 1.声明两个byte类型的变量并初始化
		byte b1 = 11;
		byte b2 = 13;
		// 2.打印变量的数值
		System.out.println("b1 = " + b1); // b1 = 11
		System.out.println("b2 = " + b2); // b2 = 13
		
		System.out.println("---------------------------------------------------");
		// 3.实现位运算符的使用
		// b1的二进制为： 0000 1011          
		// b2的二进制为： 0000 1101
		System.out.println( b1 & b2);  // 按位与：同1为1，一0为0      按位与后的二进制为：0000 1001  => 转为十进制是：9
		System.out.println( b1 | b2);  // 按位或：一1为1，同0为0      按位或后的二进制为：0000 1111  => 转为十进制是：15
		System.out.println( b1 ^ b2);  // 按位异或：相同为0，不同为1  按位异或的二进制为：0000 0110  => 转为十进制是：6
		System.out.println( ~ b1);     // 按位取反：1为0,0为1         按位取反的二进制为：1111 0100 
		// 二进制1111 0100转为十进制 => 先减1: 1111 0011 => 按位取反：0000 1100 => 转为十进制：12  => 添加负号：-12
	}
}
```

### 运算符优先级

![屏幕快照 2020-04-28 下午11.18.23](media/15879947534435/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202020-04-28%20%E4%B8%8B%E5%8D%8811.18.23.png)



