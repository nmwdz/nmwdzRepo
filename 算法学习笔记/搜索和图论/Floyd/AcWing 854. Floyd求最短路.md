**思路**

1. 初始化d数组

2. 用k, i, j 去更新d数组

```
#include<iostream>
#include<cstring>

using namespace std;

const int N = 210;

int d[N][N];
int n,m,k;

void Floyd()
{
    for(int k=1;k<=n;k++)
        for(int i=1;i<=n;i++)
            for(int j=1;j<=n;j++)
                d[i][j]=min(d[i][j],d[i][k]+d[k][j]);
}

int main()
{
    cin>>n>>m>>k;

    //初始化

    // for(int i=1;i<=n;i++)
    //     for(int j=1;j<=n;j++)
    //         if(i==j) d[i][j]=0;
    //         else d[i][j]=0x3f3f3f3f;

    memset(d,0x3f,sizeof d);
    for(int i=1;i<=n;i++) d[i][i]=0;

    while(m--)
    {
        int x,y,z;
        cin>>x>>y>>z;
        d[x][y]=min(d[x][y],z);//处理重边
    }

    Floyd();

    while(k--)
    {
        int x,y;
        cin>>x>>y;
        if(d[x][y]>0x3f3f3f3f/2) cout<<"impossible"<<endl;
        else cout<<d[x][y]<<endl;
    }

    return 0;
}
```
