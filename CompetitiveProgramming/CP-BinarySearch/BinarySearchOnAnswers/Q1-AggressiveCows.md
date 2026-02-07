n = 5
c = 3
arr = 1 2 8 4 9

how to do it
basically

0 1x 2x 3 4x 5 6 7 8x 9x 10
x are barns

we just have to find the minimum distance

l = 1    m = 4 (int 4.5)     h = 8 (9 - 1 = 8)
now we check if its possible for  m = 4

now we check for m = 2 and h = 3 and l = 1
now 2 could be

now we check for l = h = 3

l will become greater than h

anseer iss 3


```cpp

bool check (int n, int c, vector<int>&stalls, int mid){
    int cowCount = 1;
    int lastCowPosition = stalls[0];

    for (int i = 1; i< n; i++){
        if ((stalls[i] - lastCowPosition)>=mid){
            cowCount ++;
            lastCowPosition = stalls[i];
        }
    }

    if(cowCount<c){
        return false;
    }
    return true;
}
void solve(){
    int n, c;
    cin>>n>>c;

    vector<int>stalls(n);
    for (int i=0; i<n; i++){
        cin>>stals[i];
    }

     sort(stalls.begin(), stalls.end());

    int low = 1;
    int high = stalls[n-1]-stalls[0];

    while(low<= high){
        int mid= low + (high - low)/2;
        if (check(n, c, stalls, mid)){
            ans = mid;
            low = mid+1;
        }
        else{
            high = mid - 1;
        }
    }
    return ans;
}
```