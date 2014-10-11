多倍長有理数
------------

有理数を表現するクラス. 多倍長なので安心して使える.

### Source Code

``` java
// import java.math.BigInteger;
public static class BigRational implements Comparable<BigRational>{
    public static final BigRational ZERO = new BigRational(0, 1);
    public static final BigRational ONE  = new BigRational(1, 1);
    public static final BigRational NaN  = new BigRational(1, 0);
    
    public final BigInteger nom, denom;
    
    public BigRational(BigInteger nom, BigInteger denom){
        this.nom = calc_nom(nom,denom); this.denom = calc_denom(nom,denom); }
    
    public BigRational(BigInteger nom){ this(nom, BigInteger.valueOf(1)); }
    public BigRational(long nom, long denom){
        this(BigInteger.valueOf(nom), BigInteger.valueOf(denom)); }
    public BigRational(long nom){ this(nom, 1); }
    
    private static BigInteger inner_lcm(BigInteger a, BigInteger b){
        return a.multiply(b).divide(a.gcd(b));}
    
    private static BigInteger calc_nom(BigInteger nom, BigInteger denom){
        nom = nom.divide(nom.gcd(denom));
        if(nom.signum() * denom.signum() < 0){ nom = nom.abs().negate(); }
        return nom; }
    private static BigInteger calc_denom(BigInteger nom, BigInteger denom){
        denom = denom.divide(nom.gcd(denom));
        if(nom.equals(BigInteger.ZERO)) { return BigInteger.ONE; }
        if(nom.signum() * denom.signum() < 0){ denom = denom.abs(); }
        return denom; }
    
    public BigRational minus(){ return new BigRational(nom.negate(), denom); }
    public BigRational inv()  { return new BigRational(denom, nom); }
    public int sign() { return nom.signum(); }
    public BigRational abs()  { return new BigRational(nom.abs(), denom); }
    public BigRational add(BigRational o)  { 
        final BigInteger lcm = inner_lcm(this.denom, o.denom);
        return new BigRational(lcm.divide(this.denom).multiply(this.nom)
                .add(lcm.divide(o.denom).multiply(o.nom)), denom); }
    public BigRational sub(BigRational o){ return this.add(o.minus()); }
    public BigRational mul(BigRational o){ 
        return new BigRational(this.nom.multiply(o.nom), this.denom.multiply(o.denom)); }
    public BigRational div(BigRational o){ return this.mul(o.inv()); }
    public BigRational gcd(BigRational o){
        return new BigRational(inner_gcd(this.nom, o.nom), this.denom.lcm(o.denom)); }
    public BigRational lcm(BigRational o){ 
        return new BigRational(inner_lcm(this.nom, o.nom), this.denom.gcd(o.denom)); }
    public BigRational pow(int p){ return new BigRational(nom.pow(p), denom.pow(p)); }
    
    @Override
    public int compareTo(BigRational arg0){
        return this.nom.multiply(arg0.denom).compareTo(this.denom.multiply(arg0.nom)); }
}
```

### Verified

-   [Maximum-Cup 2013 (C - 白蛇のお守り)](http://maximum-cup-2013.contest.atcoder.jp/tasks/maximum_2013_c)
