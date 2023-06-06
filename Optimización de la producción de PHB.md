# Optimización de la producción de polihidroxibutirato (PHB) por Azohydromonas lata mediante el uso de redes neuronales artificiales
## Introducción
La contaminación ambiental debido a la utilización a gran escala del poliéster sintético y su dependencia de los recursos petroleros, hace que sea necesario encontrar rutas alternativas en la producción de polimeros que sean respetuosas con el medio ambiente y renovables en la naturaleza. Teniendo esto en cuenta, la producción de biopolímeros microbianos puede ser una gran alternativa para satisfacer estas necesidades. Los polihidroxialcanoatos (PHA) son biomateriales que son acumulados intracelularmente por las células bacterianas en respuesta al desequilibrio de nutrientes y al estrés ambiental. El polihidroxibutirato (PHB) es uno de los PHA que se estudia y caracteriza más ampliamente.

Uno de los principales factores que impide la aplicación comercial de PHB es su alto costo de producción en comparación con los poliésteres sintéticos derivados de productos petroquímicos. Es por tanto, importante diseñar un medio de producción adecuado con un bioproceso bien definido para obtener la máxima biomasa y altos rendimientos de los productos metabólicos deseados. Azohydromonas lata es la bacteria más estudiada, que utiliza eficientemente las fuentes de carbono simples y baratas, como glucosa, fructosa y sacarosa para acumular gran cantidad de PHB termoplástico.

Se han utilizado varios enfoques para la optimización del proceso de producción de PHB, el tradicional que es mediante la variación de las concentraciones de los sustratos en el medio, una a la vez, pero resulta en un proceso laborioso y lento. La optimización de las variables del medio para que se pueda desarrollar el bioproceso, tiene que ser considerado bajo el análisis estratégico para una producción de PHB rentable. Con este proyecto se pretende desarrollar un modelo de redes neuronales para encontrar la concentración optima de dichas variables, que lleven a una producción de PHB lo más alta posible.

## Modelado de redes neuronales artificiales para la optimización de las variables del medio
Para la realización de este proyecto se utilizó una arquitectura feedfoward, conocida como multilayer perceptron (MLP), con el algoritmo de aprendizaje backpropagation, para construir los modelos predictivos con concentraciones de tres variables en el medio como input, y las concentraciones de biomasa y PHB como output.

Todas las entradas y salidas se normalizan para garantizar la uniformidad durante el proceso de entrenamiento. Después del proceso de entrenamiento, el valor optimizado de la variable se vuelve a reescalar para obtener las unidades deseadas.

![image](https://github.com/julioelias-o/MCD/assets/134743799/e5675aad-f845-4508-8c01-ef7ee55a85b0)
![image](https://github.com/julioelias-o/MCD/assets/134743799/50adbd38-162d-4fa3-b7f9-6710aec5213a)
## Esquema general de la red neuronal
![Diagramas de flujo](https://github.com/julioelias-o/MCD/assets/134743799/64d5c8f7-6032-4e8b-bf3a-2bf0e6583a1a)

El número de neuronas en la capa de entrada corresponde a los valores normalizados de la concentración de Sucrosa, Urea y Solución TE, y en la capa de salida a los de la concentración de biomasa y concentración de THB. El numero de neuronas se determinó variando el número de nodos de 1 a 6 en la capa oculta. Durante el proceso de entrenamiento, el error cuadrático medio (mean square error) entre el valor experimental y el valor estimado se calcula y se propaga a través de la red utilizando el algoritmo de backpropagation. El algoritmo de retropropagación ajusta los pesos en cada capa sucesivamente para reducir el error. Este procedimiento se repite hasta que el error entre el valor experimental y sus correspondientes valores predichos satisface ciertos criterios de error.

## Descripción matematica
Inicialmente, se introducen pesos y sesgos de manera aleatoria para cada conexión entre los perceptrones en las 3 capas de la red (capa de entrada, capa oculta y capa de salida).

![image](https://github.com/julioelias-o/MCD/assets/134743799/4cd5fa1f-41a2-49d9-88be-9b78c9deddd1)

Dado un conjunto de datos de entrada, se propagan los valores a través de la red neuronal para obtener valores de salida, esto es conocido como foward propagation. Después de la capa de entrada, los valores de entrada se multiplican por los pesos correspondientes y se suman los sesgos, luego ocurre una suma ponderada de todos los productos de la capa anterior y se le aplica una función de activación. Esto se repite hasta llegar a la capa de salida. Existen varias funciones de activación con propiades diferentes, una comúnmente utilizada es la función sigmoide, que se define como:

![image](https://github.com/julioelias-o/MCD/assets/134743799/399d927b-9c1f-4110-83e6-cb08bb8dd1cd)

Donde:

__f(x)__ es el valor de salida de la función sigmoide para un valor de entrada x

__e__ es la base del logaritmo natural

__x__ es el valor de entrada al que se aplica la función sigmoide.

El propósito de incluir una función de activación en la red es introducir no linealidad en el modelo y permitir que la red pueda aprender y modelar relaciones complejas en los datos. Si solo se utilizan operaciones lineales en una red neuronal, como la multiplicación de matrices y sumas ponderadas, la salida de cada capa sería simplemente una combinación lineal de las entradas, limitando al modelo en términos de capacidad de representación y aprendizaje de patrones no lineales, los cuales son, por lo general, los que ocurren en problemas reales. Esto se puede distinguir de manera representativa en la siguiente imagen:

![image](https://github.com/julioelias-o/MCD/assets/134743799/9d731344-2454-4ee5-8f86-ec24538c47af)

Posteriormente, se hace un calculo de la diferencia entre las salidas obtenidas por la red neuronal y las salidas reales o deseadas del conjunto de datos. Este calculo se conoce como función de pérdida, y una comúnmente utilizada es el error cuadrático medio (MSE, por sus siglas en inglés), que se calcula mediante la siguiente fórmula:

![image](https://github.com/julioelias-o/MCD/assets/134743799/6f289ce8-7d1b-4643-8698-9f1b895184b8)

Donde:

__MSE__ es el error cuadrático medio.

__n__ es el número de muestras en el conjunto de datos.

__y__ es la salida predicha por el modelo.

__&#x0233;__ es el valor deseado o verdadero correspondiente a cada muestra.

El siguiente paso es minimizar la función de perdida, esto es clave para ajustar los pesos de la red neuronal. Esto se logra mediante la retropropagación del error (Backpropagation). Para cada peso en la red neuronal, se calcula la derivada parcial del error con respecto a ese peso. Esto se realiza en sentido inverso, de la capa de salida a la capa de entrada, de ahí su nombre. Para cada neurona, se calcula el gradiente local, que es el producto de la derivada de la función de activación con respecto a la suma ponderada de las entradas y el gradiente anterior (propagado desde las capas superiores).
La derivada de la función de activación se denota como f'(z), donde z es la suma ponderada de las entradas a la neurona.
El gradiente local se calcula como: δ = f'(z) * gradiente_anterior

donde se calculan las derivadas parciales del error con respecto a los pesos y sesgos de la red neuronal utilizando la regla de la cadena. Actualizamos los pesos y sesgos utilizando el algoritmo de descenso de gradiente, que ajusta los valores en la dirección opuesta al gradiente para minimizar la función de pérdida. La actualización de los pesos y sesgos se realiza mediante la siguiente fórmula:
w_nuevo = w_actual - tasa_aprendizaje * dE/dw
Donde w_nuevo es el nuevo valor del peso, w_actual es el valor actual del peso, tasa_aprendizaje es una constante que controla la velocidad de aprendizaje, y dE/dw es la derivada parcial del error con respecto a un peso específico.

![image](https://github.com/julioelias-o/MCD/assets/134743799/3e042afa-bd90-4df7-bb5c-53b7e3273d12)

La idea central es que, a traves de un conjunto completo de datos, se minimicen los errores que la red pueda cometer. Para optimizar las pérdidas de la red, se necesita encontrar un conjunto de pesos (w) que minimicen la funcion de pérdida

![image](https://github.com/julioelias-o/MCD/assets/134743799/2a7e8dfb-c1e3-4c4e-8d6d-85ffb55eb6ab)

****************Siendo la funcion de pérdida una funcion continua, es posible calcular las derivadas de los puntos en este espacio. Para saber como la pérdida en la red esta cambiando, se puede calcular un gradiente con puntos en la red y saber en que direccionalidad se debe de seguir para llegar al valor minimo de la funcion. De esta forma, se repiten los calculos de gradiente con multiples valores de w (pesos) y se ajustan al propagarse por la red neuronal, una y otra vez hasta converger en un minimo. 

Una vez terminado este proceso de entrenamiento, que puede verse como el ajuste de estos pesos en la red neuronal, osea encontrar una combinación de pesos que lleven a la red a hacer predicciónes lo más cercanas a la realidad posible.

## Resultado en la optimización de la producción de PHB
En esta aplicación, se tomaron componentes del medio como parametros para los inputs, consto de 20 sets de valores iniciales. Una vez entrenado el modelo, se comparo con los valores experimentales demostrando muy buenas estimaciones de la concentración final de PHB y de biomasa. 

![res](https://github.com/julioelias-o/MCD/assets/134743799/fef303b5-f4aa-466d-9ad3-d05fd068d327)

