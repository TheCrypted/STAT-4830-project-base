I’m trying to build a simple routing algorithm for an online map, but I’m not sure where to start.

That’s a great project! Routing algorithms generally work by representing the map as a graph, where locations are nodes and roads are edges with weights like distance or travel time. Do you have any preference for the technology stack?

I want something straightforward that I can build within a 5 days.

Got it! There are a few ways to approach this:

Custom Graph Implementation – You can manually define a graph and implement Dijkstra’s or A* search from scratch using Python.
Using NetworkX – A powerful Python library for graph operations, where you can construct a graph and use built-in shortest path algorithms.
Using OSMnx – A library specifically designed for working with OpenStreetMap data, letting you easily extract real-world road networks and analyze them with NetworkX.
Would you prefer a fully custom implementation, or are you open to using existing tools?

Existing tools would save me time. NetworkX and OSMnx look good. How do i use them for this work ?


Use OSMnx to fetch the road network for a city.
Convert it into a NetworkX graph, where roads are edges with a "length" attribute.
Implement Dijkstra’s algorithm to find the shortest path between two points.
Here’s an implementation you can use:

import osmnx as ox
import networkx as nx

def get_city_roads(city_name, network_type='drive'):
G = ox.graph_from_place(city_name, network_type=network_type)
nodes, edges = ox.graph_to_gdfs(G)
return G, nodes, edges

ok what about the algorithm here
January 31 at 9:55 PM
import osmnx as ox
import networkx as nx

def get_city_roads(city_name):
G = ox.graph_from_place(city_name, network_type='drive')
return G

def dijkstra(graph, start_node, end_node):
distances = {node: float('inf') for node in graph.nodes}
distances[start_node] = 0
predecessors = {}
visited = set()

while start_node != end_node:
visited.add(start_node)
neighbors = graph.neighbors(start_node)

for neighbor in neighbors:
new_distance = distances[start_node] + graph[start_node][neighbor]["weight"]
if new_distance < distances[neighbor]:
distances[neighbor] = new_distance
predecessors[neighbor] = start_node

start_node = min((node for node in graph.nodes if node not in visited), key=lambda node: distances[node])

path = []
current = end_node
while current != start_node:
path.insert(0, current)
current = predecessors[current]
path.insert(0, start_node)

return path, distances[end_node]

G = get_city_roads("Edinburgh, UK")
start = list(G.nodes)[0]
end = list(G.nodes)[-1]

shortest_path, shortest_distance = dijkstra(G, start, end)
print("Shortest path:", shortest_path)
print("Distance:", shortest_distance)

why doesnt this work
January 31 at 9:55 PM
Nice work! This is a solid attempt, but I see a few issues:

You’re using "weight" as the edge attribute, but in OSMnx, road lengths are usually stored under the "length" attribute. Your code might fail if "weight" isn’t present.
You're modifying start_node inside the loop, which might cause unexpected behavior if no valid node is found.
The loop condition (while start_node != end_node) may fail if a node is disconnected, leading to an infinite loop.
You're not checking if predecessors actually leads to start_node before backtracking the path. If there’s no path, this will throw an error.
Would you like me to help refine it?

fix these issues?

def dijkstra(graph, start_node, end_node):
"""Implements Dijkstra's algorithm to find the shortest path between two nodes"""
~~ corrected code
January 31 at 9:56 PM
how can I optimize this further?

Switch to A Search*

Instead of blindly exploring all nodes like Dijkstra, A* uses a heuristic function to estimate the remaining distance to the goal, making it significantly faster.
The most common heuristic is the haversine distance (straight-line distance between two points on the Earth).
Use a Directed Graph

Currently, your graph is undirected, but real-world roads are usually one-way or two-way. Using a DiGraph (directed graph) in NetworkX can better model real-world constraints and reduce unnecessary computations.
Precompute Shortest Paths

If you’re running multiple queries on the same city, consider precomputing shortest paths using Floyd-Warshall or Johnson’s Algorithm.
Alternatively, you could build a contraction hierarchy for ultra-fast lookups.
Reduce the Graph Size

Instead of using the full road network, you could extract only main roads (highways, arterial roads) using OSMnx’s network_type="all_private" or network_type="bike".
If you're optimizing for pedestrians, use network_type="walk".
Parallelize Path Computation

If you need to find multiple paths at once (e.g., routing for many users), you can use multithreading or GPU-based solutions like cuGraph in RAPIDS AI.

I’d like to see the actual route on a map. Can we plot it?
Yes! OSMnx has built-in functions to visualize the path. You can use ox.plot_graph_route() to overlay the shortest path on the road network.

Here’s how you do it:
import matplotlib.pyplot as plt

# Plot the shortest path on the map
fig, ax = ox.plot_graph_route(G, shortest_path, route_linewidth=4, node_size=0, bgcolor='white')
plt.show()
