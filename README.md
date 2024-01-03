# Analisis y modelamiento de Scoring de clientes de Banco

## 1. Audiencia

Participantes de BootCamp "Data Science" del ProfeAlejo

## 2. Descripcion general

Este repositorio contiene el análisis de un dataset relacionado con el scoring de los clientes del banco XXX para evaluación del riesgo crediticio.   El objetivo es desarrollar y entrenar modelos de machine learning para predecir la solvencia de los clientes.

## 3. Dataset

### Descripción

The dataset contiene información de historial crediticio y caracteristicas de los clientes con la cual se pretende realizar la predicción de si el cliente tiene solvencia o no para hacer crédito.  Incluye caracteristicas como edad, sexo, tiempo en empresa actual, tiempo de residencia, extranjero, tiene propiedad, ingresos, ahorros, monto del crédito, plazo de credito, deuda en otros bancos. 

La variable a predecir es denominada como DEFAULT la cual tiene como valores 0 y 1 que indican si el cliente es bueno o malo.

### Fuente de datos

El archivo de datos fue suministrado por el banco XXXXX.

## 4. Preprocesamiento de los datos

Se realiza preprocesamiento de datos, manejo de valores faltantes.  Se realiza conversión de variables categorías a enteros (int64) aplicando mapeo entre el diccionario de datos y el dataset.

## 5. Feature Engineering

Se realiza Feature Engineering para discretizar variables numéricas de tal forma que los valores estén clasificados en rangos lo cual facilita el entrenamiento de los modelos predictivos.

## 6. Exploración de los datos

En el dataset suministrado se encuentra que el 70% de las solicitudes son clasificados como "Cliente bueno" y el 30% como "Cliente malo"

![Alt text](/imagenes/propbuenosymalos.png)

### Distribuciones de variables plazo, monto y edad

![Alt text](/imagenes/distri_plazo.png)

![Alt text](/imagenes/distri_edad.png)

![Alt text](/imagenes/distri_monto.png)

### Proporción de buenos y malos por característica

Para determinar que variables afectan el indicador de si el cliente es BUENO o MALO se generan las siguientes gráficas que comparan el indicador con cada variable para el dataset suministrado:

![Alt text](/imagenes/tasamalos_acccheckst.png)

![Alt text](/imagenes/tasamalos_credit_hist.png)

![Alt text](/imagenes/tasamalos_extranjero.png)

![Alt text](/imagenes/tasamalos_otrasdeudas.png)

![Alt text](/imagenes/tasamalos_propiedad.png)

![Alt text](/imagenes/tasamalos_purpose.png)

![Alt text](/imagenes/tasamalos_savings.png)

![Alt text](/imagenes/tasamalos_tiempoempresa.png)

![Alt text](/imagenes/tasamalos_tiemporesidencia.png)

### Análisis de correlaciones

En las siguientes gráficas se puede observar relaciones entre las variables:

![Alt text](/imagenes/correlaciones1.png)

![Alt text](/imagenes/correlaciones2.png)


Con base en el análisis exploratorio en principio se podrian utilizar las siguientes variables del modelo:

- account_check_status
- credit_history
- purpose
- savings
- present_emp_since
- other_debtors*
- property*
- other_installments_plans*
- housing*
- credit_this_bank
- foreign_worker
- rango_edad*
- rango_plazo
- rango_valor_credito*

Durante la fase de entrenamiento se pueden encontrar variables que no segmentan la clasificación.

## 7. Model Training

### Ejecución de modelo base

Se ejecutaron varios algoritmos de clasificación como regresión logística (RL), arboles de decisión (DT), Random forest (RF) y regresión gausiana (NB) usando el dataset original para tener métricas bases con las se puedan comparar los posteriores ajustes a nivel de columnas e hiperparámetros.  Las métricas obtenidas fueron las siguientes:

![Alt text](/imagenes/metricas_modelobase.png)

<table id="T_df850">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th id="T_df850_level0_col0" class="col_heading level0 col0" >Precision</th>
      <th id="T_df850_level0_col1" class="col_heading level0 col1" >Recall</th>
      <th id="T_df850_level0_col2" class="col_heading level0 col2" >F1-score</th>
      <th id="T_df850_level0_col3" class="col_heading level0 col3" >Accuracy</th>
      <th id="T_df850_level0_col4" class="col_heading level0 col4" >ROC-AUC</th>
      <th id="T_df850_level0_col5" class="col_heading level0 col5" >KS</th>
      <th id="T_df850_level0_col6" class="col_heading level0 col6" >Gini</th>
    </tr>
    <tr>
      <th class="index_name level0" >Algoritmo</th>
      <th class="blank col0" >&nbsp;</th>
      <th class="blank col1" >&nbsp;</th>
      <th class="blank col2" >&nbsp;</th>
      <th class="blank col3" >&nbsp;</th>
      <th class="blank col4" >&nbsp;</th>
      <th class="blank col5" >&nbsp;</th>
      <th class="blank col6" >&nbsp;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_df850_level0_row0" class="row_heading level0 row0" >RL</th>
      <td id="T_df850_row0_col0" class="data row0 col0" >0.581395</td>
      <td id="T_df850_row0_col1" class="data row0 col1" >0.416667</td>
      <td id="T_df850_row0_col2" class="data row0 col2" >0.485437</td>
      <td id="T_df850_row0_col3" class="data row0 col3" >0.735000</td>
      <td id="T_df850_row0_col4" class="data row0 col4" >0.644048</td>
      <td id="T_df850_row0_col5" class="data row0 col5" >0.288095</td>
      <td id="T_df850_row0_col6" class="data row0 col6" >0.288095</td>
    </tr>
    <tr>
      <th id="T_df850_level0_row1" class="row_heading level0 row1" >DT</th>
      <td id="T_df850_row1_col0" class="data row1 col0" >0.492537</td>
      <td id="T_df850_row1_col1" class="data row1 col1" >0.550000</td>
      <td id="T_df850_row1_col2" class="data row1 col2" >0.519685</td>
      <td id="T_df850_row1_col3" class="data row1 col3" >0.695000</td>
      <td id="T_df850_row1_col4" class="data row1 col4" >0.653571</td>
      <td id="T_df850_row1_col5" class="data row1 col5" >0.307143</td>
      <td id="T_df850_row1_col6" class="data row1 col6" >0.307143</td>
    </tr>
    <tr>
      <th id="T_df850_level0_row2" class="row_heading level0 row2" >RF</th>
      <td id="T_df850_row2_col0" class="data row2 col0" >0.675000</td>
      <td id="T_df850_row2_col1" class="data row2 col1" >0.450000</td>
      <td id="T_df850_row2_col2" class="data row2 col2" >0.540000</td>
      <td id="T_df850_row2_col3" class="data row2 col3" >0.770000</td>
      <td id="T_df850_row2_col4" class="data row2 col4" >0.678571</td>
      <td id="T_df850_row2_col5" class="data row2 col5" >0.357143</td>
      <td id="T_df850_row2_col6" class="data row2 col6" >0.357143</td>
    </tr>
    <tr>
      <th id="T_df850_level0_row3" class="row_heading level0 row3" >NB</th>
      <td id="T_df850_row3_col0" class="data row3 col0" >0.500000</td>
      <td id="T_df850_row3_col1" class="data row3 col1" >0.616667</td>
      <td id="T_df850_row3_col2" class="data row3 col2" >0.552239</td>
      <td id="T_df850_row3_col3" class="data row3 col3" >0.700000</td>
      <td id="T_df850_row3_col4" class="data row3 col4" >0.676190</td>
      <td id="T_df850_row3_col5" class="data row3 col5" >0.352381</td>
      <td id="T_df850_row3_col6" class="data row3 col6" >0.352381</td>
    </tr>
  </tbody>
</table>

Aunque las resultados del Random Forest son ligeramente superiores al Naive Bayes, se observa que la diferencia no es muy grande; y teniendo en cuenta la complejidad de los modelos se decide tomar como modelo base el **Gausian Naive Bayes.**

### Selección de variables

Con base en el análisis exploratorio y técnicas como PCA y regresión LASSO se seleccionaron la siguientes variables para la creación del modelo.  Se obtenieron métricas entrenado el algoritmo GaussianNB para cada de una de las variables de forma individual para determinar cuales métricas por si solas tienen capacidad de predicción de la variable 
objetivo:

<table id="T_653c7">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th id="T_653c7_level0_col0" class="col_heading level0 col0" >accuracy</th>
      <th id="T_653c7_level0_col1" class="col_heading level0 col1" >precision</th>
      <th id="T_653c7_level0_col2" class="col_heading level0 col2" >recall</th>
      <th id="T_653c7_level0_col3" class="col_heading level0 col3" >f1_score</th>
      <th id="T_653c7_level0_col4" class="col_heading level0 col4" >roc_auc</th>
      <th id="T_653c7_level0_col5" class="col_heading level0 col5" >ks</th>
      <th id="T_653c7_level0_col6" class="col_heading level0 col6" >gini</th>
    </tr>
    <tr>
      <th class="index_name level0" >variable</th>
      <th class="blank col0" >&nbsp;</th>
      <th class="blank col1" >&nbsp;</th>
      <th class="blank col2" >&nbsp;</th>
      <th class="blank col3" >&nbsp;</th>
      <th class="blank col4" >&nbsp;</th>
      <th class="blank col5" >&nbsp;</th>
      <th class="blank col6" >&nbsp;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_653c7_level0_row0" class="row_heading level0 row0" >account_check_status</th>
      <td id="T_653c7_row0_col0" class="data row0 col0" >0.725000</td>
      <td id="T_653c7_row0_col1" class="data row0 col1" >0.545455</td>
      <td id="T_653c7_row0_col2" class="data row0 col2" >0.500000</td>
      <td id="T_653c7_row0_col3" class="data row0 col3" >0.521739</td>
      <td id="T_653c7_row0_col4" class="data row0 col4" >0.660714</td>
      <td id="T_653c7_row0_col5" class="data row0 col5" >0.321429</td>
      <td id="T_653c7_row0_col6" class="data row0 col6" >0.321429</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row1" class="row_heading level0 row1" >rango_plazo</th>
      <td id="T_653c7_row1_col0" class="data row1 col0" >0.730000</td>
      <td id="T_653c7_row1_col1" class="data row1 col1" >0.636364</td>
      <td id="T_653c7_row1_col2" class="data row1 col2" >0.233333</td>
      <td id="T_653c7_row1_col3" class="data row1 col3" >0.341463</td>
      <td id="T_653c7_row1_col4" class="data row1 col4" >0.588095</td>
      <td id="T_653c7_row1_col5" class="data row1 col5" >0.176190</td>
      <td id="T_653c7_row1_col6" class="data row1 col6" >0.176190</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row2" class="row_heading level0 row2" >credit_history</th>
      <td id="T_653c7_row2_col0" class="data row2 col0" >0.715000</td>
      <td id="T_653c7_row2_col1" class="data row2 col1" >0.666667</td>
      <td id="T_653c7_row2_col2" class="data row2 col2" >0.100000</td>
      <td id="T_653c7_row2_col3" class="data row2 col3" >0.173913</td>
      <td id="T_653c7_row2_col4" class="data row2 col4" >0.539286</td>
      <td id="T_653c7_row2_col5" class="data row2 col5" >0.078571</td>
      <td id="T_653c7_row2_col6" class="data row2 col6" >0.078571</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row3" class="row_heading level0 row3" >purpose</th>
      <td id="T_653c7_row3_col0" class="data row3 col0" >0.700000</td>
      <td id="T_653c7_row3_col1" class="data row3 col1" >0.000000</td>
      <td id="T_653c7_row3_col2" class="data row3 col2" >0.000000</td>
      <td id="T_653c7_row3_col3" class="data row3 col3" >0.000000</td>
      <td id="T_653c7_row3_col4" class="data row3 col4" >0.500000</td>
      <td id="T_653c7_row3_col5" class="data row3 col5" >0.000000</td>
      <td id="T_653c7_row3_col6" class="data row3 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row4" class="row_heading level0 row4" >savings</th>
      <td id="T_653c7_row4_col0" class="data row4 col0" >0.700000</td>
      <td id="T_653c7_row4_col1" class="data row4 col1" >0.000000</td>
      <td id="T_653c7_row4_col2" class="data row4 col2" >0.000000</td>
      <td id="T_653c7_row4_col3" class="data row4 col3" >0.000000</td>
      <td id="T_653c7_row4_col4" class="data row4 col4" >0.500000</td>
      <td id="T_653c7_row4_col5" class="data row4 col5" >0.000000</td>
      <td id="T_653c7_row4_col6" class="data row4 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row5" class="row_heading level0 row5" >present_emp_since</th>
      <td id="T_653c7_row5_col0" class="data row5 col0" >0.700000</td>
      <td id="T_653c7_row5_col1" class="data row5 col1" >0.000000</td>
      <td id="T_653c7_row5_col2" class="data row5 col2" >0.000000</td>
      <td id="T_653c7_row5_col3" class="data row5 col3" >0.000000</td>
      <td id="T_653c7_row5_col4" class="data row5 col4" >0.500000</td>
      <td id="T_653c7_row5_col5" class="data row5 col5" >0.000000</td>
      <td id="T_653c7_row5_col6" class="data row5 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row6" class="row_heading level0 row6" >installment_as_income_perc</th>
      <td id="T_653c7_row6_col0" class="data row6 col0" >0.700000</td>
      <td id="T_653c7_row6_col1" class="data row6 col1" >0.000000</td>
      <td id="T_653c7_row6_col2" class="data row6 col2" >0.000000</td>
      <td id="T_653c7_row6_col3" class="data row6 col3" >0.000000</td>
      <td id="T_653c7_row6_col4" class="data row6 col4" >0.500000</td>
      <td id="T_653c7_row6_col5" class="data row6 col5" >0.000000</td>
      <td id="T_653c7_row6_col6" class="data row6 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row7" class="row_heading level0 row7" >other_debtors</th>
      <td id="T_653c7_row7_col0" class="data row7 col0" >0.700000</td>
      <td id="T_653c7_row7_col1" class="data row7 col1" >0.000000</td>
      <td id="T_653c7_row7_col2" class="data row7 col2" >0.000000</td>
      <td id="T_653c7_row7_col3" class="data row7 col3" >0.000000</td>
      <td id="T_653c7_row7_col4" class="data row7 col4" >0.500000</td>
      <td id="T_653c7_row7_col5" class="data row7 col5" >0.000000</td>
      <td id="T_653c7_row7_col6" class="data row7 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row8" class="row_heading level0 row8" >present_res_since</th>
      <td id="T_653c7_row8_col0" class="data row8 col0" >0.700000</td>
      <td id="T_653c7_row8_col1" class="data row8 col1" >0.000000</td>
      <td id="T_653c7_row8_col2" class="data row8 col2" >0.000000</td>
      <td id="T_653c7_row8_col3" class="data row8 col3" >0.000000</td>
      <td id="T_653c7_row8_col4" class="data row8 col4" >0.500000</td>
      <td id="T_653c7_row8_col5" class="data row8 col5" >0.000000</td>
      <td id="T_653c7_row8_col6" class="data row8 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row9" class="row_heading level0 row9" >property</th>
      <td id="T_653c7_row9_col0" class="data row9 col0" >0.700000</td>
      <td id="T_653c7_row9_col1" class="data row9 col1" >0.000000</td>
      <td id="T_653c7_row9_col2" class="data row9 col2" >0.000000</td>
      <td id="T_653c7_row9_col3" class="data row9 col3" >0.000000</td>
      <td id="T_653c7_row9_col4" class="data row9 col4" >0.500000</td>
      <td id="T_653c7_row9_col5" class="data row9 col5" >0.000000</td>
      <td id="T_653c7_row9_col6" class="data row9 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row10" class="row_heading level0 row10" >housing</th>
      <td id="T_653c7_row10_col0" class="data row10 col0" >0.700000</td>
      <td id="T_653c7_row10_col1" class="data row10 col1" >0.000000</td>
      <td id="T_653c7_row10_col2" class="data row10 col2" >0.000000</td>
      <td id="T_653c7_row10_col3" class="data row10 col3" >0.000000</td>
      <td id="T_653c7_row10_col4" class="data row10 col4" >0.500000</td>
      <td id="T_653c7_row10_col5" class="data row10 col5" >0.000000</td>
      <td id="T_653c7_row10_col6" class="data row10 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row11" class="row_heading level0 row11" >credits_this_bank</th>
      <td id="T_653c7_row11_col0" class="data row11 col0" >0.700000</td>
      <td id="T_653c7_row11_col1" class="data row11 col1" >0.000000</td>
      <td id="T_653c7_row11_col2" class="data row11 col2" >0.000000</td>
      <td id="T_653c7_row11_col3" class="data row11 col3" >0.000000</td>
      <td id="T_653c7_row11_col4" class="data row11 col4" >0.500000</td>
      <td id="T_653c7_row11_col5" class="data row11 col5" >0.000000</td>
      <td id="T_653c7_row11_col6" class="data row11 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row12" class="row_heading level0 row12" >job</th>
      <td id="T_653c7_row12_col0" class="data row12 col0" >0.700000</td>
      <td id="T_653c7_row12_col1" class="data row12 col1" >0.000000</td>
      <td id="T_653c7_row12_col2" class="data row12 col2" >0.000000</td>
      <td id="T_653c7_row12_col3" class="data row12 col3" >0.000000</td>
      <td id="T_653c7_row12_col4" class="data row12 col4" >0.500000</td>
      <td id="T_653c7_row12_col5" class="data row12 col5" >0.000000</td>
      <td id="T_653c7_row12_col6" class="data row12 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row13" class="row_heading level0 row13" >people_under_maintenance</th>
      <td id="T_653c7_row13_col0" class="data row13 col0" >0.700000</td>
      <td id="T_653c7_row13_col1" class="data row13 col1" >0.000000</td>
      <td id="T_653c7_row13_col2" class="data row13 col2" >0.000000</td>
      <td id="T_653c7_row13_col3" class="data row13 col3" >0.000000</td>
      <td id="T_653c7_row13_col4" class="data row13 col4" >0.500000</td>
      <td id="T_653c7_row13_col5" class="data row13 col5" >0.000000</td>
      <td id="T_653c7_row13_col6" class="data row13 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row14" class="row_heading level0 row14" >telephone</th>
      <td id="T_653c7_row14_col0" class="data row14 col0" >0.700000</td>
      <td id="T_653c7_row14_col1" class="data row14 col1" >0.000000</td>
      <td id="T_653c7_row14_col2" class="data row14 col2" >0.000000</td>
      <td id="T_653c7_row14_col3" class="data row14 col3" >0.000000</td>
      <td id="T_653c7_row14_col4" class="data row14 col4" >0.500000</td>
      <td id="T_653c7_row14_col5" class="data row14 col5" >0.000000</td>
      <td id="T_653c7_row14_col6" class="data row14 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row15" class="row_heading level0 row15" >foreign_worker</th>
      <td id="T_653c7_row15_col0" class="data row15 col0" >0.700000</td>
      <td id="T_653c7_row15_col1" class="data row15 col1" >0.000000</td>
      <td id="T_653c7_row15_col2" class="data row15 col2" >0.000000</td>
      <td id="T_653c7_row15_col3" class="data row15 col3" >0.000000</td>
      <td id="T_653c7_row15_col4" class="data row15 col4" >0.500000</td>
      <td id="T_653c7_row15_col5" class="data row15 col5" >0.000000</td>
      <td id="T_653c7_row15_col6" class="data row15 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row16" class="row_heading level0 row16" >sexo</th>
      <td id="T_653c7_row16_col0" class="data row16 col0" >0.700000</td>
      <td id="T_653c7_row16_col1" class="data row16 col1" >0.000000</td>
      <td id="T_653c7_row16_col2" class="data row16 col2" >0.000000</td>
      <td id="T_653c7_row16_col3" class="data row16 col3" >0.000000</td>
      <td id="T_653c7_row16_col4" class="data row16 col4" >0.500000</td>
      <td id="T_653c7_row16_col5" class="data row16 col5" >0.000000</td>
      <td id="T_653c7_row16_col6" class="data row16 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row17" class="row_heading level0 row17" >estado_civil</th>
      <td id="T_653c7_row17_col0" class="data row17 col0" >0.700000</td>
      <td id="T_653c7_row17_col1" class="data row17 col1" >0.000000</td>
      <td id="T_653c7_row17_col2" class="data row17 col2" >0.000000</td>
      <td id="T_653c7_row17_col3" class="data row17 col3" >0.000000</td>
      <td id="T_653c7_row17_col4" class="data row17 col4" >0.500000</td>
      <td id="T_653c7_row17_col5" class="data row17 col5" >0.000000</td>
      <td id="T_653c7_row17_col6" class="data row17 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row18" class="row_heading level0 row18" >rango_edad</th>
      <td id="T_653c7_row18_col0" class="data row18 col0" >0.700000</td>
      <td id="T_653c7_row18_col1" class="data row18 col1" >0.000000</td>
      <td id="T_653c7_row18_col2" class="data row18 col2" >0.000000</td>
      <td id="T_653c7_row18_col3" class="data row18 col3" >0.000000</td>
      <td id="T_653c7_row18_col4" class="data row18 col4" >0.500000</td>
      <td id="T_653c7_row18_col5" class="data row18 col5" >0.000000</td>
      <td id="T_653c7_row18_col6" class="data row18 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row19" class="row_heading level0 row19" >rango_valor_credito</th>
      <td id="T_653c7_row19_col0" class="data row19 col0" >0.700000</td>
      <td id="T_653c7_row19_col1" class="data row19 col1" >0.000000</td>
      <td id="T_653c7_row19_col2" class="data row19 col2" >0.000000</td>
      <td id="T_653c7_row19_col3" class="data row19 col3" >0.000000</td>
      <td id="T_653c7_row19_col4" class="data row19 col4" >0.500000</td>
      <td id="T_653c7_row19_col5" class="data row19 col5" >0.000000</td>
      <td id="T_653c7_row19_col6" class="data row19 col6" >0.000000</td>
    </tr>
    <tr>
      <th id="T_653c7_level0_row20" class="row_heading level0 row20" >other_installment_plans</th>
      <td id="T_653c7_row20_col0" class="data row20 col0" >0.625000</td>
      <td id="T_653c7_row20_col1" class="data row20 col1" >0.222222</td>
      <td id="T_653c7_row20_col2" class="data row20 col2" >0.100000</td>
      <td id="T_653c7_row20_col3" class="data row20 col3" >0.137931</td>
      <td id="T_653c7_row20_col4" class="data row20 col4" >0.475000</td>
      <td id="T_653c7_row20_col5" class="data row20 col5" >0.050000</td>
      <td id="T_653c7_row20_col6" class="data row20 col6" >-0.050000</td>
    </tr>
  </tbody>
</table>


- account_check_status
- credit_history
- purpose
- savings
- present_emp_since
- other_debtors*
- property*
- other_installments_plans
- housing*
- credit_this_bank
- foreign_worker
- rango_edad*
- rango_plazo
- rango_valor_credito*

(*) La variable por si sola no muestra un potencial para segmentar el nivel de default. Sin embargo, por conocimiento de negocio se decide utilizarla para la creación del modelo

### Separación de datos de entrenamiento y datos de prueba

Se hace Split al dataset en sets de entrenamiento y pruebas para evaluar el performance de los modelos de machine learning.

### Entrenamiento de Modelos

Train the selected models on the training data and tune hyperparameters for better performance.

## 8. Evaluación de modelos

Evaluate the trained models using the testing dataset. Metrics such as accuracy, precision, recall, and ROC-AUC can be used to assess the model's performance.

## 9. Resultados

Present the results of the analysis, including model performance metrics, important features, and any insights gained from the analysis.

## 10. Conclusiones

Summarize the findings and conclusions drawn from the analysis. Discuss the practical implications and potential use of the trained models for credit scoring in a real-world scenario.

## 11. Dependencias

List the dependencies required to run the analysis, including programming languages, libraries, and versions.

## 12. Uso

Provide instructions on how to reproduce the analysis, train the models, and make predictions on new data.

## 13. Licencia

Specify the license under which this analysis is released.

---

Feel free to modify the content based on your specific dataset, analysis, and preferences.
