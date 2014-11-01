Rolling Hash
------------

文字列をハッシュする関数. 部分文字列に対するハッシュを定数時間で行える. 文字列\(s[0, n)\) に対して

\(hash(s) = (s[n-1] + s[n-2]*b + ... + s[0]*b^{n-1}) \; mod \; M \; (b, Mは互いに素)\)

### 使い方

#### 部分文字列のハッシュ

\(hash(s[l, r)) = hash[r] - hash[l] * b^{r-l}\)

### 計算量

\(O(N) ... nは文字列の長さ\)

### Source Code

``` java
public static long rolling_hash(String s, final long b, final long m){
    long ret = 0l;
    for(char c : s.toCharArray()){
        ret *= b; ret %= m;
        ret += c; ret %= m;
    }
    return ret;
}
```

### Verified
