---
layout: post
title:  "快速排序详解（精细到每一帧）"
date:   2020-01-02 13:25:35 +0200
categories: jekyll update
---

说到排序算法，很多小伙伴都并不陌生。快速排序作为排序算法中时间复杂度较低 `(O(n * logn)` 的一种，在许多其他算法中都有重大作用。本文将试图从最细致到角度，将快速排序算法的每一帧变化都还原出来，给让小伙伴们**还原来自算法的美**

## 算法背景

快速排序思想的本质是来源于冒泡排序，冒泡排序是通过比较相邻的两个元素，每次将最小的元素调换到最顶端。显而易见，对于长度为5的数组，共需要比较 4 + 3 + 2 + 1次。 所以冒泡排序的时间复杂度(Time Complexity)是O(n * n), 当我们需要更快的排序算法时，一种思路是使用递归来辅助排序，1960年快速排序应运而生。

## 基本原理

Quick Sort快速排序的关键是规定排序点Pivot, 然后给数组两边各放一个指针。当左指针指向的数大于等于排序点Pivot，而右指针指向的点小于等于排序点Pivot时，交换两点数值。当右指针位于左指针左侧时，停止循环并开启左右两次递归。

## 具体样例 

当数组 l = `[3, 20, 1, 6, 11, 9, 15]` 时：
我们取迎面双指针， 左指针指向数组起始点Start，右指针指向数组终止点End

 ![](https://lh5.googleusercontent.com/FlVK5rZ-aOvCcgSEi9f57ZlubQA_t4_qN9DtxVmAVlr-Er6xKRnnUhQq5Uq2Ack9ez-pJIfbdRPbZKWzUXKKjS6Ie8YxEGVvkiMbNJd5kFl5J-pPy6OtkMgQirZWnntzKXHGaFyO)

对于中间值 Pivot取数组两端的中间值

Pivot = (`Nums[start]` + `Nums[end]`)  / `2` 
Pivot = (`3` + `15`) / `2` = `9`

下一步开始从左指针开始移动：

对于左 (Left) 指针 3 < 9, 满足左指针右移条件

![](https://lh6.googleusercontent.com/KnYXKB3lCVG4a4cWMjq0CLu6E2corShmBjXQ3hqGzq0zJ7pLe1LI7K-6Ho7BT90uqGE0Cq6H-Ilzn0qFZ4Av-6qsavxq8opu7UshITwHT6cU5e5Q0XN76ze9rbIcchpF67p2A96_)

发现20的值大于Pivot，左指针停止

![](https://lh5.googleusercontent.com/gzBtC8D38gv6jLEBl9Ud93IW3JtoHU6xtpIJjd42dHX3qSqZY0AQ9f86tfSQVzayhObCKMEd3DzVI06_hXMAoS4Tlo5q-xirK-qupD1b6uf3AlZrRI0itsaRPEkd1BZruOqWE-76)

开始将右指向左移动移动，直到发现9小于等于Pivot 9

![](https://lh4.googleusercontent.com/BeVWtDN_k5yzoZrOuutj-9IJ5ial1OwWXgC-1XdJKigHH69HEKxhQCw3HLLkxClOcfZrhyIQqS5DYMR2VqiGfkZDYqJSxMPVTf5KHQmGdZpldCAQU0JCHzF0RFNZkYVsQ2BbtgeL)

交换左右指针指向的值

![](https://lh6.googleusercontent.com/B4268jfyblYtvulaMiKUV5AsHXtkBpiIJFVB2iZmN1iO1J69_MDU5gGK9Zpcyt3RFYMmw50cCKfr3FpcbEkRX_ng5duUKIGSYF-TBh_C24pMh0mqBasxvuC6vZYvtFRc6SK2NuKr)

由于交换过后左右指针指向的数必然满足要求（左指针小于Pivot， 右指针大于Pivot）

左 (Left) 指针继续向左移动 右 (Right) 指针继续向右移动各一位

![](https://lh3.googleusercontent.com/WG7q9_E86Ly9g0fdHaqGMT1cC-ZhIIlkD2g1bmMwIWpJipt6OT14XjPS3uNTQHOCppYTuRMoi8hMzqvcaWis1xgafZuFAdPBMsGWuN0QRC_akBp_t1Kf9QxcZ-sFQc3FHIT_SB9W)

1小于9，左指针右移

![](https://lh3.googleusercontent.com/XRa1Ua0xvssxGUgA5gOOaIlgfEwXpBPH29kYuzQlJpbsg5LU-g4KZRFZYYPMXVscXhkhrpD7b1ILHtYb_NuzhYpTpVOvW4zHmTYi8ooMMzbW0Et-RUF8QGaVUfq4yKAoAO3YxjSi)

6小于9，左指针右移

![](https://lh3.googleusercontent.com/QyZMtyJwNELXaP6xwBZq2KE9bpS3kcQoG7L2vuJTu7nlkpJnb-AV43MElzSazwKgBUE2pPvEZXoLzXGmeR09mPoP2sxx3bD_oSLbTR5KcTB55ebugae3kDmCORL8vVpD1BzEcMSb)

11大于9， 左指针不动。 排查右指针， 11大于9，满足右指针移动条件， 右指针左移

![](https://lh5.googleusercontent.com/iLdLY6ONJ-D94ZrtO7TMb01AmFz8L41zDHGaHWNhrITCTiUDDWB2qs2fSKXVuqKVkJOKah-WXzvj7gRMw9FJj7YWq1_NB11ohZvaOmuY4LWqyU8kNxYrUj_yAWIScIBCnpsJg_BZ)

右指针（绿色指针）位于左指针左侧， While循环跳出 数组分成两部分：

![](https://lh3.googleusercontent.com/hCcl1nu2Gx3Usb1VQf9DFHFGr4cF6piBVFkYbyDUdkKenrJ0Tfv5OaOVyjcWij60zFGTqucG6Hs_oV28tXuvqCBkabBwQ9ZkRHDb479Mh_69SZopTxbYg7_a9jU3yTSXJWolu3j4)

左侧数组由数组起始位置（start）到 右侧数组由Left指针（红色指针）

Right指针（绿色指针）的最终位置 的最终位置到数组结束位置（end）

![](https://lh5.googleusercontent.com/QZUp2bK0zcx--QYqXXWIf788XjtoLNMCUIH9nqDNlWkbnIHLsUBUOW-pJ41twikT0ZumiOTebVjUwgFnTnNPmrLeS8fj6iC7XKguHqU3QVv7K_Yngr4n8HyTBFXjjSSMV7eu-t5_)

对于左边数组(黄色数组)： 
Pivot = (`Nums[start]` + `Nums[end]`)  /  `2` 
Pivot = 4.5

对于右边数组(粉色数组)：
Pivot = (`Nums[start]` + `Nums[end]`)  /  `2` 
Pivot = 13

![](https://lh4.googleusercontent.com/z4HrFsjevZvMDXLC_UG7NLvG0PbOeZDAgsmkC8Tj6AypmX8i0O1nZB90E5rMgNWTDAgl1Ad1UiPlVoZOpPgbrB07TqCf8GisJ7rJpMW-DMi41iR7iVst3SZ_tUXiVXzOB9oswmKB)

再增加一层递归：

![](https://lh6.googleusercontent.com/6Infeheeyktx5cAe4snTHnJBl5pNIyqq9iaL28jNOf1jsL4Utve4Y9WBvr_geTBvrYItvtNcc1cE5GeK43sR0rSF7OhLI5sSQpwf9i_YS43h3aW4_o2ueTNIk8ohSGkZK6Eb1ruC)

  
  

当长度为一时数组返回，这样排序就完成了

  

![](https://lh6.googleusercontent.com/D2WMcX3Gp3WYatqJa8zaZk5yzPiyQCtbZu2zfn7pM_Sy4agnLRTdxK55YtNDnqjkLzuRR3GhhpwIPae4VlHb_zRskesbHWBlngvl7mAdDjJPP-dVkm7Qs0Gyw_E0HgfsiowaoLW_)

  

## 代码实现

### Python

```python  
def quicksort(nums, start, end):
	if start >= end:
		return
	
	i, j = start, end
	pivot = (nums[start] + nums[end]) / 2
	while i <= j:
		while i <= j and nums[i] < pivot:
			i += 1
		while i <= j and nums[j] > pivot:
			j -= 1
		if i <= j:
			nums[i], nums[j] = nums[j], nums[i]
			i += 1
			j -= 1
	
	quicksort(nums, start, j)
	quicksort(nums, i, end)
	return
```
  

快速排序算法的时间复杂度时O(n * logn), 空间复杂度是O(n). 巧妙地使用了递归的思路加快了排序的进程。类似的时间复杂度为N的算法还有归并排序和选择排序。

  
## 相关题目

Leetcode 912. Sort an Array：
[https://leetcode.com/problems/sort-an-array/](https://leetcode.com/problems/sort-an-array/)

LeetCode 624. Maximum Distance in Arrays
[https://leetcode.com/problems/maximum-distance-in-arrays](https://leetcode.com/problems/maximum-distance-in-arrays)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxMDA1MzkxOCwxNTExOTkxNTA5XX0=
-->