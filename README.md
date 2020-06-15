# Reference

DATA STRUCTURES



DEPTH FIRST SEARCH



Algorithm:
1. Let us start search at vertex j
2. Push j onto stack
3. Mark all vertices as unvisited
           for i=1 to n do
                 visited[i]=0
4. While not empty stack do
           begin
                    v=pop(stack)
                    if (not visited(v))
                            visited[v]=1
                            push all adjacent unvisited vertices of v onto stack
           end
5. Stop



Implementation: (using recursion)

// C++ program to print DFS traversal from 
// a given vertex in a given graph 
#include<bits/stdc++.h> 
using namespace std; 

// Graph class represents a directed graph 
// using adjacency list representation 
class Graph 
{ 
	int V; // No. of vertices 

	// Pointer to an array containing 
	// adjacency lists 
	list<int> *adj; 

	// A recursive function used by DFS 
	void DFSUtil(int v, bool visited[]); 
public: 
	Graph(int V); // Constructor 

	// function to add an edge to graph 
	void addEdge(int v, int w); 

	// DFS traversal of the vertices 
	// reachable from v 
	void DFS(int v); 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
	adj[v].push_back(w); // Add w to v’s list. 
} 

void Graph::DFSUtil(int v, bool visited[]) 
{ 
	// Mark the current node as visited and 
	// print it 
	visited[v] = true; 
	cout << v << " "; 

	// Recur for all the vertices adjacent 
	// to this vertex 
	list<int>::iterator i; 
	for (i = adj[v].begin(); i != adj[v].end(); ++i) 
		if (!visited[*i]) 
			DFSUtil(*i, visited); 
} 

// DFS traversal of the vertices reachable from v. 
// It uses recursive DFSUtil() 
void Graph::DFS(int v) 
{ 
	// Mark all the vertices as not visited 
	bool *visited = new bool[V]; 
	for (int i = 0; i < V; i++) 
		visited[i] = false; 

	// Call the recursive helper function 
	// to print DFS traversal 
	DFSUtil(v, visited); 
} 

// Driver code 
int main() 
{ 
	// Create a graph given in the above diagram 
	Graph g(4); 
	g.addEdge(0, 1); 
	g.addEdge(0, 2); 
	g.addEdge(1, 2); 
	g.addEdge(2, 0); 
	g.addEdge(2, 3); 
	g.addEdge(3, 3); 

	cout << "Following is Depth First Traversal"
			" (starting from vertex 2) \n"; 
	g.DFS(2); 

	return 0; 
} 



BREADTH FIRST SEARCH



Algorithm:

1. Let us start search at vertex j
2. Mark all vertices as unvisited
            for i=1 to n do
                    visited[i]=0
3. Mark j as visited
           visited[j]=1
4. Add j in queue
5. While not queue empty do
           begin
                   i=queue.pop
                   for all vertices j adjacent to i do
                               if(not visited[j]==1)
                                             add j in queue
                                             visited[j]=1
           end
6. Stop



Implementation:

 // Program to print BFS traversal from a given 
// source vertex. BFS(int s) traverses vertices 
// reachable from s. 
#include<iostream> 
#include <list> 

using namespace std; 

// This class represents a directed graph using 
// adjacency list representation 
class Graph 
{ 
	int V; // No. of vertices 

	// Pointer to an array containing adjacency 
	// lists 
	list<int> *adj; 
public: 
	Graph(int V); // Constructor 

	// function to add an edge to graph 
	void addEdge(int v, int w); 

	// prints BFS traversal from a given source s 
	void BFS(int s); 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
	adj[v].push_back(w); // Add w to v’s list. 
} 

void Graph::BFS(int s) 
{ 
	// Mark all the vertices as not visited 
	bool *visited = new bool[V]; 
	for(int i = 0; i < V; i++) 
		visited[i] = false; 

	// Create a queue for BFS 
	list<int> queue; 

	// Mark the current node as visited and enqueue it 
	visited[s] = true; 
	queue.push_back(s); 

	// 'i' will be used to get all adjacent 
	// vertices of a vertex 
	list<int>::iterator i; 

	while(!queue.empty()) 
	{ 
		// Dequeue a vertex from queue and print it 
		s = queue.front(); 
		cout << s << " "; 
		queue.pop_front(); 

		// Get all adjacent vertices of the dequeued 
		// vertex s. If a adjacent has not been visited, 
		// then mark it visited and enqueue it 
		for (i = adj[s].begin(); i != adj[s].end(); ++i) 
		{ 
			if (!visited[*i]) 
			{ 
				visited[*i] = true; 
				queue.push_back(*i); 
			} 
		} 
	} 
} 

// Driver program to test methods of graph class 
int main() 
{ 
	// Create a graph given in the above diagram 
	Graph g(4); 
	g.addEdge(0, 1); 
	g.addEdge(0, 2); 
	g.addEdge(1, 2); 
	g.addEdge(2, 0); 
	g.addEdge(2, 3); 
	g.addEdge(3, 3); 

	cout << "Following is Breadth First Traversal "
		<< "(starting from vertex 2) \n"; 
	g.BFS(2); 

	return 0; 
} 



SPANNING TREE


KRUSKAL'S ALGORITHM

1. Remove all loops and parallel edges
2.Arrange all edges in their increasing order of weight
3. Add the edge which has the least weightage
4. Leave the edge if it forms loop
5. Repeat 3 and 4 until all edges are covered


PRIM'S ALGORITHM

1. Remove all loops and parallel edges
2. Choose any arbitrary node as root node
3. Check outgoing edges and select the one with less cost.


RED BLACK TREE

INSERTION:

1. Check whether tree is empty.
2. If tree is empty then insert the newnode as root node with color BLACK and exit from the operation.
3. If tree is not empty then insert the newnode as leaf node with color RED
4. If the parent of newnode is black then exit from the operation.
5. If the parent of newnode is Red then check the color of parent node's sibling of newnode
6. If it is colored Black or NULL then make suitable Rotation and Recolor it.
    LL,RR- interchange parent and grandparent's color
    LR,RL- interchange newnode and grandparent's color
7. If it is colored Red, then recolor.
        change parent and uncle color to black.
        if  grandparent is root node, exit.
        else
               change grandparent to Red.
               Repeat 4 to 7.


BINARY HEAP TREE

      Binary heap tree is a complete binary tree except at the last level. At the last level all its elements are towards left. It is implemented using arrays. Inserting in heap tree is adding elements to the next position and so on. On inserting an element, we do heapify up. That is , the last element added is compared with its parent , if it is max, swap or move up and repeat. Delete- deleting the root. Here we make last element as root and decrements the size and do heapify down. The root is compared with its child that is max. If root is max move down and repeat or else swap, move down and repeat.


