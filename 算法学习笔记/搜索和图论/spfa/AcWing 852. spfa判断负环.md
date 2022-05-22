**思路**

在原spfa基础上加上cnt[]数组

cnt[]数组的含义：表示点出现的次数

1. 由于spfa第二层循环中遍历的是每个节点的临界点，
只要当一个点出现的次数大于等于n（节点总个数）
抽屉原理，这个图一定存在一个环

2. 由cnt[j]=cnt[t]+1;更新每个点出现的次数
又由于只有当dist[j]>dist[t]+w[i];时dist[t]才会被更新
既 由起点->j的距离大于起点->t->j的距离（说明每一条边为负权）

所以这个环一定是负环

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
int cnt[N];

int n,m;

//a b间加上一条权重为c的边
void add(int a,int b,int c)
{
    w[idx]=c;
    e[idx]=b,ne[idx]=h[a],h[a]=idx++;
}

int spfa()
{

    queue<int> q;
    q.push(1);
    st[1]=true;

    for(int i=1;i<=n;i++)
    {
        q.push(i);
        st[i]=true;
    }

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
                cnt[j]=cnt[t]+1;

                if(cnt[j] >= n) return true;
                if (!st[j])//如果这个点没被用过，将其入队
                {
                    q.push(j);
                    st[j] = true;
                }
            }
        }
    }

    return false;
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
    if(spfa()) cout<<"Yes";
    else cout<<"No";
    return 0;
}
```
