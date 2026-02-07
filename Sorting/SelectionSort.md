we find the minimum and replace with minimum index

so psuedocode is

find minimum
put to i = 0 index
change i ++ so now we do replaement at this index
and reiterate post i

simple as hell


```cpp
void selectionSort (int arr[], int n)
{
    for (int i=0; i<=n-2; i++)
    {
        int mini = 1;
        for (int j=1; j<=n-1; j++)
        {
            if(arr[j] < arr[mini])
            {
                mini = j;
            }
        }

        int temp = arr[mini];
        arr[mini] = arr[i];
        arr[i] = temp;
   }
}

int main()
{
    int n;
    cin>>n;
    int arr[n];
    for(int i=0; i<n; i++) cin>> arr[i];
    selectionSort(arr, n);
    for (int i=0; i<n; i++)
    {
        cout<<arr[i]<<" ";
    }
    return 0;
}
```