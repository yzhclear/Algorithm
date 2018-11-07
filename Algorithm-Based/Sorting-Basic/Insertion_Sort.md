插入排序的思想是:   
从数组的第二个元素开始(因为第一个元素只有一个元素，默认是有序的)，不停地与前面的元素进行比较，如果小于的话，就交换位置。直至数组的最后一个元素。
```
void insertionSort(int arr[], int n) {

    for( int i = 1 ; i < n ; i ++ ) {

        //寻找元素arr[i]合适插入的位置
        for( int j = i ; j > 0 ; j -- ) {
            if( arr[j] < arr[j-1] )
                swap( arr[j], arr[j-1] )
            else
                break;
        }
    }
}
```
插入排序的优化：   
在前面，当发现当前元素`i`比它前一个元素`i-1`要小时，我们不着急做交换操作，而是复制一个`i`的副本`i'`，将这个`i'`与`i-1`进行比较，如果发现`i'`小于`i-1`,
则将元素`i-1`的值赋值给元素`i`,如果大于的话，就将当前元素的值赋值为`i'`。即将原来比较之后的交换操作变成赋值操作，性能更优。

```
void insertionSort(int arr[], int n) {

    for( int i = 1 ; i < n; i ++ ) {
        //寻找元素arr[i]合适插入的位置
        int e = arr[i];
        int j;
        for( j = i ; j > 0 && arr[j-1] > e ; j -- ) {
            arr[j] = arr[j-1];
        }
        arr[j] = e;
    }
}
```
因为插入排序第二层循环可以提前结束，而选择排序第一层第二层循环需要扫描数组中每一个元素，所以插入排序理论上要比选择排序快。    
当一个数组近乎有序时，插入排序的效率会非常高。    
插入排序是稳定的排序算法。