隣接行列
--------

### Source Code

``` java
public static final long INF = Long.MAX_VALUE / 2 - 1;

public static long[][] init_adj(final int n){
    long[][] ret = new long[n][n];
    for(int i = 0; i < n; i++){
        for(int j = 0; j < n; j++){
            ret[i][j] = i == j ? 0l : INF;
        }
    }
    return ret;
}
```

### Verified

隣接リスト
----------

### Source Code

``` java
public static ArrayList<Integer,LinkedHashMap<Integer,Long>> init_adj(final int n){
    ArrayList<Integer, LinkedHashMap<Integer, Long>> ret =
        new ArrayList<Integer, LinkedHashMap<Integer, Long>>();
    for(int i = 0; i < n; i++){
        ret.add(new LinkedHashMap<Integer, Long>());
    }
    return ret;
}
```

### Verified
