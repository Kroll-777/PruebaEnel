# Prueba Kaggle-Springleaf
Kaggle competition: Springleaf Marketing Response by team CCTO

Competencia de Kaggle: Marketingarketing de Springleaf por parte del equipo KarolCastillo

## Introduccion
Este repositorio contiene cuadernos de ipython preparados para la competencia Kaggle: Springleaf Marketing Response. Springleaf ofrece a sus clientes préstamos personales y para automóviles que los ayudan a tomar el control de sus vidas y sus finanzas. El correo directo es una forma importante en que el equipo de Springleaf puede conectarse con los clientes que pueden necesitar un préstamo. Para mejorar su esfuerzo específico, a Springleaf le gustaría centrarse en los clientes que probablemente respondan y sean buenos candidatos para sus servicios.

Usando un gran conjunto de funciones  y Data anonimizada <em>anonimizadas</em>, Springleaf nos pide que predigamos qué clientes responderán a una oferta de correo directo. 

## Data
Contamos con un conjunto de datos  <em>anonymized</em> cse proporciona información del cliente. Cada entrada (fila) corresponde a un cliente. la variable de respuesta es binaria. Hay más de 140.000 entradas tanto en el conjunto de prueba como en el de entrenamiento.

## Guia Proyecto
### Procesamiento de la Data
In the preprocessing folder, feature data were processed differently based on different data types. 
  1. Numerical data was preprocessed in data_preprocessing_SL_Oct20_train_test_th60.ipynb. Key processing include missing value imputation, outlier detection, log-transform of right-skewed columns, standardization of numerical columns, etc. Besides basic numerical columns, 10 numerical columns were derived. Categorical columns with limited number of values were transformed using DictVectorizer (OneHot encoding). Numerical columns with too few values are separated from other numerical columns, so as the time series columns.
  2. Time series data were processed in data_preprocessing_SL_oct20_time_series_normalization.ipynb
  3. Categorical columns with too many values as well as numerical columns with too few values were processed in data_preprocessing_SL_oct20_cat_num_normalization.ipynb
  4. All other categorical columns were preprocessed using OneHot encoding in data_preprocessing_SL_oct20_th60_cat_label_encoding.ipynb
  
  En la carpeta de preprocesamiento, los datos de características se procesaron de manera diferente en función de los diferentes tipos de datos.
  1. Los datos numéricos se preprocesaron en data_preprocessing_SL_Oct20_train_test_th60.ipynb. El procesamiento clave incluye imputación de valores perdidos, detección de valores atípicos, transformación logarítmica de columnas sesgadas a la derecha, estandarización de columnas numéricas, etc. Además de las columnas numéricas básicas, se derivaron 10 columnas numéricas. Las columnas categóricas con un número limitado de valores se transformaron utilizando DictVectorizer (codificación OneHot). Las columnas numéricas con muy pocos valores se separan de otras columnas numéricas, al igual que las columnas de series temporales.
  2. Los datos de series temporales se procesaron en data_preprocessing_SL_oct20_time_series_normalization.ipynb
  3. Las columnas categóricas con demasiados valores, así como las columnas numéricas con muy pocos valores, se procesaron en data_preprocessing_SL_oct20_cat_num_normalization.ipynb
  4. Todas las demás columnas categóricas se preprocesaron con la codificación OneHot en data_preprocessing_SL_oct20_th60_cat_label_encoding.ipynb

### Feature selection
Feature selection were done with notebooks in the feature_selection folder. Multiple methods were used to do feature selection, including RFECV, greedy forward selection, backward selection and the SelectKBest from sklearn.
Model inputs for different models:
  1. linear models (Logistic, SVM, Passive aggressive): numerical variables
  2. tree-based models (xgBoost, random forest, scikit learn gradient boosting): numerical + catigorical variables

### Grid search and model optimization
Grid search for hyperparameter tuning was done using either sklearn gridsearchCV or the home-built method that generates prediction on the test set during cross-validation, the prediction can be used later as meta-features. Grid search were done with different algorithms such as xgboost, random forest, online svm and logistic regression.

### Final prediction
Final predictions are made with both level-0 and level-1 models using both basic features, derived features, and meta-features, using models including xgBoost, RandomForest, SGD-logistic regression, SGD support vector machines, SDG passive agressive classfier.

### Model ensembling
Model ensembling using greedy bagging method: http://www.cs.cornell.edu/~caruana/ctp/ct.papers/caruana.icml04.icdm06long.pdf

The idea is to select the models from a library of models to achieve the highest cross-validation score (AUC in this case).
The models are selected using a forward greedy approach with replacement, i.e., at each step a new model is added to the existing model bag to optimize the score. At the end of the selection, the weight of each model is given by the number of times it appears in the bag, and is used to perform the final ensembling on the test predictions.

