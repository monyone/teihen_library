おまけ
------

簡単なテンプレ
--------------

入力が少ない(n \< 100000)場合はJava標準の Scanner で大丈夫.

### Source Code

``` java
import java.util.Scanner;

public class Main {
    public static void debug(Object ... objs){
        System.out.println(Arrays.toString(objs));
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        // input here
        sc.close();
    }
}
```

自作Scanner
-----------

入力が多い場合は, Java標準のScannerでは間に合わない. なので, 正規表現を使わないScannerを自作する必要がある.

### Source Code

``` java
public static class Scanner {
    private BufferedReader br;
    private StringTokenizer tok;

    public Scanner(InputStream is) throws IOException {
        br = new BufferedReader(new InputStreamReader(is));
    }

    private void getLine() throws IOException {
        while (!hasNext()) { tok = new StringTokenizer(br.readLine()); }
    }

    private boolean hasNext() {
        return tok != null && tok.hasMoreTokens();
    }

    public String next() throws IOException {
        getLine(); return tok.nextToken();
    }

    public int nextInt() throws IOException {
        return Integer.parseInt(next());
    }
    // 他のnextXXXもXXX.parseXXX()メソッドを使って作れるので省略
    
    public void close() throws IOException {
        br.close();
    }
}
```
