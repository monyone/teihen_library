累乗 (mod m)
------------

累乗 \(a^e \: (mod \: m)\) に関しては, バイナリ法で高速に計算できる.

### 計算量

\(O(log \: e)\) ※log(指数)オーダー

### Source Code

再帰関数で計算するコードはこちら.

``` java
public static long mod_pow(long a, long e, long m){
    if(e == 0){
        return 1;
    }else if(e % 2 == 0){
        long ret = mod_pow(a, e / 2, m);
        return (ret * ret) % m;
    }else{
        return (mod_pow(a, e - 1, m) * a) % m;
    }
}
```

ループで下位のケタから計算するコードはこちら.

``` java
public static long mod_pow(long a, long e, long m){
    long ret = 1;
    for(; e > 0; e /= 2){
        if (e % 2 != 0) ret = (ret * a) % m;
        a = (a * a) % m;
    }
    return ret;
}
```

### Verified

する予定
