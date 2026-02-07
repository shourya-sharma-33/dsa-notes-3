setting a bit is turning it into 1
clearing is becoming 0

flipping is flipping explain this chatgpt
```
n|(1<<x) : sets the xth bit in the number n
n^(1<<x) : flips the xth bit in the nmber n
n&~(1<<x) : clears the xth bit in the number n
```

give an example in each for x = 1011001;

# Check if a bit is set

basically we will AND it with the number and see whats up

101101 check if the second bit is checked
101101>>2 = 10110
10110 & 1 = 0

its unsigned

```cpp
bool isSet(unsigned int number, int x){
    return (number >> x) & 1;
}
```

# check if integer is power of 2

any power of 2 is 10000000
and one less is 11111111
(explain this gpt)

```cpp
bool isPowerOfTwo(unsigned int n){
    return n && !(n & (n-1));
}
```


# clear the right most set bit
clear the right most bit as in turning the first to the right 1 to 0
10110100
we wanna turn it to 10110000

we do n&(n-1)

# Brian Kernighan Algorithm

counting set bit

```cpp
int countSetBits(int n){
    int count = 0;
    while(n){
n=n&n-1;
count++
    }
    return couny
}
```