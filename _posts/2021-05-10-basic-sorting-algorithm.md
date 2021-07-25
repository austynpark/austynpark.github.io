---
layout: post
title: Eight basic sorting algorithm
subtitle: sorting algorithm
categories: algorithm
tags: [algorithm, sort]
---

There are various kinds of algorithm for sorting. So what do we use most and why?

### Bubble Sort
---
* Iterate the array and repeat the following process 
	+ Start from `0`, compare with element `1`, if $element`0` > element `1`$
	+ Start from `1`, compare with element `2`, if $element`1` > element `2`$
	+ Start from `2`, compare with element `3`, if $element`2` > element `3`$
	+ Repeat until `n - 1` element...
* Element with bigger value will be sorted first (Because larger bubble rises first, it is called Bubble Sort)

|  Average  |   worst   | memory | stability |
|:---------:|:---------:|:------:|:---------:|
|  $N^{2}$  |  $N^{2}$  |  O(1)  |     O     |

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
---
* One of the simple sorting algorithm
* Iterate the array and repeat the following process 
	+ Start from `0`, find the minimum value and swap with element `0`
	+ Start from `1`, find the minimum value and swap with element `1`
	+ Start from `2`, find the minimum value and swap with element `2` 
	+ Repeat until `n - 1` element...
* Since the selction algorithm is all about selecting minimum value (or maximum), it is called **selection sort**
* Also can be implemented by selecting maximum value and to start from `n` to `0`

|  Average  |   worst   | memory | stability |
|:---------:|:---------:|:------:|:---------:|
|  $N^{2}$  |  $N^{2}$  |  O(1)  |     X     |

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
---
* One of the simple sorting algorithm
* Little bit harder than bubble, selection sort
* Iterate the array and repeat the following process
	+ Select a current element
	+ Compare with visited elements and decide where to insert to maintain sort

|  Average  |   worst   | memory | stability |
|:---------:|:---------:|:------:|:---------:|
|  $N^{2}$  |  $N^{2}$  |  O(1)  |     X     |

```java
	public static void insertionSort(int[] nums) {
		for(int i = 0; i < nums.length; ++i) {
			int index = i;
			// Find place for element i
			for(int l = i - 1; l >= 0; ++l) {
				if(nums[l] > nums[index]) {
					swap(nums, index, l);
				} 
				else {
					break;
				}
			}
		}
	}
```

### Quick Sort
---
* Most Common Sorting algorithms in the field
	+ It is the fastest sort in general
* Divide & Conquer algorithm
	+ visits all of the elements
* Divide the array by the pivot
	+ standard of dividing is the pivot value (bigger or smaller)
	+ repeats the process recursively
	+ everytime that recursive process gets deeper, selects new pivot value

|  Average  |   worst   |    memory     | stability |
|:---------:|:---------:|:-------------:|:---------:|
| N$log{N}$ |  $N^{2}$  |  O($log{N}$)  |     X     |

```java
	public static int partition(int[] nums, int left, int right, int pivot) {
		int index = left - 1;

		for(int i = left; i < right; ++i) {
			if(nums[i] < pivot) {
				++index;
				swap(nums, i, index);
			}
		}
		// index is nums[end] sorted place
		++index;
		swap(nums, index, end);

		return index;
	}


	public static void quickSort(int[] nums, int start, int end) {
		if(start >= end) {
			return;
		}

		int index = partition(nums, start, end, nums[end]);
		quickSort(nums, start, index - 1);
		quickSort(nums, index + 1, end);
	}
```

### Merge Sort
---
* Divide Input array to half recursively and make an array with one element

### Heap Sort
---
 