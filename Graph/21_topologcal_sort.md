トポロジカルソート
------------------

閉路検出は, DFSの探索で帰りがけ順に見れば良い.

### 計算量

### Source Code

``` java
public static final int unvisited = 0;
public static final int visiting = 1;
public static final int visited = 2;

public static boolean dfs(int node, boolean[][] adj, int[] state, LinkedList<Integer> list){
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
    list.addFront(node);
    return true;
}

public static boolean topological_sort(long[][] ad, LinedList<Integer> list){
    int[] state = new int[adj.length];
    for(int i = 0; i < adj.length; i++){
        state[i] = unvisited;
    }
    for(int i = 0; i < adj.length; i++){
        if(state[i] == unvisited){
            if(!dfs(i, adj, state, list)){
                return false;
            }
        }
    }
    return true;
}
```

### Verified
