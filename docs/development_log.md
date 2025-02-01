# Development Log

## Week 3 Self-Critique
After our first week in implementing a pathfinding algorithm for EVs, we have come across a multitude of strengths, weaknesses, and risks that we are faced with going forwards.

**Strengths:**
- With rising popularity of electric vehicles, this algorithm proves to be highly relevant in accounting for the preferences of EV owners today
- Our project is highly scalable, meaning that if we are able to successfully apply our idea to NYC, it can be applied elsewhere too, given we have the data
- The project has the potential to be integrated with real-time traffic data to adjust edge weights; we can enable dynamic route modifications that minimize energy consumption effectively.

**Areas for Improvement:**
- Poor performance on Large Graphs: Dijkstra’s Algorithm runs in O(V²) time with an unoptimized approach (without priority queues).
- Lack of consideration for real-time factors such as traffic and geographic factors such as terrain/change in altitude along a route
- Our current graph model uses a undirected graph: could pose issues for one way streets, a commonality in NYC and other cities

**Critical Risks/Assumptions:**
	We are assuming currently that congestion/traffic will be available. However even if it is available, it is static and does not represent a real world case where traffic is constantly changing even if certain trends persist. Also we must consider the differences between different EV brands and even models within the same brand, as energy consumption while idle, at certain speeds, and in certain terrain may be different from vehicle to vehicle.
 
**Concrete Next Actions:**
- Implement Dijkstras with a priority queue to bring runtime down to O(Elog(V)) using heapq or networkx.shortest_path_length()
- Find data on traffic and terrain, and utilize equations that relate these features to energy consumption, recalculate edge weights and run Dijkstras or a better algorithm again
- Convert our undirected graph into a directed one via nx.DiGraph(), OSMnx graphs are already directed by default

**Resource Needs:**
	Most important necessity currently is finding data for traffic and terrain in our preferred city (likely NYC) and then utilizing equations we have that relate these factors to energy consumption. Will look at topographic data on NYC, as well as traffic congestion data from congestion pricing policy. Also would be advisable that we focus on one EV model for the time being before expanding our scope to other models. Likely will be a Tesla model.
