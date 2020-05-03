## JavaSE - Module 1 - Task 5 - 数组

### 一维数组

#### 一维数组的相关概念

当需要在 java 程序中记录单个数据内容时，则声明一个变量即可。但当需要在 java 程序中记录多个**类型相同的数据内容**时则声明一个一维数组即可。

一维数组本质上就是在内存空间中申请一段连续的存储单元。

数组是相同数据类型的多个元素的容器，元素按线性顺序排列，在 java 语言中体现为一种引用数据类型。

#### 一维数组的声明及使用

一维数组的声明格式：

```java
数据类型[] 数组名称 = new 数据类型[数组的长度]

或

数据类型 数组名称[] = new 数据类型[数组的长度] 不推荐
```

* 数组的长度可以通过 `数组名称.length` 获取

* 可以通过下标的方式访问数组中的每一个元素。需要注意的是，数组的下标从 `0` 开始，对于长度为 n 的数组，下标的取值范围为 `0 ~ n-1 `，取值超出下标的取值范围时会报错。

一维数组的使用请参考代码 `ArrayTest.java`

```java
/*
    编程实现一维数组的声明和使用
 */
public class ArrayTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个长度为2元素类型为int类型的一维数组
		// 数据类型[] 数组名称 = new 数据类型[数组的长度];
		//int arr1[] = new int[2];    // 两种方式从结果上来说是一样的，不推荐使用
		//int num = 2;                // 声明一个初始值为2的变量 
		int[] arr1 = new int[2];      // 推荐该方式，更容易与变量的声明区分，提高了代码的可读性   动态方式
		
		// 2.打印一维数组的长度以及每个元素的数值
		System.out.println("数组的长度是：" + arr1.length); // 2   下标从0 ~ 1
		System.out.println("下标为0的元素是：" + arr1[0]);  // 0  默认值
		System.out.println("下标为1的元素是：" + arr1[1]); 	// 0  
        //System.out.println("下标为2的元素是：" + arr1[2]); 	// 编译ok，运行发生ArrayIndexOutOfBoundsException数组下标越界异常

		System.out.println("------------------------------------------------");
		// 3.使用for循环打印数组中的所有元素
		for(int i = 0; i < arr1.length; i++) {
			System.out.println("下标为" + i + "的元素是：" + arr1[i]); // 全是0
		}
		// 7.直接通过数组名来打印数组中的所有元素
		System.out.println("arr1 = " + arr1); // 地址信息
		
		System.out.println("------------------------------------------------");
		// 4.声明一个长度为5元素类型为double类型的一维数组
		double[] arr2 = new double[5];
		// 打印数组中每个元素值
		for(int i = 0; i < arr2.length; i++) {
			System.out.println("下标为" + i + "的元素是：" + arr2[i]); // 全是0.0 
		}
		
		System.out.println("------------------------------------------------");
		// 5.声明数组的同时就对数组中的元素进行初始化   静态方式的简化版
		char[] arr3 = {'a', 'b', 'c', 'd'};
		// 打印数组中的每个元素值
		for(int i = 0; i < arr3.length; i++) {
			System.out.println("下标为" + i + "的元素是：" + arr3[i]); // a b c d
		}
		
		System.out.println("------------------------------------------------");
		// 6.特殊的写法   静态方式
		boolean[] arr4 = new boolean[]{true, true, false, false};
		// 打印数组中的每个元素值
		for(int i = 0; i < arr4.length; i++) {
			System.out.println("下标为" + i + "的元素是：" + arr4[i]); // true true false false
		}
	}
}
```

#### 一维数组的初始化

* 动态初始化

在**一维数组的声明及使用**章节中曾介绍了一维数组的声明方式：

```java
数据类型[] 数组名称 = new 数据类型[数组的长度]

或

数据类型 数组名称[] = new 数据类型[数组的长度] 不推荐
```

这种方式由于没有对初始值进行定义，称为动态初始化。

在动态初始化时，基本类型的数组(数据元素为基本类型)创建后，其元素的初始值：byte, short, char, int, long 为 0， float, double 为 0.0， boolean 为 false

* 静态初始化

可以在数组声明的同时进行初始化，这种方法称为静态初始化，具体如下：

```java
数据类型[] 数组名称 = new 数据类型[]{初始值1，初始值2···} 

或简化版

数据类型[] 数组名称 = {初始值1，初始值2···} 推荐使用
```

#### 一维数组特点

* 可以直接通过下标访问指定位置的元素，速度很快

* 数组要求所有元素的类型必须相同

* 要求内存空间必须连续且内存长度一旦确定无法修改

如果是在内存空间不足，则应考虑申请一段更大的内存并将原有内存中的数据依次拷贝。

* 增加和删除元素时可能会移动大量元素，效率低

#### 内存结构分析

```java
数据类型[] 数组名称 = new 数据类型[数组的长度]
```
在上述声明中，`=左边` 代表的是变量的声明，`=右边` 代表的是一维数组的声明，那么声明一维数组时究竟是如何申请内存空间的，这就要了解 `栈区` 和 `堆区` 的概念。

* 栈区

栈用于存放程序运行过程中所有的局部变量。一个运行的 java 程序从开始到结束会有多次变量的声明。

例如所有在方法体中直接声明且随着方法体执行结束而释放的变量叫做局部变量，`int 变量名 = 变量值` 就是声明局部变量的一种表现形式。此时，在栈区为声明的变量申请了内存空间。

* 堆区

JVM 会在其内存空间中开辟一个称为 `堆` 的存储空间，这部分用于存储使用 `new` 关键字创建的数组和对象。

如上介绍可知，当声明一维数组时 `int[] arr = new int[5]` 中， `=` 右边为在堆区申请一段长度为 5 的内存，并填入初始值 0， 这一段堆区内存会有一个地址，假设地址为 `0x10`，`=` 左边为在栈区申请一个 int 数据类型的内存叫做 arr，`=` 的作用是将地址 `0x10` 填入 arr 的内存,当访问一维数组 arr 时，则根据 `0x10` 这一地址找到堆区中的那段内存。

而在这一过程中，原本作为基本数据类型的 `int` 在此时也由于变成 `int[]` 且引用了堆区的内存地址而被称为**引用数据类型。**

#### 一维数组的案例

##### 案例一： 一维数组的 CRUD 案例

请使用一维数组完成如下要求：

* 声明一个长度为 5 元素类型为 `int` 类型的数组，打印数组中所有元素的值

* 使用元素 11，22，33，44 分别对数组中前四个元素赋值后再打印

* 将元素 55 插入到下标为 0 的位置，原有元素向后移动，再打印所有元素值

* 将元素 55 从数组中删除，删除方式为后续元素向前移动，最后位置置为 0 并打印

* 查找数组中是否存在 22，若存在则修改为 220 并再次打印所有元素

实现代码请参考 `ArrayOpTest.java`

```java
/*
    编程实现一维数组的增删改查操作
*/
public class ArrayOpTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个长度为5元素类型为int类型的一维数组
		int[] arr = new int[5];
		// 打印数组中所有元素的数值
		System.out.print("数组中的元素有：");
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + " "); // 全是默认值0
		}
		System.out.println();
		
		System.out.println("-------------------------------------------------");
		// 2.将数据11 22 33 44依次对数组中前四个元素赋值
		/*
		arr[0] = 11;
		arr[1] = 22;
		arr[2] = 33;
		arr[3] = 44;
		*/
		for(int i = 0; i < arr.length-1; i++) {
			arr[i] = (i+1)*11;
		}
		// 打印数组中所有元素的数值
		System.out.print("数组中的元素有：");
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + " "); // 11 22 33 44 0
		}
		System.out.println();
		
		System.out.println("-------------------------------------------------");
		// 3.将数据55插入到下标为0的位置，原有元素向后移动
		/*
		arr[4] = arr[3];
		arr[3] = arr[2];
		arr[2] = arr[1];
		arr[1] = arr[0];
		arr[0] = 55;
		*/
		for(int i = arr.length-1; i > 0; i--) {
			arr[i] = arr[i-1];
		}
		arr[0] = 55;
		// 打印数组中所有元素的数值
		System.out.print("数组中的元素有：");
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + " "); // 55 11 22 33 44
		}
		System.out.println();
		
		System.out.println("-------------------------------------------------");
		// 4.将数据55从数组中删除，删除方式为后续元素向前移动，最后一个位置置为0
		/*
		arr[0] = arr[1];
		arr[1] = arr[2];
		arr[2] = arr[3];
		arr[3] = arr[4];
		*/
		for(int i = 0; i < arr.length-1; i++) {
			arr[i] = arr[i+1];
		}
		arr[4] = 0;
		// 打印数组中所有元素的数值
		System.out.print("数组中的元素有：");
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + " "); // 11 22 33 44 0
		}
		System.out.println();
		
		System.out.println("-------------------------------------------------");
		// 5.查找数组中是否有元素22，若有则修改为220
		for(int i = 0; i < arr.length; i++) {
			if(22 == arr[i]) {
				arr[i] = 220;
			}
		}
		// 打印数组中所有元素的数值
		System.out.print("数组中的元素有：");
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + " "); // 11 220 33 44 0
		}
		System.out.println();
	}
}
```

##### 案例二：一维数组之间元素的拷贝案例

请实现如下要求：

* 声明一个初始值为 `11 22 33 44 55` 的一维数组并打印所有元素

* 声明一个长度为 3 数据类型为 int 的一维数组并打印所有元素

* 实现将第一个数组 `中间三个` 元素复制到第二个数组中

* 打印第二个数组的所有元素

实现，优化，官方提供的数组拷贝功能 `System.arraycopy` 以及注意点请参考代码 `ArrayCopyTest.java`

```java
/*
    编程实现数组之间元素的拷贝
 */
public class ArrayCopyTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个初始值为11、22、33、44、55的一维数组
		int[] arr = {11, 22, 33, 44, 55};
		// 打印数组中的所有元素
		System.out.print("第一个数组中的元素有：");
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + " "); // 11 22 33 44 55
		}
		System.out.println();
		
		System.out.println("----------------------------------------------------------");
		// 2.声明一个长度为3元素类型为int类型的一维数组
		int[] brr = new int[3];
		// 打印数组中的所有元素
		System.out.print("第二个数组中的元素有：");
		for(int i = 0; i < brr.length; i++) {
			System.out.print(brr[i] + " "); // 0 0 0
		}
		System.out.println();
		
		System.out.println("----------------------------------------------------------");
		// 3.将第一个数组中的中间3个元素赋值到第二个数组中
		/*
		brr[0] = arr[1];
		brr[1] = arr[2];
		brr[2] = arr[3];
		*/
		/*
		for(int i = 0; i < brr.length; i++) {
			brr[i] = arr[i+1];
		}
		*/
		// 可以直接使用Java官方提供的拷贝功能
		// 表示将数组arr中下标从1开始的3个元素拷贝到数组brr中下标从0开始的位置
		System.arraycopy(arr, 1, brr, 0, 3);
		// 打印第二个数组中的所有元素
		System.out.print("第二个数组中的元素有：");
		for(int i = 0; i < brr.length; i++) {
			System.out.print(brr[i] + " "); // 22 33 44
		}
		System.out.println();
		
		System.out.println("----------------------------------------------------------");
		// 4.笔试考点
		// 表示将变量arr的数值赋值给变量brr，覆盖变量brr中原来的数值
		// 数组名arr的内存空间中存放的是数据在堆区中的内存地址信息，赋值后让brr变量中存放了arr所指向堆区的内存地址
		// 也就是让brr和arr指向了同一块堆区空间，有本质上就是改变指向而已
		brr = arr;
		// 打印第二个数组中的所有元素
		System.out.print("第二个数组中的元素有：");
		for(int i = 0; i < brr.length; i++) {
			System.out.print(brr[i] + " "); // 22 33 44
		}
		System.out.println();	
		
	}
}
```

##### 案例三：一维数组统计数字次数案例

要求：编程统计用户输入任意一个正整数中每个数字出现的次数。

例：数字 `123123` 中，1，2，3分别出现 2 次。 

* 原理分析

首先为了对用户输入的正整数中各个数字出现的次数进行统计，需要对输入的正整数并进行拆分。

```
123123 % 10 = 3 拆分末位
123123 / 10 = 12312 丢弃末位
12312 % 10 = 2 拆分末位
12312 / 10 = 1231 丢弃末位
·
·
·
1 / 10 = 0 0 为终止条件
```

拆分后就可以对各个数字进行统计。已知数字由 0 ～ 9 组成，因此可以组成一个由 0 ～ 9 组成的 10 位一维数组。而拆分出的末位数字(例如 i )就可以作为一维数组的下标 `arr[i]`，0 ～ 9 中的数字每出现一次，就通过 `arr[i]++` 对值进行更新，最终获得各个数字出现的次数。


| 数字出现次数(值) | 0 | 2  | 2 | 2 | 0 | 0 | 0 | 0 | 0 | 0  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 统计数字(下标) | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

* 代码实现

具体实现请参考代码 `ArrayCountTest.java`

```java
/*
    编程使用数组实现正整数中每个数字出现次数的统计
 */

import java.util.Scanner; 
 
public class ArrayCountTest {
	
	public static void main(String[] args) {
		
		// 1.提示用户输入一个正整数并使用变量记录
		System.out.println("请输入一个正整数：");
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		
		// 2.准备一个长度为10元素类型int类型的一维数组，默认值为0
		int[] arr = new int[10];
		
		// 3.拆分正整数中的每个数字并统计到一维数组中
		int temp = num;
		while(temp > 0) {
			arr[temp%10]++;
			temp /= 10;
		}
		
		// 4.打印最终的统计结果
		for(int i = 0; i < arr.length; i++) {
			if(arr[i] > 0) {
				System.out.println("数字" + i + "出现了" + arr[i] + "次！");
			}
		}
	}
}
```

##### 案例四：学生考试成绩的录入与打印

要求：

* 提示用户输入学生的人数及每个学生的成绩并打印出来

* 计算该班级的总分和平均分并打印

具体实现请参考代码 `ArrayScoreTest.java`

```java
/*
    编程使用数组来记录学生的考试成绩并打印
 */
 
import java.util.Scanner; 
import java.util.Arrays;
 
public class ArrayScoreTest {
	
	public static void main(String[] args) {
		
		// 1.提示用户输入学生的人数并使用变量记录
		System.out.println("请输入学生的人数：");
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		
		// 2.根据学生的人数来声明对应长度的数组负责记录学生的考试成绩
		// 变长数组 ： 主要指变量可以作为数组的长度，但绝不是数组的长度可以发生改变
		int[] scores = new int[num];
		
		// 3.提示用户输入每个学生的考试成绩并记录一维数组中
		for(int i = 0; i < num; i++) {
			System.out.println("请输入第" + (i+1) + "个学生的考试成绩：");
			scores[i] = sc.nextInt();
		}
		
		// 4.打印所有学生的考试成绩
		System.out.print("本班学生的考试成绩分别是：");
		for(int i = 0; i < scores.length; i++) {
			System.out.print(scores[i] + " ");
		}
		System.out.println();
		
		System.out.println("----------------------------------------------");
		// 5.计算本班级学生的总分以及平均分并使用变量记录
		int sum = 0;
		for(int i = 0; i < scores.length; i++) {
			sum += scores[i];
		}
		double avg = sum*1.0 / num;
		// 打印最终的计算结果
		System.out.println("本班级学生的总分是：" + sum + "，平均分是：" + avg);
		
		System.out.println("----------------------------------------------");
		// 6.查找本班所有学生考试成绩中的最低分和最高分并打印出来
		System.out.println("原始的考试成绩是：" + Arrays.toString(scores));
		// 调用工具类中的排序方法对所有考试成绩进行从小到大的排序
		Arrays.sort(scores);
		System.out.println("排序后的考试成绩是：" + Arrays.toString(scores));
		System.out.println("最低分是：" + scores[0] + "，最高分是：" + scores[num-1]);
		
		System.out.println("----------------------------------------------");
		// 从数组中查找指定元素所在的下标位置
		System.out.println("59分在数组中的下标位置是：" + Arrays.binarySearch(scores, 59));
		System.out.println("60分在数组中的下标位置是：" + Arrays.binarySearch(scores, 60));
	}
}
```

#### 数组相关常用工具类

* static String toString(int[] a) 

功能：输出数组中的内容。

用法：`Arrays.toString(数组名)`。

* static void fill(int[] a, int Val)

功能：将参数指定元素赋值给数组中的所有元素。

用法：`Arrays.fill(数组名, 填充数)`。

* static boolean equals(int[] a, int[] b)

功能：判断两个数组的元素内容和次序是否相同，完全相同返回 `true`，反之返回 `false`。

用法：`Arrays.equals(数组名1, 数组名2)`。

* static void sort(int[] a)

功能：对数组的元素进行从小到大排序。

用法：`Arrays.sort(数组名)`。

* static int binarySearch(int[] a, int Key)

功能：从数组中查找参数指定元素所在位置。

用法：`Arrays.binarySearch(arr, 1)` 

返回值：`arr[1]` 所在位置。

各个常用工具类的使用请参考代码 `ArraysTest.java`

```java
/*
    编程实现数组工具类的使用
 */

import java.util.Arrays; 
 
public class ArraysTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个初始值为10、20、30、40、50的一维数组
		int[] arr1 = {10, 20, 30, 40, 50};
		// 2.使用原始方式打印数组中的所有元素，要求打印格式为：[10, 20, 30, 40, 50]
		System.out.print("第一个数组中的元素有：[");
		for(int i = 0; i < arr1.length; i++) {
			// 当打印的元素是最后一个元素时，则直接打印元素本身即可
			if(arr1.length-1 == i) {
				System.out.print(arr1[i]);
			} else {
				// 否则打印元素后打印逗号加空格
				System.out.print(arr1[i] + ", ");
			}
		}
		System.out.println("]");
		
		System.out.println("---------------------------------------------------");
		// 3.使用数组工具类实现数组中所有元素的打印
		System.out.println("第一个数组中的元素有：" + Arrays.toString(arr1));  // [10, 20, 30, 40, 50]
		
		System.out.println("---------------------------------------------------");
		// 4.声明一个长度为5元素类型为int类型的一维数组
		int[] arr2 = new int[5];
		System.out.println("第二个数组中的元素有：" + Arrays.toString(arr2)); // [0, 0, 0, 0, 0]
		// 使用数组工具类中的fill方法实现数组中元素的填充并打印
		// 表示使用10来填充数组arr中的每个元素，也就是给数组中每个元素赋值为10
		Arrays.fill(arr2, 10);
		System.out.println("第二个数组中的元素有：" + Arrays.toString(arr2)); // [10, 10, 10, 10, 10]
		
		System.out.println("---------------------------------------------------");
		// 5.声明一个长度为5元素类型为int类型的一维数组并初始化
		int[] arr3 = new int[5];
		Arrays.fill(arr3, 10);
		System.out.println("第三个数组中的元素有：" + Arrays.toString(arr3)); // [10, 10, 10, 10, 10]
		// 判断该数组是否与上述数组相等并打印，若相同则打印true，否则打印false
		System.out.println(Arrays.equals(arr2, arr3)); // true
		// 修改数组3中的元素值
		arr3[4] = 20;
		System.out.println("第三个数组中的元素有：" + Arrays.toString(arr3)); // [10, 10, 10, 10, 20]
		System.out.println(Arrays.equals(arr2, arr3)); // false  要求内容要相同
		arr2[3] = 20;
		System.out.println("第二个数组中的元素有：" + Arrays.toString(arr2)); // [10, 10, 10, 20, 10]
		System.out.println(Arrays.equals(arr2, arr3)); // false  要求顺序要相同
	}
}
```

### 二维数组

####二维数组的基本概念

二维数组本质上就是由多个一维数组组合成的数组，二维数组中的每一个元素都是一维数组，而一维数组中的每个元素才是数据内容。

#### 二维数组的声明及使用

在涉及多行多列的数据时，要使用二维数组。

二维数组的声明方式：

```java
数据类型[][] 数组名称 = new 数据类型[行][列]
```

也可以预先设置行数，而不设置列数：

```java
int[][] arr = new int[3][];
arr[0] = new int[3];
arr[1] = new int[4];
arr[2] = new int[5];
```

如上所示，可以先声明一个 3 行未知列数的二维数组，然后分别为 1，2，3 行设置 3，4，5列。

二维数组与一维数组的比较：

* `一维数组.length` 代表一维数组的长度，也就是一维数组中元素的个数

* `二维数组.length` 代表二维数组的长度，也就是二维数组元素的个数，而由于二维数组是由一维数组所构成的，因此二维数组的元素为一维数组，也就是说 `二维数组.length` 代表的是二维数组中一维数组的个数,也就是二维数组的行数

* `二维数组[0].length` 代表的是二维数组第一个元素的长度，也就是二维数组中第一个一维数组的长度，也就是二维数组第一行的列数

#### 二维数组的初始化

二维数组的初始化本质上为多个一维数组的初始化。

```java
数据类型[][] 数组名称 = {{元素1, 元素2, ...}, {...}}
```

二维数组的输出要使用 `双重 for 循环(外层控制行数，内存控制列数)`。

二维数组的声明及初始化请参考代码 `ArrayArrayTest.java`

```java
/*
    编程实现二维数组的声明和使用
 */
public class ArrayArrayTest {
	
	public static void main(String[] args) {
		
		// 1.声明一个具有2行3列元素类型为int类型的二维数组
		int[][] arr1 = new int[2][3];
		// 打印数组中的每个元素
		// 使用外层for循环控制打印的行数
		for(int i = 0; i < arr1.length; i++) {
			// 使用内层for循环控制打印的列数
			for(int j = 0; j < arr1[i].length; j++) {
				System.out.print(arr1[i][j] + " "); // 全是0
			}
			System.out.println();
		}
		
		System.out.println("--------------------------------------------------");
		// 2.实现二维数组中元素的赋值
		int cnt = 1;
		// 使用外层for循环控制打印的行数
		for(int i = 0; i < arr1.length; i++) {
			// 使用内层for循环控制打印的列数
			for(int j = 0; j < arr1[i].length; j++) {
				arr1[i][j] = cnt++;
			}
		}
		// 使用外层for循环控制打印的行数
		for(int i = 0; i < arr1.length; i++) {
			// 使用内层for循环控制打印的列数
			for(int j = 0; j < arr1[i].length; j++) {
				System.out.print(arr1[i][j] + " "); // 1 2 3   4 5 6
			}
			System.out.println();
		}
		
		System.out.println("--------------------------------------------------");
		// 3.二维数组元素的初始化操作
		int[][] arr2 = {{11, 22, 33, 44}, {55, 66, 77, 88}};
		// 使用外层for循环控制打印的行数
		for(int i = 0; i < arr2.length; i++) {
			// 使用内层for循环控制打印的列数
			for(int j = 0; j < arr2[i].length; j++) {
				System.out.print(arr2[i][j] + " "); // 11 22 33 44   55 66 77 88
			}
			System.out.println();
		}
		
		System.out.println("--------------------------------------------------");
		// 4.考点
		int[][] arr3 = new int[3][];
		arr3[0] = new int[3];
		arr3[1] = new int[4];
		arr3[2] = new int[5];
	}
}
```

#### 二维数组的案例

请用二维数组实现用户输入行数，生成等价行数的 `杨辉三角形`。

已知杨辉三角形所有外边数字为 1，其他位置数字为上一行当前列与前一列的和。

```
1
11
121
1331
14641
```

具体实现请参考代码 `ArrayArrayTriangleTest.java`

```java
/*
    编程使用二维数组来实现杨辉三角的生成和遍历
 */

import java.util.Scanner; 
 
public class ArrayArrayTriangleTest {
	
	public static void main(String[] args) {
		
		// 1.提示用户输入一个行数并使用变量记录
		System.out.println("请输入一个行数：");
		Scanner sc = new Scanner(System.in);
		int num = sc.nextInt();
		
		// 2.根据用户输入的行数来声明对应的二维数组
		int[][] arr = new int[num][];
		
		// 3.针对二维数组中的每个元素进行初始化，使用双重for循环
		// 使用外层for循环控制二维数组的行下标
		for(int i = 0; i < num; i++) {
			// 针对二维数组中的每一行进行内存空间的申请
			arr[i] = new int[i+1];
			// 使用内层for循环控制二维数组的列下标
			for(int j = 0; j <= i; j++) {
				// 当列下标为0或者列下标与当前行的行下标相等时，则对应位置的元素就是1
				if(0 == j || i == j) {
					arr[i][j] = 1;
				} else {
					// 否则对应位置的元素就是上一行当前列的元素加上上一行前一列的元素
					arr[i][j] = arr[i-1][j] + arr[i-1][j-1];
				}
			}
		}
		
		// 4.打印最终生成的结果
		for(int i = 0; i < num; i++) {
			for(int j = 0; j <= i; j++) {
				System.out.print(arr[i][j] + " ");
			}
			System.out.println();
		}
	}
}
```

