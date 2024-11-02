```cpp
namespace kecoder {
    template <ll mod>
    class modint{
        ll v;
        static constexpr ll rd(ll x){return x<mod?x:x-mod;}
        public:
        modint(ll x=0){v=rd(x%mod+mod);}
        ll val()const{return v;}
        bool operator==(modint o)const{return v==o.v;}
        bool operator!=(modint o)const{return v!=o.v;}
        modint operator-()const{return mod-v;}
        modint &operator+=(modint o){v=rd(v+o.v);return *this;}
        modint &operator-=(modint o){v=rd(v+mod-o.v);return *this;}
        modint &operator*=(modint o){v=(ll)v*o.v%mod;return *this;}
        modint &operator/=(modint o){return *this*=o.inv();}
        modint pow(ll o){modint res=1,x=*this;while(o){if(o&1)res*=x;x*=x;o>>=1;}return res;}
        friend modint operator+(modint a,modint b){return a+=b;}
        friend modint operator-(modint a,modint b){return a-=b;}
        friend modint operator*(modint a,modint b){return a*=b;}
        friend modint operator/(modint a,modint b){return a/=b;}
        modint &operator++(){return *this+=1;}
        modint &operator--(){return *this-=1;}
        modint operator++(int){modint ret=*this;++*this;return ret;}
        modint operator--(int){modint ret=*this;--*this;return ret;}
        friend istream &operator>>(istream &is,modint &a){return is>>a.v;}
        friend ostream &operator<<(ostream &os,modint a){return os<<a.v;}
        modint inv(){return pow(mod-2);}
    };
    typedef modint<998244353> modint998244353;
    typedef modint<1000000007> modint1000000007;
}
using namespace kecoder;
```

为简易版 AtCoder Library 模板。