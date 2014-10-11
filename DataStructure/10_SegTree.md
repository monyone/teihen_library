SegmentTree
-----------

範囲に関わるクエリを高速に処理するデータ構造.

### 計算量

-   add(k) : O(log n) ※単一の値の更新
-   get(s,t): O(log n) ※範囲の値の計算

### Source Code

``` java
public static class SegTree{
    int n;
    long[] dat;
    
    public SegTree(int n_) {
        int n = 1;
        while(n < n_){
            n *= 2;
        }
        
        this.n = n;
        dat = new long[this.n * 2 - 1];
        for(int i = 0; i < this.n * 2 - 1 ; i++){
            dat[i] = 0;
        }
    }
    
    public long calc(long fst, long snd){
        return fst + snd;
    }
        
    public void update(int k, long a){
        k += n - 1;
        dat[k] = a;
        
        while(k > 0){
            k = (k - 1) / 2;
            dat[k] = calc(dat[k * 2 + 1], dat[k * 2 + 2]);
        }
    }
    
    public long query(int a, int b, int k, int l, int r){
        if(r <= a || b <= l){
            return 0;
        }else if(a <= l && r <= b){
            return dat[k];
        }else {
            return calc(query(a, b, k * 2 + 1, l, (l + r) / 2), query(a, b, k * 2 + 2 , (l + r) / 2, r));
        }
    }
    
    public long query(int a, int b){
        return query(a, b, 0, 0, n);
    }
}
```

### Verified
