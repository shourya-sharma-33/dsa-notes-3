basically we have number of numbers and sequence of 1s and 2s

and we can change the order however we want 

and then we make a new string of prefix sums 

a prefix sum is like

1 2 1 1 2 1
(1) (1+2) (1+2+1) (1+2+1+1) (1+2+1+1+2) (1+2+1+1+2+1) 

and we have to check prime numbers in this

like
9
1 1 2 1 1 1 2 1 1
or
1 2 4 5 6 7 9 10 11
primes are (2, 5, 7, 11)

now we can rearrange 1 1 2 1 1 1 2 1 1

```cpp
int main(){
    int n;
    cin>>n;

    int ones = 0; twos = 0;

    for (int i = 0; i<n ; i++){
        int x;
        cin>>x;
        if (x==1) ones++;
        else two++;
    }

    if (twos == 0){
        for (int i=0; i<ones; i++) cout << "1 ";
    }
    else if (ones == 0){
        for (int i=0; i<twos; i++) cout << "2 ";
    }
    else{
        cout<<"2 1  ";
        for (int i=0; i<twos-1; i++) cout << "2 ";
        for (int i=0; i<ones-1; i++) cout << "1 ";
    }
}
```

please tell me how the logic works man chatgpt