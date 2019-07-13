[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3334316.svg)](https://doi.org/10.5281/zenodo.3334316)

# RiboswitchClassification

[riboflow](https://test.pypi.org/project/riboflow/) is a python package for classifying putative riboswitch sequences into one of 32 classes with > 99% accuracy. It is based on a [tensorflow](https://www.tensorflow.org) deep learning model. ``riboflow`` has been tested using ``Python 3.5.2``. 
The pip package was derived from this source code. This source code of ``rnnApp.py`` and ``cnnApp.py`` can easily be altered to help achieve better accuracy when the riboswitch labels change or the number of classes increase / decrease when constructing the dataset, by changing the number of NN layers, hyperparameters.  

Datasets, Models, Utility Files
------------

1.original_datasets

    a. 32_riboswitches_fasta    --> Fasta   Format of the 32 riboswitches
    b. 32_riboswitches_new_csv  --> CSV     Format of the 32 riboswitches
    
2.processed_datasets

    a. final_32classes.csv                --> Original 32 riboswitches Dataset cleaned and Frequencies calculated
    b. final_32train.csv          --> 90% of each riboswitches label in the final_32classes.csv
    c. final_32test.csv           --> Remaining 10% of each riboswitches label in the final_32classes.csv
    
3.pickled_models

    Contains all the trained sklearn models (generated by baseModels.py) in pkl format
    
4.models

    Contains the rnn and cnn model's in h5 format 
    
5.preprocess.py

    Contains various utilities for train:test splitting of the dataset, loading the datasets and other preprocessing of the data. Could be used to generate -mer frequencies, final_train.csv, final_test.csv and used for data preprocessing by all the models (i.e, both base and deep learning models: baseModels.py, rnnApp.py and cnnApp.py) 
    
6.multiclassROC.py

    Used for the ROC analysis of all models (i.e, base and the deep learning models). 
    
7.dynamic.py [IMPORTANT]
    
    Could be used on riboswitch fasta files of any number of classes to generate the equivalent processed csv files having the sequence and k-mer (for now, mono and di-) frequencies (this file can be used by baseModels.py, rnnApp.py, cnnApp.py for training purposes) 
    
Base Models Constructed using Sklearn Library
------------

    > python3  baseModels.py
    
    1. Create's a Picked Model for each of the sklearn classifers stated below:
        AdaBoostClassifier(),
        GaussianNB(),
        KNeighborsClassifier(),
        DecisionTreeClassifier(),
        RandomForestClassifier(),
        MLPClassifier()
    2. Each model is used on the test set to obtain accuracy, generate a classication report and the ROC-AUC values for each 
       of the 32 classes. 
    3. The MLPClassifier() proved to be the best among the chosen sklearn classifiers and hence Neural Networks (CNN and RNN) 
       were explored further to acheive greater accuracy.
 
 RNN
------------

    > python3  rnnApp.py
    
    1. Create's a .h5 RNN Model
    2. The model is used on the test set to obtain accuracy, generate a classication report and the ROC-AUC values for each 
       of the 32 classes. 
    3. Provides an Accuracy of 99% on the test set.
    4. New layers and hyperparameter values can be added or changed when dealing with a dataset having different number of classes
    5. The train time is fairly long ( in the magnitude of hours - suitable for system with high specs )
    
CNN
------------

    > python3  cnnApp.py
    
    1. Create's a .h5 CNN Model
    2. The model is used on the test set to obtain accuracy, generate a classication report and the ROC-AUC values for each 
       of the 32 classes. 
    3. Provides an Accuracy of 97% on the test set.
    4. New layers and hyperparameter values can be added or changed when dealing with a dataset having different number of classes.
    5. The train time is fairly short ( < 1 min - suitable for low spec systems )
 
    
Authors
------------

    1. Keshav Aditya RP
    2. Ramit Bharanikumar
    3. Ashok Palaniappan

Additional information
-------------------------
For more information, please refer to our manuscript below.

Premkumar KAR, Bharanikumar R, Palaniappan A. (2019) Classifying riboswitches with >99% accuracy. Microorganisms (to be submitted)

Please cite us if you use our software - thanks! 

Licensed under MIT License.
-------------------------

