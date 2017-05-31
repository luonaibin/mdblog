---
layout:     post
title:      "数组分割"
date:       2015-08-26
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
	<span class="dropcap">数组分割</span>有一个无序，元素个数为2n的正整数数组，要求：如何能把这个数组分割为元素个数为n的两个数组，并使子数组的和最接近。
</p>
--------

package com.jinterview;

public class ArraySeg {
	public static void TArraySeg(int[] a) {
		int alen = a.length;
		int n = alen / 2;
		if (alen % 2 == 1 || a == null) {
			return;
		}
		int sum = 0;
		for (int s : a) {
			sum += s;
		}
		sort(a);
		int[] sub1 = new int[n];
		int[] sub2 = new int[n];
		int i = 0, j = 0, m = 0;
		while (i < alen) {
			if (i % 2 == 0) {
				sub1[j++] = a[i++];
			} else {
				sub2[m++] = a[i++];
			}
		}

		for (int k = 0; k < n; k++) {
			System.out.print(sub1[k]+" ");
		}
		System.out.println();
		for (int k = 0; k < n; k++) {
			System.out.print(sub2[k]+" ");
		}
		System.out.println();
		System.out.println("-------------");

		// int x = sub1[1];
		// sub1[1] = sub2[1];
		// sub2[1] = x;
		// for (int k = 0; k < n; k++) {
		// System.out.print(sub1[k]);
		// }
		// System.out.println();
		// for (int k = 0; k < n; k++) {
		// System.out.print(sub2[k]);
		// }
		// System.out.println();
		// System.out.println("-------------");

		int sub1sum = 0, sub2sum = 0;
		// for (int k = 0; k < n; k++) {
		// sub1sum += sub1[k];
		// sub2sum += sub2[k];
		// }
		int div;
		for (int p = 0; p < alen; p++) {
			sub1sum = sub2sum = 0;
			for (int k = 0; k < n; k++) {
				sub1sum += sub1[k];
				sub2sum += sub2[k];
			}
			div = Math.abs(sub1sum - sub2sum);
			for (int k = 0; k < n; k++) {

				int s1 = sub1sum - sub1[k] + sub2[k];
				int s2 = sum - s1;
				if (Math.abs(s1 - s2) < div) {
					div = Math.abs(s1 - s2);
					int t = sub1[k];
					sub1[k] = sub2[k];
					sub2[k] = t;
				}
			}
		}

		for (int k = 0; k < n; k++) {
			System.out.print(sub1[k]+" ");
		}
		System.out.println();
		for (int k = 0; k < n; k++) {
			System.out.print(sub2[k]+" ");
		}
	}

	public static void sort(int[] a) {
		for (int i = 0; i < a.length; i++) {
			for (int j = a.length - 1; j > 0; j--) {
				if (a[j] < a[j - 1]) {
					int t = a[j - 1];
					a[j - 1] = a[j];
					a[j] = t;
				}
			}
		}
	}

	public static void main(String[] args) {
		int[] a = { 11, 7, 2, 9, 15, 21 };
		sort(a);
		TArraySeg(a);
		// for (int k : a) {
		// System.out.print(k + " ");
		// }
	}
}

