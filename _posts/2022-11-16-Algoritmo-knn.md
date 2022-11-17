---
title: Algoritmo KNN
author: jdiaz
date: 2022-11-16 14:10:00 +0800
categories: [Apuntes, Machine-learning]
tags: [python, aprendizaje-supervisado, algoritmo-flojo, machine-learning, codigo]
render_with_liquid: false
math: true
mermaid: true
---

#### **Entendiendo KNN**

Podemos entender KNN como el algoritmo K de vecinos mas cercanos. Esto significa que para evaluar la categoría de un valor consideramos las muestras más cercanas a esta. Es uno de los algoritmos de aprendizaje automaticos supervisados más sencillos de entender. Es especialmente considerado cuando se plantea un problema sencillo y con un conjunto de muestras pequeño. Se le conoce como un algoritmo flojo.

#### **1.- Distancia euclidea**

![Desktop View](/assets/img/knn/distanciaeuclidea.png)

Podemos calcular la distancia entre dos puntos a traves de la formula de la distancia euclidea que se representa como: 

$$ 
DistanciaEuclidea = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2} 
$$

#### **2.- Resumen de algoritmo KNN**

El presente algoritmo nos permite predecir a que grupo pertenece una muestra en base a su comportamiento comparandola con un grupo de muestra que se conoce su clasificación. Para esto se usa el siguiente proceso:

![Desktop View](/assets/img/knn/diagramaknn.png)

*Explicando esto de forma mas detallada*

**Paso 1: Calcular las distancias**

Para iniciar se carga los datos categorizados para poder establecer un punto de comparacion inicial.

![Desktop View](/assets/img/knn/vecinosk.png)

El grafico representa un modelo donde se consideran solo dos variables. Se establecen dos categorias a las que un dato desconocido puede pertenecer *rojo* y *azul*.

En este caso buscamos conocer a que grupo pertenece un nuevo dato no categorizado, para esto calculamos la distancia entre nuestro punto sin etiqueta y nuestros puntos categorizados para saber su relación.

**Paso 2: Seleccionar los k vecinos mas cercanos**

Una vez calculados las distancias, ordenaremos los puntos considerando con prioridad a su cercanía. Finalmente consideraremos los k numeros mas cercanos a nuestro desconocido punto de interes sin etiqueta.

![Desktop View](/assets/img/knn/vecinosk2.jpeg)

En la imagen superior consideramos los 3 puntos mas cercanos (K=3). De estos puntos dos perteneces a la categoria roja y uno a la categoria azul. El algoritmo identifica el punto nuevo como al grupo que tiene mayoria dentro de la muestra k por lo que el modelo determinara que corresponde al grupo rojo.

#### **3.- ¿Por que consideramos KNN como "Algoritmo flojo"?**

KNN no tiene periodo de entrenamiento. Para cada prediccion el algoritmo necesita pasar por el mismo proceso. No hay un proceso en que esta eleccion pueda ser optimizada. Cuando el conjunto de datos es mas grande, el proceso requerirá mas tiempo.

#### **4.- Ejemplo de implementacion de KNN paso a paso**

Acontinuacion se detalla un ejemplo de como se ejecuta una implementacion de KNN

*Importar modulos*

```python
#Importar modulos requeridos
import numpy as np
from scipy.stats import mode
```

*Crear una funcion para calcular distancias*

```python
#Distancia Ecleudiana
def euclidean(p1,p2):
    dist = np.sqrt(np.sum((p1-p2)**2))
    return dist
```

Esta funcion nos permitira calcular las distancias tal como se indica en la formula de Euclides.

Luego haremos una funcion que nos permita guardar las distancia entre cada punto de referencia y nuestro punto de interes y ordenarlos segun su distancia. Finalmente seleccionaremos el grupo que tiene mayoria de cercania.

```python
#Funcion para calcular KNN
def predict(x_train, y , x_input, k):
    op_labels = []
     
    #Loop para clasificar datos
    for item in x_input: 
         
        #Array para almacenar distancias
        point_dist = []
         
        
        for j in range(len(x_train)): 
            distances = euclidean(np.array(x_train[j,:]) , item) 
            #calcula Distancia
            point_dist.append(distances)
            
        point_dist = np.array(point_dist) 
        
        #Ordena array manteniendo k puntos prioritarios
        dist = np.argsort(point_dist)[:k] 
         
        labels = y[dist]
         
        #Voto mayoritario
        lab = mode(labels) 
        lab = lab.mode[0]
        op_labels.append(lab)
 
    return op_labels
```

Creamos una funcion *predict* para encontrar la prediccion para un grupo de muestras.

