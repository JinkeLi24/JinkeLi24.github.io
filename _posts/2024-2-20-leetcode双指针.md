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
> 输入: nums = [0,1,0,3,12]
> 输出: [1,3,12,0,0]

**思路**：使用快慢指针，慢指针为0且快指针不为0时调换顺序。当慢指针对应数值与后续所有数判断完成后，慢指针+=1
```
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
```

## leetcode26 （删除有序数组重复项）
> 给你一个 非严格递增排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。
> 元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数。考虑 nums 的唯一元素的数量为 k ，你需要做以下事情
> 确保你的题解可以被通过：更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。
> nums 的其余元素与 nums 的大小不重要。返回 k 。
> 输入：nums = [1,1,2]
> 输出：2, nums = [1,2,_]
