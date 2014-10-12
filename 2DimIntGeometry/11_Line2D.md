2次元の直線
-----------

### 依存

-   [2次元の点(有理数) ](.\library.html#TwoIntDimPoint)

### Source Code

``` java
public static class Line2D{
    private Point2D begin, end;
    
    public Line2D(Point2D begin, Point2D end){
        assert(begin != null && end != null);
        this.begin = begin; this.end = end;
    }
    
    public Point2D get_begin(){ return begin; }
    public Point2D get_end(){ return end; }
    public Point2D get_dir(){ return this.end.sub(this.begin); }
    
    public boolean is_orthogonal(Line2D o){
        return Rational.ZERO.equals(this.get_dir().dot(o.get_dir()));
    }
    public boolean is_parallel(Line2D o){
        return Rational.ZERO.equals(this.get_dir().cross(o.get_dir()));
    }
        
    public Point2D line_corss(Line2D o){
        if(is_parallel(o)) { return Point2D.NaN; }
        final Point2D this_dir = this.get_dir();
        final Point2D o_dir = o.get_dir();
        
        return this.begin.add(this_dir.mul(o_dir.cross(o.begin.sub(this.begin))).div(o_dir.cross(this_dir)));
    }
    
    public boolean ss_intersects(Line2D o){
        return this.begin.ccw(this.end, o.begin) * this.begin.ccw(this.end, o.end) <= 0
                && o.begin.ccw(o.end, this.begin) * o.begin.ccw(o.end, this.end) <= 0;
    }
    
    @Override
    public String toString(){ return this.begin + " -> " + this.end; }  
}
```
