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

## leetcode 283
> 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
> 请注意 ，必须在不复制数组的情况下原地对数组进行操作。
> 输入: nums = [0,1,0,3,12]
> 输出: [1,3,12,0,0]

**思路**：使用快慢指针，慢指针为0且快指针不为0时调换顺序。当慢指针对应数值与后续所有数判断完成后，慢指针+=1
``
def moveZeros(nums:list[int])->None:
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
``
