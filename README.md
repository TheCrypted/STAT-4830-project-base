# Optimizing Vehicle Routing with Graph-Based and Probabilistic Models

## Team Members
Vishva Gajaraj, Darren Mo, Aman Sharma

## High-Level Summary

This project tackles the challenge of optimizing vehicle routing by developing algorithms that minimize both travel time and energy consumption. We've created a comprehensive approach that provides more detailed insights than current routing applications by considering trip-specific features, geographic data, infrastructure elements, and traffic patterns.

Our key contributions include:
- A systematic pipeline for modeling travel behavior and energy usage
- Benchmark statistics comparing different routing models

## Repository Structure

```
├── src/                  # Source code for final models and algorithms
├── notebooks/            # Jupyter notebooks for analysis and demonstrations
├── docs/                 # Documentation files
├── dataset                 # dataset files
├── report.md             # Comprehensive project report with methodology and findings
├── requirements.txt      # Python dependencies
└── named_development_history/ # Archive of development process and iterations
```

The `named_development_history/` folder contains our journey through model exploration and development, preserved for reference purposes. However, the final, optimized code exists in the `src` directory.

## Setup Instructions

### Prerequisites
- Python 3.8 or higher
- Git

### Environment Setup
1. Clone the repository:
   ```
   git clone [repository-url]
   cd [repository-name]
   ```

2. Create and activate a virtual environment (recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

4. API Keys (if needed):
   - OpenStreetMap API is used but doesn't require authentication

5. Running Code
   - The Code works in isolation as long as the data is stored locally. (we have attached the data to a folder called dataset).


### Demo Notebook

We left out the data processing and model training and simply inputted a saved model.pth file that can be downloaded from within our repo (for the sake of computational resources for the reproducer). 

This notebook provides a step-by-step walkthrough of our approach of benchmarking our key successful models against the deterministic approaches of models like A* and Djikstra.

## [Interactive Demo] https://drive.google.com/file/d/1TLNbLeSUoYlhsLNXXKqOkOlkR76TOOoM/view?usp=sharing 
