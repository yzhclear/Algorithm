```
// 将arr[l...mid]和arr[mid+1...r]两部分进行归并
void __merge(int arr[], int l, int mid, int r) {

    int aux[r-l+1];
    for( int i = l ; i <= r ; i ++ )
        aux[r-l] = arr[l];

    int i = l, j = mid + 1;
    for( int k = l; k <= r; k++ ) {

        if( i > mid ) {
            arr[k] = aux[j-l];
            j ++;
        }
        else if( j > r ) {
            arr[k] = aux[i-l];
            i ++;
        }
        else if( aux[i-l] < aux[j-l] ) {
            arr[k] = aux[i-l];
            i ++;
        }
        else {
            arr[k] = aux[j-l];
            j ++;   
        }
    }

}

// 递归使用归并排序，对arr[l..r]范围元素进行排序
void __mergeSort(int arr[], int l, int r) {
    // if( l >= r )
    //    return;

    // 利用插入排序进行优化
    if( r - l <= 15 ) {
        insertSort(arr, l, r);
        return;
    }

    int mid = (l + r)/2;
    __mergeSort(arr, l, mid);
    __mergeSort(arr, mid+1, r);
    if( arr[mid] > arr[mid+1] ) // 优化
        __merge(arr, l, mid, r);
}

void mergeSort(int arr[], int n) {
    __mergeSort( arr, 0, n-1 );
}

void insertionSort(int arr[], int l, int r) {

    for( int i = l+1 ; i <= r ; i ++ ) {

        int e = arr[i];
        int j;
        for( j = i ; j > l && arr[j-1] > e; j -- )
            arr[j] = arr[j-1];

        arr[j] = e;
    }
    return
}
```
O(nlogn)
