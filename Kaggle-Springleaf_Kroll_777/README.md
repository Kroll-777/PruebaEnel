# Prueba Kaggle-Springleaf
Kaggle competition: Springleaf Marketing Response 

Competencia de Kaggle: Marketingarketing de Springleaf por parte del equipo KarolCastillo

## Introduccion
Este repositorio contiene cuadernos de ipython preparados para la competencia Kaggle: Springleaf Marketing Response. Springleaf ofrece 
a sus clientes préstamos personales y para automóviles que los ayudan a tomar el control de sus vidas y sus finanzas. El correo directo 
es una forma importante en que el equipo de Springleaf puede conectarse con los clientes que pueden necesitar un préstamo.
Para mejorar su esfuerzo específico, a Springleaf le gustaría centrarse en los clientes que probablemente respondan 
y sean buenos candidatos para sus servicios.

Usando un gran conjunto de funciones  y Data anonimizada <em>anonimizadas</em>, Springleaf nos pide que predigamos qué clientes responderán a una 
oferta de correo directo. 

## Data
Contamos con un conjunto de datos  <em>anonymized</em> cse proporciona información del cliente. 
Cada entrada (fila) corresponde a un cliente. la variable de respuesta es binaria. 
Hay más de 140.000 entradas tanto en el conjunto de prueba como en el de entrenamiento.

## Guia Proyecto
### Procesamiento de la Data
  En la carpeta de preprocesamiento, los datos de características se procesaron de manera diferente en función de los diferentes tipos de datos.
  1. Los datos numéricos se preprocesaron en data_preprocessing_SL_Feb2022_train_test_th60.ipynb. 
     El procesamiento clave incluye imputación de valores perdidos, detección de valores atípicos, transformación logarítmica 
	 de columnas sesgadas a la derecha, estandarización de columnas numéricas, etc. Además de las columnas numéricas básicas, 
	 se derivaron 10 columnas numéricas. Las columnas categóricas con un número limitado de valores se transformaron 
	 utilizando DictVectorizer (codificación OneHot). Las columnas numéricas con muy pocos valores se separan de otras columnas numéricas, 
	 al igual que las columnas de series temporales.
	 
  2. Los datos de series temporales se procesaron en data_preprocessing_SL_Feb2022_time_series_normalization.ipynb
  3. Las columnas categóricas con demasiados valores, así como las columnas numéricas con muy pocos valores,
     se procesaron en data_preprocessing_SL_Feb2022_cat_num_normalization.ipynb
	 
  4. Todas las demás columnas categóricas se preprocesaron con la codificación OneHot en data_preprocessing_SL_Feb2022_th60_cat_label_encoding.ipynb

### Caracteristicas de la seleccion
Estas Caracteristicas de Seleccion estan en la carpeta  seleccion_característicascaracterísticas. Se escogieron multiples metodos, incluyendo RFECV, greedy forward selection, backward selection and the SelectKBest from sklearn.
Entrada de los Modelos:
  1. Modelo Lineal (Logistic, SVM, Passive aggressive): numerical variables
  2. A´rbol de Busqueda (xgBoost, random forest, scikit learn gradient boosting): numerical + veriables categoricas

### Optimizacion Modelos
Entrenamiento de Modelos gridsearchCV o el  home-built método que genera predicción en el conjunto de prueba durante la validación cruzada, la predicción se puede usar más adelante como metacaracterísticas. La búsqueda en cuadrícula se realizó con diferentes algoritmos, como xgboost, random forest, online svm y regresión logística.

### Prediccion Final
Las predicciones finales se realizan con modelos de nivel 0 y nivel 1 utilizando características básicas, características derivadas y metacaracterísticas, utilizando modelos que incluyen xgBoost, RandomForest, regresión logística SGD, máquinas de vectores de soporte SGD, clasificador pasivo-agresivo SDG.

### Modelos
La idea es selecccionar el Modelo más optimo
