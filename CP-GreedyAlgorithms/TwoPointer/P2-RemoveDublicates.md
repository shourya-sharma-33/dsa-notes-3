Remove the dublicates from sorted array

arr=[0,0,1,1,1,2,5,5,5,5,6,6]

to arr=[0,1,2,5,6]

```cpp
int removeDuplicates(vector<int>& nums){
    int n=nums.size();
    int start=0;
    for (int i=1; i<n; i++){
        if(nums[i]!=nums[start]){
            start+=1;
            nums[start]=nums[i];
        }
    }
    return start+1
}
```