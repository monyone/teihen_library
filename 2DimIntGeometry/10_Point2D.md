2次元の点
---------

### 依存

-   [有理数 ](.\library.html#Rational) or [多倍長有理数 ](.\library.html#BigRational)

### Source Code

``` java
public static class Point2D implements Comparable<Point2D>{
    public static final Point2D NaN = new Point2D(Rational.NaN, Rational.NaN);
    
    private Rational x, y;
    
    public Point2D(Rational x, Rational y){
        assert(x != null && y != null); // nullを入れたら殺す!
        this.x = x; this.y = y;
    }
    
    public Rational get_x(){ return x; }
    public Rational get_y(){ return y; }
    public Rational norm(){ return this.x.pow(2).add(this.y.pow(2)); }
    
    public Point2D add(Point2D o){return new Point2D(x.add(o.x),y.add(o.y)); }
    public Point2D sub(Point2D o){return new Point2D(x.sub(o.x),y.sub(o.y)); }
    public Point2D mul(Rational r){ return new Point2D(x.mul(r), y.mul(r)); }
    public Point2D div(Rational r){ return new Point2D(x.div(r), y.div(r)); }
    
    public Rational dot(Point2D o)  { return x.mul(o.x).add(y.mul(o.y)); }
    public Rational cross(Point2D o){ return x.mul(o.y).sub(y.mul(o.x)); }
    public Rational dist(Point2D o) { return o.sub(this).norm(); }
    
    public long ccw(Point2D r, Point2D s){
        final Point2D a = r.sub(this), b = s.sub(this);
        final long sign = a.cross(b).sign();
        
        if(sign != 0){ return sign;
        }else if(a.x.mul(b.x).sign() < 0 || a.y.mul(b.y).sign() < 0){
            return -1;
        }else if(a.norm().compareTo(b.norm()) < 0){
            return 1;
        }else{ return 0; }
    }
    
    @Override
    public boolean equals(Object obj) { //必要ならHashCodeも生成する事
        if(!(obj instanceof Point2D)){ return false; }
        Point2D o = (Point2D) obj;
        if(!this.x.equals(o.x) || !this.y.equals(o.y)){ return false; }
        return true;
    }

    @Override
    public int compareTo(Point2D o) {
        if(this.x.compareTo(o.x) != 0){ return this.x.compareTo(o.x); }
        else if(this.y.compareTo(o.y) != 0){ return this.y.compareTo(o.y); }
        else { return 0; }
    }
}
```
