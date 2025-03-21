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

# **Self-Critique – Week 5**  

## **Progress This Week**  
This week, we made significant strides in implementing and visualizing our approach to solving the problem. Specifically, we **developed an A\*** (**A-star**) algorithm, which provided a structured method for pathfinding and decision-making. The core of our implementation involved:  

1. **State Representation & Heuristics**  
   - We carefully designed our state space to ensure efficient traversal, using an admissible heuristic to guide the search effectively.  
   - The heuristic function played a critical role in balancing optimality and computational efficiency.  
   - By tuning different heuristic functions, we observed variations in performance, highlighting the importance of selecting the right heuristic for our problem.  

2. **Priority Queue for Optimal Path Selection**  
   - We correctly implemented the priority queue, allowing us to always expand the most promising node first.  
   - The cost function was well-integrated, ensuring that the algorithm consistently found the optimal path when possible.  

3. **Visualization of Search Progress**  
   - A major accomplishment was building a **visualization tool** to track the A\* search in action.  
   - This not only helped with debugging but also provided insights into how the algorithm navigates the solution space.  
   - The visualization confirmed that our implementation worked as expected but also highlighted inefficiencies in certain cases, which could be optimized further.  

## **Areas for Improvement**  

Despite these advancements, there are still key areas where we need to focus our efforts:  

### **1. Data Integration & Cleaning**  
   - While we have a functional algorithm, it still operates on a controlled dataset. We need to ensure **real-world data integration** so that the system can work on diverse inputs.  
   - Data inconsistencies (such as missing or noisy values) may impact performance, so implementing a **robust data cleaning pipeline** is crucial.  
   - Standardizing data formats, handling missing values, and feature encoding should be our next priorities.  

### **2. Exploring Alternative Approaches**  
   - While A\* provided a structured approach, it’s important to consider **machine learning-based alternatives**, such as a **neural network model**.  
   - A neural network could potentially learn patterns in the data that a traditional search algorithm might overlook, leading to better generalization.  
   - We need to test different architectures, experiment with hyperparameter tuning, and compare neural networks against our A\* model to determine feasibility.  

### **3. Performance Optimization**  
   - One observation from our implementation was that the A\* algorithm’s efficiency heavily depends on the heuristic function.  
   - Further optimization could include **precomputing heuristic values** or **using more sophisticated heuristics** (e.g., learning-based heuristics).  
   - We should analyze time complexity and consider **pruning techniques** to improve runtime performance.  

## **Next Steps**  

1. **Complete data integration** and develop a thorough data-cleaning pipeline.  
2. **Investigate neural network models** and benchmark them against our A\* approach.  
3. **Optimize the A\* implementation** by refining heuristics and pruning unnecessary computations.  
4. **Enhance visualization tools** to allow for better interpretability and debugging.  

By addressing these areas, we can build a more scalable, data-driven solution while also exploring the strengths and limitations of different methodologies.  


# Week 7 Self-Critique: EV Route Optimization in NYC

## What We Accomplished  
This week, we focused on developing a graph-based route optimization model for electric vehicles (EVs) in NYC. We implemented a Graph Neural Network (GNN) to predict energy efficiency, congestion levels, and route quality. Additionally, we:  

- Successfully loaded and processed the NYC road network using OSMnx.  
- Designed a neural network-based routing model that scores routes based on energy consumption, congestion, and efficiency.  
- Implemented a probabilistic route selection strategy using softmax-weighted sampling.  
- Visualized the NYC road network and the optimized route using Matplotlib and OSMnx.  

## What Worked Well  
- **Graph Representation & Feature Engineering** – We effectively encoded the road network into a graph structure, assigning meaningful edge weights like congestion levels, energy cost, and distance.  
- **Neural Network Integration** – The GNN model was able to learn from node embeddings, allowing us to refine route selection using deep learning.  
- **Route Visualization** – Our Matplotlib & OSMnx-based visualization effectively highlighted the optimized route, making it easier to interpret model results.  

## Challenges & Areas for Improvement  
- **Data Integration & Cleaning Issues** – We still face inconsistencies in edge and node attributes, leading to gaps in model inputs. Some nodes lack key features like speed limits or elevation, which might impact route scoring.  
- **Probabilistic Route Selection Refinements** – Our softmax-based selection is sensitive to score variations. Some low-quality routes are occasionally selected, and we may need to fine-tune weight assignments.  
- **Better Evaluation Metrics** – While we score routes using a combined weighting system, we lack a benchmark comparison against traditional methods like A* search or Dijkstra’s algorithm.  

## Next Steps  
- **Fix Data Preprocessing Issues** – Ensure all node and edge attributes are correctly assigned, reducing missing values in energy cost and congestion features.  
- **Explore Transformer-Based Approaches** – We are considering testing a BERT model for route sequence optimization, which could provide better context-aware decision-making.  
- **Compare Against Baselines** – Implement A* search and Dijkstra’s algorithm to validate whether our GNN-based model actually improves upon traditional heuristics.  



 
