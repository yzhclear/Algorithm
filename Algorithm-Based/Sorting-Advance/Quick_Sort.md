![](https://github.com/yzhclear/Algorithms/blob/master/img/quickSort_1.png)
```
// 对arr[l...r]部分进行partition操作
// 返回p，使得arr[l...p-1] < arr[p] ; arr[p+1...r] > arr[p]
int partition(int arrp=[], int l, int r) {

    int v = arr[l];

    // arr[l+1...j] < v ; arr[j+1...i) > v
    int j = l;
    for( int i = l + 1; i <= r ; i ++ ) {
        if( arr[i] < v ) {
            swap( arr[j+1], arr[i]);
            j ++;
        }
    }

    swap( arr[l], arr[j]);

    return j;
}

// 对arr[l...r]部分进行快速排序
void __quickSort(int arr[], int l, int r) {
    if( l >= r )
        return;

    int p = __partition(arr, l, r);
    __quickSort(arr, l, p-1);
    __quickSort(arr, p+1, r);
}

void quickSort( int arr[], int n) {
    __quickSort(arr, 0, n-1);
}
```
归并排序每次都是平均的将数组分成两半，而快速排序分出来的两个子数组长度可能不一样。   
当数组近乎有序或者就是有序数组时，而每次选择的元素`v`都是最小的元素，即为最左侧的元素，快速排序的时间复杂度就会退化为O(n^2)   
因此需要编写一个随机算法，来随机化选择元素`v`。然后当数组中未排序的元素变的很少时，利用插入排序进行优化
```
// 优化1

// 对arr[l...r]部分进行partition操作
// 返回p，使得arr[l...p-1] < arr[p] ; arr[p+1...r] > arr[p]
int partition(int arrp=[], int l, int r) {

    swap(arr[l], arr[rand()%(r-l+1)+l]);
    int v = arr[l];

    // arr[l+1...j] < v ; arr[j+1...i) > v
    int j = l;
    for( int i = l + 1; i <= r ; i ++ ) {
        if( arr[i] < v ) {
            swap( arr[j+1], arr[i]);
            j ++;
        }
    }

    swap( arr[l], arr[j]);

    return j;
}

// 对arr[l...r]部分进行快速排序
void __quickSort(int arr[], int l, int r) {

    if( r - l <= 15 ) {
        insertionSort(arr, l, r);
        return;
    }

    int p = __partition(arr, l, r);
    __quickSort(arr, l, p-1);
    __quickSort(arr, p+1, r);
}

void quickSort( int arr[], int n) {

    srand(time(NULL));
    __quickSort(arr, 0, n-1);
}
```
当数组中出现大量的重复元素时，partition操作就会将数组划分成极度不平衡的两部分，快速排序的时间复杂度就会退化成O(n^2)。所以再应该对partition操作进行优化    
![](https://github.com/yzhclear/Algorithms/blob/master/img/quickSort_2.png)    
```
// 优化2

// 对arr[l...r]部分进行partition操作
// 返回p，使得arr[l...p-1] < arr[p] ; arr[p+1...r] > arr[p]
int partition2(int arrp=[], int l, int r) {

    swap(arr[l], arr[rand()%(r-l+1)+l]);
    int v = arr[l];

    // arr[l+1...i] <= v ; arr[j...r) >= v
    int i = l + 1, j = r;
    while(true) {
        while( i <= r && arr[i] < v ) i ++;
        while( j >= l + 1 && arr[i] > v ) j --;
        if( i > j ) break;

        swap( arr[i], arr[j] );
        i ++;
        j --;
    }

    swap( arr[l], swap[j] );

    return j;

}

// 对arr[l...r]部分进行快速排序
void __quickSort(int arr[], int l, int r) {

    if( r - l <= 15 ) {
        insertionSort(arr, l, r);
        return;
    }

    int p = __partition2(arr, l, r);
    __quickSort(arr, l, p-1);
    __quickSort(arr, p+1, r);
}

void quickSort( int arr[], int n) {

    srand(time(NULL));
    __quickSort(arr, 0, n-1);
}
```   
最后来看一下三路快排是如何实现的     
![](https://github.com/yzhclear/Algorithms/blob/master/img/quickSort_3.png)     
```
void __quickSort3Ways(int arr[], int l, int r) {

    if ( r - l <= 15 ) {
        insertionSort(arr, l, r);
        return;
    }

    // partition
    swap(arr[l], arr[rand()%(r-l+1)+l]);
    int v = arr[l];

    int lt = l;     // arr[l+1...lt] < v
    int gt = r + 1;  // arr[gt...r] > v
    int i = l + 1;   // arr[lt+1...i) == v

    while( i < gt ) {
        if ( arr[i] < v ) {
            swap( arr[i], arr[lt+1] );
            lt ++;
            i ++;
        }
        else if ( arr[i] > v ) {
            swap( arr[i], arr[gt-1] );
            gt --;
        }
        else { // arr[i] == v
            i ++;
        }
    }

    swap( arr[l], arr[lt] );

    __quickSort3Ways(arr, l, lt-1);
    __quickSort3Ways(arr, gt, r);

}

void quickSort3Ways(int arr[], int n) {
    scrand(time(NULL));
    __quickSort3Ways( arr, 0, n-1 );
}
```
