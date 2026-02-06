given an array of integers nums calculate the pivot index of this array

the pivot point is the index where the sum of all numbers stricyly to the right of the inde is eql to strictly to the left 

if the index is on the left edge of array then the left sum is 0 because there are no elements to the left this also applies to the right edge of the array

return the leftmost pivot index id no sich index exist -1 return


```cpp
int pivotIndex(vector<int>& nums)
{
    int n = nums.size();
    int totalSum = 0, leftSum = 0;

    for (int i=0; i<n; i++)
    {
        totalSum+=nums[i];
    }

    for (int i = 0; i<n; i++)
    {
        int rightSum = totalSum-leftSum-nums[i];
        if(leftSum==rightSum) return i;
        leftSum+=nums[i];
    }

    return -1;
}
```