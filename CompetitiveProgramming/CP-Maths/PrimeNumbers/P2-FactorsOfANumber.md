```cpp
void printFactors(int n){
    for (int i =1; i<=n; i++){
        if(n%i==0){
            cout <<i << "";
        }
    }
}
```

we can with better time complexity btw

think about it

if for 12, we found out factor is 2, then without iterating all the way by 12/2 = 6

so we really just have to iterate half way
and this reduces time complexity to sqrt(n)

```cpp
void printFactors(int n){
    for (int i =1; i<=n; i++){
        if(n%i==0){
            cout <<i << "";
            if(i!=(n/i)){
                cout<<n/i<<" ";
            }
        }
    }
}
```
we can also apply in primechecking fucntin
we can only go to the sqrt to n and it will verify 
i is less than sqrt of n
```cpp
bool checkPrime (int n) {
    if(n==0||n==1) return false;

    for (int i=2, i*i<=n; i++){
        if(n%i==0){
            return false
        }
    }

    return true;
}
```
