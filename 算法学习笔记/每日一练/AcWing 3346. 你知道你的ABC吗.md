**思路：**

由分析可知a[0],a[1]分别为A B

a[7] 为 A + B + C

(原来我自己也能acXD)
```
#include<iostream>
#include<algorithm>

using namespace std;

const int N = 10;

int a[N];

int main()
{
    for(int i=0;i<7;i++) cin>>a[i];

    sort(a,a+7);

    cout<<a[0]<<" "<<a[1]<<" "<<a[6]-a[0]-a[1];
}
```
