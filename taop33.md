# Viktor Bergström summary of TAOP33

## 1. Linear programming

### 1.1 Objective function

In linear programming the objective function is a mathematical function used to model some value to be optimized. It consists of a sum of variables, each multiplied by some linear constant. An example would be
$$z = 5x_1 + 13+x_2 - 2x_3.$$
This can be written more generally as
$$z = c^Tx,$$
where x is the variable vector, and c the coefficient vector for the variables.

### 1.2 Linear constraints

To model a real world linear optimization problem we combine an objective function with one or more linear constraints. A linear constraint consists of the sum of some variables multiplied by constants coupled with a comparison to some constant. An example would be
$$5x_1 + 3x_2 \leq 5.$$
This can be written more generally as
$$Ax = b, $$
where x is the variable vector, A the coefficient matrix for the variables, and b the constraint vector.

### 1.3 Slack variables

Any linear constraint describing an inequality can be converted into another linear constraint describing an equality. This is done by adding a so called *slack variable*.
$$5x_1 + 3x_2 \leq 5. \iff 5x_1 + 3x_2 + x_3 = 5,$$
$$5x_1 + 3x_2 \geq 5. \iff 5x_1 + 3x_2 - x_3 = 5.$$

### 1.4 Standard form

### 1.4 Modell formulation

## 2. The simplex method

### 2.1 Theory and explanation

A set $C \subseteq R^n$ is said to be *convex* if the line segment between any two points in $C$ lies in $C$, i.e,
$$\forall x_1,x_2 \in C,\forall \lambda \in [0,1] : \lambda x_1 + (1-\lambda)x_2 \in C.$$
The simplest form of convex set would be a line segment of any length in some n-dimensional space.

For all linear constraints in standard form. By adding a artificial variable we can turn it into an inequality.

For an then it is the space below or above some infinite line, including the line itself. In n dimensions, this is called a halfspace, which is defined mathematically as
$$\{x: a^Tx \leq b\}.$$

A halfspace is not an affine set, since the normal line of the equation splitting the space includes points in the half space but also goes outside it. However, it can be farily easily prooven to be a convex set.
$$\text{For some halfspace } C,$$
$$x_1, x_2\in C \iff a^Tx_1 \leq b \land a^Tx_2 \leq b. $$
$$\implies \forall \lambda \in [0,1] : a^T(\lambda x_1 + (1-\lambda)x_2) = \lambda a^Tx + (1-\lambda)a^Tx_2 \leq \lambda b+(1-\lambda)b = b.$$
$$ \text{Therefore, C is a convex set. } \square$$

Because equality and inequality constraints are either affine or convex, all linear constraints are either affine or convex. Thus, because all affine sets are convex, all linear constraints are convex.

Furthermore, it holds that the intersection of one or multiple convex sets is also a convex set.
$$(\forall X_i \in X : X_i \text{ is convex}) \implies \cap_iX_i \text{ is convex}.$$

Because the possible values resulting from multiple active linear constraints is their intersection, it follows that multiple active linear constraints are also a convex set.

The geometric interpretation of a n-dimensional convex set is a n-dimensional convex polytope. Furthermore, a n-dimensional convex polytope with n+1 vertices is known as a *Simplex*.

The fact that the intersection of multiple linear constraints can be represented as a simplex is of major importance because of the following theorem.

The optimum for our objective function must lie in one of the extreme points of our Simplex generated from our constraints. Thus, to solve any linear optimization problem, all we have to do is traverse the extreme points of our Simplex until we reach an optimal value. This process is known as the *Simplex method* and was developed by George Danzig.

### 2.2 General algorithm

## 3. The dual solution

### 3.1 Theory and explanation

Linear constraints enforce boundary's on the domains of variables in an objective function.

Consequently, because an objective functions feasible values depend on the domains of it's variables. Linear constraints also enforce boundary's on the range of the objective function itself.

This fact can be used to reformulate an LP problem in order to view it through a different lense.

Consider the following maximization problem:

$$ \text{max } z = 3x_1 + 4x_2$$
$$\frac{1}{2}x_1 + 2x_2 \leq 30 \text{ (1) }$$
$$3x_1 + x_2 \leq 25 \text{ (2)}$$
$$x_1, x_2 \geq 0.$$
By multiplying both sides of (1) by 6 it follows that
$$3x_1 + 12x_2 \leq 180 \iff z = 3x_1 + 4x_2 \leq 3x_1 + 12x_2 \leq 180.$$
So we've concluded that based on (1) our objective function cannot be greater than 180.

We could also try multiplying both sides (2) by 4 way to get another bounding value.
$$12x_1 + 4x_2 \leq 100 \iff z = 3x_1 + 4x_2 \leq 12x_1 + 4x_2 \leq 100.$$

In fact, any linear combination of these two constraints resulting in variable coefficients larger or equal to those in the objective function would result in an upper bound.

This can be written mathematically as:

$\forall y_1, y_2 \in \mathbb{R},$
$$z \leq y_1 \cdot (1) + y_2 \cdot (2) \iff$$

$$\iff z \leq(\frac{1}{2}y_1 + 3y_2)x_1 + (2y_1 + y_2)x_2 \leq 30y_1 + 25y_2. \text{ (3)}$$
The right side expression of this equation is the upper bound of our objective function. We can use this to define a new function w.
$$w = 3y_1 + 25y_2$$

Additionally, based on (3) we get 2 linear constraints for w.

$$ \text{(3)}\implies  3x_1 + 4x_2 \leq (\frac{1}{2}y_1 + 3y_2)x_1 + (2y_1 + y_2)x_2 \iff$$
$$\iff \frac{1}{2}y_1 + 3y_2 \geq 3 \; \land \; 2y_1 + y_2\geq 4.$$

It can now be deduced, that becuase
$z \leq w,$
it follows that the lowest possible value for w must be equal to the greatest possible value for z.

Thus, to solve our original maximization problem, we must solve a new minimization problem, with w as our objective function along with it's constraints.

This reformulated problem is known as the *dual*, while the original problem is called the *primal*. The dual for a maximum problem will always be a minimum and vice versa.

* Weak duality property:
  
    $\forall \bar{z} \in Z, \forall \bar{w} \in W,$
    where Z and W are the sets of feasible solutions for the primal/dual.
    $$\text{max} \implies \bar{z} \leq \bar{w},$$
    $$\text{min} \implies \bar{z} \geq \bar{w}.$$
* Unboundness property:
  
    If the either the primal or dual to a problem has an unbounded solution, then the remaining one will be infeasible.
* Strong duality property:
  
    If the primal or dual problem has a finite optimal solution, then so does the remaining one. And the values of the primal and dual are equal at their optimal solutions.

The optimal solution of the dual contains the so called *shadow prices* also known as *margins*.

### 3.2 Formulating the dual

## 4. Integer programming

In general terms the variables found in linear programming can be divided into one of two categories.

* Continuos variables
* Integer variables
  
Continuos variables can assume any value on the real line, and therefore put no additional constraints on the range of an objective function.

Integer variables however, pose an additional challenge, as the feasible values of an objective function containing them must have a solution that's discrete in one or more dimensions.

### 4.1 Binary variables

A binary variable is an integer variable that can only assume the values 1 or 0.
$$x = \{0,1\} \lor 0 \leq x \leq 1$$

## 5. Graph theory

### 5.1 General notation

* Nodes: $N = \{i\}$.
* Edges: $B = \{(i,j)\}, \text{ for } i,j \in N$.
* Graph: $G = (N, B)$.
* $\delta(i)$: The set of edges with node i as their start or endpoint.  
* $\delta^+(i)$: The set of edges with i as their endpoint.
* $\delta^-(i)$: The set of edges with i as their start point.
* $\delta^+(A)$: The set of edges exiting the set of nodes A.
* $\delta^-(A)$: The set of edges entering the set of nodes A.
* $\delta(A)$: The set of edges exiting or entering the set of nodes A.
* $\gamma(i)$: The set of edges contained in the set of nodes A.

### 5.2 Types of graphs

* Path: Sequence of connected nodes which edges are all distinct.
* Cycle: Path that starts and ends at the same node.
* Simple path: A path without any cycles.
* Simple cycle: A cycle without any sub-cycles.
* Connected graph: A graph with a path between every pair of nodes.
* Tree: A connected graph without any cycles.
* Forest: A graph without any cycles, aka one or more trees.
* Complete graph: A graph with an edge connecting every pair of nodes.
* Isomorphic graph: A grap/colh which nodes can be divided into two sets such that, no edge has it's start and endpoint in the same set.
* Planar graph: A graph which can be drawn such that no edges intersect outside of the nodes of the graph.
* Eulercycle: A cycle that traverses each edge exactly once.
* Hamiltoncycle: A cycle that traverses each node exactly once.
* Hamiltonpath: A path that traverses  each node exactly once.
* Subgraph: A graph all of wholes nodes and edges are contained in a larger graph.
* Click: A complete subgraph
* Spanning tree: A subgraph that is a tree and includes all nodes of the original graph.

### 5.3 Graph properties

For a graph with n nodes the following definitions are equivalet:

* A spanning tree
* A connected graph with n-1 edges
* A graph with n - 1 edges that does not contain any cycles

For a tree with n > 1 nodes:

* The tree has n - 1 edges
* There is a unique path between each pair of nodes
* If another edge is added to the tree exactly one cycle is constructed
* If an edge is removed the tree will split into two trees
For a graph with n nodes the following are equivalent

### 5.4 Coloring

* Node coloring: Color all nodes of a graph such that no two neighboring nodes share the same color.
* Edge coloring: Color all edges of a graph so that no two adjacent edges share the same color.

### 5.5 Common graph problems

* Minimum spanning tree (MST)
* Traveling salesman problem (TSP)
* Matching problem
* Vehicle routing problem (VRP)
* The Chinese postman problem or route inspection problem (rip)

## 6. Cheapest path problem

### 6.1 Problem description

### 6.2 Fords algorithm

### 6.3 Dijkstra's algorithm  

## 7. Network flow problem

## 8. Heuristics
