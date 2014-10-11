逆元 (mod p)
------------

\(a\)の \(mod \: p\) での逆元は, フェルマーの小定理より, \(a^{-1} = a^{\: p-2} \: (mod \: p)\)

### 計算量

\(O(log \: p)\) ※累乗にバイナリ法が使える

### 依存

-   [累乗 (mod m) ](.\library.html#BinaryPowerMethodMOD)

### Source Code

``` java
public static long mod_inv(long a, long p){
    return mod_pow(a, p-2, p);
}
```

### Verified

する予定

逆元列挙 (mod p)
----------------

\(mod \: p\) の逆元は1からNまで\(O(N)\)で計算できる.

### 計算量

\(O(N)\) ※列挙する最大の数

### Source Code

``` java
//long[] inv = new long[MAX]; //1-indexed
public static void mod_inv(long[] inv, long p){
    inv[1] = 1;
    for(int i = 2; i <= N; i++){
        inv[i] = p - (p / i) * inv[p % i] % p;
    }
}
```

### Verified

する予定
