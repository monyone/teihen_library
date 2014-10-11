遅延評価SegmentTree
-------------------

SegmentTreeでは区間に対する更新に \(O(n \; log\; n)\) かかってしまう.

### 計算量

-   add(s,t): O(log n) ※範囲の値の更新
-   get(s,t): O(log n) ※範囲の値の取得

### Source Code

``` java
public static class SegTree{
    int n;
    long[] dat, lazy;

    public SegTree(int n_) {
        int n = 1;
        while(n < n_){ n *= 2;} this.n = n;
        dat = new long[this.n * 2 - 1];
        lazy = new long[this.n * 2 - 1];
        for(int i = 0; i < this.n * 2 - 1 ; i++){
            dat[i] = 0; lazy[i] = 0;
        }
    }
    
    private void lazy_evaluate_node(int k, int a, int b){
        dat[k] += lazy[k] * (b - a);
        if(k < n - 1){
            lazy[2 * k + 1] += lazy[k]; lazy[2 * k + 2] += lazy[k];
        }
        lazy[k] = 0;
    }
        
    public void update_node(int k){
        dat[k] = dat[2 * k + 1] + dat[2 * k + 2];
    }
    
    public void update(long v, int a, int b, int k, int l, int r){
        lazy_evaluate_node(k, l, r);
        
        if(r <= a || b <= l){ return;
        }else if(a <= l && r <= b){
            lazy[k] += v; lazy_evaluate_node(k, l, r);
        }else {
            update(v, a, b, k * 2 + 1, l , (l + r) / 2);
            update(v, a, b, k * 2 + 2, (l + r) / 2, r);
            update_node(k);
        }
    }
    
    public long get(int a, int b, int k, int l, int r){
        lazy_evaluate_node(k, l, r);
    
        if(r <= a || b <= l){ return 0;
        }else if(a <= l && r <= b){ return dat[k];
        }else {
            long v1 = get(a, b, k * 2 + 1, l , (l + r) / 2);
            long v2 = get(a, b, k * 2 + 2, (l + r) / 2, r);
            update_node(k); return v1 + v2;
        }
    }
        
    public int size(){ return this.n; }
}
```

### Verified

TODO
