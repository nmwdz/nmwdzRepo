**思路**

1.将所有边权从小到大排序<br>
2.从小到大枚举每条边a,b 权值为c<br>
如果a,b不连通 则将这条边加入集合中
```
#include<iostream>
#include<algorithm>

using namespace std;

const int N = 100010,M = 200010,INF = 0x3f3f3f3f;
int n,m;
int p[N];//保存并查集

struct Edge
{
    int a,b,w;
    //通过边长进行排序
    bool operator<(const Edge &W)const
    {
        return w<W.w;
    }
}edges[M];

//找到x的祖宗节点
int find(int x)
{
    if(p[x]!=x) p[x]=find(p[x]);
    return p[x];
}

int kruskal()
{
    //按边权从小到大排序
    sort(edges,edges+m);

    //初始化集合
    for(int i=1;i<=n;i++) p[i]=i;

    //res记录的权重和，cnt记录加入树中的节点数
    int res=0,cnt=0;
    for(int i=0;i<m;i++)//遍历每条边
    {
        int a=edges[i].a,b=edges[i].b,w=edges[i].w;

        //如果a,b不在一个集合中，既不连通，就将其加入集合中
        a=find(a),b=find(b);
        if(a!=b)
        {
            p[a]=b;
            res+=w;
            cnt++;
        }
    }

    if(cnt<n-1) return INF;
    return res;
}

int main()
{
    cin>>n>>m;
    for(int i=0;i<m;i++)
    {
        int a,b,w;
        cin>>a>>b>>w;
        edges[i]={a,b,w};
    }

    int t=kruskal();

    if(t==INF) cout<<"impossible";
    else cout<<t;

    return 0;
}
```
