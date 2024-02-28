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
def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left, right = 0, 1
        while right < len(nums):
            if nums[left] != 0:
                left += 1
            elif nums[left] ==0 and nums[right]:
                nums[left],nums[right] = nums[right], 0
                left += 1
            right += 1
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
def removeDuplicates(self, nums: List[int]) -> int:
        left, right = 0, 1
        while right < len(nums):
            if nums[left] != nums[right]:
                left += 1
                nums[left] = nums[right]
            right += 1
        return left + 1
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
>
>输入：nums1 = [1], m = 1, nums2 = [], n = 0
>输出：[1]
>解释：需要合并 [1] 和 [] 。
>合并结果是 [1] 。
>
>输入：nums1 = [0], m = 0, nums2 = [1], n = 1
>输出：[1]
>解释：需要合并的数组是 [] 和 [1] 。
>合并结果是 [1] 。
>注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。

**思路**：因为两个数组为非递减，左右指针分别从m-1和n-1开始，如果右大于左就将右放在nums1未判断位置的最后一个，右小于左就将左放在未判断位置最后一个。应该判断m+n次。本质上是在两个数组中找最大的值放在后面。

```
def merge(nums1:list[int], m:int, nums2:list[int], n:int)->list[int]:
    p1, p2 = m-1, n-1 
    for i in range(m+n-1, -1, -1):
        # 如果p1遍历完了，说明nums2剩下的数都比nums1第一个数小
        if p1 == -1:
            nums1[0:i+1] = nums2[0:p2+1]
            break
        # 如果p2遍历完了，说明nums1剩下的数都比nums2中数小，不用动
        elif p2 == -1:
            break
        elif nums1[p1] >= nums1[p2]:
            nums1[i] = nums1[p1]
            p1 -= 1
        elif nums1[p1] < nums1[p2]:
            nums1[i] = nums2[p2]
            p2 -= 1
    return nums1
print(merge([1,2,3,4,0,0,0,0],4,[9,10,11,12],4))
print(merge([10,20,30,40,0,0,0,0],4,[9,10,10,11],4))
```

