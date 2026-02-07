binary search is better for searching

unsorted -(nlog2n) sorted- (log2n) - search


first og all we strictly want a sorted array
we will sort the array in our algorithm

however in production systems
the data is already sorted, or is made in such a way their algorithm is

so in production systems we expect data to be regularly searched quaries out of to be sorted

so practially complexity is log2n

to put that in perspective

say we have 1024 items in array
with o(n) linear we need to do 1024 perations
in binary seacrch we only need 10

this is insane optimisations
however companies have better algorithms and overall well planned code infrastructure


how do we work with it then?

```
arr = 2 4 7 8 9 11 15 24 30
```

so we put an l and an r in the left and rightmost endpoints respectibvely and a pointer in middle
the target to be searched is say mid = 9

now we compare middle value to that to be searched
if its greater than the middle value
we shoft l to mid point and middle point to now the middle point of the l and r

and keep going unyil we find

it chips off the array half each time

```cpp
int search(vector<int>& nums, int target){
    int n = nums.size();
    int l = 0;
    int r = n-1;

    while(l<=r){
        int mid = (l+r)/2;
        if (nums[mid]==target){
            return mid;
        } else if(target>= nums[mid]){
            l = mid + l;
        }
        else{
            r=mid-l;
        }
    }
    return -1;
}
```


