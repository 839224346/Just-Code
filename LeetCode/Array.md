<span id = "00"></span>
## 基础		
 - [27	Remove Element]
 - [26	Remove Duplicates from Sorted Array]
 - [80	Remove Duplicates from Sorted Array II]
 - [277	Find the Celebrity]
 - [189. Rotate Array](#189-rotate-array)
 - [41. First Missing Positive](#41-first-missing-positive)
 - [299	Bulls and Cows]
 - [134	Gas Station]
 - [118	Pascal's Triangle]
 - [119	Pascal's Triangle II]
 - [169	Majority Element]
 - [229	Majority Element II]
 - [274	H-Index]
 - [275	H-Index II	Binary Search]
 - [243	Shortest Word Distance]
 - [244	Shortest Word Distance II]
 - [245	Shortest Word Distance III]
 - [217. Contains Duplicate](#217-contains-duplicate)
 - [219. Contains Duplicate II](#219-contains-duplicate-ii)
 - [220	Contains Duplicate III]
 - [55	Jump Game]
 - [45	Jump Game II]
 - [121	Best Time to Buy and Sell Stock]
 - [122	Best Time to Buy and Sell Stock II]
 - [123	Best Time to Buy and Sell Stock III]
 - [188	Best Time to Buy and Sell Stock IV]
 - [309	Best Time to Buy and Sell Stock with Cooldown]
 - [11	Container With Most Water]
 - [42	Trapping Rain Water]
 - [334	Increasing Triplet Subsequence]
 - [128	Longest Consecutive Sequence]
 - [164	Maximum Gap	Bucket]
 - [287	Find the Duplicate Number]
 - [135	Candy]
 - [330	Patching Array]
## 提高		
 - [4	Median of Two Sorted Arrays]
 - [321	Create Maximum Number]
 - [327	Count of Range Sum]
 - [289	Game of Life]
## Interval		
 - [57. Insert Interval](#57-insert-interval)
 - [56. Merge Intervals](#56-merge-intervals)
 - [986. Interval List Intersections](#986-interval-list-intersections)
 - [252	Meeting Rooms]
 - [253	Meeting Rooms II]
 - [352	Data Stream as Disjoint Intervals]
## Counter		
 - [239. Sliding Window Maximum](#239-sliding-window-maximum)
 - [295	Find Median from Data Stream]
 - [53	Maximum Subarray]
 - [325	Maximum Size Subarray Sum Equals k]
 - [209. Minimum Size Subarray Sum](#209-minimum-size-subarray-sum)
 - [238	Product of Array Except Self]
 - [152	Maximum Product Subarray]
 - [228	Summary Ranges]
 - [163	Missing Ranges]
## Sort		
 - [88. Merge Sorted Array](#88-merge-sorted-array)
 - [75. Sort Colors](#75-sort-colors)
 - [283. Move Zeroes](#283-move-zeroes)
 - [376	Wiggle Subsequence]
 - [280	Wiggle Sort]
 - [324	Wiggle Sort II]

## 189. Rotate Array

Given an array, rotate the array to the right by k steps, where k is non-negative.

给定一个数组，将数组向右旋转k步，其中k为非负数。

**Example:1**

> Input: [1,2,3,4,5,6,7] and k = 3
> Output: [5,6,7,1,2,3,4]
> Explanation:
> rotate 1 steps to the right: [7,1,2,3,4,5,6]
> rotate 2 steps to the right: [6,7,1,2,3,4,5]
> rotate 3 steps to the right: [5,6,7,1,2,3,4]

**Example:2**

> Input: [-1,-100,3,99] and k = 2
> Output: [3,99,-1,-100]
> Explanation:
> rotate 1 steps to the right: [99,-1,-100,3]
> rotate 2 steps to the right: [3,99,-1,-100]

---

### Python Solution
**分析：** 可以用 Python 的列表的交换做，也可以通过翻转来做，推荐第二种Solution

**Solution 1:**

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        k %= len(nums)
        if k == 0:return
        nums[:k], nums[k:] = nums[-k:], nums[:-k]
```

**Solution 2:**

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        def reverse(i, j):
            while i < j:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
                j -= 1
        k %= len(nums)
        reverse(0, len(nums) - 1)
        reverse(0, k - 1)
        reverse(k, len(nums) - 1)
```

[返回目录](#00)

## 41. First Missing Positive

Given an unsorted integer array, find the smallest missing positive integer.

给定未排序的整数数组，找到最小的缺失正整数。

**Example:1**

> Input: [3,4,-1,1]
> Output: 2

**Example:2**

> Input: [1,2,0]
Output: 3

---

### Python Solution
**分析：** Hard 难度的题目，但是思路很简单：就是把 1 到 len(nums) 的数放到对应下标（即减一）的位置，然后从头遍历，找到第一个不满足条件的值。

```python
class Solution:
    def firstMissingPositive(self, nums):
        for i in range(len(nums)):
            while 0 <= nums[i] < len(nums) and nums[nums[i] - 1] != nums[i]:
                tmp = nums[i] - 1
                nums[i], nums[tmp] = nums[tmp], nums[i]
        for i, v in enumerate(nums):
            if v != i + 1:
                return i + 1
        return len(nums) + 1
```

[返回目录](#00)

## 217. Contains Duplicate

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

给定一个整数数组，查找数组是否包含任何重复项。 如果数组中任何值至少出现两次，则函数应返回true，如果每个元素都不相同，则返回false。

**Example:1**

> Input: [1,2,3,1]
> Output: true

**Example:2**

> Input: [1,2,3,4]
> Output: false

---

### Python Solution
**分析：** 用 set 作 hash 表，如果存在重复的元素，则 set 的长度一定小于 nums 的长度。

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(nums) > len(set(nums))
```

[返回目录](#00)

## 219. Contains Duplicate II

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

给定一个整数数组和一个整数k，找出数组中是否存在两个不同的索引i和j，使得nums [i] = nums [j]并且i和j之间的绝对差值最多为k。

**Example:1**

> Input: nums = [1,2,3,1], k = 3
> Output: true

**Example:2**

> Input: nums = [1,2,3,1,2,3], k = 2
> Output: false

---

### Python Solution
**分析：** 建立哈希表，存储距离最近的上一次索引，判断距离，如果满足条件了将 flag 设为 True ，否则不满足返回 flag = Flase 。

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        used = {}
        flag = False
        for i, v in enumerate(nums):
            if v in used and not flag:
                flag = (i - used[v] <= k)
            used[v] = i
        return flag
```

[返回目录](#00)

## 239. Sliding Window Maximum

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

给定一个数组nums，有一个大小为k的滑动窗口，它从数组的最左边移动到最右边。 您只能在窗口中看到k编号。 每次滑动窗口向右移动一个位置。 返回最大滑动窗口。

**Example**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7]
Explanation:

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

---

### Python Solution
**分析：**

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        dq = collections.deque()
        res = []
        for i, v in enumerate(nums):
            while dq and nums[dq[-1]] < v:
                dq.pop()
            dq += i,
            if dq[0] == i - k:
                dq.popleft()
            if i >= k - 1:
                res += nums[dq[0]],
        return res
```

[返回目录](#00)

## 57. Insert Interval

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

给定一组非重叠区间，在区间中插入新区间（必要时合并）。 您可以假设区间最初是根据其下限排序的。

**Example**

> Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
> Output: [[1,2],[3,10],[12,16]]
> Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

---

### Python Solution
**分析：** 虽然这是一道 Hard 难度的题，但其实并没有难度。Talk is cheap, show you the code.

```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        start, end = newInterval
        left, right = [], []
        for i in intervals:
            if i[1] < start:
                left += i,
            elif i[0] > end:
                right += i,
            else:
                start = min(start, i[0])
                end = max(end, i[1])
        return left + [[start, end]] + right
```

[返回目录](#00)

## 56. Merge Intervals

Given a collection of intervals, merge all overlapping intervals.

给定包含一些区间的集合，合并所有重叠的区间。

**Example**

> Input: [[1,3],[2,6],[8,10],[15,18]]
> Output: [[1,6],[8,10],[15,18]]
> Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

---

### Python Solution
**分析：** 先根据区间下限对给定的区间集合进行排序，然后逐个区间与 res 中存在的最后一个区间进行比较。如果没有交集，则将新的区间存入 res 作为新的最后一个区间；如果有交集，则将最后一个区间的上限更新为更大的那个上限。

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key = lambda x : x[0])
        res = []
        for i in intervals:
            if not res or res[-1][1] < i[0]:
                res += i,
            else:
                res[-1][1] = max(res[-1][1], i[1])
        return res
```

**优化** 在 LeetCode 上提交发现 Runtime 较低，应该是每次都对 res 进行读取的原因，所以我们设置两个变量来降低读取 res 的频率。但是它带来的问题就是需要判断区间集合是否为空。

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals:
            return []
        intervals.sort(key = lambda x : x[0])
        res = []
        l, r = intervals[0]
        for i in range(1, len(intervals)):
            il, ir = intervals[i]
            if r < il:
                res += [l, r],
                l, r = il, ir
            else:
                r = max(r, ir)
        res += [l, r],
        return res
```

[返回目录](#00)

## 986. Interval List Intersections

Given two lists of closed intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

(Formally, a closed interval [a, b] (with a <= b) denotes the set of real numbers x with a <= x <= b.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of [1, 3] and [2, 4] is [2, 3].)

给定两个闭合间隔列表，每个间隔列表是成对不相交的并且按排序顺序。 返回这两个间隔列表的交集。 （形式上，闭区间[a，b]（a <= b）表示实数x的集合，其中a <= x <= b。两个闭区间的交集是一组空的实数 或者可以表示为闭区间。例如，[1,3]和[2,4]的交集是[2,3]。）

**Example**

> Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
> Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
> Reminder: The inputs and the desired output are lists of Interval objects, and not arrays or lists.

---

### Python Solution
**分析：** 双指针进行比对，如果有交集则在 res 中添加。移动拥有更小末尾的指针，进行判断下一个区间和当前较大末尾的区间是否有交集。

```python
class Solution:
    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:
        res = []
        i = j = 0
        while i < len(A) and j < len(B):
            a1, a2 = A[i][0], A[i][1]
            b1, b2 = B[j][0], B[j][1]
            if b2 >= a1 and a2 >= b1:
                res += [max(a1, b1), min(a2, b2)],
            if a2 < b2: i += 1
            else: j += 1
        return res
```

[返回目录](#00)

## 209. Minimum Size Subarray Sum

Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

给定n个正整数和正整数s的数组，找到连续子阵列的最小长度，其总和≥s。 如果没有，则返回0。

**Example**

> Input: s = 7, nums = [2,3,1,2,4,3]
> Output: 2
> Explanation: the subarray [4,3] has the minimal length under the problem constraint.
---

### Python Solution
**分析：** 滑动窗口的思路，窗口的右端每右移一位就进行判断，如果总和大于等于 s ，则将滑动窗口的左端向右移动到满足条件的最边界位置，当前的窗口长度与最小长度进行比较更新。

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        i, sum, res = 0, 0, float('inf')
        for j in range(len(nums)):
            sum += nums[j]
            while sum >= s:
                i, sum, res = i + 1, sum - nums[i], min(res, j - i + 1)
        return 0 if res == float('inf') else res
```

[返回目录](#00)

## 88. Merge Sorted Array

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

给定两个排序的整数数组nums1和nums2，将nums2合并为nums1作为一个排序的数组。。

**Example**

> Input:
> nums1 = [1,2,3,0,0,0], m = 3
> nums2 = [2,5,6],       n = 3
>
> Output: [1,2,2,3,5,6]

---

### Python Solution
**分析：** 从尾部进行数组的比较和填充不会移动之前的元素，比较高效。最后确保 nums2 中的元素全部移到了 nums1 中，因为 nums2 的前几个元素可能比 nums1 的第一个元素都小。

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        while m > 0 and n > 0:
            if nums1[m - 1] >= nums2[n - 1]:
                nums1[m + n - 1] = nums1[m - 1]
                m -= 1
            else:
                nums1[m + n - 1] = nums2[n - 1]
                n -= 1
        nums1[:n] = nums2[:n]
```

[返回目录](#00)

## 75. Sort Colors

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

给定一个具有红色，白色或蓝色的n个对象的数组，对它们进行就地排序，使相同颜色的对象相邻，颜色顺序为红色，白色和蓝色。

这里，我们将使用整数0,1和2分别表示红色，白色和蓝色。

**Example**

> Input: [2,0,2,1,1,0]
> Output: [0,0,1,1,2,2]

---

### Python Solution
**分析：** 三路快排的思想，用三个指针，但是只关注左边 0 的位置和右边 2 的位置即可，排序交换完结果肯定中键都是 1 。

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        zero = i = 0
        two = len(nums)
        while i < two:
            if nums[i] == 1:
                i += 1
            elif nums[i] == 2:
                two -= 1
                nums[i], nums[two] = nums[two], nums[i]
            else:
                nums[i], nums[zero] = nums[zero], nums[i]
                zero += 1
                i += 1
```

[返回目录](#00)

## 283. Move Zeroes

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

给定一个数组nums，写一个函数将所有0移动到它的末尾，同时保持非零元素的相对顺序。

**Example**

> Input: [0,1,0,3,12]
> Output: [1,3,12,0,0]

---

### Python Solution
**分析：** k 永远指向的是遍历到的交换后最开头的一个 0 ，并且与当前遍历到的不为 0 的数进行交换。当遍历到最后的时候，即完成了所有的交换，将所有 0 交换到了末尾。

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        k = 0
        for i in range(len(nums)):
            if nums[i]:
                if i != k:
                    nums[i], nums[k] = nums[k], nums[i]
                k += 1
```

[返回目录](#00)
