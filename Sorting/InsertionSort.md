we go like

14 9 15 12 6 8 13

is 14 sorted : yes
is 14 9 sorted : no -> sort -> 9 14
is 9 14 15 sorted : yes
is 9 14 15 12 sorted : no -> {
    now we validate which is smaller than 12
    15 > 12 : true,
    14 > 12 : true,
    9 > 12 : false,

    now we right shift everything and place12
}

```cpp
void insertionSort(int arr[], int n)
{
    for (inr i = 0; i<=n-1; i++)
    {
        int j = i;
        while(j>0 && arr[j-1]>arr[j])
        {
            int temp = arr[j-1];
            arr[j-1] = arr[j];
            arr[j] = temp;
            j--;
            cout<<"Runs";
        }
    }
}
```