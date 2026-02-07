the basic logic is

n is a prime number and we have to find 2 prme numbers (a, b) such that a+b=n

n -> 2 
|
+--> (n-2) is prime (2, n-2) is answer else (-1) ans 

say for 11

2, 11-2 =  2, 9 but 9 aint prime so it coudnt

```cpp
void solve(int n){
    if(checkPrime(n-2)){
        cout<<"2 "<<n-2<<"\n";
    }
    else{
        cout << "-1\n"
    }
}
```