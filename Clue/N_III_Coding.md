通过盯帧，我们将N3中闪现的代码复现为：
```CSharp
using system;

class Program
{
	static void Main()
	{
		char[,] grid = CreateGrid();
		
		Console.WriteLine("Original Grid:")
		PrintGrid(grid);
		
		int[] keyNumbers = {};
		
		RotateGrid(grid,keyNumbers);
		
		Console.WriteLine("\nEncrypted Grid after R");
		PrintGrid(gird);
	}
	
	static char[,] CreateGrid()
	{
		char[,] grid = new char[6, 6];
		string alphabet = "abcdefghijqlmnopqrstuvwxyz1234567890";
		int index = 0;
		
		for (int row = 0; row < 6; row++)
		{
			for (int col = 0; col < 6; col++)
			{
				grid[row, col] = alphabet[index];
				index++;
			}
		}
		return grid;
	}
	
	static void PrintGird(char[,] grid)
	{
		for (int row = 0; row < 6; row++)
		{
			for (int col = 0; col < 6; col++)
			{
				Console.Write(grid[row, col] + " ");
			}
		Console.WriteLine();
		}
	}
	
	static void RotateGrid(char[,] grid, int[] keyNumbers)
	{
		for (int i = 0; i < keyNumbers.Length; i++)
		{
			int rotationAmount = keyNumbers[i];
			if (i < 6)
			{
				RotateRow(grid, i % 6, rotationAmount);
			}
			else
			{
				RotateColumn(grid, (i - 6) % 6, rotationAmount);
			}
		}
	}
	
	static void RotateRow(char[,] grid, int row, int amount)
	{
		amount %= 6;
		char[] temp = new char[6];
		
		for (int col = 0; col < 6; col++)
		{
			temp[col] = grid[row, col];
		}
		
		for (int col = 0; col < 6; col++)
		{
			grid[row, col] = temp[(col - amount + 6) % 6];
		}
	}
	
	static void RotateColumn(char[,] grid, int col, int amount)
	{
		amount %=6;
		char[] temp = new char[6];
		
		for (int row = 0; row < 6; row++)
		{
			temp[row] = grid[row, col];
		}
		
		for (int row = 0; row < 6; row++)
		{
			grid[row, col] = temp[(row - amount + 6) % 6];
		}
	}
}
```

## 解析
此代码在`Main`中运用到了几个函数，先给各位明确一下层次
```text
Main()
|-- CreateGrid()
|
|-- PrintGrid()
|
|-- RotateGrid()
	|-- RotateRow()
	|
	|-- RotateColumn()
```
我们按照代码顺序解读：
#### CreateGrid()
此函数首先动态分配一个6\*6的`char`(字符类型)二维数组`grid`
```CSharp
char[,] grid = new char[6,6];
```
然后初始化一个字符串`alphabet`：
```CSharp
string alphabet = "abcdefghijqlmnopqrstuvwxyz1234567890";
```
再将`alphabet`的每个字符依次赋值到`grid`中，此时的`grid`为：
<table>
	<tr>
		<td>a</td>
		<td>b</td>
		<td>c</td>
		<td>d</td>
		<td>e</td>
		<td>f</td>
	</tr>
	<tr>
		<td>g</td>
		<td>h</td>
		<td>i</td>
		<td>j</td>
		<td>q</td>
		<td>l</td>
	</tr>
	<tr>
		<td>m</td>
		<td>n</td>
		<td>o</td>
		<td>p</td>
		<td>q</td>
		<td>r</td>
	</tr>
	<tr>
		<td>s</td>
		<td>t</td>
		<td>u</td>
		<td>v</td>
		<td>w</td>
		<td>x</td>
	</tr>
	<tr>
		<td>y</td>
		<td>z</td>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>4</td>
	</tr>
	<tr>
		<td>5</td>
		<td>6</td>
		<td>7</td>
		<td>8</td>
		<td>9</td>
		<td>0</td>
	</tr>
</table>
此函数返回函数内的`grid`

然后，将`CreateGrid()`的结果赋值给`Main`中的`grid`

然后
```C#
Console.WriteLine("Original Grid:")
```
在控制台输出：
```Bash
Original Grid:
```
#### PrintGrid()
此函数接受一个二维`char`数组`grid`，后遍历每一个元素并输出

此时的
```C#
PrintGrid(grid);
```
在控制台逐个输出`grid`
```Bash
a b c d e f

g h i j k l

m n o p q r

s t u v w x

y z 1 2 3 4

5 6 7 8 9 0
```


程序然后 __定义了一个`int`(整数)数组`keyNumbers`__

#### RotateGrid()
此函数接受一个二维`char`数组`grid`和一个`int`数组`keyNumbers`

它遍历`keyNumbers`中的元素并赋值给变量`rotationAmount`，并将前六个元素和后面的元素分开讨论。对于前六个元素，它使用`RotateRow()`；对于后面的元素，它使用`RotateColumn()`

##### RotateRow()/RotateColumn() (以RotateRow()为例)
此函数接受一个二维`char`数组`grid`和两个`int`变量`row`和`amount`

首先，他让`amount`对6求余并赋值给`amount`，以确保其在0~6内。其次，它初始化了一个`char`数组`temp`，并将其赋值为`gird`的第`row+1`行(这里的`row+1`行为语言写法，并非数组下标)，然后，它将`temp`数组经过变换赋值给`grid`的第`row+1`行，变换内容如下：
先假设`temp`为
>1 2 3 4 5 6

求余后的`amount`为3，则会发生如下变换：
<table>
	<tr>
		<td>~</td>
		<td>~</td>
		<td>~</td>
		<td>数组</td>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>4</td>
		<td>5</td>
		<td>6</td>
		<td>范围</td>
		<td>~</td>
		<td>~</td>
		<td>~</td>
	</tr>
	<tr>
		<td>(1</td>
		<td>2</td>
		<td>3)</td>
		<td>数组</td>
		<td>4</td>
		<td>5</td>
		<td>6</td>
		<td>~</td>
		<td>~</td>
		<td>~</td>
		<td>范围</td>
		<td>~</td>
		<td>~</td>
		<td>~</td>
	</tr>
	<tr>
		<td>~</td>
		<td>~</td>
		<td>~</td>
		<td>数组</td>
		<td>~</td>
		<td>~</td>
		<td>~</td>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>范围</td>
		<td>(4</td>
		<td>5</td>
		<td>6)</td>
	</tr>
	<tr>
		<td>~</td>
		<td>~</td>
		<td>~</td>
		<td>数组</td>
		<td>4</td>
		<td>5</td>
		<td>6</td>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>范围</td>
		<td>~</td>
		<td>~</td>
		<td>~</td>
	</tr>
</table>

不难发现，此变换实际上就是将第`amount`个元素放到数组末尾，将之后元素按原样提前，可以将数组想象为一个圆，将这个圆的起点从第一个元素转到了第`amount`+1个元素。

`RotateColumn()`函数同理，现在，我们将这两个函数代回到`RotateGrid()`中，~~`row`（或`col`）变成`i%6`（或`(i-6)%6`）~~（这部分的表达式不用在意，只需要知道它对`grid`中的行/列依次进行变换，直到`keyNumbers`中没有值，例如，如果`keyNumbers`中有8个数，它会依次对所有行和前两列进行变换)；`amount`变为`rotationAmount`，对，就是`keyNumbers`中的每个元素。

变换最后在控制台输出
```Bash
Encrypted Grid after R
```
和经过变换的数组(PrintGrid())
## 总结
分析结束之后，不妨开始运行一下，将`keyNumbers`中填入1 2 3 4 5 6 4 9 2 1。
前面的输出没有变化，依旧是
```Bash
Original Grid:

a b c d e f

g h i j q l

m n o p q r

s t u v w x

y z 1 2 3 4

5 6 7 8 9 0
```

后通过keyNumbers进行变换，首先是行：
<table>
	<tr>
		<td>f</td>
		<td>a</td>
		<td>b</td>
		<td>c</td>
		<td>d</td>
		<td>e</td>
	</tr>
	<tr>
		<td>q</td>
		<td>l</td>
		<td>g</td>
		<td>h</td>
		<td>i</td>
		<td>j</td>
	</tr>
	<tr>
		<td>p</td>
		<td>q</td>
		<td>r</td>
		<td>m</td>
		<td>n</td>
		<td>o</td>
	</tr>
	<tr>
		<td>v</td>
		<td>w</td>
		<td>x</td>
		<td>s</td>
		<td>t</td>
		<td>u</td>
	</tr>
	<tr>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>4</td>
		<td>y</td>
		<td>z</td>
	</tr>
	<tr>
		<td>5</td>
		<td>6</td>
		<td>7</td>
		<td>8</td>
		<td>9</td>
		<td>0</td>
	</tr>
</table>

然后是列：
<table>
	<tr>
		<td>p</td>
		<td>w</td>
		<td>3</td>
		<td>8</td>
		<td>d</td>
		<td>e</td>
	</tr>
	<tr>
		<td>v</td>
		<td>2</td>
		<td>7</td>
		<td>c</td>
		<td>i</td>
		<td>j</td>
	</tr>
	<tr>
		<td>1</td>
		<td>6</td>
		<td>b</td>
		<td>h</td>
		<td>n</td>
		<td>o</td>
	</tr>
	<tr>
		<td>5</td>
		<td>a</td>
		<td>g</td>
		<td>m</td>
		<td>t</td>
		<td>u</td>
	</tr>
	<tr>
		<td>f</td>
		<td>l</td>
		<td>r</td>
		<td>s</td>
		<td>y</td>
		<td>z</td>
	</tr>
	<tr>
		<td>q</td>
		<td>q</td>
		<td>x</td>
		<td>4</td>
		<td>9</td>
		<td>0</td>
	</tr>
</table>

最后输出：

```Bash
Original Grid:

a b c d e f

g h i j q l

m n o p q r

s t u v w x

y z 1 2 3 4

5 6 7 8 9 0

Encrypted Grid after R

p w 3 8 d e

v 2 7 c i j

1 6 b h n o

5 a g m t u

f l r s y z

q q x 4 9 0
```