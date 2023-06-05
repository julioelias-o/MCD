# Optimización de la producción de polihidroxibutirato (PHB) por Azohydromonas lata mediante el uso de redes neuronales artificiales
## Introducción
La contaminación ambiental debido a la utilización a gran escala del poliéster sintético y su dependencia de los recursos petroleros, hace que sea necesario encontrar rutas alternativas en la producción de polimeros que sean respetuosas con el medio ambiente y renovables en la naturaleza. Teniendo esto en cuenta, la producción de biopolímeros microbianos puede ser una gran alternativa para satisfacer estas necesidades. Los polihidroxialcanoatos (PHA) son biomateriales que son acumulados intracelularmente por las células bacterianas en respuesta al desequilibrio de nutrientes y al estrés ambiental. El polihidroxibutirato (PHB) es uno de los PHA que se estudia y caracteriza más ampliamente.

Uno de los principales factores que impide la aplicación comercial de PHB es su alto costo de producción en comparación con los poliésteres sintéticos derivados de productos petroquímicos. Es por tanto, un paso importante diseñar un medio de producción adecuado con un bioproceso bien definido para obtener la máxima biomasa y altos rendimientos de los productos metabólicos deseados. Azohydromonas lata es la bacteria más estudiada, que utiliza eficientemente las fuentes de carbono simples y baratas, como glucosa, fructosa y sacarosa para acumular gran cantidad de PHB termoplástico.

Se han utilizado varios enfoques para la optimización del proceso de producción de PHB, el tradicional que es mediante la variación de las concentraciones de los sustratos en el medio, una a la vez, pero resulta en un proceso laborioso y lento. La optimización de las variables del medio para que se pueda desarrollar el bioproceso, tiene que ser considerado bajo el análisis estratégico para la producción de PHB rentable. Con este proyecto se pretende desarrollar un modelo de redes neurnoales para encontrar la concentración optima de dichas variables, que lleven a una producción de PHB lo más alta posible.

## Modelado de redes neuronales artificiales para la optimización de las variables del medio
Para la realización de este proyecto se utilizó una arquitectura feed foward, también conocida como multilayer perception (MLP), con el algoritmo de back propagation, para construir los modelos predictivos con concentraciones escaladas de tres variables medias como input, y las concentraciones de biomasa y PHB como output.

Todas las entradas y salidas se normalizan dentro de un rango uniforme de (0,1 a 0,9) para garantizar la uniformidad durante el proceso de entrenamiento. Las nuevas variables escaladas se calculan mediante la ecuación. Después del proceso de entrenamiento, el valor optimizado de la variable se vuelve a reescalar para obtener las unidades deseadas.

![image](https://github.com/julioelias-o/MCD/assets/134743799/e5675aad-f845-4508-8c01-ef7ee55a85b0)
![image](https://github.com/julioelias-o/MCD/assets/134743799/50adbd38-162d-4fa3-b7f9-6710aec5213a)
## Esquema general de la red neuronal
![Diagramas de flujo](https://github.com/julioelias-o/MCD/assets/134743799/64d5c8f7-6032-4e8b-bf3a-2bf0e6583a1a)

El número de neuronas en la capa de entrada corresponde a la concentración de Sucrosa, Urea y Solución TE, y en la capa de salida a la concentración de biomasa y concentración de THB. En esta aplicación, el numero de neuronas se determino variando el número de nodos de 1 a 6 en la capa oculta. Durante el proceso de entrenamiento, el error cuadrático medio (mean square error) entre el valor experimental y el valor estimado se calcula y se propaga a través de la red utilizando el algoritmo de back propagation. El algoritmo de retropropagación ajusta los pesos en cada capa sucesivamente para reducir el error. Este procedimiento se repite hasta que el error entre el valor experimental y sus correspondientes valores predichos satisface ciertos criterios de error.

## Descripción matematica
Los valores normalizados de los inputs son introducidos en la red en los perceptrones de entrada y luego son multiplicados por los pesos, posteriormente se realiza una suma de todas estas multiplicaciones juntas. Al numero resultante se le aplica una funcion de activacion no lineal, para introduccir la no linealidad a la red, y esto finalmente produce el output, en este modelo son dos outputs.

![image](https://github.com/julioelias-o/MCD/assets/134743799/4cd5fa1f-41a2-49d9-88be-9b78c9deddd1)

Esta ecuacion también puede ser vista con terminos de algrebra lineal, como vectores y puntos, donde todos los inputs pertenecen a un vector X y son multiplicados por otro vector, que seria W.

Una vez sumados y multiplicados, antes de que pasen a otra neurona se les aplica una funcion de activación, que existen varias, como por ejemplo, la funcion sigmoide. Esta funcion va de 0 a 1, y se puede introducir cualquier numero real.

![image](https://github.com/julioelias-o/MCD/assets/134743799/399d927b-9c1f-4110-83e6-cb08bb8dd1cd)

Como se comentaba previamente, el proposito de las funciones de activación, es para introducir la no linealidad a la red y tener así la capacidad de poder abordar problemas no lineales

![image](https://github.com/julioelias-o/MCD/assets/134743799/9d731344-2454-4ee5-8f86-ec24538c47af)

Para comenzar el entrenamiento de la red, se necesita una funcion de perdida, que va a considerar las predicciones generadas por la red, contra la predicción verdadera o el resultado esperado. Entonces, esta diferencia entre las predicciones dan una nocion de que tanta perdida tiene la red.

![image](https://github.com/julioelias-o/MCD/assets/134743799/3e042afa-bd90-4df7-bb5c-53b7e3273d12)

La idea central es que, a traves de un conjunto completo de datos, se minimicen los errores que la red pueda cometer. Para optimizar las perdidas de la red, se necesita encontrar un conjunto de pesos (w) que minimicen la funcion de perdida

![image](https://github.com/julioelias-o/MCD/assets/134743799/2a7e8dfb-c1e3-4c4e-8d6d-85ffb55eb6ab)

Siendo la funcion de perdida una funcion continua, es posible calcular las derivadas de los puntos en este espacio. Para saber como la perdida en la red esta cambiando, se puede calcular un gradiente con puntos en la red y saber en que direccionalidad se debe de seguir para llegar al valor minimo de la funcion. De esta forma, se repiten los calculos de gradiente con multiples valores de w (pesos) y se ajustan al propagarse por la red neuronal, una y otra vez hasta converger en un minimo. 

Una vez terminado este proceso de entrenamiento, que puede verse como el ajuste de estos pesos en la red neuronal, osea encontrar una combinación de pesos que lleven a la red a hacer predicciónes lo más cercanas a la realidad posible.

## Resultado en la optimización de la producción de PHB
En esta aplicación, se tomaron componentes del medio como parametros para los inputs, consto de 20 sets de valores iniciales. Una vez entrenado el modelo, se comparo con los valores experimentales demostrando muy buenas estimaciones de la concentración final de PHB y de biomasa. 

![res](https://github.com/julioelias-o/MCD/assets/134743799/fef303b5-f4aa-466d-9ad3-d05fd068d327)

