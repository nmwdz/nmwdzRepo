**思路**

1.一号点的距离初始化为零，其他点初始化成无穷大

2.将一号点放入堆中

3.不断循环，直到堆空，每一次循环中执行的操作为：
```
弹出堆顶
用该点更新临界点的距离，若更新成功就加入到堆中
```
```
#include<iostream>
#include<queue>
#include<cstring>

using namespace std;

typedef pair<int,int> PII;

const int N = 1000010;

int h[N],e[N],ne[N],idx;// 稀疏图用邻接表来存
int w[N];//存权重
int dist[N];//存距离
bool st[N];//存状态

int n,m;

//a b间加上一条权重为c的边
void add(int a,int b,int c)
{
    w[idx]=c;
    e[idx]=b,ne[idx]=h[a],h[a]=idx++;
}

int Dijkstra()
{
    memset(dist,0x3f,sizeof dist);
    dist[1]=0;

    //创建PII类型的小根堆
    priority_queue<PII,vector<PII>,greater<PII>> heap;
    heap.push({0,1});//顺序不能倒，pair排序时是先根据first，再根据second，这里显然要根据距离排序

    while(heap.size())
    {
        //取出堆顶元素
        auto t = heap.top();
        heap.pop();

        int ver = t.second,distance = t.first;
        if(st[ver]) continue;
        st[ver] = true;

        //拓展ver这个节点邻接点的距离
        for(int i=h[ver];i!=-1;i=ne[i])
        {
            int j=e[i];//i只是个下标(指针)，e中在存的是i这个下标对应的点

            //初始化dist数组为无穷大，所以离起点最短距离的t点与权重即为拓展后的距离
            if(dist[j]>distance+w[i])
            {
                dist[j]=distance+w[i];
                heap.push({dist[j],j});
            }
        }
    }

    if(dist[n]==0x3f3f3f3f) return -1;
    return dist[n];
}

int main()
{
    memset(h,-1,sizeof h);

    cin>>n>>m;

    while(m--)
    {
        int a,b,c;
        cin>>a>>b>>c;
        add(a,b,c);
    }

    cout<<Dijkstra()<<endl;
    return 0;
}
```
