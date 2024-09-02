# Market Penetration Optimization

## Problem Statement

We are preparing to market a new product and have already conducted initial tests with 10% of our fidelity clients to determine their likelihood of purchase. Our goal now is to identify which of the remaining 90% of clients should receive a product sample. This will help us maximize our profit while achieving effective market penetration.

### Financial Overview

- **Revenue per Sale**: $15
- **Cost per Sample**: $4.46

### Objective

Our objective is to:
- **Maximize Profit**: Increase overall profit by targeting the most promising clients for sampling.
- **Achieve Market Penetration**: Effectively reach potential buyers to expand market reach.

### Available Data

We have detailed information about our customers, which includes:

- **Demographic Information**: Attributes such as affluence grade, age, neighborhood group, gender, geographic region, and TV region.
- **Loyalty Program Details**: Information on loyalty status (e.g., Tin, Silver, Gold, Platinum), total amount spent, and duration as a loyalty card member.

### Approach

1. **Analyze Initial Test Data**: Review the results from the initial 10% sample to understand which clients purchased the product.
2. **Predict Likelihood for Remaining Clients**: Use the information from the initial test to build a predictive model estimating the likelihood of purchase for the remaining 90% of clients.
3. **Optimize Sampling Strategy**: Apply optimization techniques to select the most promising customers for sampling to balance costs and potential revenue.
4. **Test and Refine**: Implement the sampling strategy on a small scale to validate its effectiveness before broader application.

## Test Data Analysis

1. **Data Cleaning**: 
   - Imputed missing values using the mode where necessary.
   - Transformed categorical variables to numerical formats to facilitate machine learning.

2. **Feature Selection and Preparation**: 
   - Checked for collinearity among features to ensure model stability.

3. **Model Training and Evaluation**: 
   - Divided the dataset into training and test sets.
   - Fitted various models on the training set and evaluated their performance on the test set. The models tested include:
     - Logistic Regression
     - Ridge
     - Decision Tree
     - Random Forest
     - Support Vector Machine (SVM)
     - Linear Discriminant Analysis (LDA)
     - Quadratic Discriminant Analysis (QDA)
     - K-Nearest Neighbors (KNN)
     - Generalized Additive Model (GAM)
     - Neural Network

4. **Performance Metrics**: 
   - Assessed models based on total error, accuracy, false negatives (FN), false positives (FP), sensitivity, specificity, false discovery rate (FDR), precision, and F1 score.

### Model Performance

| Method              | Accuracy | Total Error | FN   | FP  | Sensitivity | Specificity | FDR      | Precision | F1 Score |
|---------------------|----------|-------------|------|-----|-------------|-------------|----------|-----------|----------|
| Logistic Regression | 0.804049 | 0.195951    | 691  | 180 | 0.359       | 0.947       | 0.317    | 0.683     | 0.471    |
| Ridge               | 0.806749 | 0.193251    | 755  | 104 | 0.300       | 0.969       | 0.244    | 0.756     | 0.429    |
| Decision Tree       | 0.714286 | 0.285714    | 602  | 668 | 0.442       | 0.802       | 0.584    | 0.416     | 0.428    |
| Random Forest       | 0.792576 | 0.207424    | 645  | 277 | 0.402       | 0.918       | 0.390    | 0.610     | 0.484    |
| SVM                 | 0.803825 | 0.196175    | 752  | 120 | 0.302       | 0.964       | 0.269    | 0.731     | 0.428    |
| LDA                 | 0.805174 | 0.194826    | 691  | 175 | 0.359       | 0.948       | 0.311    | 0.689     | 0.472    |
| QDA                 | 0.804049 | 0.195951    | 548  | 323 | 0.492       | 0.904       | 0.379    | 0.621     | 0.549    |
| KNN                 | 0.779978 | 0.220022    | 678  | 300 | 0.371       | 0.911       | 0.429    | 0.571     | 0.450    |
| GAM                 | 0.815073 | 0.184927    | 613  | 209 | 0.431       | 0.938       | 0.310    | 0.690     | 0.531    |
| Neural Network      | 0.802475 | 0.197525    | 670  | 208 | 0.378       | 0.938       | 0.338    | 0.662     | 0.482    |

### Model Selection

Based on the performance metrics, the following observations were made:

- **GAM (Generalized Additive Model)** appears to be the best model overall. It offers a good balance between sensitivity, precision, and F1 score, making it effective for identifying customers who are likely to be interested in our new product.
- **QDA (Quadratic Discriminant Analysis)** is also a strong contender with high sensitivity and F1 score, which makes it valuable for identifying potential customers without missing too many.
- **Neural Network** is a robust model but might require more tuning and computational resources compared to GAM or QDA.

**Choice**: We have selected GAM for implementation as it generally provides better interpretability. GAMs offer a more transparent view of how features contribute to the model, which is valuable for understanding and explaining the model's predictions.

## Client Segmentation and Profit Analysis

We divided clients into deciles based on their probability of purchasing. For each decile, the following table summarizes the total number of clients, probability threshold, count of good and bad outcomes, cumulative counts, and the associated profit:

| Decile | Total | Prob Threshold | Good | Bad | Cumm Good | Cumm Bad | % Cumm Good | % Cumm Bad | % Cumm Bad Avoided | Profit |
|--------|-------|----------------|------|-----|-----------|----------|-------------|------------|---------------------|--------|
| 1      | 455   | 0.5979         | 337  | 118 | 337       | 118      | 0.1395      | 0.0350     | 0.965               | 3043.9 |
| 2      | 455   | 0.4045         | 231  | 224 | 568       | 342      | 0.2351      | 0.1016     | 0.898               | 1453.9 |
| 3      | 455   | 0.2737         | 141  | 314 | 799       | 656      | 0.3307      | 0.1948     | 0.805               | 103.9  |
| 4      | 455   | 0.2074         | 107  | 348 | 1030      | 1004     | 0.4263      | 0.2982     | 0.702               | -406.1 |
| 5      | 455   | 0.1654         | 87   | 368 | 1261      | 1372     | 0.5219      | 0.4075     | 0.593               | -706.1 |
| 6      | 455   | 0.1321         | 60   | 395 | 1492      | 1767     | 0.6175      | 0.5248     | 0.475               | -1111.1|
| 7      | 455   | 0.1006         | 51   | 404 | 1723      | 2171     | 0.7132      | 0.6448     | 0.355               | -1246.1|
| 8      | 455   | 0.0749         | 29   | 426 | 1954      | 2597     | 0.8088      | 0.7713     | 0.229               | -1576.1|
| 9      | 455   | 0.0418         | 25   | 430 | 2185      | 3027     | 0.9044      | 0.8990     | 0.101               | -1636.1|
| 10     | 350   | 0.0037         | 10   | 340 | 2416      | 3367     | 1.0000      | 1.0000     | 0.000               | -1397  |

### Marketing Strategy

To maximize profit, the product should be marketed to clients in deciles with a probability threshold higher than the second decile's threshold. For maximizing market penetration, including the third decile can be beneficial.

I then refitted the model using 90% of the remaining clients and propose marketing to those with a probability threshold higher than that of the third decile.

## Conclusion

By segmenting clients into deciles based on their probability of purchasing, we were able to gain valuable insights into the profitability of targeting different customer segments. The analysis revealed that targeting clients in the higher deciles yields the greatest profit, while lower deciles tend to result in diminishing returns or even losses.

To optimize marketing efforts, focusing on clients with a probability threshold higher than the second decile ensures the highest profitability. For broader market penetration, including clients from the third decile can be advantageous. This targeted approach balances profitability with market reach, maximizing the overall impact of marketing strategies.

Additionally, by refining our model with 90% of the remaining clients and focusing on those with a threshold higher than the third decile, we aim to further enhance our marketing effectiveness. This strategy will enable us to allocate resources more efficiently, improve decision-making, and ultimately drive better business outcomes.

The insights and strategies derived from this analysis provide a solid foundation for optimizing marketing efforts and achieving strategic goals.
