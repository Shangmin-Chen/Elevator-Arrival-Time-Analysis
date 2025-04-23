# Assignment 1 - Elevator Arrival Time Analysis

## Overview
This project involves collecting and analyzing elevator arrival times on the ground floor of the Center for Data Science (CDS) to determine the optimal waiting location that minimizes the expected walking distance to the next arriving elevator. The dataset was collaboratively recorded by the class, with training data collected on September 16-17, 2024, and test data on September 18-19, 2024. The analysis includes data processing, visualization, hypothesis formulation, and evaluation of the proposed waiting location.

## Objectives
- Practice collecting, interacting, and visualizing data.
- Develop and test a hypothesis using training and test datasets to find the optimal elevator waiting location.

## Repository Structure
- **assignment1.ipynb**: Jupyter Notebook containing the full analysis, including data collection notes, code for processing, calculations, and results.
- **README.md**: This file, providing an overview and instructions for the project.
- **cds_elevators.jpg**: Diagram of the elevator layout with coordinates (in meters) used for distance calculations (embedded in the notebook).

## Prerequisites
To run the notebook, you need the following:
- Python 3.x
- Required libraries:
  - `pandas`
  - `numpy`
- Jupyter Notebook or JupyterLab
- Access to the Google Spreadsheet with elevator arrival data (requires BU email login).
- Google Form responses exported as a CSV file for test data analysis.

Install the required libraries using:
```bash
pip install pandas numpy
```

## Data Collection
- **Training Data**: Collected on September 16-17, 2024, from 10 AM to 5 PM, via a Google Form where students recorded elevator arrivals during assigned 5-minute slots.
- **Test Data**: Collected on September 18-19, 2024, following the same procedure.
- **Data Access**: Available in a Google Spreadsheet (linked in the notebook). Students must download the data as a CSV and filter out rows before September 18 for test data analysis.
- **Elevator Layout**: Six elevators with coordinates (in meters) as shown in the diagram:
  - Elevator 1: (1, 3)
  - Elevator 2: (3, 3)
  - Elevator 3: (5, 3)
  - Elevator 4: (5, 0)
  - Elevator 5: (3, 0)
  - Elevator 6: (1, 0)

## Analysis Steps
1. **Data Processing**:
   - Sorted timestamps and identified gaps (>5 minutes) in data collection to calculate total recorded time.
   - Computed the number of arrivals and average frequency (arrivals per second) for each elevator.
2. **Frequency Analysis**:
   - Created a table of average frequencies to assess elevator arrival patterns.
   - Noted elevators 3 and 4 had slightly higher frequencies.
3. **Probability Calculation**:
   - Calculated the probability of each elevator being the next to arrive based on frequencies.
   - Ensured probabilities summed to 1.
4. **Optimal Location**:
   - Determined the optimal waiting location as the weighted center of elevator coordinates, weighted by arrival frequencies or probabilities.
   - Result: (3.0489, 1.4893), close to the naive guess of (3, 1.5).
5. **Distance Calculation**:
   - Implemented `get_average_walk_distance` function to compute the average Euclidean distance from a waiting location to the arriving elevator.
   - Compared distances for the naive location (3, 1.5) and optimal location (3.0489, 1.4893) on training and test data.
6. **Evaluation**:
   - The optimal location slightly reduced the average walking distance compared to the naive location, confirming a successful hypothesis.

## Results
- **Frequency Table** (Training Data):
  | Elevator ID | Total Time (s) | Arrivals | Avg Frequency (arrivals/s) |
  |------------|----------------|----------|----------------------------|
  | 1          | 24260          | 155      | 0.006389                   |
  | 2          | 24260          | 162      | 0.006678                   |
  | 3          | 24260          | 170      | 0.007007                   |
  | 4          | 24260          | 168      | 0.006925                   |
  | 5          | 24260          | 167      | 0.006884                   |
  | 6          | 24260          | 159      | 0.006554                   |

- **Probability Table** (Training Data):
  | Elevator ID | Probability |
  |------------|-------------|
  | 1          | 0.1580      |
  | 2          | 0.1651      |
  | 3          | 0.1733      |
  | 4          | 0.1713      |
  | 5          | 0.1702      |
  | 6          | 0.1621      |

- **Average Walking=inverted pyramid**
  | Avg Distance Walked (m) | Training Data | Test Data |
  |-------------------------|---------------|-----------|
  | (3, 1.5)                | 2.1646        | 2.1638    |
  | (3.0489, 1.4893)        | 2.1640        | 2.1635    |

- **Conclusion**: The optimal location (3.0489, 1.4893) slightly outperforms the naive location (3, 1.5), with marginally shorter average walking distances on both training and test data. The near-uniform arrival frequencies across elevators explain the small improvement.

## Usage
1. Clone or download this repository.
2. Open `assignment1.ipynb` in Jupyter Notebook or JupyterLab.
3. Download the elevator arrival data from the Google Spreadsheet as a CSV file.
4. For test data analysis, filter out rows before September 18, 2024, and upload the CSV to your environment (e.g., Google Colab's file panel).
5. Run the notebook cells sequentially to reproduce the analysis.
6. Ensure the `train_df` and `test_df` variables reference your CSV data.

## Notes
- The notebook assumes access to `train_df` and `test_df` as pandas DataFrames. You may need to load your CSV files using `pd.read_csv()`.
- The `get_average_walk_distance` function uses Euclidean distance for simplicity, assuming unobstructed paths to elevators.
- The analysis accounts for data collection gaps by subtracting periods with no observations (>5 minutes) from the total time.

## License
This project is for educational purposes and does not include a specific license. Please use it in accordance with academic integrity policies.

## Acknowledgments
- Thanks to the class (CS506) for collectively gathering the elevator arrival dataset.
- The Center for Data Science (CDS) for providing the environment for data collection.