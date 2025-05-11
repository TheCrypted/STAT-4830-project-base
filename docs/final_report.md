# Optimizing Vehicle Routing with Graph-Based and Probabilistic Models

## Executive Summary

This report presents our research on optimizing vehicle routing using graph-based and probabilistic models. Our project aimed to develop algorithms that minimize travel time and energy consumption while providing detailed insights beyond what current routing applications offer. We explored multiple approaches including BERT-based models, Reinforcement Learning, and Graph Neural Networks to address this NP-complete problem.

## Problem Statement

Modern routing software provides limited insights into the eco-friendliness and efficiency of trips. Our research aimed to:

1. Create a systematic pipeline that considers trip-specific features, geographic data, infrastructural elements, and traffic patterns to accurately model travel behavior and energy usage
2. Calculate concrete statistics benchmarking different models and explore novel approaches to this NP-complete problem with energy consumption constraints
3. Provide richer, more detailed insights on vehicle energy consumption compared to contemporary routing applications

## Motivation

With growing emphasis on reducing energy consumption in modern society, accurate vehicle metrics and efficient routing algorithms can play a crucial role in minimizing overall energy usage. Our project explored novel approaches to this NP-complete problem with specific energy consumption constraints that are increasingly relevant in today's sustainability-focused world.

## Success Metrics

Our algorithms provide two valuable predictions:

1. Optimal route prediction that minimizes time to destination and energy consumption
2. Energy consumption prediction for trips based on geographical data, traffic, infrastructural elements, and start/end coordinates

We evaluated these predictions by:

1. Comparing route predictions against baseline models (Dijkstra's algorithm) and historically efficient routes
2. Comparing predicted energy consumption against actual energy used in historical trips with the same start and end points

## Data Sources

1. **OSMnx**: Python package for processing street networks using OpenStreetMap API to create graph structures
2. **Extended Vehicle Energy Dataset (eVED)**:
   - GPS trace records from 383 vehicles driving over 370,000 miles in Ann Arbor, Michigan
   - Road elevation data
   - Speed limits
   - Calibrated latitude/longitude
   - Energy usage approximations (MAF[g/sec] × trip duration)
3. **Electric Vehicle Trip Energy Data**:
   - 1-minute interval driving records of EVs (June 2015 - June 2016)
   - Energy consumption in KwH for each trip
   - Average latitude and longitude
   - Current, voltage, and battery temperature data

## Technical Approach

### Data Transformations
- Haversine Formula: Calculated distance between points using latitude and longitude coordinates
- Graph Structure Overlay: Created a graph structure incorporating location, trip, and vehicle information
- Data Normalization: Normalized coordinates to focus on spatial trip structure rather than minute coordinate differences

### Baseline Algorithms

1. **Dijkstra's Algorithm**:
   - Simple graph algorithm finding shortest path between points in a weighted graph
   - Intersections and dead ends as nodes, streets as edges, road distances as weights
   - Runtime complexity: O((V + E)logV)

2. **A* Algorithm**:
   - More advanced algorithm using formula f(n) = g(n) + h(n)
   - g(n): Cost to reach current node
   - h(n): Predicted cost to reach destination
   - Selects node with lowest f(n) until destination is reached

<img width="1026" alt="image" src="https://github.com/user-attachments/assets/41417f39-27e8-4807-979c-666d099e10db" />

### Advanced Models

#### BERT Model

Inspired by "BERT-Trip: Effective and Scalable Trip Representation using Attentive Contrast Learning" (Kuo et al., 2023), we designed a BERT-based model that:

- Encodes source and destination nodes as special tokens to capture bidirectional context
- Employs an MLP (Multilayer Perceptron) head to regress the full trip trajectory in a single forward pass
- Uses mean squared error as the loss function

Data processing included:
- Loading ~10GB of CSVs in 100k-row chunks
- Deriving sequences of latitudes and longitudes sorted by timestamps
- Calculating a bounding box to normalize coordinates
- Padding/truncating to 100 waypoints per route
- Creating a custom tokenizer by augmenting BERT vocabulary with synthetic latitude and longitude tokens

Optimizations:
- Better initialization through positional encoding
- Initially freezing embedding layer and pretrained BERT weights
- Normalization of coordinates (biggest performance boost)
- Vanilla learning rate decay

Results:
- Path error curve converged to ~0.01 MSE
- Average Haversine error ≈ 20 km per point
- ~65% training accuracy
- Loss remained relatively high due to BERT being trained primarily for text sequences

<img width="505" alt="image" src="https://github.com/user-attachments/assets/ebd21f92-895b-45af-8bf6-82b4d8e42b29" />

#### Reinforcement Learning

Based on "Multi-objective reinforcement learning approach for trip recommendation" (Chen et al., 2023), we implemented:

- A Markov Decision Process model where states represent positions in a trip
- A Deep Q-Network (DQN) approach for discrete action spaces
- A target network based on the Bellman equation for training stability
- Soft updates to gradually adjust target network parameters

Reward shaping included:
- Change in shortest-path distance to goal
- Goal bonus (+10), step penalty (–0.1), invalid action (–1.0), timeout penalty (–10)
- Clipped final reward to [–5, +5] to stabilize learning

Optimizations:
- Switched from simple Q-learning to Rainbow DQN agent
- Added residual connections to prevent exploding gradients
- Deferred learning until sufficient buffer fill

Results:
- Reward improved from –300+ to ~–80 after graph node alignment and shaping
- Model showed learning via improved recent average reward but remained noisy
- Training time limitations prevented full convergence given the massive state space

<img width="505" alt="image" src="https://github.com/user-attachments/assets/311b3dd7-720b-489e-9bdc-ccd4495b81bd" />

#### Graph Neural Network for Energy Consumption

Inspired by "Electric vehicle energy consumption modelling and prediction based on road information" (Wang et al., 2015), we developed a GNN that:

- Learned representations of road networks with nodes as intersections and edges as roads
- Used edge features like length and speed limit
- Processed sequences of nodes using GRU (recurrent neural network) to learn energy accumulation patterns

Optimizations:
- Normalization of coordinates, road lengths, and speed limits
- Hierarchical information processing (GNN layers for embeddings, GRU for sequences)
- Dropout (30%) to prevent overfitting

Results:
- Successfully predicted energy-efficient routes
- Example comparison: Dijkstra's path (14,037.92m) vs. GNN path (14,652.49m) with improved energy efficiency
- Average loss for energy consumption prediction of about 0.49
<img width="338" alt="image" src="https://github.com/user-attachments/assets/6fa92f08-5e02-491f-b2c4-20dd463cd4e2" />

<img width="510" alt="image" src="https://github.com/user-attachments/assets/909554a2-8333-460e-89c7-61daa5bf3dd4" />

## Challenges & Reflections

### Data Integration Challenges
- Difficulty locating and integrating disparate data sources
- Limited access to free, comprehensive EV behavior data
- Project evolution due to data constraints leading to a pivot toward general vehicle energy consumption

### Effective Approaches
- LLM assistance for ideation, preliminary coding, and debugging
- Efficient data preprocessing once objectives were reframed
- Comprehensive literature review to inform model development

## Conclusion

Our research demonstrates the viability of using advanced machine learning techniques to optimize vehicle routing for both time and energy efficiency. While each approach had strengths and limitations, the Graph Neural Network showed particular promise in predicting energy-efficient routes. Future work could benefit from more specialized electric vehicle data and additional computational resources to train models more thoroughly.

## Acknowledgements

- Professor Davis
- Zhang, S., Fatih, D., Abdulqadir, F., Schwarz, T., & Ma, X. (2022). Extended vehicle energy dataset (eVED): an enhanced large-scale dataset for deep learning on vehicle trip energy consumption. arXiv preprint arXiv:2203.08630.
- Devlin, Jacob, et al. "Bert: Pre-training of deep bidirectional transformers for language understanding." Proceedings of the 2019 conference of the North American chapter of the association for computational linguistics: human language technologies, volume 1 (long and short papers). 2019.
