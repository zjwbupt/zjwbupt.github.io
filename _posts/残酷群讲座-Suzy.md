二分查找 / 滑动窗口/ 单调栈

## 二分搜索

条件：数据储存在可以随机访问的线性结构中， Key有序

```java
int binary_search(int start, int end, int key) {
  int ret = -1;
  int mid;
  while (start <= end) {
    mid = start + ((end-start) >> 1);
    if (arr[mid] < key)
      start = mid + 1;
    else if (arr[mid] > key)
      end = mid+1;
    else {
      ret = mid;
      break;
    }
    return ret;
  }
}
```

mid写法 (溢出和取整)

1. mid = (left+right)/2;

2. mid = (left+right+1)/2;

3. mid = left + (right-left)/2;

4. mid = left +  (right-left+1)/2;

   Note: *(right-left)/2* -> *(right-left)>>2*

**LC300: 最长上升子序列**

f[i]: 长度为i的上升子序列的最后一个元素的值

**LC162: FindPeak**

eg: nums = [1,2,3,1], return 2

​	nums = [1,2,1,3,5,6,3] return 1, 





## 滑动窗口

本质上是证明解的单调性，将二维问题压缩到一维

Leetcode1371



## 单调栈

LeetCode 503. 下一个更大的元素II

*LeetCode84. 柱状图中最大的矩形

LeetCode85. 最大矩形