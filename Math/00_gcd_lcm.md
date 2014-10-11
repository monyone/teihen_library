GCD, LCM
--------

基本的な算術用の関数. いつもお世話になる.

### 計算量

軽い. O(log b) くらい

### Source Code

``` java
public static long gcd(long a, long b){
    return b == 0 ? a : gcd(b, a % b);
}
public static long lcm(long a, long b){
    return a / gcd(a, b) * b;
}
```

### Verified
