**思路**
```
for 遍历1-n个点：
    if i没有被染色
    dfs(i,随意颜色)
```
```
#include<iostream>
#include<cstring>

using namespace std;

const int N = 100010,M = 200010;

int n,m;
int h[N],e[M],ne[M],idx;//邻接表
int color[N];//表示染色，0为未被染色，1 2分别表示被染的不同颜色

void add(int a,int b)//添加a—>b的一条边
{
    e[idx]=b,ne[idx]=h[a],h[a]=idx++;
}

bool dfs(int u,int c)//判断是否能将u染成c
{
    color[u]=c;

    for(int i=h[u];i!=-1;i=ne[i])//遍历所有临边
    {
        int j=e[i];
        /*
            临边有两种情况：
                1.没被染色，则递归处理其临边，看其是否能被染色
                2.被染色，判断是否为不同颜色
        */
        if(!color[j])
        {
            if(!dfs(j,3-c)) return false;
        }
        else if(color[j]!=3-c) 
        return false;
    }
    //当循环完所有临边都没被返回则说明此点能被染成改颜色
    return true;
}

int main()
{
    cin>>n>>m;

    memset(h,-1,sizeof h);

    for(int i=0;i<m;i++)//添加所有边
    {
        int a,b;
        cin>>a>>b;
        add(a,b),add(b,a);
    }

    //循环n次判断是否有冲突的染色
    for(int i=1;i<=n;i++)
    {
        if(!color[i]&&!dfs(i,2))//如果一个点没被染色就将其染色，如果不能染色输出No，否则说明染色成功
        {
                cout<<"No";
                return 0;
        }
    }
    //循环完n个点都能被染色说明不冲突
    cout<<"Yes";
    return 0;
}
```
