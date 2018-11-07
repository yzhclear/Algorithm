二分查找法
```
int binarySearch(int arr[], int n, int target) {
    int l = 0,
        r = n - 1;

    while ( l <= r ) {

        // int mid = (l + r) / 2;
        int mid = l + (l-r)/2; //防止整型溢出

        if( arr[mid] == target)
            return mid;

        if( arr[mid] < target )
            r = mid - 1;
        else
            l = mid + 1;
    }

    return -1;

}
```

用递归的方式写二分查找法
```
int __binarySearch2(int arr[], int l, int r, int target){

    if( l > r )
        return -1;

    int mid = (l+r)/2;
    if( arr[mid] == target )
        return mid;
    else if( arr[mid] > target )
        return __binarySearch2(arr, 0, mid-1, target);
    else
        return __binarySearch2(arr, mid+1, r, target);

}

int binarySearch2(int arr[], int n, int target){

    return __binarySearch2( arr , 0 , n-1, target);
}
```
