explain what two pointer is

here we solve a problem and see whats up

say we have a sorted array and we have to find two numbers that return this sum

Sorted Array

arr = [ 5, 7, 11, 20, 35, 40, 52 ]
n = 7 target = 42

given a 1-indexed array of integers `numbers` that is already sorted in non descending order, find two numbers suc that they add up to a specific taret number let these two numbers be numbers[index] and numbers[index] where i<= index1 < index2 <= numbers.lenght

return the indices of the two numbers index1 and index2 added by one as an inteher aeeay [index1, index2] of length 2.

the tests are generated such that there is exactly one solutoon

u may not use same element twice

```cpp
vector<int> twoSum(vector<int>& numbers, int target){
    int n = numbers.size();
    for (int i=0; i<n; i++){
        for (int j=i+1; j<n; j++){
            if ((numbers[i]+numbers[j]) == target){
                return{i+1, j+1}
            }
        }
    }
    return {-1, -1};
}
```


this approach is brute force


hint is that this array is sorted so

the first one is the smallest and the last one is largest

arr = [ 5, 7, 11, 20, 35, 40, 52 ]
sum = 5 + 52 = 57
57>42
so we shift the j to get lower
40 + 5 = 45 > 42
now we shift j
35+5 = 40

40 is less than 42
we shift i for greater

35 + 7 = 42

```cpp
vector<int> twoSum(vector<int>& numbers, int target){
    int n = numbers.size();

    int i = 0;
    int j = n-1;

    while(i>j){
        int sum = numbers[i]+numbers[j];
        if(sum==target){
            return {i+1, j+1};
        }
        else if(sum<target){
            i++;
        }
        else{
            j--;
        }
    }
    return {-1, -1}
}
```