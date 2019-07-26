---
title: 十大经典排序算法
date: 2019-07-26 14:09:40
tags:
    - 经典算法
---
## <table><tr><td bgcolor=Gold><font size=5>0.算法概述</font></td></tr></table>
### 0.1算法分类
十种常见的排序算法可以分为两大类：
- <font color=#DC143C>比较类排序：</font>通过比较来决定元素间的相对次序，由于其时间复杂度不能突破O(nlogn)，因此也称为非线性时间比较类排序。
- <font color=#DC143C>非比较类排序：</font>不通过比较来决定元素间的相对次序，它可以突破基于比较排序的时间下界，以线性时间运行，因此也称为线性时间非比较类排序。
<!--more-->
![](排序算法分类.jpg)

### 0.2算法时间复杂度比较
不同的算法在时间和空间上的复杂度各不相同，一般来说，算法所需要的运算空间越小，时间越短，则表明该算法更优。
本文涉及的十种经典算法的复杂度如下:
![](十大经典算法复杂度.png)

### 0.3算法中的相关概念
- <b>稳定性：</b> 在a=b的情况下，a原本排在b之前，若算法稳定的话，排序之后a依旧在b之前；若算法不稳定，排序之后a可能会出现在b之后。
- <b>时间复杂度：</b> 指算法对排序数据的总的操作次数。反映当数据个数的n变化时，其操作次数的增减规律。
- <b>空间复杂度：</b> 指算法在计算机内执行所需的存储空间。反映其随着数据个数n变化的增减规律。

## <table><tr><td bgcolor=Gold><font size=5>1.冒泡排序（Bubble Sort）</font></td></tr></table>
冒泡排序的基本思想是：重复比较相邻的两个元素，若顺序错误就将它们的位置交换，直到被排序的所有元素不再需要交换位置时，表明该数列已经排序完成。该算法的名字由来是因为越小的元素会随着排序的进行慢慢“漂浮（冒泡）”到数列的顶端。
### 1.1算法步骤
- 比较相邻的两个元素。若第一个比第二个大，则交换位置，将小元素放在前面；
- 对每一对相邻的元素都执行相同的操作，从开始第一对到最后一对，排序之后，最后一个元素应该是最大的数；
- 除去最后一个元素，针对所有元素重复1、2两步；
- 重复1~3步，直到排序完成。
![](1.冒泡排序.gif)

### 1.2代码实现
```
function bubbleSort(arr) {
    var len = arr.length;
    for (var i = 0; i < len - 1; i++) {
        for (var j = 0; j < len - 1 - i; j++) {
            if (arr[j] > arr[j+1]) {        // 相邻元素两两对比
                var temp = arr[j+1];        // 元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}
```
## <table><tr><td bgcolor=Gold><font size=5>2.选择排序（Selection Sort）</font></td></tr></table>
选择排序是一种简单直观的排序算法。基本思想是：首先在未排序序列中找到最小（大）的元素，存放到排序序列的起始位置，然后再从剩余的未排序元素中选出最小（大）元素，放到已排序序列的末尾。以此类推，直到所有元素都被选择完。
### 2.1算法步骤
假设有n个数据，那么可以通过n-1次直接选择排序得到有序结果。具体的算法如下：
- 初始状态：无序区为R[1..n]，有序区为空；
- 第i趟排序(i=1,2,3…n-1)：排序之前的有序区为R[1..i-1]，无序区为R(i..n）。该趟排序从无序区中选择出关键字最小的记录R[k]，将它与无序区的第1个记录R交换，排序之后的新有序区为R[1..i]，新无序区为R[i+1..n）；
- n-1次排序结束，数组最终排序完成。
![](2.选择排序.gif)

### 2.2代码实现
```
function selectionSort(arr) {
    var len = arr.length;
    var minIndex, temp;
    for (var i = 0; i < len - 1; i++) {
        minIndex = i;
        for (var j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex]) {     // 寻找最小的数
                minIndex = j;                 // 将最小数的索引保存
            }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
    return arr;
}
```
### 2.3算法分析
该算法表现非常稳定，是最稳定的排序算法之一。因为无论什么数据进去都是O(n2)的时间复杂度，所以使用该算法时，数据规模越小越好。好处在于不占用额外的内存空间。理论上讲，选择排序可能是能被最多人想到的排序算法。
## <table><tr><td bgcolor=Gold><font size=5>3.插入排序（Insertion Sort）</font></td></tr></table>
插入排序是一种简单直观的排序算法。基本思想是：通过构建有序数列，对于未排序的数据，在已排序的序列中从后向前扫描，找到相应位置并插入。
### 3.1算法步骤
一般来说，插入排序采用in-place在数组上实现。具体的算法如下：
- 第一个元素可以视为已经被排序；
- 取出下一个元素，在已排序的元素序列中，从后向前扫描；
- 若已排序数列中的旧元素大于新元素，则将旧元素移到下一个位置；
- 重复步骤3，直到找到已排序数列中的旧元素小于或等于新元素的位置；
- 将新元素插入该位置；
- 重复步骤2~5。
![](3.插入排序.gif)

### 3.2代码实现
```
function insertionSort(arr) {
    var len = arr.length;
    var preIndex, current;
    for (var i = 1; i < len; i++) {
        preIndex = i - 1;
        current = arr[i];
        while (preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    return arr;
}
```
### 3.3算法分析
插入算法在实现上通常使用in-place排序，所以只需要O(1)的额外空间，因而在从后向前扫描的过程中，需要反复把已排序元素逐步向后移动位置，为新元素提供插入空间。
## <table><tr><td bgcolor=Gold><font size=5>4.希尔排序（Shell Sort）</font></td></tr></table>
1959年由Shell发明,是第一个突破O(n2)的排序算法，是插入排序的改进版。它和插入排序的不同之处在于，它会优先比较距离较远的元素。所以希尔排序又叫做缩小增量排序。
### 4.1算法步骤
将整个待排序的序列分割称为若干子序列，分别进行直接插入排序，具体的算法如下：
- 选择一个增量序列t1，t2，…，tk，其中ti>tj，tk=1；
- 按增量序列个数k，对序列进行k次排序；
- 每次排序根据对应的增量ti，将待排序的数列分割为若干长度为m的子序列，分别对子序列进行直接插入排序。只有当增量因子变为1时，将整个数列作为一整个序列来处理，序列长度即为整个数列的长度。
![](4.希尔排序.gif)

### 4.2代码实现
```
function shellSort(arr) {
    var len = arr.length;
    for (var gap = Math.floor(len / 2); gap > 0; gap = Math.floor(gap / 2)) {
        // 注意：这里和动图演示的不一样，动图是分组执行，实际操作是多个分组交替执行
        for (var i = gap; i < len; i++) {
            var j = i;
            var current = arr[i];
            while (j - gap >= 0 && current < arr[j - gap]) {
                 arr[j] = arr[j - gap];
                 j = j - gap;
            }
            arr[j] = current;
        }
    }
    return arr;
}
```
### 4.3算法分析
希尔序列的核心在于间隔序列的设定。既可以提前设定好间隔序列，也可以动态的定义间隔序列。动态定义间隔序列的算法出自《算法（第4版）》。
## <table><tr><td bgcolor=Gold><font size=5>5.归并排序（Merge Sort）</font></td></tr></table>
归并排序是建立在归并操作上的一种有效的排序算法。该算法是分治法（Divide and Conquer）的一个典型的应用。基本思想是：将已有的子序列合并，得到完全有序的序列。即先让每个子序列有序，再使得子序列段间有序。若将两个有序表合并成为一个有序表，则可以称作2路归并。
### 5.1算法步骤
- 把长度为n的输入序列分成两个长度为n/2的子序列；
- 对这两个子序列分别采用归并排序；
- 将两个排序好的子序列合并成为一个最终的有序的序列。
![](5.归并排序.gif)

### 5.2代码实现
```
function mergeSort(arr) {
    var len = arr.length;
    if (len < 2) {
        return arr;
    }
    var middle = Math.floor(len / 2),
        left = arr.slice(0, middle),
        right = arr.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
    var result = [];

    while (left.length>0 && right.length>0) {
        if (left[0] <= right[0]) {
            result.push(left.shift());
        } else {
            result.push(right.shift());
        }
    }

    while (left.length)
        result.push(left.shift());

    while (right.length)
        result.push(right.shift());

    return result;
}
```
### 5.3 算法分析
归并排序是一种稳定的排序方法。和选择排序一样，归并排序的性能不受输入数据的影响，但是表现比选择排序要好得多，因为时间复杂度始终为O(nlogn）。代价是需要额外的内存空间。
## <table><tr><td bgcolor=Gold><font size=5>6.快速排序（Quick Sort）</font></td></tr></table>
快速排序的基本思想是：通过一趟排序将待排序的数据分割成为独立的两部分。其中一个部分记录的数据均比另一个部分的数据小，那么可以分别对这两部分的数据继续进行排序，从而达到整个序列有序的目的。
### 6.1算法步骤
快速排序使用分治法把一个串(list)分成两个子串(sub-lists)。具体的算法如下：
- 从数列中挑出一个元素，称为“基准”(pivot);
- 重新排序数列，将数列中比基准值小的数据放在基准前面，比基准值大的数据放在基准后面（相同的数据可以放到任意一边）。在该分区退出之后，该基准就处于数列的中间位置。这个操作称为分区（partition）操作；
![](6.快速排序.gif)

### 6.2代码实现
```
function quickSort(arr, left, right) {
    var len = arr.length,
        partitionIndex,
        left = typeof left != 'number' ? 0 : left,
        right = typeof right != 'number' ? len - 1 : right;

    if (left < right) {
        partitionIndex = partition(arr, left, right);
        quickSort(arr, left, partitionIndex-1);
        quickSort(arr, partitionIndex+1, right);
    }
    return arr;
}

function partition(arr, left ,right) {     // 分区操作
    var pivot = left,                      // 设定基准值（pivot）
        index = pivot + 1;
    for (var i = index; i <= right; i++) {
        if (arr[i] < arr[pivot]) {
            swap(arr, i, index);
            index++;
        }
    }
    swap(arr, pivot, index - 1);
    return index-1;
}

function swap(arr, i, j) {
    var temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```
## <table><tr><td bgcolor=Gold><font size=5>7.堆排序（Heap Sort）</font></td></tr></table>
堆排序是指利用堆这种数据结构所设计的一种排序算法。堆是一个近似完全二叉树的结构，并同时满足堆的性质：即子节点的键值或索引总是小于（大于）它的父节点。
### 7.1算法步骤
- 将初始待排序数列(R1,R2….Rn)构建成大顶堆，此堆为初始的无序区；
- 将堆顶元素R[1]与最后一个元素R[n]交换，此时新无序区为(R1,R2,……Rn-1)，新有序区为(Rn),且满足R[1,2…n-1]<=R[n]；
- 由于交换后新的堆顶R[1]可能违反堆的性质，因此将当前无序区(R1,R2,……Rn-1)调整为新堆，然后再次将R[1]与无序区最后一个元素交换，得到新无序区为(R1,R2….Rn-2)，新有序区为(Rn-1,Rn)。
- 不断重复此过程，直到有序区元素个数为n-1，则整个排序过程完成。
![](7.堆排序.gif)

### 7.2代码实现
```
var len;    // 因为声明的多个函数都需要数据长度，所以把len设置成为全局变量

function buildMaxHeap(arr) {   // 建立大顶堆
    len = arr.length;
    for (var i = Math.floor(len/2); i >= 0; i--) {
        heapify(arr, i);
    }
}

function heapify(arr, i) {     // 堆调整
    var left = 2 * i + 1,
        right = 2 * i + 2,
        largest = i;

    if (left < len && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < len && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        swap(arr, i, largest);
        heapify(arr, largest);
    }
}

function swap(arr, i, j) {
    var temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

function heapSort(arr) {
    buildMaxHeap(arr);

    for (var i = arr.length - 1; i > 0; i--) {
        swap(arr, 0, i);
        len--;
        heapify(arr, 0);
    }
    return arr;
}
```
## <table><tr><td bgcolor=Gold><font size=5>8.计数排序（Counting Sort）</font></td></tr></table>
计数排序的核心在于将输入的数据值转化为键存储在额外开辟的数组空间中。作为一种线性时间复杂度的排序，计数排序要求输入的数据必须是**有确定范围的整数**。
### 8.1算法步骤
- 找出待排序数组中的最大和最小元素；
- 统计数组中每个值为i的元素出现的次数，存入数组C的第i项；
- 对所有的计数累加（从C中的第一个元素开始，每一项和前一项相加）；
- 反向填充目标数组：将每个元素i放在新数组的第C(i)项，每放一个元素就将C(i)减去1。
![](8.计数排序.gif)

### 8.2代码实现
```
function countingSort(arr, maxValue) {
    var bucket = new Array(maxValue + 1),
        sortedIndex = 0;
        arrLen = arr.length,
        bucketLen = maxValue + 1;

    for (var i = 0; i < arrLen; i++) {
        if (!bucket[arr[i]]) {
            bucket[arr[i]] = 0;
        }
        bucket[arr[i]]++;
    }

    for (var j = 0; j < bucketLen; j++) {
        while(bucket[j] > 0) {
            arr[sortedIndex++] = j;
            bucket[j]--;
        }
    }

    return arr;
}
```
### 8.3算法分析
计数算法是一个稳定的排序算法。当输入的元素是n个0到k之间的整数时，时间复杂度为O(n+k)，空间复杂度也是O(n+k)，它的排序速度快于任何比较排序算法。当k不是很大且序列比较集中时，计数排序是一个很有效的排序算法。
## <table><tr><td bgcolor=Gold><font size=5>9.桶排序（Bucket Sort）</font></td></tr></table>
桶排序是计数排序的升级版。它利用了函数的映射关系，高效与否的关键在于这个映射函数。基本思想是：假设输入数据服从均匀分布，将数据分到有限数量的桶里，每个桶再分别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排）。
### 9.1算法步骤
- 设定一个定量的数组当做空桶；
- 遍历输入数据，并且把数据一个个放到对应的桶中；
- 对每个不是空的桶进行排序；
- 从不是空的桶里把已排序的数据拼接起来。
![](9.桶排序.png)

### 9.2代码实现
```
function bucketSort(arr, bucketSize) {
    if (arr.length === 0) {
      return arr;
    }

    var i;
    var minValue = arr[0];
    var maxValue = arr[0];
    for (i = 1; i < arr.length; i++) {
      if (arr[i] < minValue) {
          minValue = arr[i];                // 输入数据的最小值
      } else if (arr[i] > maxValue) {
          maxValue = arr[i];                // 输入数据的最大值
      }
    }

    // 桶的初始化
    var DEFAULT_BUCKET_SIZE = 5;            // 设置桶的默认数量为5
    bucketSize = bucketSize || DEFAULT_BUCKET_SIZE;
    var bucketCount = Math.floor((maxValue - minValue) / bucketSize) + 1;
    var buckets = new Array(bucketCount);
    for (i = 0; i < buckets.length; i++) {
        buckets[i] = [];
    }

    // 利用映射函数将数据分配到各个桶中
    for (i = 0; i < arr.length; i++) {
        buckets[Math.floor((arr[i] - minValue) / bucketSize)].push(arr[i]);
    }

    arr.length = 0;
    for (i = 0; i < buckets.length; i++) {
        insertionSort(buckets[i]);                      // 对每个桶进行排序，这里使用了插入排序
        for (var j = 0; j < buckets[i].length; j++) {
            arr.push(buckets[i][j]);
        }
    }

    return arr;
}
```
### 9.3算法分析
桶排序最好情况下的时间复杂度为O(n)，桶排序的时间复杂度，取决与对各个桶之间数据进行排序的时间复杂度，因为其它部分的时间复杂度都为O(n)。很显然，桶划分的越小，各个桶之间的数据越少，排序所用的时间也会越少。缺点是相应的空间消耗就会增大。
## <table><tr><td bgcolor=Gold><font size=5>10.基数排序（Radix Sort）</font></td></tr></table>
基数排序是按照数列的低位先排序（例如个位），然后收集；再按照数列的高位排序（例如十位），然后再收集；以此类推，直到最高位。有时候有些属性有优先级顺序，先按低优先级排序，再按高优先级排序。最后的结果就是高优先级在前，高优先级相同的话则低优先级高的在前。
### 10.1算法步骤
- 取得数组中的最大数，并且取得数组的位数；
- arr为原始数组，从最低位开始每个位组成radix数组；
- 对radix进行计数排序（利用计数排序适用于小范围数的特点）。
![](10.基数排序.gif)

### 10.2代码实现
```
var counter = [];
function radixSort(arr, maxDigit) {
    var mod = 10;
    var dev = 1;
    for (var i = 0; i < maxDigit; i++, dev *= 10, mod *= 10) {
        for(var j = 0; j < arr.length; j++) {
            var bucket = parseInt((arr[j] % mod) / dev);
            if(counter[bucket]==null) {
                counter[bucket] = [];
            }
            counter[bucket].push(arr[j]);
        }
        var pos = 0;
        for(var j = 0; j < counter.length; j++) {
            var value = null;
            if(counter[j]!=null) {
                while ((value = counter[j].shift()) != null) {
                      arr[pos++] = value;
                }
          }
        }
    }
    return arr;
}
```
### 10.3算法分析
1.基数排序是分别排序，分别收集，所以总体上是稳定的。不过基数排序的性能比桶排序差一点，每一次数据的桶分配都需要O(n)的时间复杂度，且分配之后得到的新的数据序列又需要O(n)的时间复杂度。假如待排序的数据可以分为d组，那么基数排序的时间复杂度将是O(d*2n)，当然d要远远小于n，因此基本上还是线性级别的。
2.基数排序的空间复杂度为O(n+k)，其中k为桶的数量。一般来说n>>k，因此额外空间需要大概n个左右。





































