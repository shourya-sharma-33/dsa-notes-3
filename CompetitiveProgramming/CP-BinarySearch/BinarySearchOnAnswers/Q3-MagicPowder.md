4 3
4 3 5 6
11 12 14 20

n = 4
k = 3 (maic powder)
4, 3, 5, 6 gram per ingredient
11 12 14 20 gram available

maxiumum items

we can apply binary search
low = 0  mid =2    high = 10
low = 0  mid =5    high = 10
low = 3

```cpp

bool check (int n, int k, vector<int>&a, vector<int>&b, int mid){
    for (int i=0; i<n; i++){
        int required = a[i]*mid;
        required -= b[i];
        if (required>=0) {
            if(k<= required){
                k-=required;
            }
            else{
                return false;
            }
        }
    }
    return true;
}

int main(){
    int n, k;
    cin>>n>>k;

    vector<int>a(n);
    vector<int>b(n);

    for (int i=0; i<n; i++){
        cin>>a[i];
    }

    for (int i=0; i<n; i++){
        cin>>b[i];
    }

    int low = 0;
    int high = 5000;

    while(low<=high){
        int mid = low + (high + low)/2;
    }

    
    return 0;
}
```