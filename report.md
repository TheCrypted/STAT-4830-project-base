# Optimization of NYC Travel for Electric Vehicles
## Problem Statement
### What are you trying to optimize?  
By integrating several city-specific elements into a graph-based model, we are refining the pathfinding algorithm for electric vehicle (EV) travel in New York City. To start, we'll apply Dijkstra's method to find the best routes to specified places. In order to create a more effective and useful route optimization system, we will next improve the algorithm incorporating energy consumption statistics, congestion fees, and real-time traffic data.
### Why is this issue important?  
As EV use rises and municipal rules like congestion pricing change, it is essential to optimize travel routes for sustainability and efficiency. In contrast to conventional navigation software, our study seeks to offer accurate insights on energy-efficient travel while accounting for urban constraints. The objective is to determine a better strategy for electric car consumers, since current software (like Tesla's navigation system) frequently necessitates extra fees. Our goal is to create an affordable substitute that will help both private consumers and automakers who want to contract with other parties to determine energy use.
### How are you going to gauge success?  
A number of important measures will be used to gauge the project's success. First, we will contrast our findings with a baseline model that uses Dijkstra's algorithm to construct routes based solely on basic distance-based approaches. The model will then be improved by adding more city-specific variables, such energy usage, traffic jams, and toll prices, to the graph. The performance of our system will then be compared to that of proprietary EV routing software and other navigation tools currently in use, such as Google Maps, in order to determine how effective it is. Our objective is to ascertain whether our strategy provides more energy-efficient routes while preserving or enhancing journey durations. In order to set standards for route planning optimization, we will also examine the power consumption and energy savings of EVs.
### What limitations do you have?  
A number of important limitations could affect how well our optimization strategy works. The inability to obtain real-time traffic data and congestion pricing information, which are crucial for precisely forecasting the best routes, is one of the main obstacles. Furthermore, since the graph's complexity rises with the number of roads, crossings, and changing traffic conditions, guaranteeing computational efficiency when pathfinding on extensive NYC road networks poses a substantial challenge. Lastly, as the fastest route may not always be the most energy-efficient, balancing the trade-off between travel time and energy efficiency is a crucial component of the project. This calls for a methodical optimization approach that takes user preferences and real-world limitations into account.
### What information is required?  
The following data sources must be accessible in order for us to use and improve our optimization model:  
To precisely model route architecture and congestion patterns, use the **NYC road network and traffic flow data**.  
- **Models of electric car energy consumption** to calculate power consumption on various routes.  
**Details of congestion tax and toll pricing** to take into consideration the monetary expenses related to transport.  
- **Weather and road condition data** to account for outside factors that impact trip times and energy usage.  
### What might not work?  
A number of possible obstacles could reduce our strategy's efficacy:  
Inaccurate route forecasts could arise from **incomplete or unreliable traffic and pricing data**.  
Processing large-scale road networks may result in sluggish performance due of the high computational complexity.  
Route optimization may be restricted or access to essential data may be restricted due to unforeseen legal or regulatory constraints.  
We anticipate that combining many data sources into a single system will be the largest obstacle. Synchronization is challenging since these datasets frequently originate from several sources and have differing formats and quality levels. To guarantee the dependability of our optimization model, these discrepancies must be fixed.
---
## Technical Method
### Formulation in Mathematics  
Our strategy is based on minimizing a cost function that takes into account several aspects of travel:  
The objective is to minimize a cost function that includes the costs of congestion, energy use, and travel time.  
Congestion pricing zones, traffic hotspots throughout the day, traffic restrictions, and the availability of charging stations are some of the limitations.  
### Algorithm/Approach Choice and Justification  
A multi-phase method will be used to improve our pathfinding algorithm:  
1. The starting point for determining the shortest path based on distance will be **Dijkstra's algorithm**.  
2. To account for practical EV limitations like battery efficiency and charging stations, **A* or other heuristic-based algorithms** will be implemented.  
3. In order to optimize routing decisions dynamically based on historical and real-time data, **reinforcement learning techniques** will be investigated.  
### Strategy for PyTorch Implementation  
PyTorch will be used for deep learning integration in order to effectively model and optimize our pathfinding algorithm:  
- **Use graph neural networks (GNNs) to create graph-based representations** of the road network in New York City.  
- **Use a neural network model** to dynamically forecast travel expenses that take tolls, energy efficiency, and congestion into account.  
- **Use deep reinforcement learning to optimize pathfinding** to incrementally enhance route selection by utilizing past outcomes.
We also are looking for new ways to incorporate novel model techniques as potential ways to optimize path finding. We have looked into one example in the following (TransPath algorithm: https://airi-institute.github.io/TransPath/). This could be a promising tool that we could optimize and localize for our given problem.
### Methods of Validation  
We will use a variety of validation tools to make sure our strategy is effective:  
To evaluate the effectiveness of our algorithm, compare its routes with those found on Google Maps.  
To assess practicality, **simulate EV travel under various constraints**. We will try to localize our problem to a given subset of EVs such that we are able to best maximize car specs and potentially increase the scale from there.  
To assess the model's predicted accuracy, test it using historical traffic and congestion data.  
### Resource Needs and Limitations  
Given the size of NYC's road network, our model's implementation necessitates access to high-performance computing resources. Another significant limitation that might affect model accuracy is the acquisition of trustworthy real-time traffic and congestion data.
Perhaps the biggest problem we may run into is the obtaining of car specific routing algorithms as certain vehicles may use alternatives that are not easily accessible. 
---
## Preliminary Findings
### Proof That Your Implementation Is Effective  
Paths inside the NYC road network are successfully calculated by our first application of Dijkstra's algorithm. 
The algorithm's ability to locate the shortest paths is confirmed by early experiments, providing a solid basis for further improvements.
Djikstra's on a path in NYC is simply the easiest way to traverse through a set of nodes and the most intuitive approach, but we hope to incorporate the mulitude of edge weights to determine the optimal configuration using edge weights.
### Fundamental Performance Indicators  
The following metrics will be used to assess our model: **Execution time:** Quantifying the algorithm's effectiveness in calculating pathways under various circumstances.  
- **Accuracy of energy estimation:** Verifying power efficiency calculations by comparing expected and actual EV energy usage.  
### Test Case Outcomes  
Paths have been correctly calculated in preliminary testing on tiny NYC road network portions. Nevertheless, we have to still implement the other metrics that we hope to finally utilize as tools to guide our decision making process. 
### Present Restrictions  
Even though the preliminary findings show viability, there are still a number of restrictions:  
Dynamic responsiveness is limited by the early implementation's **lack of real-time traffic updates**.  
The energy consumption model needs to be improved in order to take into consideration the differences between various EV models and driving circumstances.  
### Measures of Resource Usage  
We are keeping an eye on computational efficiency as we grow our model, paying particular attention to memory and processor load during extensive testing.
### Unexpected Difficulties  
Integrating real-world congestion pricing data into our model has proven to be a significant difficulty. Additional preparation steps are necessary because this data is frequently inconsistently structured or lacking.
---
## Next Actions
### Immediate Enhancements Are Required  
The following enhancements are given priority in order to strengthen our model:  
To increase routing accuracy, **incorporate real-time traffic and congestion pricing data**.  
To improve forecasts for various EV kinds, the energy consumption model should be improved. We also need to find ways to obtain vehicle specific routing algorithms. 
### Technical Difficulties to Handle  
As we scale our method, we must overcome a number of technological obstacles:  
To guarantee computational viability, large-scale road networks must be handled well.  
By adding real-time traffic variations and recent policy changes, the algorithm is **adapted to dynamic city conditions**.  
### Queries You Need Answered  
In order to increase the prediction accuracy of our model, we require outside perspectives on the following: **Best sources for real-time congestion data**.  
Real-world datasets are used to validate EV energy consumption models.  
### Other Strategies to Try  
We will investigate more strategies in addition to our present ones:  
To increase dynamic adaptability, **machine learning-based route prediction** is being tested.  
Road closures, pedestrian zones, and temporary traffic limits are examples of **incorporating additional urban factors**.  
We will also experiemnt with a mulitude of different existing path-finding algorithms that have been optimized by a variety of sources and try to localize those algorithms given our cosntraints and our problem.
### What You Have Discovered Thus Far  
Our preliminary research has shed important light on whether EV-specific pathfinding is feasible:  
- **Traditional techniques such as Dijkstra's can be used to efficiently implement basic pathfinding**.  
It is difficult but essential to include real-world restrictions when developing a workable and significant solution.  
Our goal is to create a navigation tool that is more efficient, effective, and customized for EV travel in New York City by further improving our methodology.

