---
layout: post
title: 8 Basic sorting algorithm
subtitle: This is basic 8 sorting algorithm
categories: algorithm
tags: [algorithm] [sorting]
---

There are various kinds of algorithm for sorting. So what do we use most and why?

### Bubble Sort

```java
    public static void bubbleSort(int[] nums) {
        for (int i = 0; i < nums.length - 1; ++i) {
            for (int l = 0; l < nums.length - i - 1; ++l) {
            	// Swap
                if (nums[l] > nums[l + 1]) {
                    int temp = nums[l];
                    nums[l] = nums[l + 1];
                    nums[l + 1] = temp;
                }
            }
        }
    }
```

### Selection Sort
|: average :||: worst :||: memory :||: stability :|
|:----------||---------||----------||-------------|
|:  $n^2$  :||: $n^2$ :||: O(1) :||: X :|

* one of the simple sorting algorithm
* iterate the array and repeat the following process 
	+ start from `0`, find the minimum value and swap with element `0`
	+ start from `1`, find the minimum value and swap with element `1`
	+ start from `2`, find the minimum value and swap with element `2` 
	+ repeat until `n - 1` element...
* because the algorithm is all about selecting minimum value, it is called **selection sort**
* selecting maximum value has same implementation but to start from `n` to `0`

```java
	public static void selectionSort(int[] nums) {
		for(int i = 0; i < nums.length; ++i) {
			int min = nums[i];
			int index = i;
			// Find Min value
			for(int l = 1; l < nums.length; ++l) {
				if(min > nums[l]) {
					index = l;
					min = nums[l];
				}
			}

			// Swap
			int temp = nums[index];
            nums[index] = nums[i];
            nums[i] = temp;
		}
	}
```

### Insertion Sort
* one of the simple sorting algorithm
* little bit harder than bubble, selection sort
* iterate the array and repeat the following process
	+