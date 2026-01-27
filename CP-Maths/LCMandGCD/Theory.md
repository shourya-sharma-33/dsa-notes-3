explain LCM and GCD chatgpt


remember that gcd(60, 45) and gcd(45, 60%45) = gcd(45, 15)
gcd(15, 45%15) =
gcd(0, 15)

also remember that a*b = gcd(a, b) x lcm(a, b)

we can find out lcm from this

```cpp
int gcd(int a, int b){
    if(b==0){
        return a;
    }
    return gcd(b, a%b);
}

int lcm(int a, int b){
    return (a*b)/gcd(a, b);
}
```