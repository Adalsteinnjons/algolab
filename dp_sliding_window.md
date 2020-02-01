# Dynamic Programming and Sliding Window
## POW: Deck of Cards (simplified)
Input: n, k, and n non-negative integers v0, v1, ..., vn-1  
Output: a pair (i,j) such that sum of the intervall from i to j is equal to k.  
![](http://i.imgur.com/x7TBvUT.png)  
How can we solve it in O(n)?  
With partial sums it would be O(n^2)  
### Sliding Window
Have 2 pointers i and j, starting at the same, leftmost index.   
Check the value at that index.  
If the value is too small, increase the right pointer (makes it bigger).
If the value is too big, increase the left pointer (makes it smaller).  
Some problems in which you need to find some __optimal intervall__ can be solved in linear time using a sliding window approach.  
***
## Dynamic Programming
### Fibonacci Numbers
<pre><code>int F(int n){
	if(n ==1 || n ==2) return 1;
	return F(n-1) + F(n-2);</code></pre>
We have overlapping subproblems. If we call F(5).  
We get: F(5) = F(4) + F(3) = F(3) + F(2) + F(2) + F(1)  
As we can see we have to calculate F(3) twice.  
--> We should recall the result from memory.  
>Those who do not remember the past are condemned to repeat it.
<pre><code>vector<int> memo (n+1, -1) //The memory
int F(int n){
	if(n ==1 || n ==2) return 1;
	if(memo[n] == -1){ //We don't remember it
		memo[n] = F(n-1) + F(n-2);
	}
	return memo[n];
}</code></pre>  

This is called Top-Down DP or Memoization. Time Complexity O(n).  

### Rod Cutting  
Input: a metal rod of length n   
values p1, ..., pn denotes the price for a rod of length i.   
Output: Maximal cost of a rod of length n.
![Rod cutting example](http://i.imgur.com/PDnz9JH.png)  
Recursive Algorithm to get the best partition. We want a piece containing the left end + a partition of the rest. So we ask what is the most valuable partition.  
 Either we take pn (don't cut anything) or we take a partition. So the function is:  
r(n) = max{p(n), r(1) + r(n-1), r(2) + r(n-2), ...., r(n-1) + r(1)}
<pre><code>int r(vector<int> &p, int b) {
	if(n==0) return 0;
	int res = -1;
	for (int i =1; i <=n; i++) {
		res = max(res, p[i] + r(p, n - i));
	}
	return res;
}</code></pre>
We have overlapping subproblems. We can do this more efficiently with:  

- Topdown DP
<pre><code>vector<int> memo(n+1, -1) //Added
int r(vector<int> &p, int b) {
	if(n==0) return 0;
	if(memo[n] != -1) return memo[n]; //Added
	int res = -1;
	for (int i =1; i <=n; i++) {
		res = max(res, p[i] + r(p, n - i));
	}
	memo[n] = res; // Added
	return res;
}</code></pre>
- Bottom Up DP
<pre><code>vector<int>r(n+1, -1);
r[0] = 0;
for (int i = 1; i <=n; i++){
	for (int j = 1; j <= i; j++) {
		r[i] = max(r[i], p[j] + r[i - j]; //Current subproblem relies only on solution of the smaller subproblems
	}
}</code></pre>
Deriving a recursive algorithm is the difficult part.  
Essential elements of a DP problem:  

- Optimisation problems, (Maximise or minimize) (Maximal possible revenue in Rod Cutting)
- Optimal subproblem structure
- Overlapping subproblems  

Common Pitfalls:  
When you loop out of your "memo" vector in the for loop.   
When you do the memo vector, make sure that the default value is **not** a possible output! vector<int> memo (n+1, **0**); // better use -1  
Use memo vector not map, maps adds overhead and gives timelimit.

### Longest Increasing Subsequence
Input: n amount of numbers a1, ... an  
Output: Length of the longest increasing subsequence  
Example: **2** 4 **3** 7 **4 5**  
Result: 4  
![](http://i.imgur.com/myqFWrG.png)  
### Top Down vs Bottom Up
Top - down | Bottom Up
--- | ---
+Simple to implement | - More effort to code
+Easy to describe subproblems |  - Subproblems must be integers
+Computes only necessary subproblems | - Always computes all subproblems
-Time complexity not always obvious | + Time complexity obvious
-Overhead of function calls | + Saves some constant factors

### How to determine the runtime?
Number of subproblems * number of many choices for each subproblem

Always use vector, unless the subproblem cannot be described by integers, then use std::map.  

### How to solve these problems
1. Start by defining **recurrence relation** (on paper)
2. Implement it, it will be correct but slow
3. Are there overlapping subproblems? 
4. Add **memo** or construct a DP table

### How to get better at solving these problems?
Practice deriving recurrent relations **on paper**.   
Practice with standard DP Problems:

* Knapsack
* SubsetSum
* Coin Change
* LCS
* Edit Distance
* LIS
