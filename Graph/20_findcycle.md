閉路検出
--------

閉路検出は, DFSの探索で探索中に二度探索する部分があるかで判定する.

### 計算量

### Source Code

``` java
public static final int unvisited = 0;
public static final int visiting = 1;
public static final int visited = 2;

public static boolean dfs(int node, boolean[][] adj, int[] state){
    state[node] = visiting;
    
    for(int i = 0; i < adj.length; i++){
        if(!adj[node][i]){ continue; }
        else if(state[i] == unvisited){
            if(!dfs(i, adj, state)){ //
                state[node] = visited; return false;
            }
        }else if(state[i] == visiting){ //cycle!
            return false;
        }
    }
    
    state[node] = visited;
    return true;
}

public static boolean find_cycle(boolean[][] adj){
    int[] state = new int[adj.length];
    for(int i = 0; i < adj.length; i++){
        state[i] = unvisited;
    }
    for(int i = 0; i < adj.length; i++){
        if(state[i] == unvisited){
            if(!dfs(i, adj, state)){
                return false;
            }
        }
    }
    return true;
}
```

### Verified
