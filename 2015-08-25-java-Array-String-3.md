---
layout:     post
title:      "剑指offer-Java实现(41--66)"
date:       2015-08-28
---

<style type="text/css">
p{
	text-indent: 2em;
}
.post img {
  margin-bottom: 0rem;
}
</style>

--------

### 四十、 数组中只出现一次的数字
**题目描述**

一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

		//num1,num2分别为长度为1的数组。传出参数
		//将num1[0],num2[0]设置为返回结果
		public class Solution {
			public void FindNumsAppearOnce(int [] array,int num1[] , int num2[]) {
				if(array==null || array.length<2){
					return;
				}
				int resultExclusiveOR = 0;
				for(int i=0;i<array.length;i++){
					resultExclusiveOR ^= array[i];
				}
				int index=FindFirstBitIs1(resultExclusiveOR);
				num1[0]=0;
				num2[0]=0;
				for(int j=0;j<array.length;j++){
					if(IsBit1(array[j],index)){
						num1[0]^=array[j];
					}else{
						num2[0]^=array[j];
					}
				}
			}
			 
			public static int FindFirstBitIs1(int num){
				int indexBit=0;
				while((num&1)==0){
					num=num>>1;
					indexBit++;
				}
				return indexBit;
			}
			 
			public static boolean IsBit1(int num,int indexBit){
				num=num>>indexBit;
				return (num & 1)==1;
			}
					   
		}

### 四十一、 和为S的连续正数序列

### 四十二、 和为S的两个数字
**题目描述**

输入一个递增排序的数组和一个数字S，在数组中查找两个数，是的他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。 
输出描述:
对应每个测试案例，输出两个数，小的先输出。

		import java.util.ArrayList;
		public class Solution {
			public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
				ArrayList<Integer> list=new ArrayList<>();
				int len=array.length;
				int i=0;
				int j=len-1;
				int product=0;
				int min=sum*sum;
				for(;i<j;){
					if(array[i]+array[j]>sum){
						j--;
					}else if (array[i]+array[j]<sum) {
						i++;
					}else {
		//              list.clear();
						product=array[i]*array[j];
						if(min>product){
							min=product;
							list.add(array[i]);
							list.add(array[j]);
						}
						i++;
					}
				}
				return list;
			}
		}

### 四十三、 左旋转字符串
**题目描述**

汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

		public class Solution {
			public String LeftRotateString(String str,int n) {
				if(str==null || str.length()<n){
					return "";
				}
				char[] ch=str.toCharArray();
				while (n > 0) {
					rotate(ch);
					n--;
				}
				return String.valueOf(ch);
			}
			public  void rotate(char[] ch) {
		//      char[] ch = str.toCharArray();
				char c = ch[0];
				for (int i = 1; i < ch.length; i++) {
					ch[i - 1] = ch[i];
				}
				ch[ch.length - 1] = c;
			}
		}

### 四十四、 翻转单词顺序列
**题目描述**

JOBDU最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

		public class Solution {
			public String ReverseSentence(String str) {
				if(str == null || str == "" || str.length() == 0)
					return str;
				String[] s=str.split(" ");
				if(s.length <= 1)
					return str;
				int i=0;
				int j=s.length-1;
				while(i<j){
					String st=s[i];
					s[i++]=s[j];
					s[j--]=st;
				}
				StringBuffer sb=new StringBuffer();
				for(int k=0;k<s.length-1;k++){
					sb.append(s[k]+" ");
				}
				sb.append(s[s.length-1]);
				return sb.toString();
			}
		}

### 四十五、 扑克牌顺子

### 四十六、 孩子们的游戏(圆圈中最后剩下的数)

### 四十七、 求1+2+3+...+n
**题目描述**
求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

		public class Solution {
			public int Sum_Solution(int n) {
				return (1+n)*n/2;
			}
		}

### 四十八、 不用加减乘除做加法
**题目描述**

写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。

		public class Solution {
			public int Add(int a,int b) {
				if(b==0)
					return a;
				int sum,carry;
				sum=a^b;
				carry=(a&b)<<1;
				return Add(sum,carry);
			}
		}

### 四十九、 把字符串转换成整数
**题目描述**
将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。

		public class Solution {
			public int StrToInt(String str) {
				if (str.length() == 0) {
					return 0;
				}
				boolean flag = true;
				long num = 0;
				if (str != null) {
					char[] cstr = str.toCharArray();
					int i = 0;
					if (cstr[i] == '+') {
						i++;
					} else if (cstr[i] == '-') {
						i++;
						flag = false;
					}
					while (i < str.length() && cstr[i] != '\0') {
						if (cstr[i] >= '0' && cstr[i] <= '9') {
							num = num * 10 + (cstr[i] - '0');
		 
							i++;
						} else {
							num = 0;
							break;
						}
					}
					if (!flag) {
						num = 0 - num;
					}
					if (num > Integer.MAX_VALUE) {
						return 0;
					}
					if (num < Integer.MIN_VALUE) {
						return 0;
					}
				}
				return (int)num;
			}
		}

### 五十、 数组中重复的数字

### 五十一、 构建乘积数组
**题目描述**
给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。

		import java.util.ArrayList;
		public class Solution {
			int[] multiply(int[] A) {
				int n = A.length;
				int[] left = new int[n];
				int[] right = new int[n];
				left[0] = 1;
				right[n - 1] = 1;
				int[] result = new int[n];
				for (int i = 0; i < n - 1; ++i) {
					left[i + 1] = left[i] * A[i];
					right[n - 2 - i] = right[n - 1 - i] * A[n - 1 - i];
				}
				for (int i = 0; i < n; i++) {
					result[i] = left[i] * right[i];
				}
				return result;
			}
		}

### 五十二、 正则表达式匹配

### 五十三、 表示数值的字符串

### 五十四、 字符流中第一个不重复的字符

### 五十五、 链表中环的入口结点

### 五十六、 删除链表中重复的结点

### 五十七、 二叉树的下一个结点

### 五十八、 对称的二叉树

### 五十九、 按之字形顺序打印二叉树
 
### 六十、 把二叉树打印成多行

### 六十一、 序列化二叉树

### 六十二、 二叉搜索树的第k个结点

### 六十三、 数据流中的中位数

### 六十四、 滑动窗口的最大值

### 六十五、 矩阵中的路径

### 六十六、 机器人的运动范围







