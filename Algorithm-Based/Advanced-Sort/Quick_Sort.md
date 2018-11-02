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

    swap( arr[i], arr[j]);

    return j;
}
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
