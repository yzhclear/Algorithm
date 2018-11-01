冒泡排序(稳定)
```
void bubbleSort(int arr[], int n) {

    bool swapped;

    do {
        swapped = false;

        for( int i = 1 ; i < n ; i ++ ) {
            if( arr[i-1] > arr[i] ) {
                swap(arr[i-1], arr[i]);
                swapped = true;
            }
        }

        n --;
    }while(true);
}
```
