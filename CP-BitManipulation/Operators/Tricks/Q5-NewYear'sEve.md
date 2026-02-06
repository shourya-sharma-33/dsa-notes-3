1 to n array

k = 3 
atmost k = 3 numbers that xor is maximum

say we have

1 2 3 4 5 6

we can choose 6 and 1
6^1 = 7
110 ^ 001 is 111

basically simple thing is
1. we jsut find the number of bits in the largest number
2. turn it into 1111

```cpp
int main(){
    long long n, k;
    cin>>n>>k;

    if (k==1){
        cout<<n<<"\n";
    }

    long long ans = 1;
    while (ans < n){
        ans *= 2;
        ans += 1;
    }

    cout<<ans<<"\n"
    return 0;
}
```