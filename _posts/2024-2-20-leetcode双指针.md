---
layout:     post
title:      leetcode双指针
subtitle:   
date:       2024-02-20
author:     JinLi
header-img: img/john-towner-JgOeRuGD_Y4-unsplash.jpg
catalog: true
tags:
    - leetcode刷题
---

## leetcode 283 （Move Zeros）
> 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
> 请注意 ，必须在不复制数组的情况下原地对数组进行操作。
> 
> 输入: nums = [0,1,0,3,12]
> 输出: [1,3,12,0,0]

**思路**：使用快慢指针，慢指针为0且快指针不为0时调换顺序。当慢指针对应数值与后续所有数判断完成后，慢指针+=1
```
def moveZeros(nums:list[int])->list[int]:
    if len(nums) == 0:
        return None
    slow, fast = 0, 1
    while fast < len(nums):
        if nums[slow] == 0 and nums[fast] != 0:
            nums[slow] == nums[fast]
            nums[fast] == 0 
            slow += 1
        fast += 1
    return nums
```

## leetcode26 （删除有序数组重复项）
> 给你一个 非严格递增排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。
> 元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数。考虑 nums 的唯一元素的数量为 k ，你需要做以下事情
> 确保你的题解可以被通过：更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。
> nums 的其余元素与 nums 的大小不重要。返回 k 。
> 
> 输入：nums = [1,1,2]
> 输出：2, nums = [1,2,_]

**思路**：使用快慢指针，慢指针与快指针相等时，快指针往后移动，当不相等时，将慢指针下一位置为快指针的值
```
def moveZeros(nums:list[int])-> int:
    if len(nums) == 0:
        return 0
    slow, fast = 0, 1
    while fast < len(nums):
        if nums[slow] != nums[fast]:
            slow += 1
            nums[slow] = nums[fast]
        fast += 1
    return slow + 1
```

## leetcode88（合并两个有序数组）
>给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。
>请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。

>注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个>元素为 0 ，应忽略。nums2 的长度为 n 。
>
>输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
>输出：[1,2,2,3,5,6]
>解释：需要合并 [1,2,3] 和 [2,5,6] 。
>合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。
