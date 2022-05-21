**思路**

进行k(最短路径的变数)次循环

每次循环：<br>
1.先备份数组(防止串联)<br>
2.然后遍历每条边：进行松弛操作`dist[b]=min(dist[b],dist[a]+w)`

```
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 510, M = 10010;

//只要能将每条边保存下来即可
struct Edge
{
    int a, b, w;
}edges[M];

int n, m, k;//k代表最短路径最多有k条边
int dist[N];
int back[N];//备份数组防止串联

void bellman_ford()
{
    //一定要记得初始化
    memset(dist,0x3f,sizeof dist);
    dist[1]=0;

    //k次循环
    for(int i=0;i<k;i++)
    {
        memcpy(back,dist,sizeof dist);//备份数组
        for(int j=0;j<m;j++)//遍历所有边
        {
            auto e=edges[j];
            dist[e.b]=min(dist[e.b],back[e.a]+e.w);
        }
    }
}

int main()
{
    cin>>n>>m>>k;

    //m条边
    for (int i = 0; i < m; i ++ )
    {
        int a, b, w;
        cin>>a>>b>>w;
        edges[i] = {a, b, w};
    }

    bellman_ford();

    if (dist[n] > 0x3f3f3f3f / 2) puts("impossible");
    else printf("%d\n", dist[n]);

    return 0;
}

作者：柠檬味的猪已黑化
链接：https://www.acwing.com/activity/content/code/content/3498366/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
