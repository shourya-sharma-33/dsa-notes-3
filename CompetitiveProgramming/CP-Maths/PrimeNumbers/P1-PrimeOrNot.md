program to check if a number is prime or not

there are two solution

if n is 0 or 1 we dont deal with the quetion we return false

we have to start from 2 and devide it with each number

if any of them devides we return false
else true

```cpp
bool checkPrime (int n) {
    if(n==0||n==1) return false;

    for (int i=2, i<=n-1; i++){
        if(n%i==0){
            return false
        }
    }

    return true;
}
```

we can also apply in primechecking fucntin