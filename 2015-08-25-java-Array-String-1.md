# 剑指offer-Java实现(1--20)

_2015-08-28_

<style type="text/css">
p{
	text-indent: 2em;
}
.post img {
  margin-bottom: 0rem;
}
</style>


### 一、二维数组中的查找

**题目描述**
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
	
	/**
			 * Java二维数组中的查找
			 * 
			 * @param array
			 * @param target
			 */
		public class Solution {
			public boolean Find(int [][] array,int target) {
				int m = array.length;
				int n = array[0].length;
				for (int i = 0; i < m; i++) {
					for (int j = 0; j < n; j++) {
						if(array[i][j]==target){
							return true;
						}
					}
				}
				return false;
			}
		}
	
	
### 二、替换空格
**题目描述**
请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

		public class Solution {
			public String replaceSpace(StringBuffer str) {
				char[] ch=str.toString().toCharArray();
				String s="";
				for(int i=0;i<ch.length;i++){
					if(ch[i]==' '){
						s+="%20";
					}else{
						s+=ch[i];
					}
				}
				return s;
			}
		}

### 三、从尾到头打印链表
**题目描述**
输入一个链表，从尾到头打印链表每个节点的值。

		/**
		*    public class ListNode {
		*        int val;
		*        ListNode next = null;
		*
		*        ListNode(int val) {
		*            this.val = val;
		*        }
		*    }
		*
		*/
		import java.util.ArrayList;
		import java.util.Iterator;
		import java.util.Stack;
		public class Solution {
			public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
				Stack<Integer> stack = new Stack();
				ArrayList<Integer> alist = new ArrayList();
				if (listNode == null) {
					return alist;
				}
				ListNode p = listNode;
				while (p != null) {
					stack.push(p.val);
					p = p.next;
				}
				Iterator<Integer> it = stack.iterator();
				while (it.hasNext()) {
					alist.add(stack.pop());
				}
				return alist;
			}
		}


	    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
	        ArrayList<Integer> alist = new ArrayList<>();
	        if (listNode != null) {
	            if (listNode.next != null) {
	                alist=printListFromTailToHead(listNode.next);
	            }
	            alist.add(listNode.val);
	        }
	        return alist;
	     
	    }

### 四、重建二叉树
**题目描述**输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。 


    public TreeNode reConstructBinaryTree(int[] pre, int[] in) {
        return reConstructBinaryTree(pre, 0, pre.length - 1, in, 0, in.length - 1);
    }
 
    public TreeNode reConstructBinaryTree(int[] pre, int pstart, int pend, int[] in, int istart, int iend) {
        if (pre == null || in == null) {
            return null;
        }
        if (pstart > pend || istart > iend) {
            return null;
        }
        TreeNode pNode = new TreeNode(pre[pstart]);
        pNode.left = null;
        pNode.right = null;
        for (int i = istart; i <= iend; i++) {
            if (in[i] == pre[pstart]) {
                pNode.left = reConstructBinaryTree(pre, pstart + 1, pstart + i - istart, in, istart, i - 1);
                pNode.right = reConstructBinaryTree(pre, i-istart+pstart + 1, pend, in, i + 1, iend);
            }
 
        }
        return pNode;
    }


### 五、用两个栈实现队列
**题目描述**
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

		import java.util.Stack;
		import java.util.Iterator;
		 
		public class Solution {
			Stack<Integer> stack1 = new Stack<Integer>();
			Stack<Integer> stack2 = new Stack<Integer>();
			 
			public void push(int node) {   
					stack1.push(node);
				 
			}
		 
			public int pop() {
				Iterator<Integer> it1=stack1.iterator();
				//Iterator<Integer> it2=stack2.iterator();
				if (!stack2.isEmpty()) {
					return stack2.pop();
				}else {
					if (!stack1.isEmpty()) {
						while(it1.hasNext()){
							stack2.push(stack1.pop());
						}
						return stack2.pop();
					}else {
						return -1;
					}
				}
			}
		}
### 六、旋转数组的最小数字
**题目描述**
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减序列的一个旋转，输出旋转数组的最小元素。例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。

		import java.util.ArrayList;
		public class Solution {
			public int minNumberInRotateArray(int [] array) {
				if(array == null || array.length==0){
					return 0;
				}
				int min = array[0];
				for(int i=1;i<array.length;i++){
					if(array[i]<min){
						min=array[i];
					}
				}
				return min;
			}
		}

### 七、斐波那契数列
**题目描述**
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。

		public class Solution {
			public int Fibonacci(int n) {
				int[] dp=new int[3];
				dp[0]=0;   
				dp[1]=1;
				dp[2]=1;
				if(n<2){
					return dp[n];
				}
				for(int i=2;i<=n;i++){
					dp[2]=dp[0]+dp[1];
					dp[0]=dp[1];
					dp[1]=dp[2];
				}
				return dp[2];
			}
		}

### 八、 跳台阶
**题目描述**
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

		public class Solution {
			public int JumpFloor(int target) {
				int[] dp=new int[3];
				dp[0]=0;
				dp[1]=1;
				dp[2]=2;
				if(target<=2){
					return dp[target];
				}
				for(int i=3;i<=target;i++){
					dp[0]=dp[1]+dp[2];
					dp[1]=dp[2];
					dp[2]=dp[0];
					System.out.println("dp[2]"+dp[2]);
				}
				return dp[2];
			}
		}

### 九、 变态跳台阶
**题目描述**
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。


		public class Solution {
			public int JumpFloorII(int target) {
				int[] fib=new int[target+1];
				fib[0]=0;
				fib[1]=1;
				for(int i=2;i<=target;i++){
					fib[i]=2*fib[i-1];
				}
				return fib[target];
			}
		}

### 十、 矩形覆盖
**题目描述**我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

		public class Solution {
			public int RectCover(int target) {
				int[] fib=new int[target+1];
				fib[0]=1;
				fib[1]=1;
			   // fib[2]=2;
				for(int i=2;i<=target;i++){
					fib[i]=fib[i-1]+fib[i-2];
				}
				return fib[target];
			}
		}


### 十一、 二进制中1的个数
**题目描述**输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

    public int NumberOf1(int n) {
        int count=0;
        while(n!=0){
            n=n&(n-1);
            count++;
        }
        return count;
    }

### 十二、 数值的整数次方
**题目描述**给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

		class Solution {
		public:
			double Power(double base, int exponent) {
				if(base==0 && exponent!=0){
					return 0;
				}
				if(exponent<0){
					return 1/Pow(base,-exponent);
				}else{
					return Pow(base, exponent);
				}
			}
			 
			double Pow(double x, int n){
				if(n==0){
					return 1.0;
				}
				double v=Pow(x,n/2);
				if(n%2==0){
					return v*v;
				}else{
					return v*v*x;
				}
			}
		};


### 十三、 调整数组顺序使其奇数位于偶数前面
**题目描述**输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

		import java.util.LinkedList;
		import java.util.Queue;
		public class Solution {
			public  void reOrderArray(int[] array) {
				Queue<Integer> odd_queue = new LinkedList<>();// 奇数列
				Queue<Integer> even_queue = new LinkedList<>();// 偶数列
				for (int i = 0; i < array.length; i++) {
					if (isOdd(array[i])) {
						odd_queue.add(array[i]);
					} else {
						even_queue.add(array[i]);
					}
				}
				int i = 0;
				while (!odd_queue.isEmpty()) {
					array[i++] = odd_queue.poll();
				}
				while (!even_queue.isEmpty()) {
					array[i++] = even_queue.poll();
				}
			}
		 
			public  boolean isOdd(int x) {// 判断是否是奇数
				if (x % 2 == 1) {
					return true;
				} else {
					return false;
				}
			}
		}


### 十四、 链表中倒数第k个结点
**题目描述**输入一个链表，输出该链表中倒数第k个结点。

		/*
		public class ListNode {
			int val;
			ListNode next = null;
		 
			ListNode(int val) {
				this.val = val;
			}
		}
		*/
		public class Solution {
			public ListNode FindKthToTail(ListNode head,int k) {
				if(head==null || k==0){
					return null;
				}
				ListNode p=head;
				ListNode q=head;
				while(k-->1){
					q=q.next;
					if(q==null){
						return null;
					}
				}
				while(q.next!=null){
					q=q.next;
					p=p.next;
				}
				return p;
			}
		}

### 十五、 反转链表
**题目描述**输入一个链表，反转链表后，输出链表的所有元素。

		/*public class ListNode {
			int val;
			ListNode next = null;
		 
			ListNode(int val) {
				this.val = val;
			}
		}*/
		public class Solution {
			public ListNode ReverseList(ListNode head) {
		if(head==null){
					return null;
				}
				ListNode p1=head;
				ListNode p2=p1.next;
				ListNode p3;
				while(p2!=null){
					p3=p2.next;
					p2.next=p1;
					p1=p2;
					p2=p3;
				}
				head.next=null;
				head=p1;
				return head;
			}
		}

### 十六、 合并两个排序的链表
**题目描述**输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

		/*
		public class ListNode {
			int val;
			ListNode next = null;
		 
			ListNode(int val) {
				this.val = val;
			}
		}
		*/
		public class Solution {
			public ListNode Merge(ListNode list1,ListNode list2) {
				if (list1 == null) {
					return list2;
				} else if (list2 == null) {
					return list1;
				}
		 
				ListNode p = null;
				if (list1.val < list2.val) {
					p = list1;
					p.next = Merge(list1.next, list2);
				} else {
					p = list2;
					p.next = Merge(list1, list2.next);
				}
				return p;
			}
		}

### 十七、 树的子结构
**题目描述**
输入两颗二叉树A，B，判断B是不是A的子结构。

		/**
		public class TreeNode {
		    int val = 0;
		    TreeNode left = null;
		    TreeNode right = null;
		 
		    public TreeNode(int val) {
		        this.val = val;
		 
		    }
		 
		}
	*/
	public class Solution {
    public boolean HasSubtree(TreeNode root1, TreeNode root2) {
        boolean rflag = false;
        if (root1 != null && root2 != null) {
            if (root1.val == root2.val) {
                rflag = DoesTree1HaveTree2(root1, root2);
            }
            if (!rflag) {
                rflag = HasSubtree(root1.left, root2);
            }
            if (!rflag) {
                rflag = HasSubtree(root1.right, root2);
            }
        }
        return rflag;
    }
 
    public static boolean DoesTree1HaveTree2(TreeNode root1, TreeNode root2) {
        if (root2 == null) {
            return true;
        }
        if (root1 == null) {
            return false;
        }
        if (root1.val != root2.val) {
            return false;
        }
        return DoesTree1HaveTree2(root1.left, root2.left) && DoesTree1HaveTree2(root1.right, root2.right);
    }
}

### 十八、 二叉树的镜像
**题目描述**
操作给定的二叉树，将其变换为源二叉树的镜像。 
输入描述:
二叉树的镜像定义：源二叉树 
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
		
		
			/*
		public class TreeNode {
			int val = 0;
			TreeNode left = null;
			TreeNode right = null;
		 
			public TreeNode(int val) {
				this.val = val;
		 
			}
		 
		}
		*/
		public class Solution {
			public void Mirror(TreeNode root) {
				if (null == root) {
					return;
				}
				if (null == root.left && null == root.right) {
					return;
				}
				TreeNode leftTmp = root.left;
				root.left = root.right;
				root.right = leftTmp;
				Mirror(root.left);
				Mirror(root.right);
			}
		}	

### 十九、 顺时针打印矩阵

**题目描述**
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.


	import java.util.ArrayList;
	public class Solution {
    public ArrayList<Integer> printMatrix(int[][] matrix) {
        if (matrix == null) {
            return null;
        }
        ArrayList<Integer> alist = new ArrayList<>();
        int rows = matrix.length;
        int columns = matrix[0].length;
        int start = 0;
        while (rows > start * 2 && columns > start * 2) {
            alist.addAll(printMatrixCircle(matrix, columns, rows, start));
            start++;
        }
        return alist;
    }
 
    public static ArrayList<Integer> printMatrixCircle(int[][] matrix, int columns, int rows, int start) {
        ArrayList<Integer> alist = new ArrayList<>();
        int endX = columns - 1 - start;
        int endY = rows - 1 - start;
        for (int i = start; i <= endX; ++i) {
            alist.add(matrix[start][i]);
        }
        if (start < endY) {
            for (int i = start + 1; i <= endY; ++i) {
                alist.add(matrix[i][endX]);
            }
        }
 
        if (start < endX && start < endY) {
            for (int i = endX - 1; i >= start; i--) {
                alist.add(matrix[endY][i]);
            }
        }
        if (start < endX && start < endY - 1) {
            for (int i = endY - 1; i >= start + 1; i--) {
                alist.add(matrix[i][start]);
            }
        }
        return alist;
    }
}
### 二十、 包含min函数的栈

**题目描述**
定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数。


	import java.util.Stack;
	import java.util.ArrayList;
	public class Solution {
	     
    ArrayList<Integer> list = new ArrayList<>();
    int i = 0;
 
    public void push(int node) {
        list.add(node);
        i++;
    }
 
    public void pop() {
        list.remove(i - 1);
        i--;
    }
 
    public int top() {
        return list.get((i--) - 1);
    }
 
    public int min() {
        int min = list.get(0);
        for (int i = 1; i < list.size(); i++) {
            if (min > list.get(i)) {
                min = list.get(i);
            }
        }
        return min;
    }
	}
