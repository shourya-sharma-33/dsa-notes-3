sort colors

given  an array nums with n objects colored red, white and blue sort them inplace so that objects of same color are adjacent with the colors in order of red white and blue

we will use the integer 0, 1, 2 to represent the color red white and blue respectively

[1,0,2,2,1,0,1,0,0,2,1]
to
[1,1,1,1,0,0,0,0,2,2,2]

```cpp
void sortColors(vector<int>& nums){
    int n = nums.size();
    int left = 0;
    int right = n-1;
    int i=0;

    while (i<=right)
    {
        if(arr[i]==0)
        {
            swap(arr[i], arr[left]);
            left++;
            i++;
        }
        else if(arr[i]==2)
        {
            swap(arr[i],arr[right]);
            right--;
        }
        else
        {
            i++;
        }
    }
}
```