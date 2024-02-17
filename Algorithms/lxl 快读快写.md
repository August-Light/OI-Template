# lxl 快读快写

## 代码

```cpp
namespace IO{
    const int BUF_SZ=1<<16;
    char ib[BUF_SZ+1],*ip=ib+BUF_SZ;
    void ipre(int n){
        int c=ib+BUF_SZ-ip;
        if(c<n){
            memcpy(ib,ip,c);
            ip=ib;
            fread(ib+c,1,BUF_SZ-c,stdin)[ib+c]=0;
        }
    }
    template<class T>
    T read(T L,T R){
        ipre(100);
        T x=0,f=1;
        while(*ip<'0'||*ip>'9')if(*ip++=='-')f=-f;
        while(*ip>='0'&&*ip<='9')x=x*10+*ip++-'0';
        x*=f;
        if(!(L<=x&&x<=R)){
            std::cerr<<x<<" not in ["<<L<<","<<R<<"]\n";
            exit(1);
        }
        return x;
    }
    char ob[BUF_SZ+1],*op=ob;
    void opre(int n){
        int c=ob+BUF_SZ-op;
        if(c<n){
            fwrite(ob,1,BUF_SZ-c,stdout);
            op=ob;
        }
    }
    template<class T>
    void write(T x){
        opre(100);
        char ss[100],*sp=ss;
        if(x<T(0))x=-x,*op++='-';
        do *sp++=x%10+'0';while(x/=10);
        while(sp!=ss)*op++=*--sp;
    }
    template<class T>
    void write(T x,char c){
        write(x);
        *op++=c;
    }
    struct __{
        __(){}
        ~__(){
            fwrite(ob,1,op-ob,stdout);
        }
    }_;
};
using IO::read;
using IO::write;
```

## 注

lxl 于 进阶算法计划【前期 / 冬春】分享。