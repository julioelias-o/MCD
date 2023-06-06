# Optimización de la producción de polihidroxibutirato (PHB) por Azohydromonas lata mediante el uso de redes neuronales artificiales
## Introducción
La contaminación ambiental debido a la utilización a gran escala del poliéster sintético y su dependencia de los recursos petroleros, hace que sea necesario encontrar rutas alternativas en la producción de polimeros que sean respetuosas con el medio ambiente y renovables en la naturaleza. Teniendo esto en cuenta, la producción de biopolímeros microbianos puede ser una gran alternativa para satisfacer estas necesidades. Los polihidroxialcanoatos (PHA) son biomateriales que son acumulados intracelularmente por las células bacterianas en respuesta al desequilibrio de nutrientes y al estrés ambiental. El polihidroxibutirato (PHB) es uno de los PHA que se estudia y caracteriza más ampliamente.

Uno de los principales factores que impide la aplicación comercial de PHB es su alto costo de producción en comparación con los poliésteres sintéticos derivados de productos petroquímicos. Es por tanto, importante diseñar un medio de producción adecuado con un bioproceso bien definido para obtener la máxima biomasa y altos rendimientos de los productos metabólicos deseados. Azohydromonas lata es la bacteria más estudiada, que utiliza eficientemente las fuentes de carbono simples y baratas, como glucosa, fructosa y sacarosa para acumular gran cantidad de PHB termoplástico.

Se han utilizado varios enfoques para la optimización del proceso de producción de PHB, el tradicional que es mediante la variación de las concentraciones de los sustratos en el medio, una a la vez, pero resulta en un proceso laborioso y lento. La optimización de las variables del medio para que se pueda desarrollar el bioproceso, tiene que ser considerado bajo el análisis estratégico para una producción de PHB rentable. Con este proyecto se pretende desarrollar un modelo de redes neuronales para encontrar la concentración optima de dichas variables, que lleven a una producción de PHB lo más alta posible.

## Modelado de redes neuronales artificiales para la optimización de las variables del medio
Para la realización de este proyecto se utilizó una arquitectura feedfoward, conocida como multilayer perceptron (MLP), con el algoritmo de aprendizaje backpropagation, para construir los modelos predictivos con concentraciones de tres variables en el medio como input, y las concentraciones de biomasa y PHB como output. Para la estimación del error, se implemento el error cuadratico medio (mean square error) y se utilizó una función de activación sigmoide.

Todas las entradas y salidas se normalizan para garantizar la uniformidad durante el proceso de entrenamiento. Después del proceso de entrenamiento, el valor optimizado de la variable se vuelve a reescalar para obtener las unidades deseadas.

![image](https://github.com/julioelias-o/MCD/assets/134743799/e5675aad-f845-4508-8c01-ef7ee55a85b0)
![image](https://github.com/julioelias-o/MCD/assets/134743799/50adbd38-162d-4fa3-b7f9-6710aec5213a)
## Esquema general de la red neuronal
![Diagramas de flujo (1)](https://github.com/julioelias-o/MCD/assets/134743799/106747ca-1ff5-467c-a0e1-d18fa8038b43)

El número de neuronas en la capa de entrada corresponde a los valores normalizados de la concentración de Sucrosa, Urea y Solución TE, y en la capa de salida a los de la concentración de biomasa y concentración de THB. El numero de neuronas en la capa oculta fue variando del 1 al 6 hasta encontrar la que diera mejores resultados. Durante el proceso de entrenamiento, el error cuadrático medio (mean square error) entre el valor experimental y el valor estimado se calcula y se propaga a través de la red utilizando el algoritmo de backpropagation. El algoritmo de retropropagación ajusta los pesos en cada capa sucesivamente para reducir el error. Este procedimiento se repite hasta que el error entre el valor experimental y sus correspondientes valores predichos satisface ciertos criterios de error.

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

El siguiente paso es minimizar la función de perdida, esto es clave para ajustar los pesos de la red neuronal. Esto se logra mediante la retropropagación del error (Backpropagation). Primero, se calcula el gradiente local en la capa de salida, este gradiente se basa en la derivada parcial de la función de pérdida y la derivada de la función de activación de la capa de salida, Después, se propaga este gradiente desde la capa de salida hasta la capa de entrada de la red neuronal, de ahí el nombre "backpropagation". Para cada neurona en las capas ocultas y las de entrada, se calcula el gradiente local utilizando el gradiente anteriormente calculado (propagado desde las capas superiores) y la derivada de la función de activación (f') para cada neurona. En la siguiente imagen se puede visualizar mejor lo que ocurre desde la perspectiva de una neurona.

![image](https://github.com/julioelias-o/MCD/assets/134743799/43bae897-efb3-48bd-81ce-7a0224f2d484)

Los pesos se actualizan utilizando la regla del descenso de gradiente. La nueva actualización del peso se calcula restando el producto del gradiente y la tasa de aprendizaje, al peso actual.

![image](https://github.com/julioelias-o/MCD/assets/134743799/7c3fdbb6-2019-4b30-a515-f4eebdb191c5)

Donde: 

__W__ es el peso

__n__ es la tasa de aprendizaje y determina el tamaño del paso que se toma en la dirección opuesta al gradiente.

El descenso de gradiente es un proceso iterativo que busca minimizar el error gradualmente ajustando los pesos de la red en la dirección opuesta al gradiente de la función de pérdida. La idea central es que, a traves de un conjunto completo de datos, se minimicen los errores que la red pueda cometer. Para optimizar las pérdidas de la red, se necesita encontrar un conjunto de pesos (w) que minimicen la funcion de pérdida.

![image](https://github.com/julioelias-o/MCD/assets/134743799/2a7e8dfb-c1e3-4c4e-8d6d-85ffb55eb6ab)

## Resultado en la optimización de la producción de PHB
![asdfasdfasdfsdfs](https://github.com/julioelias-o/MCD/assets/134743799/d4d3e733-0cb8-4be9-aa67-88d54ab940a5)

En esta aplicación, se tomaron componentes del medio como parametros para los inputs, consto de 20 sets de valores iniciales. Una vez entrenado el modelo, se comparo con los valores experimentales demostrando buenas estimaciones de la concentración final de PHB y de biomasa. 
