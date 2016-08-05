# 快速排序

### 思路：和合并排序类似，快速排序时基于分支模式

* 分解：数组A\[n\]被划分为两个子数组A\[0...q-1\]和A\[q+1...n\]，使得对于数组A\[0...q-1\]中的元素都小雨A\[q\]，A\[q+1...n\]中的元素都大于等于A\[q\].此时A\[q\]就得排好序
* 解决：通过递归调用快速排序，对子数组A\[0...q-1\]和A\[q+1...n\]进行排序
* 合并：因为两个子数组已经是就地排好序的，整个数组已经排好序了

```cpp
void quickSort(int A[], int begin, int end) {
   if ( A==NULL || begin > end )
      return;
   int part = getPartition(A, begin, end);
   quickSort(A, begin, part-1);
   quickSort(A, part+1, end); 
}
```

* ```cpp
  int getPartition(int* A, int begin, int end)
  {
     if (begin <= end)
     {
        int part = A[begin];
        while(begin <= end && part <= A[end])
           --end;
        swap(&A[begin], &A[end]);
        while(while <= end && part >= A[begin])
           ++begin;
        swap(&A[begin], &A[end]);
     }   
      return begin;
  }
  ```


_时间复杂度：O（n\*lgn）_

_最坏：O（n^2）_

_空间复杂度：O（n\*lgn）_

_不稳定。_

# 归并排序

## 思路：分治法

* 分解：将序列每次折半划分
* 合并：将划分后的序列段两两合并后排序

```cpp
/*一次归并排序
 *参数说明：begin    第一个待排序列起始位置
 *         mid      第一个待排序列结束位置
 *         mid+1    第二个待排序列起始位置
 *         end      第二个待排序列结束位置
 */
void merge(int A[], int begin, int mid, int end)
{
    int i = begin;
    int j = mid + 1;
    int k = 0;
    int *pTempA = new int[end - begin + 1];
    while (i <= mid && j <= high)
    {
        if (A[i] < A[j])
            pTempA[k++] = A[i];
        else
            pTempA[k++] = A[j];        
    }
    while (i <= mid)     pTempA[k++] = A[i++];
    while (j <= end)     pTempA[k++] = A[j++];
    for (int i = begin, k = 0; i < end + 1; i++, k++)
        A[i] = pTempA[k]; 
    delete[] pTempA;
} 
```

若子表个数为奇数，则最后一个子表无须和其他子表归并（即本趟处理轮空）：若子表个数为偶数，则要注意到最后一对子表中后一个子表区间的上限为n-1

```cpp

//自下而上
void mergeSort(int A[], int iArrayLen)
{
    int length = 1;
    int i = 0;
    for (; i+2*length-1 < iArrayLen; i += 2*length)
        merge(A, i, i+length-1, i+2*length-1)
    //余下两个子表，后者长度小于length
    if (i+length-1 < iArrayLen)
        merge(A, i, i+length-1, iArrayLen-1);
}

//自上而下(递归)
void mergeSort(int A[], int begin, int end)
{
    int mid = (end + begin) / 2;
    if (begin < end)
    {    
        mergeSort(A, begin, mid);
        mergeSort(A, mid+1, end);
        merge(A, begin, mid, end);
    }
}
```

### **时间复杂度**

归并排序的形式就是一棵二叉树，它需要遍历的次数就是二叉树的深度，而根据完全二叉树的可以得出它的时间复杂度是**O\(n\*log2n\)**。

### **空间复杂度**

由前面的算法说明可知，算法处理过程中，需要一个大小为**n**的临时存储空间用以保存合并序列。

### **算法稳定性**

在归并排序中，相等的元素的顺序不会改变，所以它是**稳定的**算法。

