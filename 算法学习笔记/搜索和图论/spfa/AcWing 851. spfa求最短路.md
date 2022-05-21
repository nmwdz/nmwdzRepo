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

int spfa()
{
    memset(dist,0x3f,sizeof dist);
    dist[1]=0;

    queue<int> q;
    q.push(1);
    st[1]=true;

    while(q.size())
    {
        //取出队头元素
        auto t = q.front();
        q.pop();

        st[t] = false;

        //拓展这个节点邻接点的距离
        for(int i=h[t];i!=-1;i=ne[i])
        {
            int j=e[i];//i只是个下标(指针)，e中在存的是i这个下标对应的点

            //初始化dist数组为无穷大，所以离起点最短距离的t点与权重即为拓展后的距离
            if(dist[j]>dist[t]+w[i])
            {
                dist[j]=dist[t]+w[i];
                if (!st[j])//如果这个点没被用过，将其入队
                {
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }

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
    int t=spfa();
    if(t==0x3f3f3f3f) cout<<"impossible";
    else cout<<t<<endl;
    return 0;
}
```
