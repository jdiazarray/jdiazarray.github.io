---
title: Apuntes de ML conceptos iniciales
type: page
description: Primera parte de conceptos de Machine Learning
topic: data-science
---

### Que es Machine Learning

Se puede entender como Machine Learning el como le "enseñamos" a nuestro computador a tomar decisiones. 
Una definicion en 1997 Tom Mitchell:

> Se dice que un programa informático aprende de la experiencia E con respecto a alguna tarea T y alguna medida de rendimiento P, si su rendimiento en T, medido por P, mejora con la experiencia E.

Su filtro de spam es un programa de aprendizaje automático que, a partir de ejemplos de correos spam (marcados por los usuarios) y ejemplos de correos normales (no spam, también llamados "ham"), puede aprender a marcar el spam. Los ejemplos que el sistema utiliza para aprender se denominan conjunto de entrenamiento. Cada ejemplo de entrenamiento se denomina instancia (o muestra) de entrenamiento. La parte de un sistema de aprendizaje automático que aprende y realiza predicciones se denomina modelo. Las redes neuronales y los bosques aleatorios son ejemplos de modelos.

En este caso, la tarea T es marcar el spam de los nuevos correos electrónicos, la experiencia E son los datos de entrenamiento y hay que definir la medida de rendimiento P; por ejemplo, se puede utilizar la proporción de correos electrónicos clasificados correctamente. Esta medida de rendimiento se denomina precisión y se utiliza a menudo en tareas de clasificación.

### Por que usar Machine Learning

Respuesta corta: queremos automatizar decisiones que no nos alcanzan solamente con if-else (o switch). 
Respuesta larga: Considere el caso de los correos, la filtracion de nuestros datos hacen que cada dia estemos en riesgos de que nos lleguen decenas o cientos de correos basura o no deseado. En teoria estos serian facil de identificar (por su peso, nombre del correo, estructura, etc.) sin embargo por la canitidad de correos que puede ser confiamos en que sea el algoritmo de nuestro correo quien realize este filtro. Imaginemos por ejemplo que los correos spam tienen en su asunto el texto "For You", podriamos considerar una regla que si el correo cumple con ciertas condiciones y tiene el texto "For You", probablemente sea spam. Pero si quien realiaza el correo no deseado identifica que esta siendo eliminado por esto pordria cambiar el texto por otro similar como "For U" o "4 U" o "F0R Y0U" texto que tambien podria agregar a nuestras reglas. Considerar tantas reglas (por distintos casos de asuntos, o remitente, o peso) puede ser algo tedioso y facil de establecer, es por esto que en vez de utilizar reglas, le enseñamos a nuestros software a identificar patrones situaciones mas alla de casos especificos, aca es donde vemos lo que es Machine Learning.
Otro ejemplo puede ser la identificacion de texto para pasarlo a audio, un software deberia ser capaz de identificar la diferencia entre dos sonidos diferentes y capaz de distinguir su contenido independiente del tono, acento y otras variables. 

Otros casos en que Machine learning puede ser util puede ser:

* Analisis de imagenes de productos en una linea de produccion para identificar anomalias.

* Detectar tumores en scan cerebrales, via analisis de imagen. 

* Clasificar automaticamente articulos de noticias.

* Identificar comentarios ofensivos en foros de discucion.

* Resumir textos.

* Crear chatbots que puedan responde de forma natural



### Tipos de sistemas de ML

Estos se pueden clasificar en diferentes criterios entre los que encontramos:

* Si son supervisados durante su entrenamiento (supervisado, no supervisados, semi supervisados, auto supervisados u otros).

* Si pueden aprender de forma incrementar sobre la marcha (online o batch).

* Si trabajan comparando nuevos datos o detectando patrones y entrenando modelos predictivo (aprendizaje basado en instancias o aprendizaje basado en modelos).

Estos criterios no son excluyentes y se pueden mezclar de diferentes maneras. Por ejemplo un filtro de spam puede usar un modelo de redes neuronales entrenado en redes neuronales se alimenta constantemente con ejemplos de spam y ham proveida por personas. Esto significa que es un sistema online, basado en modelos de aprendizaje supervisado. 

### Supervision en el entrenamiento

Sistemas de ML se pueden clasificar segun la cantidad y tipo de supervision que reciben durante su entrenamiento, los principales son: aprendizaje supervisado, aprendizaje no supervisado, aprendizaje auto supervizado, semi-supervizado y por refuerzo.

#### Aprendizaje supervizado

En este caso el set de entremiento del algoritmo se alimenta con la solucion deseada (que en este caso se le llama *label* o *categoria*).
Un ejemplo de esto es el mismo caso de los correos spam donde le decimos al algoritmo que correos son spam y cuales ham y el algoritmo pueda identificar patrones para los casos siguientes.

#### Aprendizaje no supervizado

En este caso el algoritmo recibe solo los datos sin categoria, por lo que debe ser el mismo sistema el encargado de encontrar la relacion entre los datos sin ayuda de nosotros.
Supongamos que un blog de noticias, recibe informacion via cookies de sus principales lectores, estos pueden ser de diferentes rangos etareos, gustos o habitos de consumos. Un algoritmo de aprendizaje no supervizado puede identificar diferentes grupos lo que le podria orientar a saber como establecer su estrategia de marketing o sus futuras publicaciones.

#### Aprendizaje semi-supervizado

Un caso mixto entre ambos casos anteriores. 
Considere las imagenes de Facebook. El algoritmo es capaz de identificar las caras cuales siguen un patron similar. Sin embargo, esas caras no tienen nombre hasta que se relacionan con los diferentes perfiles que uno puede tener agregado, entonces es uno cuando confirma quienes son.

#### Aprendizaje auto supervisado

Algoritmos que aprenden de datos no etiquetados sin la ayuda de un humano.
Un ejemplo es un modelo que aprende a representar imágenes de forma que imágenes similares se agrupen juntas en un espacio de representación. El modelo logra esto al intentar reconstruir una imagen original a partir de una versión alterada (por ejemplo, cortando una parte de la imagen o aplicando algún tipo de distorsión) sin recibir información explícita sobre la clase o categoría de la imagen. Al aprender a reconstruir imágenes similares, el modelo aprende a representarlas de manera efectiva en el espacio de representación. Estos modelos son comúnmente utilizados en tareas de clasificación de imágenes, detección de objetos y segmentación semántica.

#### Aprendizaje por refuerzo

EL sistema de aprendizaje, llamado *agente* puede observar el ambiente, seleccionar el curso de accion y tener una *recompensas* (o una penalidad si se determina que el curso no fue el correcto). EL agente debe aprender la estrategia para tener mas recompensas, llamada *politica*. Esta establecera cual sera la forma de actuar dependiendo de la situacion. Un sencillo ejemplo de esto puede ser un robot que aprende a jugar un videojuegos y los puntos se considera la recomensa. En cada iteracion o prueba de juego el robot optimizara su estrategia de juego para tener una mayor puntuacion.

### Batch Versus Online

El aprendizaje en batch implica entrenar el modelo con un conjunto de datos completo de una sola vez, es decir, el modelo procesa todos los datos de entrenamiento disponibles y luego actualiza sus parámetros. Esta técnica es adecuada cuando se dispone de grandes cantidades de datos y recursos de computación para procesarlos. Sin embargo, el entrenamiento en batch puede requerir mucho tiempo y memoria, especialmente cuando se manejan grandes conjuntos de datos.

Por otro lado, el aprendizaje en línea implica entrenar el modelo de manera incremental, es decir, actualizar el modelo con cada nuevo punto de datos a medida que llega. Esto permite una adaptación más rápida a los cambios en los datos y es útil en situaciones en las que el conjunto de datos cambia con el tiempo. Sin embargo, el aprendizaje en línea puede ser más susceptible al ruido en los datos y puede requerir una cuidadosa selección de hiperparámetros para garantizar el rendimiento óptimo.

En términos de rendimiento, el aprendizaje en línea es más rápido y consume menos memoria que el aprendizaje en batch. Sin embargo, el rendimiento puede verse afectado por la selección de la tasa de aprendizaje y otros hiperparámetros. En general, el aprendizaje en línea es útil en situaciones en las que los datos cambian con el tiempo, mientras que el aprendizaje en batch es más adecuado para conjuntos de datos grandes y estables.

### Aprendizaje basado en instancias Versus Basado en Modelo

El aprendizaje basado en instancias es una técnica en la que el modelo se entrena utilizando los ejemplos específicos de datos de entrenamiento en lugar de construir un modelo general. El enfoque se basa en la similitud entre los ejemplos de entrenamiento y los nuevos datos a los que se aplicará el modelo. El modelo recuerda todos los datos de entrenamiento y clasifica los nuevos ejemplos basándose en su similitud con los ejemplos de entrenamiento previos.

Por ejemplo, si se quiere predecir el precio de una casa, el modelo basado en instancias se basaría en ejemplos de ventas de casas similares en la misma zona o barrio, y luego utilizaría estas ventas anteriores como base para predecir el precio de la casa objetivo.

Por otro lado, el aprendizaje basado en modelo es una técnica en la que el modelo se entrena a través de la construcción de una representación generalizada de los datos de entrenamiento. En este enfoque, se construye un modelo matemático que generaliza los patrones en los datos de entrenamiento y utiliza esta representación general para hacer predicciones en nuevos datos.

Por ejemplo, en un modelo de regresión lineal para predecir el precio de una casa, se ajustaría una línea a los datos de entrenamiento que describa la relación entre las características de las casas y sus precios. Luego, se utilizaría esta relación lineal para hacer predicciones sobre el precio de una casa utilizando sus características.

El aprendizaje basado en instancias es útil en situaciones donde los datos de entrenamiento son muy específicos y los nuevos datos pueden ser muy diferentes a los datos de entrenamiento. Por otro lado, el aprendizaje basado en modelo es útil cuando se dispone de datos suficientes para construir un modelo generalizado que pueda hacer predicciones precisas en nuevos datos.