---
layout: post
title: Eight basic sorting algorithm
subtitle: sorting algorithm
categories: algorithm
tags: [algorithm, sort]
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

| Average | worst | memory | stability |
| :-----: | :---: | :----: | :-------: |
| $$n^2$$ | $$n^2$$ | O(1) | X         |

| Stage | Direct Products | ATP Yields |
| ----: | --------------: | ---------: |
|Glycolysis | 2 ATP                   ||
|^^         | 2 NADH      | 3--5 ATP   |
|Pyruvaye oxidation | 2 NADH | 5 ATP   |
|Citric acid cycle  | 2 ATP           ||
|^^                 | 6 NADH | 15 ATP  |
|^^                 | 2 FADH | 3 ATP   |
| 30--32 ATP                         |||


* One of the simple sorting algorithm
* Iterate the array and repeat the following process 
	+ Start from `0`, find the minimum value and swap with element `0`
	+ Start from `1`, find the minimum value and swap with element `1`
	+ Start from `2`, find the minimum value and swap with element `2` 
	+ Repeat until `n - 1` element...
* Since the selction algorithm is all about selecting minimum value (or maximum), it is called **selection sort**
* Also can be implemented by selecting maximum value and to start from `n` to `0`

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
* One of the simple sorting algorithm
* Little bit harder than bubble, selection sort
* Iterate the array and repeat the following process
	+ Select a current element
	+ Compare with visited elements and decide where to insert to maintain sort

### Quick Sort
* Most Common Sorting algorithms in the field
	+ It is the fastest sort in general
* Divide & Conquer algorithm
	+ visits all of the elements
* Divide the array by the pivot
	+ standard of dividing is the pivot value (bigger or smaller)
	+ repeats the process recursively
	+ everytime that recursive process gets deeper, selects new pivot value


### Merge Sort
* Divide Input array to half recursively and make an array with one element

### Heap Sort
 