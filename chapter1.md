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

```cpp
int getPartition(int* A, int begin, int end)
{
   if (begin <= end)
   {
      int part = begin;
      for (int i = begin+1; i <= end; ++i)
      {
         if (A[i] <= A[end])
         {
            swap(A[part+1], A[i]);
            ++part;     
         }  
      }
   swap(A[begin], A[part]);
   return part;
   }   
}
```

_时间复杂度：O（n\*lgn）_

_最坏：O（n^2）_

_空间复杂度：O（n\*lgn）_

_不稳定。_

