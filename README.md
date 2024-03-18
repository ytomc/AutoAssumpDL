Replication Package of the Paper: An exploratory study on automatic identification of assumptions in the development of deep learning frameworks

# Organization of the files
1. `30k-clean.model`: The model file for sentence piece tokenization.  
2. `30k-clean.vocab`: The vocabulary file that the ALBERT model was trained on.  
3. `dataset.csv`: The AssuEval dataset.
4. `Assumption_Miner.pdf`: Introduction of the Assumption Miner tool.

# Experiment replication steps
# Phase 1: Data collection
1. Use Assumption Miner to collect the data of the TensorFlow and Keras repositories.
2. Check the correctness and completeness of the data collected.
# Phase 2: Dataset management
1. Create three labels, i.e., NA with a value 0, PA with a value 1, and SCA with a value 2, which represents non-assumptions, potential assumptions, and self-claimed assumptions, respectively.
2. Labele the data following the criteria using Assumption Miner. NAs are labeled as “0”, PAs are labeled as “1”, and SCAs are labeled as “2”.
3. Check the labeled data.
4. Export the labeled data using Assumption Miner.
5. Remove all duplicates of the labeled data. Note that duplicates in this study mean that sentences are exactly the same, not only the meaning of sentences, but also the words, symbols, and spaces used, which can increase the diversity of the data. For example, we considered “# 32 floats > compression factor 24.5, assuming the input is 784 floats” and “# 32 floats > compression of factor 24.5, assuming the input is 784 floats” as two different data, though they have the same meaning.
6. Select all manually identified SCAs from the TensorFlow and Keras repositories. Randomly select PAs and NAs with the same number of SCAs to construct the AssuEval dataset.
7. Review the selected data.
8. Create the final SCA, PA, and NA dataset file. In the dataset file, the label “0” represents NA, “1” represents PA, and “2” represents SCA.
# Phase 3: Training
1. Split the dataset into a training set (80%) and a testing set (20%).
2. Transform all the loaded data into the lower case.
3. Use the same vocabulary with a size of 30,000 as in ALBERT and SentencePiece to tokenize the data in the training set and the test set.
4. Used scikit-learn to implement and train the seven ML models based on the AssuEval dataset. 
5. Use the TensorFlow framework to train the ALBERT model based on the AssuEval dataset.
6. Use the pre-trained ChatGPT model without retraining or further fine-tuning to identify assumptions using the test set of the AssuEval dataset.
# Phase 4: Data analysis
1. Use confusion matrix, accuracy, precision, recall, and f1-score to measure the classification performance of different models.
