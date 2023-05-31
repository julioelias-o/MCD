Redes neuronales

Introduccion 
¿Qué es una red neuronal?
Una red neuronal es un modelo computacional inspirado en el funcionamiento del cerebro humano. Está compuesta por un conjunto interconectado de nodos llamados *neuronas artificiales*. Estas neuronas artificiales se organizan en capas, donde cada capa se conecta con la siguiente mediante conexiones llamadas *pesos*. Su entrenamiento permite realizar una amplia gama de tareas, como reconocimiento de patrones, clasificación de datos o predicciones.

![esquemared](https://github.com/julioelias-o/MCD/assets/134743799/00c7b737-889d-4ff2-9539-4fcb23c6b7cb)

La red neuronal procesa información de entrada a través de estas conexiones y realiza cálculos para producir una salida. Cada neurona en una capa toma como entrada los valores de salida de las neuronas de la capa anterior, realiza una operación matemática y produce un valor de salida. La operación matemática que realiza una neurona es multiplicar cada valor de entrada por un peso asociado y luego sumarlos. Posteriormente, se aplica una función de activación a la suma ponderada para introducir no linealidad en la red.

La función de activación puede variar, pero ejemplos comunes son la función sigmoide (que produce valores entre 0 y 1), la función ReLU (que devuelve 0 para valores negativos y el valor original para valores positivos), o la función tangente hiperbólica (que produce valores entre -1 y 1).

La información fluye hacia adelante en la red neuronal, desde la capa de entrada a través de las capas ocultas hasta la capa de salida. Durante el entrenamiento de la red neuronal, los pesos de las conexiones se ajustan iterativamente utilizando algoritmos de aprendizaje como el descenso de gradiente y la retropropagación del error. Esto permite que la red aprenda a realizar tareas específicas y a mejorar su precisión con el tiempo.

Aplicaciones

En el ambito de la química, algunos ejemplos de la aplicación de las redes neuronales pueden ser:
Diseño de fármacos
Las redes neuronales se utilizan para acelerar el proceso de diseño de fármacos. Estas redes pueden predecir la actividad biológica de compuestos químicos y ayudar a identificar nuevos candidatos a fármacos. También pueden optimizar propiedades químicas, como la solubilidad o la estabilidad, para mejorar la eficacia y la seguridad de los medicamentos.

Predicción de propiedades químicas
Las redes neuronales pueden predecir diversas propiedades químicas de compuestos, como la solubilidad, la reactividad química o la toxicidad. Esto es útil en la selección de compuestos en etapas tempranas del desarrollo de fármacos o en el diseño de materiales químicos con propiedades específicas.

Análisis espectroscópico
Las redes neuronales se aplican en la interpretación de datos espectroscópicos, como espectros de resonancia magnética nuclear (RMN) o espectros infrarrojos (IR), para identificar y caracterizar compuestos químicos. Estas redes pueden acelerar el análisis y mejorar la precisión en la identificación de sustancias químicas complejas.
