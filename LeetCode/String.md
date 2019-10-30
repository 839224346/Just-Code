<span id = "00"></span>
## 基础		
 - [28	Implement strStr()]
 - [14	Longest Common Prefix]
 - [58	Length of Last Word]
 - [387	First Unique Character in a String]
 - [383. Ransom Note](#383-ransom-note)
 - [344	Reverse String]
 - [151	Reverse Words in a String]
 - [186	Reverse Words in a String II]
 - [345	Reverse Vowels of a String]
 - [205	Isomorphic Strings]
 - [293	Flip Game]
 - [294	Flip Game II]
 - [290. Word Pattern](#290-word-pattern)
 - [242. Valid Anagram](#242-valid-anagram)
 - [49	Group Anagrams]
 - [249	Group Shifted Strings]
 - [87	Scramble String]
 - [179	Largest Number]
 - [6	ZigZag Conversion]
 - [161	One Edit Distance]
 - [38	Count and Say]
 - [358	Rearrange String k Distance Apart]
 - [316	Remove Duplicate Letters]
 - [271	Encode and Decode Strings]
 - [168. Excel Sheet Column Title](#168-excel-sheet-column-title)
 - [171. Excel Sheet Column Number](#171-excel-sheet-column-number)
 - [13. Roman to Integer](#13-roman-to-integer)
 - [12. Integer to Roman](#12-integer-to-roman)
 - [273	Integer to English Words]
 - [246	Strobogrammatic Number]
 - [247	Strobogrammatic Number II]
 - [248	Strobogrammatic Number III]
## 提高		
 - [68	Text Justification]
 - [65	Valid Number]
 - [157	Read N Characters Given Read4]
 - [158	Read N Characters Given Read4 II - Call multiple times]
## Substring		
 - [76. Minimum Window Substring](#76-minimum-window-substring)
 - [30	Substring with Concatenation of All Words]()
 - [3. Longest Substring Without Repeating Characters](#3-longest-substring-without-repeating-characters)
 - [340	Longest Substring with At Most K Distinct Characters]
 - [395	Longest Substring with At Least K Repeating Characters]
 - [159	Longest Substring with At Most Two Distinct Characters]
## Palindrome		
 - [125. Valid Palindrome](#125-valid-palindrome)
 - [266	Palindrome Permutation]
 - [5	Longest Palindromic Substring]
 - [9	Palindrome Number]
 - [214	Shortest Palindrome]
 - [336	Palindrome Pairs]
 - [131	Palindrome Partitioning]
 - [132	Palindrome Partitioning II]
 - [267	Palindrome Permutation II]
## Parentheses		
 - [20	Valid Parentheses]
 - [22	Generate Parentheses]
 - [32	Longest Valid Parentheses]
 - [241	Different Ways to Add Parentheses]
 - [301	Remove Invalid Parentheses]
## Subsequence		
 - [392	Is Subsequence]
 - [115	Distinct Subsequences]
 - [187	Repeated DNA Sequences]


## 383. Ransom Note

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

给定一个任意的赎金票据字符串和另一个包含所有杂志字母的字符串，编写一个函数，如果可以从杂志中构造赎金票据，则该函数将返回true； 否则，它将返回false。 杂志字符串中的每个字母只能在赎金记录中使用一次。

**Example**

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

---

### Python Solution
**分析：** 一种是用 count，一种是用 Counter。

```python
class Solution:
   def canConstruct(self, ransomNote: str, magazine: str) -> bool:
       for letter in set(ransomNote):
           if ransomNote.count(letter) > magazine.count(letter):
               return False
       return True
```

```python
class Solution:
    def canConstruct(self, ransomNote, magazine):
        return not collections.Counter(ransomNote) - collections.Counter(magazine)
```

[返回目录](#00)

## 290. Word Pattern

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

给定一个模式和一个字符串str，找出str是否遵循相同的模式。 在此跟随是指完全匹配，因此模式中的字母与str中的非空单词之间存在双射

**Example**

```
Input: pattern = "abba", str = "dog cat cat dog"
Output: true
```

---

### Python Solution
**分析：** 将单词字母转化为序列进行比较。

```python
class Solution:
    def wordPattern(self, pattern: str, str: str) -> bool:
        s = pattern
        t = str.split()
        return list(map(s.find, s)) == list(map(t.index, t))
```

```python
class Solution:
    def wordPattern(self, pattern: str, str: str) -> bool:
        f = lambda s: map({}.setdefault, s, range(len(s)))
        return list(f(pattern)) == list(f(str.split()))
```

[返回目录](#00)

## 242. Valid Anagram

Given two strings s and t , write a function to determine if t is an anagram of s.

给定两个字符串s和t，编写一个函数来确定t是否是s的字谜。

**Example**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

---

### Python Solution
**分析：** 简单题，用排序或者用字典。这里用的是内置的 Counter。

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return collections.Counter(s) == collections.Counter(t)

        return sorted(s) == sorted(t)
```

[返回目录](#00)

## 168. Excel Sheet Column Title

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

给定一个正整数，返回其相应的列标题，如Excel工作表中所示。

**Example**

```
1 -> A
2 -> B
3 -> C
...
26 -> Z
27 -> AA
28 -> AB
...
```

---

### Python Solution
**分析：** 这是一道很简单的题，注意 (n - 1) % 26 而不是 n % 26 来避免 52 是 AZ 的情况。

```python
class Solution:
    def convertToTitle(self, n: int) -> str:
        res = ''
        while n:
            n, mod = divmod(n - 1, 26)
            res = chr(mod + 65) + res
        return res
```

[返回目录](#00)

## 171. Excel Sheet Column Number

Given a column title as appear in an Excel sheet, return its corresponding column number.

给定列标题（如Excel工作表中所示），返回其对应的列号。

**Example**

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28
...
```

---

### Python Solution
**分析：** 这是一道很简单的题，不过可以用来熟悉 reduce 的用法。r 为之前叠加的结果，c 为当前的字符， s 是 c 取值的地方，0 是 r 的初始值。多用就熟悉了。

```python
class Solution:
    def titleToNumber(self, s: str) -> int:
        res = 0
        for i in s:
            res = res * 26 + ord(i) - 64
        return res
```

```python
from functools import reduce
class Solution:
    def titleToNumber(self, s: str) -> int:
        return reduce(lambda r, c: 26*r + ord(c)-64, s, 0)
```

[返回目录](#00)

## 13. Roman to Integer

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9.
X can be placed before L (50) and C (100) to make 40 and 90.
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

罗马数字由七个不同的符号表示：I，V，X，L，C，D和M.符号值I 1 V 5 X 10 L 50 C 100 D 500 M 1000例如，两个以罗马数字II表示，只是两个加在一起。十二写为XII，简称X + II。数字二十七写为XXVII，即XX + V + II。罗马数字通常从左到右从大到小书写。但是，四个数字不是IIII。取而代之的是，数字四被写为IV。因为一个在五之前，所以我们减去它等于四。相同的原则适用于编号为IX的数字9。在六种情况下使用减法：我可以放在V（5）和X（10）之前以得到4和9.X可以放在L（50）和C（100）之前以得到40和90。可以放在D（500）和M（1000）的前面，以得到400和900。给定罗马数字，请将其转换为整数。输入保证在1到3999的范围内。

**Example**

```
Example 1:

Input: "III"
Output: 3
Example 2:

Input: "IV"
Output: 4
Example 3:

Input: "IX"
Output: 9
Example 4:

Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 5:

Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

---

### Python Solution
**分析：** 用字典会简单很多，再用 mini 存储当前较小值来判断加还是减。

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        dic = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        res = mini = 0
        for i in s[::-1]:
            if dic[i] < mini:
                res -= dic[i]
            else:
                res += dic[i]
            mini = dic[i]
        return res
```

[返回目录](#00)

## 12. Integer to Roman

题目就是上一道题的反向程序

**Example**

```
Example 1:

Input: 3
Output: "III"
Example 2:

Input: 4
Output: "IV"
Example 3:

Input: 9
Output: "IX"
Example 4:

Input: 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
Example 5:

Input: 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

---

### Python Solution
**分析：** 没有什么意义的题目。

```python
class Solution:
    def intToRoman(self, num: int) -> str:
        M = ["", "M", "MM", "MMM"]
        C = ["", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"]
        X = ["", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"]
        I = ["", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"]
        return M[num//1000] + C[(num%1000)//100] + X[(num%100)//10] + I[num%10]
```

[返回目录](#00)

## 76 Minimum Window Substring

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

给定一个字符串S和一个字符串T，找到S中的最小窗口，它将包含复杂度为O（n）的T中的所有字符。

**Example**

```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

---

### Python Solution
**分析：** 这是一道 Hard 难度的题目，我们采用滑动窗口来解决。用 need 来储存我们现在还需要的元素及其个数（可以为负），missing 代表我们现在还需要的元素的个数。小写的 i， j 是当前窗口的索引，大写的 I， J 是返回的结果窗口的索引。

```python
class Solution:
    def minWindow(self, s, t):
        need, missing = collections.Counter(t), len(t)
        i = I = J = 0
        for j, c in enumerate(s, 1):
            missing -= need[c] > 0              # 如果存在 need[c] ，missing 减一
            need[c] -= 1
            if not missing:                     # 匹配到了所有需要的元素
                while i < j and need[s[i]] < 0: # 我们找到了此时满足条件的 j
                    need[s[i]] += 1             # 现在将 i 往后移动得到满足条件的最靠近的 i
                    i += 1
                if not J or j - i <= J - I:     # 初始化结果窗口和满足条件时更新窗口
                    I, J = i, j
                missing += 1                    # 将此时满足条件的 s[i] 丢失
                need[s[i]] += 1                 # 来求下一次满足的窗口
                i += 1
        return s[I:J]
```

[返回目录](#00)

## 3 Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

给定一个字符串，找到最长子字符串的长度而不重复字符。

**Example:1**

```
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example:2**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example:3**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
```

---

### Python Solution
**分析：** 滑动窗口解决问题，如果遍历一遍 s，如果遍历到没有出现的元素，窗口右端立马扩张，并计算最大长度。如果遍历到之前出现的元素，则将窗口左端置为上次出现的位置的后一位。只有出现没有遍历过的元素才会计算最大长度。因为一旦是遍历过的元素，只有可能是保持不变或者缩小。

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        start = maxLength = 0
        used = {}
        for i, c in enumerate(s):
            if c in used and start <= used[c]:
                start = used[c] + 1
            else:
                maxLength = max(maxLength, i - start + 1)
            used[c] = i
        return maxLength
```

[返回目录](#00)

## 125. Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.

给定一个字符串，确定它是否是回文，只考虑字母数字字符并忽略大小写。 注意：出于此问题的目的，我们将空字符串定义为有效的回文。

**Example**

```
Input: "A man, a plan, a canal: Panama"
Output: true
```

---

### Python Solution
**分析：** 很容易想到我们如果先用 isalnum() 将字符或者数字选出来是不是就转换成了判断字符串是不是回文字符串的问题。那么我们用 Python 的列表推导式就可以 Pythonic 地解决这个要求。

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = [i.lower() for i in s if i.isalpha() or i.isdigit()]
        return s == s[::-1]
```

**进阶** 但实际上我们的构成新列表 s 的操作时间复杂度为 O(n)， 空间复杂度为 O(n)。之后的进行判断是否为回文字符串的操作话费相同，显得比较粗鲁。因此我们想能不能更优雅地解决判断回文字符串的要求。于是有了下面的代码：

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = [i.lower() for i in s if i.isalnum()]
        i, j = 0, len(s) - 1
        while i < j:
            if s[i] != s[j]:
                return False
            i += 1
            j -= 1
        return True
```

**再进阶** 利用双指针一前一后进行判断是否相同只要 O(n) 时间复杂度和 O(1) 的空间复杂度，比之前更有效率了。但是列表 s 仍然会花费 O(n) 的空间，所以我们将双指针不再局限在筛选后的 list 上，而是在原来的字符串上就开始工作。一前一后逼近，每次移动后判断当前位是否为字符或者数字，然后进行比较。这样只对字符串进行了一次遍历，所以只用了 O(n) 的时间复杂度，而且空间复杂度为 O(1) 。

```python
class Solution:
    def isPalindrome(self, s):
        i, j = 0, len(s) - 1
        while i < j:
            while not s[i].isalnum() and i < j:
                i += 1
            while not s[j].isalnum() and i < j:
                j -= 1
            if s[i].lower() != s[j].lower():
                return 0
            i += 1
            j -= 1
        return True
```

[返回目录](#00)
