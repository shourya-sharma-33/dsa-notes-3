kth special number -> diffrent power of n

basically

for decimal : 5 
for binary : 101
for 4th special number : 4^2 x 1 + 4^1 x 0 + 4^0 x 1 = 17 


number to binary to decimal with power of n
```cpp

string decimalToBinary(int n){
    string binary = "";

    while(n>0){
        int rem = n%2;
        binary += to_string(rem);
        n/=2;
    }

    reverse(binary.begin(), binary.end());
    return binary;
}

int binaryToDecimal(string binary, int m){
    int n = binary.size();
    int p = 1;
    int decimal = 0;

    for (int i=n-1; i>=0; i--){
        if(binary[i]=='i'){
            decimal+=p;
        }
        p*=m;
    }

    return decimal;
}

int main(){
    int n;
    cin>>n;

    cout<<decimalToBinary(n)<<"\n"
    return 0;
}
```