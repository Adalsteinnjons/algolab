# Tutorial Slides Part 1
We will focus on applying knowledge and develop intuition in algorithm design.  
Which techniques work for which problem?  
Important skills:  

* Know your algorithms
* Know tools & Libraries
* Creativity
* Problem Solving
* Time Management
* Testing

Steps to solving a problem:

1. Read the problem
2. Find the appropriate Model
3. Design a suitable Algorithm
4. Implement and test the algorithm on given data

All problems can be solved with < 100 lines of code

## Strategies:
### Brute Force:
Generate all possible solutions by trying out all the opposites. Then select the best one. This can be implemented using recursion or just looping though all possibilities.

### Greedy:
Always makes the choice that looks best at the moment. It never takes back its choices. The result a the end will be optimal if the choices are all independent of another. It is often difficult to prove that the locally optimal solution is also the global one. Example with giving back change, we want to give the least amount of coins back. Then always give the biggest possible until you have given all the money back. That works with euro money {1,2,5,10,50,100,200}, but not with every coin set.   
But with other sets it doesn't work. Example: Give 6 francs back and we have these types of coins: {1,3,4}, by using greedy we would give 4 + 1 + 1, but the optimal solution would have been 3 + 3. This disproves the greedy approach. We often can only proof that is doesn't work. 
### Divide & Conquer:
Divide the problem into smaller problems until you can solve a small problem and build up from there. It is based on recursion. This technique is used for sorting (quicksort, mergesort), multiplying large numbers and finding the closes pair of points.
### Dynamic Programming:  
Combines effectiveness of greedy with completeness of brute force/complete search. We divide the problem into sub-problems and solve them recursively storing their results. We can use DP to:
- Find an optimal solution. As large or as small as possible
- Count total number of solutions  
You can do it either top down or bottom up.  
Bottom up: construct the table and the result is in the top right corner.
Top-down: 
### Backtracking:  
Typical algorithm to solve the 8 queens problem. It goes by the trial and error principle. Uses recursion in the algorithm. Tries out until it finds error, goes always a level deeper, when it find error it goes back and starts from where there was no error anymore.  
### Binary Search:
Normal for loop complexity: O(n)
If the array is sorted, with binary search we can search through it in O(log n) time.
Array has 100 Elements:
For loop: 100 loops   
Binary Search: 6.64 Loops   
1000 Elements  
For Loop: 1000 Loops   
Binary Search: 10 Loops  
10'000 Elements:  
For Loop 10'000 Loops  
Binary Search: 13.3 Loops  
1 Million Elements:  
Binary Search: 19.93 Loops  
Also possible to use in std::binary_search(v.begin(), v.end(), value) --> returns true if found. Needs sorted vectors!
## Data Structures:

### Array
There are built in arrays, T[], but they should not be used. Instead use std::array. You need to include:  #include <array>  
std::array<int,5> a = {1,2,3,4,5}  
We can iterate with [begin(), end()]  
typedef std::array<int, 5> AI;  
AI a = {1,3,5,7,9}  
for (AI::const_iterator it = a.begin(); it != a.end(); ++it)  //This is if we dont want to chagne the contents in the loop, if we want to change we use AI::iterator instead.   
But even better just use **ranges**:  
for(int i : a){  
&nbsp;&nbsp;&nbsp; std:: cout<< i << " ";  
}

#### Vectors
Like an array bot has no fixed length. We always use vectors.   
\#include <vector>   
Insertion and deletion at the end is very fast, in constant time. But if we insert at beginning all elements have to be moved.   
std::vector<int> a(5)  
Size of vector: a.size()  
for( int i = 0; i < a.size(); i++){    
&nbsp;&nbsp;&nbsp; cout << a.at(i) << " ";  
}   

**2D Vector**  
typedef vector<int> VI;  
typedef vector<VI> VII;
Now we have a vector of int vectors. That means a 2D Matrix.  
int n = 100;  m  = 50;  
VII = (10, VI(10, -1)) //10 x 10 matrix with all elements set to -1  

### Stack
std::stack  
FILO data structure  
stack<int> s;  
s.push(17);  
int top = s.top();
s.pop();  
This is useful for graph algorithms, particularly for iterative implementation of DFS.
### Set
A set of unique objects. You can find an object iterator with set.find(3), only has O(log n) complexity. 
### Queue
FIFO  
queue<int>q;
q.push(17);  
int front = q.front();  
int back = q.back();  
q.pop()  
This one is useful when implementing BFS. 
### Tree
Just create the structure yourself with structs. Most important the binary tree. 
### Heap
Similar to a binary search tree but has faster insertion. Immediate insertion O(1). For BST its O(log(n)).  A BST is faster searching. Only log n while heap has n
### Hash-table
A table where you can store values. It hashes the values and stores them. If you want to search for an item that takes O(1) time since you only need to hash the key to get the correct index.   
Simple implementation of a hash function:   
![](http://i.imgur.com/8HfRVKy.png)
## Graph Algorithms

### DFS
Start at the starting node. Then follow the next node and stay on that path until you cant go further, then go back to last node where you can go another path. 
### BFS
Start at starting node, then visit closest node. It always visits the closest node to it. Goes through the nodes one level after another.
### MST
Is a subset of the edges of a connected, edge-weighted graph that connects all the certices together without cycles and with minimum possible weight. 
![](http://i.imgur.com/Dyg8mRh.png)
### Dijkstra
To find the shortest path to every node
## Graph Concepts

### Directed Graph
A graph with edges as arrows
### Coloring
Each node in a graph gets a color so no neighboring node has the same color. A graph is bipartite if it is possible to use just 2 colors. If a Graph has a cycle with an odd number of nodes, then it can't be colored using only 2 colors so it is not bipartite.   
Every single Map can be colored using just 4 colors. E.g. the chrome logo. 
### Matching
No 2 edges should have the same node. Maximal matching: Set of edges so that each node is connected once.   ![Maximal matching](http://i.imgur.com/i4cM8Co.png)   Maximum matching: Matching that contains the larges possible number of edges. Every maximum matching is maximal. There are a lot more maximal matchings that there are maximum matchings.   ![Maximum matching](http://i.imgur.com/qL1oRlo.png)  
Perfect matching: A matching which matches all vertices of the graph. Every vertex of the graph is incident to exactly one edge of the matching. In the image above only (b) shows perfect matching. 

### Topological sorting
Only possible if the graph is Directed Acyclic Graph (DAG). That means with arrows and no cycles. Topological sorting is a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering. This is to traverse a graph, similar to DFS but not quite. So the vertexes with edges out of it come first, then the ones below.  
![](http://i.imgur.com/Cknly69.png)  
It is used in Task Scheduling or in pre-requisite problems. 

### (Strongly) connected Components
A directed graph is strongly connected if there is a path between all pairs of vertices. So all are reachable from every vertex.

