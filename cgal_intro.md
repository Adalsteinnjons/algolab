# CGAL Tutorial 1
The Computational Geometry Algorithms Library  
## Part 1: Exact Computation, Benefits and Limitations
> Does the input fit?
> Do the results of computations fit?  

Goals:

* Know what the consequences of using limited precision arithmetic for discrete decisions
* How large is int, long double...?
* How to bound results of a computation

Some tasks require nontrivial/important computations:

- Computing Euclidian distances
- Solving a linear system
- Computing orientations of point triples  

![](http://i.imgur.com/E3qXHau.png)  
When using **limited precision** (floating point) arithmetic, the result might be incorrect due to roundoff, which could lead to a whole testcase failing. Total failure.  
**Convex hull:**  A set that is bounded by some points. You have some points and put a rubber band around them. Everything inside is the convex hull.  
![](http://i.imgur.com/DNw6tIF.png)  
The convex hull is particularly vulnerable to roundoff errors:   
![](http://i.imgur.com/4u7ivo8.png)  
With Floating point numbers, especially if the intermediate results are large but the final result is small, then the roundoff is significant.
![](http://i.imgur.com/XEA7JoV.png)  
### Exact Computation
We can use exact algebraic computation. Then we don't get roundoff errors. **But** they are very costly operations. They are assumed to have unit cost. If numbers grow, this assumptions becomes __invalid__. Then the cost grows much more.  
--> Use only as much algebra as needed  
Predicates: Result is True/False, we ask a question. Need a decision.  
Constructions: Get exact result. Intersection of 2 lines or the middle of a circle.  

* Program uses **predicats only**, numbers do not grow. :)  
* Exact constructions needed: Use as few as possible and only use "+, -, *, / ".     -_-
* Roots :(   

### Kernels
> There is no single true way to do geometric computing.   

CGAL offers different Kernels (Collection of data types and operations) to serve different needs.  

1. CGAL::Exact_predicates_inexact_constructions_kernel 
"Epic", uses double, very fast
2. CGAL::Exact_predicates_exact_constructions_kernel  "Epec", 
uses exact numbers supporting +,-,*,/. Medium Fast.  
3. CGAL::Exact_predicates_exact_constructions_kernel_with_sqrt  "Epecsqrt", same as before but supports roots, Slow!  


![](http://i.imgur.com/RrPpa5K.png)  
So avoid construction whenever you can. Example: You have many lines and a line "r". You need to output the intersection of the first line it touches. Don't construct the intersection of every line. First use predicates to check whether it even has an intersection and only construct where absolutely necessary.   
### How to avoid Roots
"For euclidian distances, we need squareroots"  
![](http://i.imgur.com/fcjeP0X.png)  
Not necesarrily. We can get much info with using just the squared distance: (px - qx)^2 + (py - qy)^2. If we compare lines like this we can get info about which on is the longest. __Usefull to compute MST.__  
***  
### Guidelines
#### 1 Avoid roots!  
 sqrt(x) < sqrt(y) <--> x < y.
#### 2 Avoid Divisions!  
a/b < c/d <--> ad < bc    (normal multiplication rule)  
### 3 Estimate to check if loss of precision's may occur.  
![](http://i.imgur.com/rrKvlNQ.png)  
***
## Part 2: Basic Programming using a CGAL Kernel  
Questions to answer: Are non-trivial (important) constructions needed? Are exact roots needed?  
Goals: Basic geometry with CGAL, 2D Kernel Objects, Intersections & Minimum enclosing circles.  
We use:  
`#include <CGAL/Exact_predicates_inexact_constructions_kernel.h>`  
typedef CGAL:: Exact\_predicates\_inexact\_constructions\_kernel K;  
K::Point_2 p(2,1), q(1,0), r(-1,-1);  
K::Line_2 l(p,q);  
K::FT d = CGAL::squared_distance(r,l);  //This one uses constructions, but no roots!   
FT = field type  
`cout<<d<<"\n";`

### 2D Kernel, all types
![](http://i.imgur.com/PwoG74m.png)    
### Intersections
![](http://i.imgur.com/jAR1oNV.png)  
### Minimum enclosing circle
![](http://i.imgur.com/j423Vz8.png)  
![](http://i.imgur.com/LwTqIAP.png)  







