from 1 to n one number is missing find that

we can also iterate but we can also use xor property

[3, 1, 0, 2, 6, 5]

3^1^0^2^6^5^0^1^2^3^4^5^6^7 = 4 the missing number

```cpp
int missingNumber(vector<int>& nums){
    int x = 0;
    int n = nums.size();

    for (int i=0; i<=n; i++){
        x^=1;
    }

    for(auto &i:nums){
        x^=i;
    }
    return x;
}
```