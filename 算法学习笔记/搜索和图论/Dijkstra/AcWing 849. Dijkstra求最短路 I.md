**思路**

将除dist[1]外的所有点的距离初始化为无穷大，点与点之间的距离为无穷大

循环n次：<br>
1.找到剩余没被用过的点中距离最短的点<br>
2.更新所有与这个点相邻的点的最短距离

这样如果distn为无穷大，返回-1<br>
否则返回dist[n]既到起点的距离
```
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;

const int N = 510;

int g[N][N];//为稠密阵所以用邻接矩阵存储
int dist[N];//用于记录每一个点距离第一个点的距离
bool st[N];//用于记录该点的最短距离是否已经确定

int n,m;

int Dijkstra()
{
    memset(dist,0x3f,sizeof dist);

    dist[1]=0;

    for(int i=0;i<n;i++)//n个点更新n次
    {
        int t=-1;//t存储当前访问到的点

        for(int j=1;j<=n;j++)//找到余下点种离起点最小值的点
            if(!st[j]&&(t==-1||dist[t]>dist[j]))
            /*
                当前点的最短距离没被确定
                且(访问的点没被确定 或 当前点的距离比存储t到起点的距离小)
                更新t(既离起点最小值的点)
            */
                t=j;

        st[t]=true;

        //以当前最短的点去初始化所有邻边距离
        for(int j=1;j<=n;j++)
            dist[j]=min(dist[j],dist[t]+g[t][j]);
    }

    if(dist[n]==0x3f3f3f3f) return -1;
    return dist[n];
}

int main()
{
    cin>>n>>m;

    memset(g,0x3f,sizeof g);

    while(m--)
    {
        int a,b,c;
        cin>>a>>b>>c;
        g[a][b]=min(g[a][b],c);//处理重边
    }

    cout<<Dijkstra();

    return 0;
}
```
