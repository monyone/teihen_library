Shift And
---------

短いパターン文字列をbit演算を使って高速に検索するアルゴリズム.

### 仕組み

探索状態をbitで全通り表現して高速に判定する. 状態のbit表現は, i番目の桁に"i番目まで一致しているか"というもの.

なぜbitで探索状態を表現するのかというと, 複数の探索状態をまとめて扱うためである. bitによって全通りの探索状態を表現しているならバックトラックをする必要がなくなる. このため, 効率的な探索を行う事が出来る.

また, パターンの文字毎の出現位置もbitで表す事で, 探索状態bitに対して bit演算だけで有り得る探索状態を抜き出せる.

なので, 現在の状態に対して, 1bit右シフト(次の文字も合致してる可能性があるため)と, 最下位bitを立てる(次の文字がパターンの開始文字である可能性があるため) を行ってから, 実際の次の文字の出現位置bitを使って, 実際の次の状態を抜き出している.

この [Shift-And Visualization](http://videlalvaro.github.io/2014/01/shift-and-visualization.html) を見た方が 早い.

### 計算量

対象文字列の長さをn, パターンの長さをmとすると

-   パターンのbit配列の構築 : O(m)
-   文字列検索 : O(n + m)

### Source Code

``` java
//Mのbit幅 >= パターンの文字列じゃないと死ぬ. 長いならBitSetを使おう.
public static int shift_and(String t, String p){ //pの長さはbit幅依存
    int[] M = new int[Character.MAX_VALUE]; // alphabet全体分の長さが必要. 
    int count = 0;
    for(int i = 0; i < p.length(); i++){
        M[p.charAt(i)] |= (1 << i);
    }
    
    for(int i = 0, S = 0; i < t.length(); i++){
        S = ((S << 1) | 1) & M[t.charAt(i)];
        
        if((S & (1 << (p.length() - 1))) != 0){
            count++; // t[i - p.length() + 1, i] 
        }
    }
    
    return count;
}
```

### Verified
