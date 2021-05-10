---
layout: post
title: 8 basic sorting algorithm
subheading: sorting algorithm
author: Austyn Park
categories: algorithm
tags: algorithm sorting
sidebar: []
---

There are various kinds of algorithm for sorting. So what do we use most and why?

## Bubble Sort

Code
```java
    public static void bubbleSort(int[] nums) {
        for (int i = 0; i < nums.length - 1; ++i) {
            for (int l = 0; l < nums.length - i - 1; ++l) {
                if (nums[l] > nums[l + 1]) {
                    int temp = nums[l];
                    nums[l] = nums[l + 1];
                    nums[l + 1] = temp;
                }
            }
        }
    }
```

## Selection Sort
|: average :||: worst :||: memory :||: stability :|
|:----------||---------||----------||-------------|
|:  $n^2$  :||: $n^2$ :||: O(1) :||: X :|
