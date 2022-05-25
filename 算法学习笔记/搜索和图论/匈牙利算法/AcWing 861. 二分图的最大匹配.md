```
#include<iostream>
#include<cstring>

using namespace std;

const int N = 510,M = 100010;

int n1,n2,m;
int h[N],e[M],ne[M],idx;//邻接表表示男生心仪的女生
int match[N];//女生所对应匹配了的男生
bool st[N];//表示女生是否被匹配

void add(int a,int b)
{
    e[idx]=b,ne[idx]=h[a],h[a]=idx++;
}

bool find(int x)
{
    for(int i=h[x];i!=-1;i=ne[i])//遍历每一个心动女生
    {
        int j=e[i];
        if(!st[j])//如果这个女生没试过则试一试能不能成
        {
            st[j]=true;
            if(match[j]==0||find(match[j]))//如果没有男朋友或者男朋友可以劈腿
            {
                match[j]=x;//成功
                return true;
            }
        }
    }
    //每个都不成功返回false
    return false;
}

int main()
{
    cin>>n1>>n2>>m;

    memset(h,-1,sizeof h);

    while(m--)
    {
        int a,b;
        cin>>a>>b;
        add(a,b);
    }

    int res=0;
    for(int i=1;i<=n1;i++)
    {
        memset(st,false,sizeof st);//初始化女生状态保证每个女生都要被尝试
        if(find(i)) res++;
    }

    cout<<res;

    return 0;

}
```
