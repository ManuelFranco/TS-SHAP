# TSG-SHAP: Interpretability for Time Series Models

## Overview
TSG-SHAP is a Shapley-based interpretability method specifically designed for **time series Machine Learning models**. Unlike traditional Shapley methods, TS-SHAP applies **a priori feature grouping strategies** to preserve temporal relationships and improve explanation quality.

This repository includes:
- The **TSG-SHAP library**, a plug-and-play Python module.
- Example Jupyter Notebook (`example.ipynb`) demonstrating the usage of TSG-SHAP on a real-world dataset.

---

## Features
1. **Model Agnostic**: TSG-SHAP can be applied to any time series Machine Learning model.
2. **Feature Grouping**:
   - **Temporal Grouping**: Grouping features by time instants.
   - **Feature Grouping**: Grouping measurements by features.
   - **Multi-Feature Grouping**: Custom groupings for logical units (e.g., industrial processes).
3. **Scalability**: Includes approximate methods to handle computational complexity.
4. **Visualization**: Offers custom plots to analyze contributions over time.

---

## Installation
To install the library, clone the repository and ensure dependencies are installed:

```bash
# Clone the repository
git clone <repo_url>
cd <repo_directory>

# Install dependencies
pip install -r requirements.txt
```

---

## Quick Start
The `example.ipynb` file provides a step-by-step guide on using TSG-SHAP. Below is a quick example:

### 1. Import TS-SHAP
```python
from tsg_shap import TSGSHAP
from tsg_shap.utils import StrategyGrouping, StrategyPrediction
```

### 2. Initialize the Model and Data
Assume `model` is a pre-trained time series model and `supportDataset` contains processed time series data.

```python
model = MyTrainedModel()
supportDataset = [...]  # List of dictionaries with 'given' key containing tensors

# Initialize TSG-SHAP
tsg_shap = TSGSHAP(
    model=model,
    supportDataset=supportDataset,
    strategyGrouping=StrategyGrouping.TIME,  # Options: TIME, FEATURE, MULTIFEATURE
    strategyPrediction=StrategyPrediction.MULTICLASS,
    m=5,  # Approximation parameter
    verbose=1,
    nclass=2,  # Number of classes
    classToExplain=1
)
```

### 3. Compute Shapley Values
Pass a test dataset to compute Shapley values:
```python
testDataset = [...]  # List of test samples
tsshap_values = tsg_shap.compute_tsgshap(testDataset)
```

### 4. Visualize Results
Use the visualization module to interpret the results:
```python
tsg_shap.visualize_tsgshap(
    shapley_values=tsgshap_values, 
    testDataset=testDataset,
    path='results/tsgshap_visualization.png'
)
```

---

## Code Structure
The repository is organized as follows:

```
.
├── tsg_shap
│   ├── __init__.py          # Module initialization
│   ├── tsg_shap.py          # TSGSHAP class implementation
│   └── utils.py             # Utility functions and strategy enums
├── example.ipynb            # Usage example notebook
├── requirements.txt         # Dependencies
└── README.md                # Documentation
```

---

## Supported Grouping Strategies
- **TIME**: Each group corresponds to a specific time instant within the time window.
- **FEATURE**: Each group represents the measurements of one feature across all time instants.
- **PROCESS**: Each group represents the measurements of multiple feature across all time instants (requires `customGroups`).

---

## Visualization
TS-SHAP provides intuitive visualizations to analyze feature contributions over time:
- Heatmaps: Represent contributions with **red** (positive influence) and **blue** (negative influence).
- Output Probability: Overlaid line showing model predictions.

---

## Example Dataset
The example notebook uses the [SWaT dataset](https://itrust.sutd.edu.sg/itrust-labs_datasets/) as a demonstration of TSG-SHAP applied to Anomaly Detection in an Industrial Control System.

---

## Citation
If you use TSG-SHAP in your research, please cite:

> Franco de la Peña, M., Perales Gómez, A.L., Fernández Maimó, L. *TSG-SHAP: A Shapley-Based Interpretability Method for Time Series Machine Learning Models Applied to Anomaly Detection*. Preprint.

---

## License
This project is licensed under the MIT License.

---

## Contact
For questions or support, contact the author:
- Manuel Franco de la Peña (manuel.francop@um.es)
