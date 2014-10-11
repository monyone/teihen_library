有理数
------

有理数を表現するクラス. longなのでintの範囲では誤差無しとして扱える.

### Source Code

``` java
// equalsメソッドは eclipse等で生成するなりして作ること
public static class Rational implements Comparable<Rational> {
    public static final Rational ZERO = new Rational(0);
    public static final Rational ONE  = new Rational(1);
    public static final Rational NaN  = new Rational(1, 0){
        public String toString(){ return "NaN"; }};
    
    private long nom, denom;
    
    public Rational(long nom, long denom) {
        if(nom == 0){ this.nom = 0; this.denom = 1; }
        else{ final long gcd = inner_gcd(nom, denom);
            this.nom = nom / gcd; this.denom = denom / gcd;
            if(this.nom * this.denom < 0){
                this.nom = -Math.abs(this.nom); 
                this.denom = Math.abs(this.denom);
            }}}
    public Rational(long num) { this(num, 1); }
    public long get_nom(){ return this.nom; }
    public long get_denom(){ return this.denom; }
    private static long inner_gcd(long a, long b){ 
        return b == 0 ? a : inner_gcd(b, a % b); }
    private static long inner_lcm(long a, long b){
        return a / inner_gcd(a, b) * b; }
    public Rational minus(){ return new Rational(-this.nom, this.denom); }
    public Rational inv(){ return new Rational(this.denom, this.nom); }
    public long sign(){
        return this.nom ==0 ? 0 : inner_lcm(this.nom,this.denom) < 0 ?-1:1;}
    public Rational abs(){
        return new Rational(Math.abs(this.nom), Math.abs(this.denom));}
    
    public Rational add(Rational o){
        final long lcm = inner_lcm(this.denom, o.denom);
        return new Rational(lcm/this.denom*this.nom + lcm/o.denom*o.nom,lcm);}
    public Rational sub(Rational o){ return this.add(o.minus()); }
    public Rational mul(Rational o){ return new Rational(this.nom * o.nom, this.denom * o.denom); }
    public Rational div(Rational o){ return this.mul(o.inv()); }
    public Rational gcd(Rational o){
        return new Rational(inner_gcd(this.nom, o.nom), inner_lcm(this.denom, o.denom)); }
    public Rational lcm(Rational o){
        return new Rational(inner_lcm(this.nom, o.nom), inner_gcd(this.denom, o.denom)); }
    public Rational pow(long p){
        if(p == 0){ return Rational.ONE;
        }else if(p % 2 != 0){ return this.mul(pow(p - 1));
        }else{ Rational ret = pow(p / 2); return ret.mul(ret); }}
    
    @Override
    public int compareTo(Rational o){
        final long det = this.nom * o.denom - this.denom * o.nom;
        if(det < 0){ return -1;
        }else if(det > 0){ return 1;
        }else{ return 0; }}
}
```

### Verified

-   [Maximum-Cup 2013 (C - 白蛇のお守り)](http://maximum-cup-2013.contest.atcoder.jp/tasks/maximum_2013_c)
