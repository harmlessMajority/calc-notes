# Viktor Bergström summary of TAOP33

## 1. Linear programming

### 1.1 Objective function

In optimization, the objective function is a mathematical function used to model some value to be optimized. For linear programming specifically, it consists of a sum of variables, each multiplied by some linear constant. An example would be

$$z = 5x_1 + 13+x_2 - 2x_3.$$

This can be written more generally as

$$z = c^Tx,$$

$$z = \sum_{i,j} x_{ij} c_{ij}$$

where x is the variable vector, and c the coefficient vector for the variables.

### 1.2 Linear constraints

To model a real world linear optimization problem we combine an objective function with one or more linear constraints. A linear constraint consists of the sum of some variables multiplied by constants coupled with a comparison to some constant. An example would be

$$5x_1 + 3x_2 \leq 5.$$

This can be written more generally as

$$Ax = b, $$

where x is the variable vector, A the coefficient matrix for the variables, and b the constraint vector.


### 1.3 Active and inactive constraints
Let $f(x) : \mathbb{R^n} \rightarrow \mathbb{R}$, for a given solution $x^{*}$, the constraints $f(x) \leq 0 \text{ and } f(x) \geq 0$, are said to be active iff

$$f(x^*) = 0.$$

This definition is extended to equalities.

Let $g(x) : \mathbb{R^n} \rightarrow \mathbb{R}$, for a given solution $x^{*}$, the constraint $g(x) = 0$ is said to be active iff

$$g(x^*) = 0.$$

In words, an inactive constraint is a constraint which could be removed from some problem without changing it's optimal solution. It is inactive in sense that it doesn't actually limit the solution in any way.

## 2. The simplex method

### 2.1 Theory and explanation

A set $C \subseteq R^n$ is said to be *convex* if the line segment between any two points in $C$ lies in $C$, i.e,

$$\forall x_1,x_2 \in C,\forall \lambda \in [0,1] : \lambda x_1 + (1-\lambda)x_2 \in C.$$

The values satisfying a linear inequality constraint make up a halfspace

$$\lbrace x: a^Tx \leq b\rbrace.$$

We can prove that halfspaces are convex sets.

$$\text{For some halfspace } C,$$

$$x_1, x_2\in C \iff a^Tx_1 \leq b \land a^Tx_2 \leq b. $$

$$\implies \forall \lambda \in [0,1] : a^T(\lambda x_1 + (1-\lambda)x_2) = \lambda a^Tx + (1-\lambda)a^Tx_2 \leq \lambda b+(1-\lambda)b = b.$$

$$ \text{Therefore, C is a convex set. } \square$$

Thus, all linear inequality constraints are convex.
Additionally, is is trivial that linear equality constraints are also convex, since the values satisfying them make a straight line.

Furthermore, it holds that the intersection of one or multiple convex sets is also a convex set.

$$(\forall X_i \in X : X_i \text{ is convex}) \implies \cap_iX_i \text{ is convex}.$$

Because the possible values resulting from multiple active linear constraints is their intersection, it follows that multiple active linear constraints are also a convex set.

The geometric interpretation of a n-dimensional convex set is a n-dimensional convex polytope. Furthermore, a n-dimensional convex polytope with n+1 vertices is known as a *Simplex*.

The fact that the intersection of multiple linear constraints can be represented as a simplex is of major importance because of the following theorem:

* The optimum for our objective function must lie in one or more of the extreme points of our Simplex generated from our constraints. 

Thus, to solve any linear optimization problem, all we have to do is traverse the extreme points of our Simplex until we reach an optimal value. This process is known as the *Simplex method* and was developed by George Danzig.

### 2.2 General algorithm
Assume we wish to solve the following optimization problem using the simplex method:

$$\text{max } z = 4x_1 + 3x_2$$

$$\text{when } 2x_1 + 3x_2 \leq 30$$

$$x_1 \leq 6$$

$$6x_1 + 4x_2 \leq 50$$

$$x_1, x_2 \geq 0$$

Before the simplex algorithm can be applied, the problem must first be converted into standard form. This means that the number of constraints must be equal to the number of basic variables, which can be achieved by modifying our original constraints.

1. Constraints of type $\leq$ must be converted to equalities by adding a slack variable.
2. Constraints of type $\geq$ must be converted to equalities by subtracting a slack variable and adding an artificial variable.
3. Constraints of type $=$ must add adding an artificial variable.

If we convert our original problem to standard form we get

$$\text{max } z = 4x_1 + 3x_2$$

$$\text{when }  2x_1 + 3x_2 + x_3 = 30$$

$$x_1 + x_4 = 6$$

$$6x_1 + 4x_2 + x_5 = 50$$

$$x_1, x_2, x_3, x_4, x_5 \geq 0$$

We now construct a tableau, with one column for each variable and one row for each equation in the standard form.

Additionally, construct a base consisting of variables who's columns are all cleared out except for a single 1.

|Base|z|$x_1$|$x_2$|$x_3$|$x_4$|$x_5$|$\hat{b}$|
|--|--|--|--|--|--|--|--|
|$z$|1|-4|-4|0|0|0|0|
|$x_3$|0|2|3|1|0|0|30|
|$x_4$|0|1|0|0|1|0|6|
|$x_5$|0|6|4|0|0|1|50|

We now wan't to alter our basis to try and achieve a greater objective value.

For this we need to select one variable to enter the base, and one to exit.

For a max problem we should pick the variable with the biggest positive non 0 coefficient in the objective function. 
Since the coefficients for our variables in the tablou are of oposite sign this means we pick $x_1$ to enter the base. 

The exiting variable should be the basic variable with the smallest resulting number when dividing the value of $\hat{b}$ in it's row, by the value of the entering variable in it's row.

By use of row operations, make shure the collumn of the new entering variable is cleared except for a single 1 where it enters.

The result tablou is 

|Base|z|$x_1$|$x_2$|$x_3$|$x_4$|$x_5$|$\hat{b}$|
|--|--|--|--|--|--|--|--|
|$z$|1|0|-3|0|4|0|24|
|$x_3$|0|0|3|1|-2|0|18|
|$x_1$|0|1|0|0|1|0|6|
|$x_5$|0|0|4|0|-6|1|14|

repeating this process we get

|Base|z|$x_1$|$x_2$|$x_3$|$x_4$|$x_5$|$\hat{b}$|
|--|--|--|--|--|--|--|--|
|$z$|1|0|0|0|-1/2|3/4|69/2|
|$x_3$|0|0|0|1|5/2|-3/4|15/2|
|$x_1$|0|1|0|0|1|0|6|
|$x_2$|0|0|1|0|-3/2|1/4|7/2|

repeat once more aditionally

|Base|z|$x_1$|$x_2$|$x_3$|$x_4$|$x_5$|$\hat{b}$|
|--|--|--|--|--|--|--|--|
|$z$|1|0|0|1/5|0|3/5|36|
|$x_4$|0|0|0|2/5|1|-3/10|10|
|$x_1$|0|1|0|-2/5|0|3/10|3|
|$x_2$|0|0|1|3/5|0|-1/5|8|

Since there are no negative coeficients for variables in the tablous that means that there is no variable which adjusting will increase the value of our objective function.

Thus the problem is solved.

From the tablou, we gather that
* The maximum value for the objective function is 36.
* The optimal solution is: $x_1 = 3, x_2 = 8$.
* The optimal dual solution is: $y_1 = 1/5, y_2 = 0, y_3 = 3/5$.
* Constraint 2 is active, since $x_4 = 3$.
* Constraints 1 and 3 are not active, since: $x_3 = 0, x_5 = 0$.

## 3. The dual solution

### 3.1 Theory and explanation

Linear constraints enforce boundary's on the domains of variables in an objective function.

Consequently, because an objective functions feasible values depend on the domains of it's variables. Linear constraints also enforce boundary's on the range of the objective function itself.

This fact can be used to reformulate an LP problem in order to view it through a different lense.

Consider the following maximization problem:

$$\text{max } z = 3x_1 + 4x_2$$

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

$$\text{(3)}\implies  3x_1 + 4x_2 \leq (\frac{1}{2}y_1 + 3y_2)x_1 + (2y_1 + y_2)x_2 \iff$$

$$\iff \frac{1}{2}y_1 + 3y_2 \geq 3 \land  2y_1 + y_2\geq 4.$$

It can now be deduced, that becuase
$z \leq w,$
it follows that the lowest possible value for w must be equal to the greatest possible value for z.

Thus, to solve our original maximization problem, we must solve a new minimization problem, with w as our objective function along with it's constraints.

This reformulated problem is known as the *dual*, while the original problem is called the *primal*. The dual for a maximum problem will always be a minimum and vice versa.



### 3.2 Properties 
Komplementaritet (i ord):
Om primala bivillkor i inte är aktivt, måste yi = 0.
Om duala bivillkor j inte är aktivt, måste xj = 0

$$\forall i \in [1 \dots m]: y_i \sum_{j=1}^n(a_{ij}x_j - b_i) = 0$$

$$\forall j \in [1 \dots n]: x_j \sum_{i=1}^m(a_{ij}y_i - c_j) = 0$$

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


### 3.3 Formulating the dual

1. For every constraint in the primal generate a variable in the dual.
The variable coeficients will equal the right side of each constraint.
2. For each variable in the primal generate a constraint in the dual. The type of constraint depends on the constraints put on the variable in the primal. The coefficients of each constraints in the dual will be the transpose of the primal constraint coeficients. Aka the constraints of each respective variable belonging to each generated constraint.
3. Complementary constraints

## 4. Graph theory

### 4.1 Notation 
* Nodes: $N = \lbrace i\rbrace$.
* Edges: $E = \lbrace (i,j)\rbrace, \text{ for } i,j \in N$.
* Graph: $G = (N, E)$.
* $\delta(i)$: The set of edges with node i as their start or endpoint.  
* $\delta^+(i)$: The set of edges with i as their endpoint.
* $\delta^-(i)$: The set of edges with i as their start point.
* $\delta^+(A)$: The set of edges exiting the set of nodes A.
* $\delta^-(A)$: The set of edges entering the set of nodes A.
* $\delta(A)$: The set of edges exiting or entering the set of nodes A.
* $\gamma(i)$: The set of edges contained in the set of nodes A.

### 4.2 Basic definitions

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
* Node coloring: Color all nodes of a graph such that no two neighboring nodes share the same color.
* Edge coloring: Color all edges of a graph so that no two adjacent edges share the same color.

### 4.3 Properties

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

## 5 Common graph problems

### 5.1 Cheapest path problem 
### 5.1 Dijkstra's algorithm  
Dijkastra's algorithm is a method for finding the shortest paths to all nodes in a graph from a given starting node. 

Note that Dijkastra's algorithm will never finish running on a graph containing one or more negative cycles. As such it can not be used reliably on graphs containing non-positive edge costs.

### Pseudocode
```
dijkstra (nodes, start_node):
    priority_queue = [node for node in nodes]
    set_cost(nodes, INFINITY)
    set_cost(start_node, 0)

    while not is_empty(priority_queue):
        current_node = pop(priority_queue)
        for edge in edges(current_node):
            relax(edge)

relax (edge):
    new_cost = node_cost(edge.from) + edge_cost(edge)
    if new_cost < node_cost(edge.to):
        set_cost(edge.to, new_cost)
        set_previous_node(edge.to, edge.from)

```

### 5.2 The Bellman-Ford (BF) algorithm
The BF algorithm also finds the shortest paths to all nodes in a graph from a starting node. It is generally slower compared to  Dijkstra's, however it has the advantage of working on graphs with non-positive edge weights. The algorithm can tell weather a graph contains a negative cycle or not.
### Pseudocode
```
func bf (nodes, edges, start_node):
    set_cost(nodes) = INFINITY 
    set_cost(start_node) = 0

    for node in nodes:
        for edge in edges:
            relax(edge)

    #Check for negative cycles
    for edge in edges:
        if relax(edge)
            "Negative cycle found"

relax (edge):
    new_cost = node_cost(edge.from) + edge_cost(edge)
    if new_cost < node_cost(edge.to):
        set_cost(edge.to, new_cost)
        set_previous_node(edge.to, edge.from)
        return true
    return false

```

### 5.2 Minimum spanning tree (MST)
Given a weighted graph, find a spanning tree of minimum weight.

To costruct a spanning tree for some graph $G(N,E)$, we must construct a subgraph to $G$ where $N_{sub} = N$ and $|E_{sub}| = |N| - 1.$

This can be achieved in $|E| \choose{|N -1|}$ $- no of cycles$ ways.

As such comparing all possible spanning trees to find the cheapest is not feasable.

For this problem we use a greedy algorithm.

### 5.2.1 Prim's algorithm
### Pseudocode
```
prim (nodes, start_node):
    priority_queue = [node for node in nodes] 
    in_tree = [false for node in nodes]
    set_cost(nodes, INFINITY) 
    set_cost(start_node, 0)

    while not is_empty(priority_queue):
        node = pop(priority_queue)
        in_tree[node] = true
        for adj_node in neighbors(node):
            new_cost = edge_cost(node, adj_node)
            if not in_tree[adj_node] and new_cost < cost(adj_node):
                set_cost(adj_node, new_cost)
                set_parent(adj_node, node)

```
### 5.2.2 Kruskal's algorithm
### Pseudocode
```
kruskal (nodes, edges, start_node):
    edges_in_tree =[]
    disj_set = {}
    for node in nodes:
        make_set(disj_set, node)
        
    sort(edges, e1 <= e2)
    for edge(node_u, node_v) in edges:
        if find_set(disj_set, node_u) != find_set(disj_set,  node_v):
            union(disj_set, node_u, node_v)
            append(edges_in_tree, edge(node_u, node_v))

```

## 5.3 Traveling salesman problem (TSP)
The traveling salesman otherwise known as the minimum hamlitoncykle problem asks to find cheapest possible hamiltoncycle for a given graph.

Generally this problem is fairly complicated. It can however be relaxed to finding the cheapest 1-tree. A one tree is a spanning tree for the nodes $N / \lbrace 1\rbrace $ connected to node one by two edges.

As such, to find the cheapest 1-tree we begin by finding the minimum spanning tree for the nodes $N / \lbrace 1\rbrace$, by using either prim or krusgals algorithm. We then add the two cheapest edges connecting to 1 to form a minimal 1-tree.

Every hamliton cycle is a 1-tree but not vice verca. Every 1-tree that is not a hamlitoncycle simply failes to meet its node requirement. Recall that a hamliton cycle by definition is a cycle that traverses each node only once. Therefore

$$\forall i \in N : \delta(i) = 2$$

As such if our 1 tree is not a hamliton cycle then it can be converted by adding or subtracting edges to meet this condition.


## 5.4 Matching problem

A matching in a given undirected graph $G(N,E),$ is a subset of edges $\hat{E} \subseteq E$, such that no two edges share a common vertecie. 

The goal of a matching problem is to maximize the amount of edges in the matching, or to maximise the sum of weight for the edges in the matching.

The problem can be formulated mathematically as 


$$ \text{max } c^Tx \text{ when } x(\delta{(i)}) \leq 1 \forall x \in N, x \in \{0,1\}^m$$

Given a matching $M$, we define an augmenting path as a path that starts and ends on unmatched nodes, and whose edges alternate between matched and unmatched. 

By finding an augmenting path to a matching, we can swap the matched and not matched edges in the path to increase the size of the matching by 1.

Furthermore, Berge's lemma states that

$$\text{Contains an augmenting path } \iff \text{Matching is not maximal}$$

Thus, to find a maximal matchning, all we have to do is either find an augmenting path, or verify that none exist. 

Cycles of length complicate the problems slightly but can be collapsed to one point. They are called blossoms, and can be reduced.

~~~
#TODO This is partly fucked

blossom (graph):
    matching = []
    aug_path = null
    while aug_path = find_aug_path(graph, matching):
        matching = augment(matching, aug_path)
        
find_aug_path (graph, matching):
    for node in unmatched_nodes(graph):
        aug_path = aug_bfs(matching, node):
        if aug_path:
            return aug_path 
    return false

aug_bfs (matching, start_node):
    queue = []
    enqueue(queue, start_node)

    while not is_empty(queue):
        node = dequeue(queue)
        for adj_node in neighbors(node):
            if adj_node not in tree and adj_node in matched: 
                tree.add(adj_node)
                for neighbor in neighbors(adj_node):
                    tree.add(neighbor)
                    enqueue(queue, neighbor)

            else if adj_node in tree AND odd-length:
                contract_cycle

            else if adj_node not in matched:
                return path
    return []

augment (matching, aug_path):
    aug_matching = copy(matching)
    for edge in aug_path:
        if edge not in matching:
            append(aug_matching, edge)
        else:
            remove(aug_matching, edge)
    return aug_matching
~~~

## 5.5 The Chinese postman problem
The chinese postman problem asks to find a minimum cost cycle which traverses each edge at least once. 

Note that the lower bound to this problem is to traverse each edge exactly once. Thus if the graph contains a Euler cycle, it must be an optimal solution to the problem. 

A graph G(N, E) contains one or more Euler cycles iff

$$\forall i \in N, \exists k \in \mathbb{Z} : \delta(i) = 2k.$$

However if this condition is not met we need to select one or more edges to traverse multiple times in order to solve the problem.

Since finding an Euler cycle is fairly trivial assuming that one does in fact exist. The problem then becomes which edges to chose to traverse multiple times. The general method consists of finding perfect matches for the nodes with an odd degree, adding those edges to the graph, and repeating untill we are left with a graph that contains an Euler cycle.

### Algorithm:
1. Let $N_U = \lbrace i \in N : \nexists k \in \mathbb{Z} : \delta(i) = 2k  \rbrace$.
2. If $N_U = \varnothing$, find an Euler cycle and break.
3. Let $E_U = \lbrace (i,j): i, j \in N_U, i \neq j\rbrace$.
4. $\forall (i,j) \in E_U : \text{cost}(i,j) = \text{cheapest path from i to j in }G(N,E)$.
5. Let $M$ be the cheapest perfect matching for $G_U(N_U,E_U)$.
6. $E \leftarrow E \cup M$.
7. Repeat.

## 6. Network flow 
### 6.1 Minimum Cost Flow problem
The minimum cost flow problem (MCFP), asks to to find the cheapest possible way of sending a certain amount of flow through a flow network. 

A flow network is defined as a graph G(N, E), where each edge has a capacity, current flow, and cost per flow.

The minimum cost flow problem can be solved using a variation of the simplex method. 

Simplex for MCFP:
1. Construct a spanning tree to use as basic by selecting the edges where the current flow does not equal the upper or lower bound.
2. Calculate the nodeprices for each node in the spanning tree.
3. Calculate the reduced costs for the remaining edges by taking the first node cost + the edge cost - the second node cost.
4. If the cost for a edge is positive we wish to decrease it's flow as much as possible, it is optimal if the flow equals the lower bound. If the cost for a edge is negative we wish to increase it's flow as much as possible, it is optimal if the flow equals the upper bound.
5. We select a non optimal edge to add into the base which creates a cycle.
6. Solve
### 6.2 Maximal flow
The maximum flow problem asks to find a the maximum flow through a single-source, single-sink flow network.

The problem can be solved using Edmonds-Karps method.

Edmonds-Karps method:
1. Let $P$ be the cheapest path from source to sink.
2. Let $f_{send} = \text{min } \lbrace \text{capacity}(i,j) - \text{flow}(i,j)  : (i,j) \in P\rbrace$.
2. If $f_{send} = 0$, break.
2. $\forall (i,j) \in P : \text{flow}(i,j) \leftarrow \text{flow}(i,j) + f_{max}$.
3. Repeat.

### 6.3 The hungarian method
The tillordnignas problem is solved by formulating and solving it's dual.

$$\text{max } \sum_{i=1}^n \alpha_i + \sum_{j=1}^n \beta_j, \text{ when } \alpha_i + \beta_y \leq c_{ij} \forall i,j.$$

Along with its complimentary constraints

$$\forall i,j : x_{ij}(\alpha_i + \beta_y - c_{ij}) = 0.$$

## 7. Integer programming

In general terms the variables found in linear programming can be divided into one of two categories.

1. Continuos variables
2. Integer variables
  
Continuos variables can assume any value on the real line, and therefore put no additional constraints on the range of an objective function.

Integer variables however, pose an additional challenge, as the feasible values of an objective function containing them must have a solution that's discrete in one or more dimensions.

### 7.1 LP-relaxation
An LP-relaxation of a problem simply removes the integrality constraints. The allowed solutionspace to the problem will be a discrete set of points contained within the bounds of the LP-relaxation. 

$$\text{max } z^* \leq \text{max } z_{LP}$$

The difference between $Z_{LP}^*$ abd $z^*$ us called the *dual gap*.
Rounding the LP-relaxation to the nearest integer point can give an infeasable point.

Every feasable solution point to the problem is a lower bound to the problem.

$$\text{max } z \leq \text{max } z^*$$

Therefore we now have an intervall for $z^*$.

$$\text{max } z \leq \text{max } z^* \leq \text{max } z_{LP}$$

By optimising this intervall, either by finding a better allowed solution, or by tightening the linear relaxation, we can achiave a smaller intervall which will result in a smaller relativ error.


### 7.2 Binary variables
A binary variable is an integer variable that can only assume the values 1 or 0.

$$x \in \lbrace 0,1\rbrace $$

Binary variables can be used to reprecent choices between different constraints.
Furthermore constraints on binary variables can be used to specify sets of possible choices that are possible to combine.

### 7.3 Methods for solving integer programming problems
### 4.3.2 Land-Doig-Dakins method

Land-Doig-Dakins method is a tree-searching algorithm for solving integer programming problems.

### Pseudocode
~~~
land_doig_dakin (c, x):
    relaxation = simplex_solve(c, x)
    lower_bound = round_down(relaxation)

    if not relaxation or relaxation <= lower_bound:
        return
    if integer_solution(relaxation):
        return relaxation

    solutions = []
    roof, floor = 0;
    for variable in relaxation:
        if not is_integer(variable):
            roof = round_up(variable)
            floor = round_down(variable)
            break

    append(solutions, land_doig_dakin(floor))
    append(solutions, land_doig_dakin(floor))

    return max(solutions) 
~~~

## 8. Heuristics
For problems deemed unsolvable in a reasonable amount of time, an approximation of the solution can instead be used as a substitute. By only requiring our solution to be "good enough", we can dramatically reduce the complexity of the problem. Algorithms used to approximate optimality are commonly referred to as heuristics.



