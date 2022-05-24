**思路**
```
S为所求的集合
1.dist[i]=INF
2.for 遍历n次：
        找到离集合最近的点
        判断离S最近的点是否联通，不连通则返回正无穷
        将当前离集合S最近的点标记为true
        用t更新所有与t的连边  由于t加入了集合，则t的连边到集合的距离可能被改变，所以遍历一遍所有点来更新
n次更新所有点都加入到集合中
```
```
#include<iostream>
#include<cstring>

using namespace std;

const int N = 510, INF = 0x3f3f3f3f;

int n,m;
int g[N][N];
int dist[N];
int st[N];

int prim()
{
    memset(dist,0x3f,sizeof dist);

    int res=0;
    for(int i=0;i<n;i++)
    {
        //找到距离集合S距离最小点
        int t=-1;
        for(int j=1;j<=n;j++)
            if(!st[j]&&(t==-1||dist[t]>dist[j]))
                t=j;

        //不连通则返回正无穷
        if(i&&dist[t]==INF) return INF;

        //将当前离集合S最近的点标记为true
        if(i) res+=dist[t];
        st[t]=true;

        //用t更新所有与t的连边  由于t加入了集合，则t的连边到集合的距离可能被改变，所以遍历一遍所有点来更新
        for(int j=1;j<=n;j++) dist[j]=min(dist[j],g[t][j]);
    }

    return res;
}

int main()
{
    cin>>n>>m;

    memset(g,0x3f,sizeof g);

    while(m--)
    {
        int a,b,c;
        cin>>a>>b>>c;
        g[a][b]=g[b][a]=min(g[a][b],c);
    }

    int t = prim();

    if(t==INF) cout<<"impossible";
    else cout<<t;

    return 0;
}
```
