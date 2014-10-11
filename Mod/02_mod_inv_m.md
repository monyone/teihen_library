逆元 (mod m)
------------

\(a\)の \(mod \: m\) での逆元は, \(a\)と\(m\)が互いに素であれば拡張ユークリッドの互助法で求められる.

### 計算量

\(O(log \: am)\) ※最悪の場合. 平均はかなり早いはず.

### Source Code

``` java
// a and m must be co-prime.
public static long mod_inv(long a, long m){
    return (a == 1 ? 1 : (1 - m*mod_inv(m%a, a)) / a + m);
}
```

### Verified

する予定

中国剰余定理
------------

\(x \; = \; a_i \; (mod \; m_i)\) という条件から, 条件を満たす \(x \; (mod \; \prod m_i )\) を求める.

### 計算量

\(O(条件の数 * log \; \sum \; m_i)\) ※計算量よりオーバーフローに気をつけること

### 依存

-   [逆元 (mod m) ](.\library.html#InvModM)

### Source Code

``` java
public static long chinese_remainder(long[] as, long[] ms){
    long prod = 1;
    for(long m : ms){ prod *= m; }
    
    long ret = 0;
    for(int i = 0; i < ms.length; i++){
        final long M = prod / ms[i];
        final long inv = mod_inv(M % ms[i], ms[i]);
        
        long a = as[i] - as[i] / prod * prod;
        if(a < 0){ a += prod; }
        
        ret = (ret + M * inv * a % prod) % prod;
    }
    
    return ret;
}
```

### Verified

する予定
