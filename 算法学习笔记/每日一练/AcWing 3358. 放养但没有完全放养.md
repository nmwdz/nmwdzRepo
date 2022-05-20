
```
#include<iostream>
#include<string>

using namespace std;

const int N = 1010;



int main()
{
    string std,hear;
    cin>>std>>hear;
    
    int ans=1;

    for(int i=1;i<hear.size();i++)
    {
        if(std.find(hear[i])<=std.find(hear[i-1])) ans++;
    }
    
    cout<<ans;
}
```
