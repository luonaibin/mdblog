---
layout: post
title:  "排序算法"
date:   2015-07-14
---
<style type="text/css">
p{
	text-indent: 2em;
}
.post img {
  margin-bottom: 0rem;
}
</style>

<p class="intro">
	<span class="dropcap">排</span>序算法，重新排列表中的元素，使表中的元素满足按关键字递增或递减排列的过程。
</p>
## 一、插入排序
### 1.1 直接插入排序
**基本思想**每次将一个待排序的记录，按其关键字大小插入到前面已经排序号的子序列中，直到全部记录插入完成。

    	/**
    	 * Java插入排序算法
    	 * 
    	 * @param a
    	 */
    	public static void insertSort1(int[] a) {
    		int i, j;
    		for (i = 1; i < a.length; i++) {
    			if (a[i - 1] > a[i]) {
    				int temp = a[i];
    
    				for (j = i - 1; j >= 0 && a[j] > temp; j--) {
    					a[j + 1] = a[j];
    				}
    				a[j + 1] = temp;
    			}
    		}
    	}
    
    	public static void insertSort2(int[] a) {
    		for (int i = 1; i < a.length; i++) {
    			for (int j = i; (j>0) && (a[j] < a[j - 1]); j--) {
    				int temp = a[j];
    				a[j] = a[j - 1];
    				a[j - 1] = temp;
    			}
    		}
    	}


### 1.2 希尔排序
**基本思想**
先将待排序表分割成若干形如L[i,i+d,i=2d......i+kd]的子表，分别进行插入排序，当整个表中的元素基本有序时，在对全体记录进行一次直接插入排序。

    	public static void shellSort(int[] a) {
    		int len = a.length;
    		for (int d = len / 2; d >= 1; d = d / 2) {
    			for (int i = d; i < len; i = i + d) {
    				if (a[i] < a[i - d]) {
    					int t = a[i];
    					int j;
    					for (j = i - d; j >= 0 && t < a[j]; j = j - d) {
    						a[j + d] = a[j];
    					}
    					a[j + d] = t;
    				}
    			}
    		}
    	}


## 二、交换排序
### 2.1 冒泡排序
**基本思想**假设待排序表长n，从后往前(从前往后)两两比较相邻元素的值，若为逆序（即A[i-1]>A[i]），则交换它们，直到序列比较完。

	/**
	 * Java的冒泡排序算法 小数下沉
	 * 
	 * @param a
	 */
	public static void bubbleSort1(int[] a) {
		for (int i = 0; i < a.length; i++) {
			for (int j = a.length - 1; j > 0; j--) {
				if (a[j] < a[j - 1]) {
					int temp = a[j];
					a[j] = a[j - 1];
					a[j - 1] = temp;
				}
			}
			System.out.println(a[i]);
		}
	}

	/**
	 * Java冒泡排序 大数上冒
	 * 
	 * @param a
	 */
	public static void bubbleSort2(int[] a) {
		for (int i = a.length - 1; i > 0; i--) {
			for (int j = 0; j < i; j++) {
				if (a[j] > a[j + 1]) {
					int temp = a[j];
					a[j] = a[j + 1];
					a[j + 1] = temp;
				}
			}
		}
	}


    void BubbleSort(int[] A,int n){//另一种写法
    	boolean flag;
    	for(int i=0;i<n-1;i++){
    		flag=false;
    		for(int j=n-1;j>i;j--){
    			if(A[j-1]>A[j]){
    				swap(A[j-1],A[j]);
    				flag=true;
    			}	
    		}
    		if(flag==false){
    			returnl;
    		}	}
    }


##2.2 快速排序
**基本思想**首先选择一个轴值（即比较的基准），将待排序记录分割成独立的两部分，左侧记录的关键码均小于或等于轴值，右侧记录的关键码均大于等于轴值，然后分别对这两部分重复上述过程直到整个序列有序。

    	    public static int Partition(int[] a,int left,int right){
    		int pivot = a[left];
    		while(left<right){
    			while(left<right && pivot<=a[right]){
    				right--;
    			}
    			a[left]=a[right];
    			while(left<right && pivot>=a[left]){
    				left++;
    			}
    			a[right]=a[left];
    		}
    		a[left]=pivot;
    		return left;
    	}
    
    
    	public static void quickSort(int[] a,int start,int end){
    		if (start<end) {
    			int mid = Partition(a,start,end);
    			quickSort(a,start,mid-1);
    			quickSort(a,mid+1,end);
    		}
    	}



####快速排序1

	public class QuickSort {
		public static void quickSort(int[] arr, int low, int high) {
			if (arr == null || arr.length == 0) {
				return;
			}
			if (low >= high) {
				return;
			}
			int middle = (low + high) / 2;
			int pivot = arr[middle];

			int i = low, j = high;
			while (i <= j) {
				while (arr[i] < pivot) {
					i++;
				}
				while (arr[j] > pivot) {
					j--;
				}
				if (i <= j) {
					int temp = arr[i];
					arr[i++] = arr[j];
					arr[j--] = temp;
				}
			}
			/*System.out.println("i=" + i);
			System.out.println("j=" + j);*/
			if (low < j) {
				quickSort(arr, low, j);
			}
			if (high > i) {
				quickSort(arr, i, high);
			}
		}

		public static void main(String[] args) {
			int[] a = { 9, 2, 7, 3, 7, 10 };
			quickSort(a, 0, a.length - 1);
			for (int k : a) {
				System.out.print(k+" ");
			}
		}
	}
####快速排序2

	public class QuickSort2 {
		private final static int CUTOFF = 10;

		public static void swapReferences(int[] a, int b, int c) {
			int tmp = a[b];
			a[b] = a[c];
			a[c] = tmp;

		}

		public static int median3(int[] a, int left, int right) {
			int center = (left + right) / 2;
			if (a[center] < a[left]) {
				swapReferences(a, left, center);
			}
			if (a[right] < a[left]) {
				swapReferences(a, left, right);
			}
			if (a[right] < a[center]) {
				swapReferences(a, center, right);
			}

			swapReferences(a, center, right - 1);
			return a[right - 1];
		}

		public static void quickSort(int[] a, int left, int right) {
			// if (left + CUTOFF <= right) {
			int pivot = median3(a, left, right);

			int i = left, j = right - 1;
			// System.out.println(a[i] + "----" + a[j]);
			for (;;) {
				while (a[++i] < pivot)
					;
				while (pivot < a[--j])
					;
				if (i >= j)
					break;
				swapReferences(a, i, j);
			}
			swapReferences(a, i, right - 1);
			// System.out.println(a[i]);
			quickSort(a, left, i - 1);
			quickSort(a, i + 1, right);
			// } else {
			// insertionSort(a, left, right);
			// }
		}

		public static void quickSort(int[] a) {
			quickSort(a, 0, a.length - 1);
		}

		public static void insertionSort(int[] a) {
			int j;
			for (int p = 1; p < a.length; p++) {
				int tmp = a[p];
				for (j = p; j > 0 && tmp < a[j - 1]; j--) {
					a[j] = a[j - 1];
				}
				a[j] = tmp;
			}
		}

		public static void insertionSort(int[] a, int left, int right) {
			insertionSort(a);
		}

		public static void main(String[] args) {
			int[] array = { 12, 234, 43, 123, 75, 87, 8, 3, 49, 99, 101, 45, 10,
					333 };
			for (int k : array) {
				System.out.print(k + "--");
			}
			System.out.println();
			int pivot = median3(array, 0, array.length - 1);
			System.out.println(pivot);
			for (int k : array) {
				System.out.print(k + "--");
			}
			System.out.println();
			System.out.println("------------------------");
			quickSort(array);
			for (int k : array) {
				System.out.print(k + "--");
			}
		}
	}

####快速排序3

	public class QuickSort3 {

		public static void quicksort(int[] a) {
			quicksort(a, 0, a.length - 1);
		}

		public static void swapReferences(int[] a, int index1, int index2) {
			int tmp = a[index1];
			a[index1] = a[index2];
			a[index2] = tmp;
		}

		private static void quicksort(int a[], int lo0, int hi0) {
			int lo = lo0;
			int hi = hi0;
			int mid;

			if (hi0 > lo0) {

				/*
				 * Arbitrarily establishing partition element as the midpoint of the
				 * array.
				 */
				swapReferences(a, lo0, (lo0 + hi0) / 2);
				mid = a[(lo0 + hi0) / 2];

				// loop through the array until indices cross
				while (lo <= hi) {
					/*
					 * find the first element that is greater than or equal to the
					 * partition element starting from the left Index.
					 */
					while ((lo < hi0) && (a[lo] < mid))
						++lo;

					/*
					 * find an element that is smaller than or equal to the
					 * partition element starting from the right Index.
					 */
					while ((hi > lo0) && (a[hi] > mid))
						--hi;

					// if the indexes have not crossed, swap
					if (lo <= hi) {
						swapReferences(a, lo, hi);
						++lo;
						--hi;
					}
				}

				/*
				 * If the right index has not reached the left side of array must
				 * now sort the left partition.
				 */
				if (lo0 < hi)
					quicksort(a, lo0, hi);

				/*
				 * If the left index has not reached the right side of array must
				 * now sort the right partition.
				 */
				if (lo < hi0)
					quicksort(a, lo, hi0);

			}
		}

		private static void insertionSort(int[] a, int low, int high) {
			for (int p = low + 1; p <= high; p++) {
				int tmp = a[p];
				int j;

				for (j = p; j > low && (tmp < a[j - 1]); j--)
					a[j] = a[j - 1];
				a[j] = tmp;
			}
		}

		public static void main(String[] args) {
			int[] a = { 12, 234, 43, 123, 75, 87, 8, 3, 49, 99, 101, 45, 10, 333 };
			quicksort(a);
			for (int k : a) {
				System.out.println(k);
			}
		}
	}

####快速排序4

	public class QuickSort4 {

		public static void quicksort(int[] a) {
			quicksort(a, 0, a.length - 1);
		}

		private static final int CUTOFF = 10;

		public static final void swapReferences(int[] a, int index1, int index2) {
			int tmp = a[index1];
			a[index1] = a[index2];
			a[index2] = tmp;
		}

		private static void quicksort(int[] a, int low, int high) {
			if (low + CUTOFF > high)
				insertionSort(a, low, high);
			else {
				 //Sort low, middle, high
				int middle = (low + high) / 2;
				if (a[middle] < a[low])
					swapReferences(a, low, middle);
				if (a[high] < a[low])
					swapReferences(a, low, high);
				if (a[high] < a[middle])
					swapReferences(a, middle, high);

				// Place pivot at position high - 1
				swapReferences(a, middle, high - 1);
				int pivot = a[high - 1];

				// Begin partitioning
				int i, j;
				for (i = low, j = high - 1;;) {
					while (a[++i] < pivot)
						;
					while (pivot < a[--j])
						;
					if (i >= j)
						break;
					swapReferences(a, i, j);
				}

				// Restore pivot
				swapReferences(a, i, high - 1);

				quicksort(a, low, i - 1); // Sort small elements
				quicksort(a, i + 1, high); // Sort large elements
			}
		}

		private static void insertionSort(int[] a, int low, int high) {
			for (int p = low + 1; p <= high; p++) {
				int tmp = a[p];
				int j;

				for (j = p; j > low && tmp < a[j - 1]; j--)
					a[j] = a[j - 1];
				a[j] = tmp;
			}
		}

		public static void main(String[] args) {
			int[] array = { 12, 234, 43, 123, 75, 87, 8, 3, 49, 99, 101, 45, 10,
					333 };
			for (int k : array) {
				System.out.print(k + " ");
			}
			System.out.println();
			quicksort(array);
			for (int k : array) {
				System.out.print(k + " ");
			}
		}
	}

	
## 三、选择排序
### 3.1 简单选择排序
**基本思想**每一趟（例如第i趟）在后面n-i+1个待排序元素中选取关键字最小的元素，作为有序子序列的第i个元素，直到第n-1趟做完，待排序元素只剩下1个，就不用再选了。
>     	public static void selectSort(int[] a, int n) {
>     		int min;
>     		for (int i = 0; i < n - 1; i++) {
>     			min = i;
>     			for (int j = i + 1; j < n; j++) {
>     				if (a[j] < a[min]) {
>     					min = j;
>     				}
>     			}
>     			if (min != i) {
>     				int t = a[i];
>     				a[i] = a[min];
>     				a[min] = t;
>     			}
>     		}
>     	}
> 

			/**
			 * 选择排序
			 * 
			 * @param a
			 */
			public static void selectSort1(int[] a) {
				for (int i = 0; i < a.length; i++) {
					for (int j = i + 1; j < a.length; j++) {
						if (a[i] > a[j]) {
							swap(a, i, j);
						}
					}
				}
			}
		
			public static void swap(int[] a, int i, int j) {
				a[i] = a[i] ^ a[j];
				a[j] = a[i] ^ a[j];
				a[i] = a[i] ^ a[j];
			}
		
			public static void selectSort2(int[] a, int n) {
				int min;
				for (int i = 0; i < n - 1; i++) {
					min = i;
					for (int j = i + 1; j < n; j++) {
						if (a[j] < a[min]) {
							min = j;
						}
					}
					if (min != i) {
						swap(a, i, min);
					}
				}
			}



### 3.2 堆排序
**基本思想**堆排序是一种树形选择排序，它的特点是：在排序过程中，将L[1...n]视为一颗完全二叉树的顺序存储结构，利用完全二叉树中双亲结点和孩子结点之间的内在关系，在当前无序区中选择关键字最大（或最小）的元素。


	/**
	 * 堆排序算法
	 * @author lnb
	 *
	 */
	public class HeapSort {
		public static int N;

		public static void MAX_HEAPITY(int[] A, int i) {
			int l = i * 2;
			int r = i * 2 + 1;
			int largest;
			if (l <= N && A[l] > A[i]) {
				largest = l;
			} else {
				largest = i;
			}
			if (r <= N && A[r] > A[i]) {
				largest = r;
			}
			if (largest != i) {
				exchange(A, i, largest);
				MAX_HEAPITY(A, largest);
			}
		}

		public static void exchange(int[] A, int i, int j) {
			A[i] = A[i] ^ A[j];
			A[j] = A[i] ^ A[j];
			A[i] = A[i] ^ A[j];
		}

		public static void BUILD_MAX_HEAP(int[] A) {
			N = A.length - 1;
			for (int i = N / 2; i >= 0; i--) {
				MAX_HEAPITY(A, i);
			}
		}

		public static void HEAPSORT(int[] A) {
			BUILD_MAX_HEAP(A);
			for (int i = N; i > 0; i--) {
				exchange(A, 0, i);
				N--;
				MAX_HEAPITY(A, 0);
			}
		}

		public static void main(String[] args) {
			int[] a = { 3, 5, 1, 9, 6, 0, 4 };
			for (int v : a) {
				System.out.print(v + " ");
			}
			System.out.println();
			HEAPSORT(a);
			for (int v : a) {
				System.out.print(v + " ");
			}
		}
	}


## 四、归并排序

### 4.1 二路归并排序
**基本思想**归并的含义是将两个或两个以上的有序表组合成一个新的有序表。假定待排序表含有n个记录，则可以视为n个有序的子表，每个子表的长度为1，然后两两归并，得到[n/2]
个长度为2或1的有序表；再两两归并，。。。如此重复，直到合并成一个长度为n的有序表为止。这种排序算法为二路归并排序

	public class MergeSort {
		public static void mergeSort1(int[] a, int low, int high) {
			if (low < high) {
				int mid = (low + high) / 2;
				mergeSort1(a, low, mid);
				mergeSort1(a, mid + 1, high);
				merge1(a, low, mid, high);
			}
		}

		public static void merge1(int[] a, int low, int mid, int high) {
			int[] b = new int[a.length];
			for (int k = low; k <= high; k++) {
				b[k] = a[k];
			}
			int i, j, k;
			for (i = low, j = mid + 1, k = i; i <= mid && j <= high; k++) {
				if (b[i] < b[j]) {
					a[k] = b[i++];
				} else {
					a[k] = b[j++];
				}
			}
			while (i <= mid) {
				a[k++] = b[i++];
			}
			while (j <= high) {
				a[k++] = b[j++];
			}
		}

		// ------------------
		public static void mergeSort(int[] a) {
			int[] tmpArray = new int[a.length];
			mergeSort(a, tmpArray, 0, a.length - 1);
		}

		public static void mergeSort(int[] a, int[] tmpArray, int left, int right) {
			if (left < right) {
				int center = (left + right) / 2;
				mergeSort(a, tmpArray, left, center);
				mergeSort(a, tmpArray, center + 1, right);
				merge(a, tmpArray, left, center + 1, right);
			}
		}

		public static void merge(int[] a, int[] tmpArray, int leftPos, int rightPos, int rightEnd) {
			int leftEnd = rightPos - 1;
			int tmpPos = leftPos;
			int numElement = rightEnd - leftPos + 1;
			while (leftPos <= leftEnd && rightPos <= rightEnd) {
				if (a[leftPos] <= a[rightPos]) {
					tmpArray[tmpPos++] = a[leftPos++];
				} else {
					tmpArray[tmpPos++] = a[rightPos++];
				}
			}
			while (leftPos <= leftEnd) {
				tmpArray[tmpPos++] = a[leftPos++];
			}
			while (rightPos <= rightEnd) {
				tmpArray[tmpPos++] = a[rightPos++];
			}
			for (int i = 0; i < numElement; i++, rightEnd--) {
				a[rightEnd] = tmpArray[rightEnd];
			}
		}

		// -------------------
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int[] a = { 4, 2, 1, 6, 3, 6, 0, -5, 1, 1 };
			mergeSort(a);
			for (int b : a) {
				System.out.print(b + " ");
			}
		}

	}


### 4.2 多路归并排序 