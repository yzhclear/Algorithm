选择排序的思想是从数组的第一个元素(i)开始，寻找在[i, n)区间中最小的元素，将其与arr[i]交换位置。    
注：n为数组的长度
```
void selection( int arr[], int n ) {

    for( int i = 0 ; i < n ; i ++ ) {
        //寻找[i, n)区间里的最小值
        int minIndex = i;
        for( int j = i + 1 ; j < n ; j ++ )
            if( arr[j] < arr[minIndex] )
                minIndex = j;

        swap( arr[i], arr[minIndex] );
    }
}
```
