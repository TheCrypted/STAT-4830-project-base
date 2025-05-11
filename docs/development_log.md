# Development Log

# Week 3 Self-Critique
After our first week in implementing a pathfinding algorithm for EVs, we have come across a multitude of strengths, weaknesses, and risks that we are faced with going forwards.

**Strengths:**
- With rising popularity of electric vehicles, this algorithm proves to be highly relevant in accounting for the preferences of EV owners today
- Our project is highly scalable, meaning that if we are able to successfully apply our idea to NYC, it can be applied elsewhere too, given we have the data
- The project has the potential to be integrated with real-time traffic data to adjust edge weights; we can enable dynamic route modifications that minimize energy consumption effectively.

**Areas for Improvement:**
- Poor performance on Large Graphs: Dijkstra's Algorithm runs in O(V²) time with an unoptimized approach (without priority queues).
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

# Week 5 Self-Critique

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
   - While A\* provided a structured approach, it's important to consider **machine learning-based alternatives**, such as a **neural network model**.  
   - A neural network could potentially learn patterns in the data that a traditional search algorithm might overlook, leading to better generalization.  
   - We need to test different architectures, experiment with hyperparameter tuning, and compare neural networks against our A\* model to determine feasibility.  

### **3. Performance Optimization**  
   - One observation from our implementation was that the A\* algorithm's efficiency heavily depends on the heuristic function.  
   - Further optimization could include **precomputing heuristic values** or **using more sophisticated heuristics** (e.g., learning-based heuristics).  
   - We should analyze time complexity and consider **pruning techniques** to improve runtime performance.  

## **Next Steps**  

1. **Complete data integration** and develop a thorough data-cleaning pipeline.  
2. **Investigate neural network models** and benchmark them against our A\* approach.  
3. **Optimize the A\* implementation** by refining heuristics and pruning unnecessary computations.  
4. **Enhance visualization tools** to allow for better interpretability and debugging.  

By addressing these areas, we can build a more scalable, data-driven solution while also exploring the strengths and limitations of different methodologies.  


# Week 7 Self-Critique

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
- **Better Evaluation Metrics** – While we score routes using a combined weighting system, we lack a benchmark comparison against traditional methods like A* search or Dijkstra's algorithm.  

## Next Steps  
- **Fix Data Preprocessing Issues** – Ensure all node and edge attributes are correctly assigned, reducing missing values in energy cost and congestion features.  
- **Explore Transformer-Based Approaches** – We are considering testing a BERT model for route sequence optimization, which could provide better context-aware decision-making.  
- **Compare Against Baselines** – Implement A* search and Dijkstra's algorithm to validate whether our GNN-based model actually improves upon traditional heuristics.  


# Week 9 Self-Critique

### What We Accomplished
This week, we made a significant pivot in our project by switching from NYC data to Michigan data, which proved to be more readily accessible and usable for our EV routing purposes. We refined our Graph Neural Network (GNN) model, explored alternative representations of our graph structure, and investigated the feasibility of using a BERT-based model for route prediction. Key accomplishments include:

- **Data Source Transition to Michigan**
  - Successfully acquired and integrated the Extended Vehicle Energy Dataset (eVED) from Ann Arbor, Michigan
  - Began working with Electric Vehicle Trip Energy Data from Michigan, containing 1-minute interval driving records
  - This data provides actual energy consumption metrics in KwH, which was lacking in our previous datasets

- **Graph Neural Network (GNN) Refinement**
  - Iterated on node and edge feature representations to improve model performance
  - Addressed missing data and complexity concerns in our initial approach
  - Adapted our graph structure to work with Michigan road networks using OSMnx
  
- **BERT Model Exploration**
  - Conducted an initial implementation of a BERT-based route prediction model
  - Identified computational challenges, including high processing overhead and complex tokenization
  - Determined the need for extensive hyperparameter tuning to improve performance

### What Worked Well
- **Michigan Data Integration** – The Michigan datasets provided much more concrete energy consumption metrics and road attributes compared to what we had for NYC
- **Graph Representation Improvements** – We explored additional representations beyond simple route rankings, considering geographic intersections, charging stations, and elevation data
- **GNN Feature Engineering** – Progress was made in refining node and edge attributes, incorporating travel time estimates, energy consumption projections, and elevation changes
- **Alternative Model Exploration** – Despite its challenges, the BERT-based approach provided valuable insights into sequence-based routing strategies

### Challenges & Areas for Improvement
1. **Data Integration Across Sources**
   - Calibrating latitude/longitude between different data sources required mathematical transformations
   - Need to better integrate the road network data with actual EV behavior records

2. **Computational Complexity**
   - The BERT model is computationally expensive and currently runs too slowly for practical implementation
   - Need to explore more efficient transformer architectures and model compression techniques

3. **Model Interpretability**
   - Understanding how features influence route selection needs further refinement
   - Developing clear and actionable metrics for evaluating route quality is a priority

### Next Steps
- **Michigan Data Processing**
  - Further refine our preprocessing pipeline for the Michigan datasets
  - Extract and normalize features like elevation, speed limits, and energy consumption

- **GNN Optimization**
  - Refine node and edge feature engineering specifically for Michigan road networks
  - Implement more sophisticated feature encoding techniques
  - Experiment with different graph representation strategies

- **BERT Model Improvement**
  - Conduct thorough hyperparameter tuning
  - Explore model compression and alternative transformer architectures

- **Comparative Analysis**
  - Benchmark the emerging approaches against traditional routing algorithms (A* search, Dijkstra's algorithm)
  - Validate improvements in efficiency, accuracy, and practicality

# Week 11 Self-Critique

## What We Accomplished  
This week, we focused on **optimizing our three primary models: BERT-based, GNN-based, and a new Reinforcement Learning (RL) approach** for the Michigan dataset, resulting in substantial performance improvements. Key achievements include:

- **BERT Model Optimization**
  - Tuned hyperparameters and extended the training duration over many epochs
  - Achieved a **significant reduction in loss**, bringing it down to a negligible value
  - Improved the model's ability to understand and predict optimal route sequences, showing better generalization across the Michigan dataset

- **GNN Optimization**
  - Further refined our node and edge feature sets, integrating richer attributes such as time-of-day congestion patterns, slope-derived energy costs, and road quality scores
  - Improved the graph representation for Michigan roads, incorporating more granular subdivisions and better encoding of directional information
  - Reduced overfitting and improved training stability through regularization techniques and model pruning

- **Reinforcement Learning Implementation**
  - Developed an RL approach to route optimization that learns from the Michigan EV data
  - Created reward functions based on energy consumption and travel time
  - Began evaluating the model's performance against our other approaches

## What Worked Well
- **GNN Performance** – The GNN model has emerged as our strongest performer, showing the most promising results for predicting energy-efficient routes in the Michigan dataset
- **Model Training Stability** – All three models (BERT, GNN, RL) trained smoothly over extended epochs, with loss curves indicating consistent convergence
- **Improved Predictive Accuracy** – Our optimized models were more aligned with real-world EV routing considerations, capturing context and constraints more effectively
- **Integrated Feature Importance** – Visualization tools helped us identify key features influencing predictions, increasing the interpretability of our models

## Challenges & Areas for Improvement
- **Data Integration Limitations**
  - Still facing challenges in properly integrating diverse data sources
  - Mathematical transformations on coordinates only partially resolved location mapping issues
  - Limited access to specialized EV behavior data remains a constraint

- **Long Training Times** – Despite the performance gains, BERT still demands significant compute resources, especially for larger datasets and longer sequences
- **Scalability Concerns** – All models perform well on curated subsets but need additional work to scale across larger networks and more diverse traffic conditions

## Next Steps
- **Further Model Comparison and Validation**
  - Complete comprehensive comparative analysis of our three approaches (GNN, BERT, RL)
  - Evaluate based on runtime efficiency, energy consumption predictions, and adaptability to real-world conditions

- **Improved Data Integration**
  - Develop more sophisticated methods for aligning geographical data across different sources
  - Create robust pipelines that can work with limited EV-specific data

- **Scalability Testing**
  - Apply the optimized models to broader areas of Michigan and analyze model performance under realistic scenarios

- **Documentation & Reproducibility**
  - Finalize detailed documentation of our model pipelines, including training configurations, evaluation metrics, and preprocessing steps
  - Prepare for potential application of our models to other geographical areas if provided with appropriate data

# Week 13 Self-Critique

## What We Accomplished
This week, we focused on refining our Reinforcement Learning model and formalizing our Exploratory Data Analysis (EDA) process to better understand the Michigan dataset. Key accomplishments include:

- **RL Model Refinement**
  - Enhanced our Q-learning algorithm with improved state representation to better capture road network characteristics
  - Implemented a more sophisticated reward function that balances energy efficiency, travel time, and route practicality
  - Developed a custom environment that more accurately simulates EV energy consumption under different driving conditions
  - Integrated elevation data more effectively into the RL state space, improving route optimization for hilly terrains

- **Formalized EDA Completion**
  - Created comprehensive visualizations of energy consumption patterns across different routes and road types
  - Analyzed correlations between elevation changes, vehicle speed, and energy usage
  - Developed interactive maps showing energy-efficient routes compared to time-efficient routes
  - Identified key factors that most significantly impact EV energy consumption in Michigan's topography and road network

- **Prediction Enhancements**
  - Generated more accurate predictions of energy consumption for specific routes
  - Created a benchmarking system to compare our three model approaches against traditional routing algorithms
  - Developed metrics to quantify energy savings across different route options
  - Built visualization tools to communicate potential energy savings to users

## What Worked Well
- **RL Approach Improvements** – While still not matching GNN performance, our reinforcement learning model now shows much stronger results with the refined reward structure
- **Data Storytelling** – Our formalized EDA has created compelling visualizations that clearly communicate the factors influencing EV energy consumption
- **Prediction Accuracy** – Our models now generate more reliable energy consumption estimates across various route types and conditions
- **Integration of Elevation Data** – Successfully incorporated topographical information into all models, with particular benefits for the Michigan dataset

## Challenges & Areas for Improvement
- **Model Transfer Limitations** – Our models remain somewhat location-specific and would require retraining for application to other geographic regions
- **Computational Efficiency** – The RL model still requires significant computational resources, making real-time applications challenging
- **Weather-Related Factors** – Current models have limited ability to account for weather conditions, which significantly impact EV performance
- **Data Gaps** – Some areas within our Michigan dataset still have sparse coverage, creating prediction uncertainties

## Final Development Priorities
- **Cross-Model Ensemble** – Explore combining predictions from all three models to leverage their complementary strengths
- **Visualization Dashboard** – Complete the development of an interactive tool for visualizing route options and energy predictions
- **Documentation Finalization** – Ensure all code, models, and data processing pipelines are thoroughly documented
- **Performance Optimization** – Make final adjustments to improve model inference speed for potential real-world applications

This week's work has significantly improved our understanding of the Michigan dataset's characteristics and enhanced our ability to predict energy consumption patterns. The formalized EDA now provides a robust foundation for communicating our findings, while the refinements to our RL model have meaningfully improved its performance, even though the GNN approach continues to lead in overall effectiveness.

# Final Project Reflection

## Project Evolution and Outcomes
As we complete this project, it's clear that our work evolved significantly from our initial NYC-focused approach to our final Michigan-based implementation. This evolution was driven primarily by data availability constraints and our growing understanding of the problem space.

## Key Findings and Model Performance
Our project culminated in the development of three distinct models:

1. **Graph Neural Network (GNN)** - This emerged as our strongest performer by a significant margin, providing the most accurate and practical results for both:
   - Predicting optimal routes to minimize time and energy consumption
   - Estimating energy consumption for trips based on geographical data, traffic patterns, and infrastructure

2. **BERT-based Model** - While showing promise in sequence prediction, it faced computational efficiency challenges and had difficulty scaling to larger route networks

3. **Reinforcement Learning (RL) Model** - Demonstrated interesting adaptability but couldn't match the GNN's performance in real-world prediction scenarios

## Data Integration Challenges
One of our most significant challenges throughout the project was data integration:
- We struggled with locating and integrating sources that were limited and unrelated
- Mathematical transformations on coordinates only partially addressed location mapping problems
- Obtaining free, accessible EV behavior data proved difficult
- Our final models are ready to work with more specialized data if provided in the future

## Key Data Sources
Our final implementation relied heavily on:

- **OSMnx**
  - Python package for processing street networks (using OpenStreetMap API)
  - Essential for creating our graph structure

- **Extended Vehicle Energy Dataset (eVED)**
  - GPS trace records from 383 vehicles driving over 370k miles in Ann Arbor, Michigan
  - Provided road elevation, speed limits, and approximations of energy usage for each trip
  - Reference: "Large Scale Dataset for Vehicle Energy Consumption Research" (Oh et al., 2020)

- **Electric Vehicle Trip Energy Data**
  - 1-minute interval driving records of EVs (June 2015 - June 2016)
  - Contains energy consumption in KwH for each trip
  - Includes average latitude/longitude and battery metrics (current, voltage, temperature)

## Project Pivot
With our successive self-critiques, we realized that our biggest problem was data availability, and the original NYC-focused problem we proposed simply did not have feasible resources to solve effectively. This led to our pivot toward energy consumption prediction for vehicles in Michigan, where better data was available. But still, we were unable to get some data on some of our relavent problems, and we were forced to reevaluate waht type of data was even present, so we decided upon using the current iteration that relied on analyses of michigan based vehicle energy performance.

## Value Proposition
Our algorithms now provide two valuable predictions:
1. An optimal route that minimizes both time to destination and energy consumption
2. An estimate of energy consumption for a trip based on geographical data, traffic patterns, infrastructure, and trip endpoints

These outcomes, while different from our initial vision, represent significant progress in the field of energy-efficient EV routing and highlight the importance of data availability in machine learning projects.
