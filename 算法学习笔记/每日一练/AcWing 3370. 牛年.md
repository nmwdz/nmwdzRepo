**注意**

( x - y ) % 12<br>
为`((x-y)%12+12)%12`<br>
而不能为`(x-y)+12)%12`<br>

因为x-y+12可能任为负数

```
#include<iostream>
#include<map>

using namespace std;

map<string,int> s={{"Ox",0} ,{"Tiger",1}, {"Rabbit",2},{ "Dragon",3}, {"Snake",4}, {"Horse",5}, {"Goat",6}, {"Monkey",7}, {"Rooster",8}, {"Dog",9}, {"Pig",10}, {"Rat",11}};

int main()
{
    int n;
    cin>>n;

    map<string,int> p;
    p["Bessie"]=0;

    while(n--)
    {
        string a[8];
        for(int i=0;i<8;i++) cin>>a[i];

        if(a[3]=="previous")
        {
            int x=p[a[7]],y=s[a[4]];
            int r=((x-y)%12+12)%12;
            if(!r) r=12;
            p[a[0]]=x-r;
        }
        else
        {
            int x=p[a[7]],y=s[a[4]];
            int r=((y-x)%12+12)%12;
            if(!r) r=12;
            p[a[0]]=x+r;
        }
    }

    cout<<abs(p["Elsie"]);
    return 0;
}
```
