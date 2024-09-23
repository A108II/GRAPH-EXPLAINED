# Graph Class Documentation

This README explains the functionality of a simple `Graph` class implemented in JavaScript, which supports undirected graphs. The class includes methods to add vertices, add edges, remove edges, and remove vertices.

## Code

```javascript
class Graph {
    constructor() {
        this.adjacencyList = {};  // Initializes an empty adjacency list
    }

    // Adds a new vertex to the graph
    addVertex(vertex) {
        if(!this.adjacencyList[vertex]) {
            this.adjacencyList[vertex] = [];
            return true;
        }
        return false;
    }

    // Adds an undirected edge between two vertices
    addEdge(vertexOne, vertexTwo) {
        if(this.adjacencyList[vertexOne] && this.adjacencyList[vertexTwo]) {
            this.adjacencyList[vertexOne].push(vertexTwo);
            this.adjacencyList[vertexTwo].push(vertexOne);
            return true;
        }
        return false;
    }

    // Removes an edge between two vertices
    removeEdge(vertexOne, vertexTwo) {
        if(this.adjacencyList[vertexOne] && this.adjacencyList[vertexTwo]) {
            this.adjacencyList[vertexOne] = this.adjacencyList[vertexOne].filter(v => v !== vertexTwo);
            this.adjacencyList[vertexTwo] = this.adjacencyList[vertexTwo].filter(v => v !== vertexOne);
            return true;
        }
        return false;
    }

    // Removes a vertex and all its connected edges
    removeVertex(vertex) {
        if(!this.adjacencyList[vertex]) return undefined;
        while(this.adjacencyList[vertex].length) {
            let temp = this.adjacencyList[vertex].pop();
            this.removeEdge(vertex, temp);
        }
        delete this.adjacencyList[vertex];
        return this;
    }
}

const myGraph = new Graph();

// Adding vertices
myGraph.addVertex('A');
myGraph.addVertex('B');
myGraph.addVertex('C');

// Adding edges
myGraph.addEdge('A', 'B');
myGraph.addEdge('B', 'C');
myGraph.addEdge('A', 'C');
```

## Explanation

### Constructor
- Initializes the `adjacencyList` as an empty object to store graph vertices and edges.

### `addVertex(vertex)`
- Adds a new vertex to the graph if it doesn't already exist.
- **Returns**: `true` if the vertex is added, `false` if it already exists.

### `addEdge(vertexOne, vertexTwo)`
- Creates an undirected edge between two vertices if both exist in the graph.
- **Returns**: `true` if the edge is successfully added, `false` otherwise.

### `removeEdge(vertexOne, vertexTwo)`
- Removes an edge between two vertices.
- **Returns**: `true` if the edge is removed, `false` if vertices are missing.

### `removeVertex(vertex)`
- Deletes a vertex and all edges connected to it.
- **Returns**: The modified graph after removal.


# BIG O OF GRAPH

## || SPACE COMPLEXITY
### ADJACENCY MATRIX
IT USES A V×V 2D ARRAY WHERE EACH CELL INDICATES WHETHER AN EDGE EXISTS BETWEEN VERTICES.  
EVEN IF AN EDGE IS MISSING, THE SPACE IS STILL ALLOCATED, RESULTING IN O(V²) SPACE.

### ADJACENCY LIST
IT ONLY STORES ACTUAL EDGES IN LINKED LISTS FOR EACH VERTEX,  
RESULTING IN O(V + E) SPACE, EFFICIENT FOR SPARSE GRAPHS.

---

## || ADDING A VERTEX
### ADJACENCY MATRIX
ADDING A VERTEX REQUIRES CREATING A NEW V×V MATRIX, COPYING THE OLD DATA,  
AND ADDING A NEW ROW AND COLUMN, WHICH TAKES O(V²) TIME.

### ADJACENCY LIST
ADDING A VERTEX IS SIMPLER, JUST ADDING A NEW EMPTY LIST, TAKING O(1) TIME.

---

## || CREATING AN EDGE
### ADJACENCY MATRIX
CREATING AN EDGE TAKES O(1) TIME, AS WE SIMPLY UPDATE THE MATRIX AT THE CORRESPONDING CELL.

### ADJACENCY LIST
CREATING AN EDGE TAKES O(1) TIME, AS WE ONLY NEED TO ADD THE EDGE TO THE LIST OF THE SOURCE VERTEX.

---

## || REMOVING AN EDGE
### ADJACENCY MATRIX
REMOVING AN EDGE TAKES O(1) TIME, AS WE SIMPLY SET THE CORRESPONDING MATRIX CELL TO 0 OR NULL.

### ADJACENCY LIST
REMOVING AN EDGE TAKES O(E) TIME IN THE WORST CASE,  
AS YOU NEED TO SEARCH THROUGH THE LIST TO FIND AND REMOVE THE EDGE.

---

## || REMOVING A VERTEX
### ADJACENCY MATRIX
REMOVING A VERTEX TAKES O(V²) TIME, AS YOU MUST DELETE THE ENTIRE ROW AND COLUMN, THEN SHIFT REMAINING DATA.

### ADJACENCY LIST
REMOVING A VERTEX TAKES O(V + E) TIME, AS YOU REMOVE THE VERTEX’S  
LIST AND SEARCH THROUGH OTHER LISTS TO DELETE EDGES CONNECTED TO IT.