# MLDS-2021-Stryker-Hackathon

![problem](https://user-images.githubusercontent.com/78955446/107764713-a9e67580-6d56-11eb-8889-600d8b4a4163.jpg)


## Detailed Description
This repository contains data and code for a problem solving session in MDLS 2021 on detection of rectangles from a set of noisy point data.

### Data
The data comprises of two csv files:
1. train_ground_truth.csv - 
This file contains 100 rows of four coordinates (x1,y1,x2,y2,x3,y3,x4,y4) of 100 rectangles in an anti-clockwise order starting from the coordinate that has lowest y value.
y1 has the lowest y value in every row. 
2. training_data.csv -
This file contains 200 rows with multiple x values in first row and y value in the next row for the 100 rectangles in the same order as the ground truth file.

The problem has been simplified to avoid singularities by not having axis aligned rectangles. So, you may not need to worry about division by zero while computing slopes.
The slopes of two lines should always be positive and the slopes of the other two lines should always be negative.

### Code
The code folder has a file - MLDS_2021_Stryker_Hackathon_Baseline_Code.ipynb

This code uses Gaussian Mixture Models to cluster the points into 4 clusters and Linear Regression on the 4 clusters to model the lines of the rectangles in the training_data.csv and produces a file output_train.csv. The code does not impose orthogonality constraint on the output rectangles and thus actually produces quadrilaterals. The code compares the point in the output_train.csv with the points in train_ground_truth.csv to measure the performance.

The performance is measured by finding the Root Mean Square Error, across 100x4 points each in output_train.csv and train_ground_truth.csv

The RMSE of the baseline algorithm implemented may vary due to the random nature of Gaussian Mixture Models.
The RMSE given by the baseline code has been observed to vary between 35.00 and 36.00. 

### Objective for the participants

Modify the GenerateLineModels(data,labels) function to meet the following objectives:
1. Improve the RMSE
2. Impose orthogonality constraint on the rectangles. 
   Currently, slopes of all the lines of the rectangle are different, making it actually a quadrilateral.
   Slopes of parallel lines should be the same and the perpendicular lines should be related (m1 x m2 = -1)
   
### Hints
Only objective 1

    1. Apply PCA to project the points in each of the clusters on the principle eigen vector before regression.
    
Both objective 1 and 2 

    2. Use the slopes from the linear regression on each of the clusters and find a single slope representing the whole data. The lines should pass through respective cluster centers.                
    3. Use the slopes from the PCA on each of the clusters and find a single slope representing the whole data. The lines should pass through respective cluster centers.
