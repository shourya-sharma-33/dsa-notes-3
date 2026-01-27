basically traversing in the array

its time complexity is o(n)

arr = 5 1 8 4 2 0 4

n = 7 and (target) t = 6

```cpp
int linearSearch (int n, vector<int>&v, int target){
    for (int i=0; i<n ; i++){
        if (arr[i]== target){
            return i;
        }
    }
    return -1;
}
```