<h1 style="color: #ff5733;">Título Principal</h1>

<h2 style="color: #33ff57;">Subtítulo 1</h2>

<h3 style="color: #3357ff;">Sub-subtítulo 1.1</h3>

<h2 style="color: #f033ff;">Subtítulo 2</h2>

<h3 style="color: #33fff5;">Sub-subtítulo 2.1</h3>


#***INFOTEC "Centro de Investigación e Innovación en Tecnologías de la Información y Comunicación"***

#**ANÁLISIS DE ALGORITMOS**

##**1A. REPORTE ESCRITO: EXPERIMENTOS Y ANÁLISIS**



##*JUAN ANTONIO VELASQUEZ MARTINEZ*

#**INTRODUCCIÓN**

En la era digital actual, el big data ha emergido como un recurso para las organizaciones, permitiéndoles extraer, procesar y analizar datos  significativos. El big data se caracteriza por sus 4 Vs: volumen, velocidad, variedad y veracidad. El volumen se refiere a la cantidad masiva de datos generados y almacenados; la velocidad, a la rapidez con la que se generan y procesan los datos; la variedad, a los diferentes tipos de datos (estructurados y no estructurados); y la veracidad, a la calidad y precisión de los datos. La capacidad de manejar y analizar estos grandes volúmenes de información de manera eficiente es crucial para aprovechar al máximo el potencial del big data.  (Müller et al., 2016)

El análisis de big data permite a las organizaciones identificar patrones, predecir tendencias y optimizar procesos, lo que puede resultar en mejoras significativas en la eficiencia operativa y en la toma de decisiones estratégicas. Sin embargo, la manipulación de grandes volúmenes de datos presenta desafíos significativos en términos de infraestructura, almacenamiento, procesamiento y análisis. Los algoritmos eficientes son esenciales para manejar estos desafíos y garantizar que los sistemas de big data funcionen de manera óptima. (Manyika et al., 2011)

Este reporte escrito se basa en comparar diferentes órdenes de crecimiento mediante simulaciones en un entorno de Jupyter. Se compararán los siguientes órdenes de crecimiento: O(1) vs O(logn), O(n) vs O(nlogn), O(n^2) vs O(n^3), O(an) vs O(n!) y O(n!) vs O(n^n). Para cada comparación, se seleccionarán rangos adecuados de n para visualizar claramente las diferencias en los órdenes de crecimiento. Se crearán figuras para cada comparación y se discutirán las observaciones obtenidas. Además, se presentará una tabla con tiempos de ejecución simulados para algoritmos ficticios con los órdenes de crecimiento mencionados, utilizando diferentes tamaños de entrada n. Este análisis proporcionará una visión clara de cómo los diferentes órdenes de crecimiento afectan el rendimiento y su eficiencia.


**BIBLIOTECAS UTILIZADAS**



```python
import numpy as np
import pandas as pd
import math
import matplotlib.pyplot as plt
```

**DEFINICIÓN DE LAS FUNCIONES DE LOS SIGUIENTES ÓRDENENES DE CRECIMIENTO**

Funciones con las que vamos a comparar los siguientes órdenes de crecimiento.


```python
# Definir las funciones de crecimiento
def constant(n):
    return 1

def logarithmic(n):
    return np.log(n)

def linear(n):
    return n

def linear_logarithmic(n):
    return n * np.log(n)

def quadratic(n):
    return n**2

def cubic(n):
    return n**3

def exponential(n, a=2):
    return a**n

def factorial(n):
    return math.factorial(n)

def double_exponential(n):
    return n**n
```

##**FIGURAS DE COMPARACIÓN**

Nota: Para cada una de las comparaciones, se eligieron rangos adecuados para n que permitan visualizar las diferencias entre los órdenes de crecimiento.


```python
# Figura de Comparaciones de las Funciones de crecimiento
def plot_comparison(funcs, labels, title, x_range):
    plt.figure(figsize=(7, 5))
    for func, label in zip(funcs, labels):
        plt.plot(x_range, [func(x) / 1e9 for x in x_range], label=label)  # Convertir a segundos
    plt.xlabel('n')
    plt.ylabel('Tiempo (s)')
    plt.title(title)
    plt.legend()
    plt.yscale('log')
    plt.xscale('log')
    plt.grid(True)
    plt.show()

# Rango de valores para n
x_range_small = np.arange(1, 10)
x_range_medium = np.arange(1, 100)

# Comparación 1: O(1) vs O(logn)
plot_comparison([constant, logarithmic], ['O(1)', 'O(logn)'], 'Figura 1 - Comparación de O(1) con O(logn)', x_range_small)

print("Discusión de la Figura 1:")
print("El grafico muestra que la función constante O(1) permanece constante independientemente del tamaño de la entrada, mientras que O(logn) crece lentamente con el tamaño de la entrada. Por lo que un algoritmo con complejidad constante O(1) es más eficiente en términos de tiempo de ejecución en comparación con un algoritmo con complejidad logarítmica O(logn).")

# Comparación 2: O(n) vs O(nlogn)
plot_comparison([linear, linear_logarithmic], ['O(n)', 'O(nlogn)'], 'Figura 2 - Comparación de O(n) con O(nlogn)', x_range_medium)

print("Discusión de la Figura 2:")
print("La función O(n) crece linealmente con el tamaño de entrada n. Mientras que la función O(n log n) crece más rápido que O(n), pero sigue siendo practico para valores moderados de n. Entonces, un algoritmo con complejidad lineal O(n) es más eficiente en términos de tiempo de ejecución en comparación con un algoritmo con complejidad linealítmica O(nlogn).")

# Comparación 3: O(n^2) vs O(n^3)
plot_comparison([quadratic, cubic], ['O(n^2)', 'O(n^3)'], 'Figura 3 - Comparación de O(n^2) con O(n^3)', x_range_medium)

print("Discusión de la Figura 3:")
print("La función cuadrática O(n^2) crece más rápidamente que la lineal, pero la función cúbica O(n^3) crece aún más rápidamente. Por lo tanto, un algoritmo con complejidad cuadrática O(n^2) es más eficiente en términos de tiempo de ejecución en comparación con un algoritmo con complejidad cúbica O(n^3)")

# Comparación 4: O(a^n) vs O(n!)
plot_comparison([lambda n: exponential(n, 2), factorial], ['O(2^n)', 'O(n!)'], 'Figura 4 - Comparación de O(2^n) con O(n!)', x_range_small)

print("Discusión de la Figura 4:")
print("El gráfico muestra la complejidad factorial de O(n!) que resulta en tiempos de ejecución mucho más alto que O(2^n) a medida que el tamaño de la entrada n aumenta. La complejidad factorial O(n!) crece mucho más rápido que la complejidad exponencial O(2^n), haciendo que los algoritmos con complejidad factorial sean prácticamente inutilizables para valores grandes de n.")

# Comparación 5: O(n!) vs O(n^n)
plot_comparison([factorial, double_exponential], ['O(n!)', 'O(n^n)'], ' Figura 5 - Comparación de O(n!) con O(n^n)', x_range_small)

print("Discusión de la Figura 5:")
print("El gráfico muestra como la función factorial O(n!) crece muy rápidamente, pero la función doble exponencial O(n^n) crece más rapido a medida del tamaño de la entrada. Por lo tanto,  los algoritmos con complejidad factorial y doble exponencial sean prácticamente inutilizables para valores grandes de n.")
```


    
![png](output_7_0.png)
    


    Discusión de la Figura 1:
    El grafico muestra que la función constante O(1) permanece constante independientemente del tamaño de la entrada, mientras que O(logn) crece lentamente con el tamaño de la entrada. Por lo que un algoritmo con complejidad constante O(1) es más eficiente en términos de tiempo de ejecución en comparación con un algoritmo con complejidad logarítmica O(logn).



    
![png](output_7_2.png)
    


    Discusión de la Figura 2:
    La función O(n) crece linealmente con el tamaño de entrada n. Mientras que la función O(n log n) crece más rápido que O(n), pero sigue siendo practico para valores moderados de n. Entonces, un algoritmo con complejidad lineal O(n) es más eficiente en términos de tiempo de ejecución en comparación con un algoritmo con complejidad linealítmica O(nlogn).



    
![png](output_7_4.png)
    


    Discusión de la Figura 3:
    La función cuadrática O(n^2) crece más rápidamente que la lineal, pero la función cúbica O(n^3) crece aún más rápidamente. Por lo tanto, un algoritmo con complejidad cuadrática O(n^2) es más eficiente en términos de tiempo de ejecución en comparación con un algoritmo con complejidad cúbica O(n^3)



    
![png](output_7_6.png)
    


    Discusión de la Figura 4:
    El gráfico muestra la complejidad factorial de O(n!) que resulta en tiempos de ejecución mucho más alto que O(2^n) a medida que el tamaño de la entrada n aumenta. La complejidad factorial O(n!) crece mucho más rápido que la complejidad exponencial O(2^n), haciendo que los algoritmos con complejidad factorial sean prácticamente inutilizables para valores grandes de n.



    
![png](output_7_8.png)
    


    Discusión de la Figura 5:
    El gráfico muestra como la función factorial O(n!) crece muy rápidamente, pero la función doble exponencial O(n^n) crece más rapido a medida del tamaño de la entrada. Por lo tanto,  los algoritmos con complejidad factorial y doble exponencial sean prácticamente inutilizables para valores grandes de n.


##**TABLA DE TIEMPOS DE EJECUCIÓN SIMULADOS**

Nota: Se creó una tabla con tiempos de ejecución simulados para algoritmos ficticios con los órdenes de crecimiento mencionados.


```python
# Tamaños de entrada
n_values = [100, 1000, 10000, 100000]

# Funciones de costo
cost_functions = {
    'O(1)': constant,
    'O(logn)': logarithmic,
    'O(n)': linear,
    'O(nlogn)': linear_logarithmic,
    'O(n^2)': quadratic,
    'O(n^3)': cubic,
    'O(2^n)': lambda n: exponential(n, 2),
    'O(n!)': factorial,
    'O(n^n)': double_exponential
}

# Elaboración de Tabla
results = []
for n in n_values:
    row = {'n': n}
    for label, func in cost_functions.items():
        try:
            row[label] = func(n) / 1e9  # Conversión a segundos
        except OverflowError:
            row[label] = 'Overflow'
    results.append(row)

df = pd.DataFrame(results)
df.set_index('n', inplace=True)
print(df)
```

                    O(1)       O(logn)          O(n)      O(nlogn)    O(n^2)  \
    n                                                                          
    100     1.000000e-09  4.605170e-09  1.000000e-07  4.605170e-07   0.00001   
    1000    1.000000e-09  6.907755e-09  1.000000e-06  6.907755e-06   0.00100   
    10000   1.000000e-09  9.210340e-09  1.000000e-05  9.210340e-05   0.10000   
    100000  1.000000e-09  1.151293e-08  1.000000e-04  1.151293e-03  10.00000   
    
                 O(n^3)                                             O(2^n)  \
    n                                                                        
    100           0.001                           1267650600228229480448.0   
    1000          1.000  1071508607186267387683686365329820259878779802...   
    10000      1000.000                                           Overflow   
    100000  1000000.000                                           Overflow   
    
                                                        O(n!)  \
    n                                                           
    100     9332621544394415476347207459720972338060818003...   
    1000                                             Overflow   
    10000                                            Overflow   
    100000                                           Overflow   
    
                                                       O(n^n)  
    n                                                          
    100     9999999999999999142677146545318765623087289762...  
    1000                                             Overflow  
    10000                                            Overflow  
    100000                                           Overflow  


**INTERPRETACIÓN DE LA TABLA**

---
Como se muestra en la tabla, el tiempo de ejecución de O(1) no dependen del tamaño de n. Este mantiene un mismo valor, lo que idnica que el tiempo de ejecución no dependen del tamaño de n. Por otro lado O(logn) los valores aumentan lentamente a mediuda que n aumenta por lo que es consistenten con la naturaleza logaritmica. En O(n) los valores aumentan de forma lineal con n.

En la tabla, los valores de O(nlogn) aumenta rápido que O(n), pero no tanto como O(n^2). Por otro lado tenemos O(n^2) donde sus valores aumentan rapidamente a medidca que incrementa los valores de n. En O(n^3) es relativamente lo mismo pero más rápido, aun en valores pequeños.

Al ejecutar el código, muestra varios Overflow en la tabla, por lo que se desbordó la memoria y no fue capaz de obtener esos valores, esto se debe a que los valores de O(2^n), O(n!) y O(n^n) para n grandes (como 10000 o 100000) son extremadamente grandes y exceden el límite de conversión de enteros a cadenas en Python.





##**IMPLICACIONES DE COSTOS DE CÓMPUTO NECESARIOS PARA MANIPULAR GRANDES VOLÚMENES DE INFORMACIÓN**

La maniuplación grande de volúmenes de información, presenta desafíos por los costos de cómputo. Estos costos se refieren al gasto monetario,  a los recursos computacionales necesarios, tiempo de procesamiento, memoria, almacenamiento, energía entre otros. A continuación se mostraran algunas de las implicaciones más importantes para la manipulación de grandes volúmenes de información.

Los costos de la infraestructura implica la manipulación de grandes volúmenes de datos que requierne una infrestructura robusta, esto incluye servidores potentes, almcanamiento masivo y redes de alta velocida, lo cual conlleva costos significativos de hardware, mantenimiento y energía. (Armbrust et al., 2010)

La energía es inplicación de los centros de datos que manejan grandes volúmenes de información ya que consumen enormes cantidades de energía, lo cual no solo aumenta los costos operativos, sino que también tiene implicaciones ambientales debido a las emisiones de carbono. (Baliga et al., 2011)

Los costos de almacenamieto implica que los grandes vbolúmnews de almcanamiento de datos requiera solcuiones de de forma escalable y eficientes. Estos costos pueden ser significativos ya que requieren almacenamiento para la recuperación. Por otro lado tenemos los costos de procesamiento estos volúmenes de datos en tiempo real o cerca de tiempo real requiere de algoritmos eficientes y recursos de cómputo significativo. Los costos de procesamiento pueden ser altos, especialmente si se utilzian tecnologias como el aprendizaje automático y la inteligencia artificial. (Wang et al., 2015)

El manipular grandes volúmenes de información implica costos significativos en términos de infraestructura, energía, almacenamiento, procesamiento, seguridad y mantenimiento. Estos deben ser cuidadosamente considerados y gestionados para aegurar eficiencia y sostenibilidad de las soluciones de big data.

##**CONCLUSIONES**
En las simulaciones, se observó que los órdenes de crecimiento más bajos como O(1), O(logn) y O(n) tienen aplicaciones que requieren alta eficiencia. Estos órdenes de crecimiento son ideales para tareas que demandan un rendimiento óptimo y tiempos de respuesta rápido.

Por otro lado, los valores de O(nlogn) y O(n^2) resultaron ser más prácticos y utilizables en una variedad de aplicaciones, ofreciendo un equilibrio entre eficiencia y practicidad.

En contraste. Los valores de O(2^n), O(n!) y O(n^n) no fueron eficientes, resultando en tiempos muy largos donde se desborda aveces la memoria sin obtener valor.

La tabla de tiempos de ejecución simulados para diferentes tamaños de entrada n muestra como los diferentes órdenes de crecimiento afectan el rendimiento de los algoritmos. Para los valores de n, los ódenes de crecimiento más altos como O(n!) y O(n^n) resultan en tiempos de ejecución extremadamente largos, mientras que los órdenes de crecimiento más bajos como O(1) y O(logn) son más eficientes.




##**REFERENCIAS**
Müller, V. C., Schal, J. M., & Meyer-Lindenberg, A. (2016). Machine Learning for Brain Imaging. Cambridge University Press.


Manyika, J., Chui, M., Brown, B., Bughin, J., Dobbs, R., Roxburgh, C., & Byers, A. H. (2011). Big data: The next frontier for innovation, competition, and productivity. McKinsey Global Institute. https://www.mckinsey.com/business-functions/mckinsey-analytics/our-insights/big-data-the-next-frontier-for-innovation

Armbrust, M., Fox, A., Griffith, R., Joseph, A. D., Katz, R. H., Konwinski, A., ... & Zaharia, M. (2010). A View of Cloud Computing. Communications of the ACM, 53(4), 50-58. doi:10.1145/1721654.1721672

J. Baliga, R. Ayre, K. Hinton, and R. S. Tucker, Energy-Efficient Telecommunications. 2011.

L. Wang, Y. Chen, and Q. Liu, Big Data Processing: A Survey. Springer, 2015.
