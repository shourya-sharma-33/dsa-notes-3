we just compare and swap elements until there is no one left basiclly

```cpp
void bubbleSort(int arr[], int n)
{
    for (int i = n-1; i>=0; i--)
    {
        for (int j=0; j<=i-1; j++)
        {
            if(arr[j]>arr[j+1])
            {
                int temp = arr[j+1];
                arr[j+1] = arr[j];
                arr[j] = temp;
                didSwap = 1;
            }
        }

        if(didSwap == 0)
        {
            break;
        }
        cout<<"runs\n"
    }
}
```