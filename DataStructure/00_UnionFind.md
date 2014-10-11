Union-Find
----------

素集合管理用のデータ構造. 超頻出データ構造.

### 用途

-   グラフの連結成分の管理

### 計算量

経路圧縮 + ランク併合 で アッカーマン関数の逆関数(大体4くらい)

### Source Code

``` java
public static class UnionFind{
    int[] par; // 
    
    public UnionFind(int n){
        par = new int[n];
        for(int i = 0; i < n; i++){ par[i] = -1; }
    }
    
    public int find(int x){
        if(par[x] < 0){
            return x;
        }else{
            return par[x] = find(par[x]);
        }
    }
    
    public boolean union(int x, int y){
        x = find(x);
        y = find(y);
        
        if(x != y){
            if(par[y] < par[x]) {  // 多い方が根になるようにスワップする.
                int tmp = x; x = y; y = tmp;
            }
            par[x] += par[y];
            par[y] = x;
            return true;
        }else{
            return false;
        }
    }
    
    public boolean same(int x, int y){
        return find(x) == find(y);
    }
    
    public int size(int x){
        return -par[find(x)];
    }
}
```

### Verified

-   [AOJ DSL-1-A (Disjoint Set: Union Find Tree)](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_A)
