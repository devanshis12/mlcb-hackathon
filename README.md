# MLCB Hackathon Group 19
Develop an accurate computational method to predict the functional impact of protein mutations using machine learning. 

## Input
train.csv: mutants with associated DMS fitness score
test.csv: mutants
sequence.fasta: protein sequence, list of amino acids

## Output
predictions.csv: test mutants with associated predicted DMS fitness score
top10.txt: mutants with top 10 predicted DMS fitness score

## Queries
Run the query.ipynb file to get first and second query mutants.

## Usage
### 1. Retrieve and Preprocess Data
Run all cells in this section to do the following: Process the seqeuence.fasta file to get all mutated sequences and add them to the loaded training and testing data files. Loaded queried mutants and add them into the training data.
### 2. ESM Model
Create mutant embeddings to add features to help train the model.
#### 2.1 Mutant Embeddings
Run all cells in this section to use the pretrained ESM2 model to get mutant embeddings for the training data.
#### 2.2 One Hot Encoding
Run all cells in this section to get one hot encodings for mutants to add to the training data.
#### 2.3 Blosum Score
Skip this section. This section was intended to compute the Blosum score for mutants to add as features to the training data. Did not include this in the final model because there was an issue with the library.
#### 2.4 Physiochemical Properties
Run all cells in the section to get the physiochemical properties associated with the wildtype and mutant amino acids and add them to the training data. All the property values were extracted from various online sources.
#### 2.5 Train Val Split on Positions
Skip this section. This section is used from training and evaluation purposes. This part of the code creates training and validation datasets with embeddings with only one mutant per position to mimic the testing data.
### 3. Model Evaluation
Load the X data from the embeddings features and the y data from the DMS fitness scores. These dataframes will be used to train and validate the results of the following models
#### 3.1 Random Forest Regressor
This section will run GridSearch CV on a random forest regressor, run the model on the best parameters and return the evaluation metrics.
#### 3.2 XGBoost Regressor
This section will run a XGBoost model, GridSearch CV, and a XGBoost model with regularization with best parameters. There is also a subsection that runs the regularized, fine-tuned XGBoost model on the train/validation data with unique positions for evalulation purposes.
#### 3.3 Ensemble Model
Run all cells in this section to run a stacked model with a random forest regressor, linear regressor, and XGBoost regressor with fine-tuned parameters. This is the final model used for predictions
#### 3.4 Convolution Neural Network
This section will run a CNN model and make predictions on the testing set. Since CNN is best for local patterns, this model was not used for the final model.
### 4. Queries
Use the test predictions from the choosen model to inform the mutants for the final query. 
#### 4.1 UCB
Run all cells in this section to use the upper confidence bound method to select the final 100 mutants to query. This is the method used for the final query to inform our model.
#### 4.2 Thompson Sampling
This section will run the Thompson Sampling method, which uses a sample function from a posterior distribution of the objective function and selects the point that maximizes this sample.
#### 4.3 Expected Improvement
This section will run the Expected Improvement method, which will select the next points that is expected to output the best observed outcome so far.
#### 4.4 Uncertainty-Based Selection
This section will run the Uncertainty-Based Selection method, which uses uncertainty to prioritize combinatorial mutants.
### 5. Final Model Predictions
Run all cells in this section to get the embeddings for the test set and get the final predictions using the choosen model (ensemble model) and the mutants with the top 10 predicted DMS fitness score.
### 6. Visualizations
Run all cells in this section to get visualizations for the ensemble model and the XGBoost model.

