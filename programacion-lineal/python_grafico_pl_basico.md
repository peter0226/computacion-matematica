# Ejemplo: Solución gráfica de programación lineal en Python

En este ejemplo se muestra cómo representar gráficamente un modelo de programación lineal utilizando Python.


## Modelo matemático

Maximizar:

Z = 40A + 30B

Sujeto a:

2A + B ≤ 40  
A + 2B ≤ 50  
A ≥ 0  
B ≥ 0  


## Paso 1: Instalar las bibliotecas necesarias

Abre la terminal y ejecuta:

```bash
pip install numpy matplotlib
```



## Paso 2: Crear el archivo de código

Crea un archivo con el nombre:

```bash
python_grafico_pl_basico.py
```



## Paso 3: Importar bibliotecas

Importa las bibliotecas necesarias para trabajar con arreglos y gráficas.
```matlab
import numpy as np   
import matplotlib.pyplot as plt
```

## Paso 4: Definir el rango de valores

Crea un rango de valores para la variable A.

```matlab
A = np.linspace(0, 50, 400)
```

Esto permitirá graficar las restricciones en el plano cartesiano.


## Paso 5: Despejar las restricciones

Expresa cada restricción en función de B.

```matlab
B1 = 40 - 2 * A 
B2 = (50 - A) / 2
```

Estas ecuaciones representan las rectas límite de las restricciones.

## Paso 6: Evitar valores negativos

Ajusta los valores negativos para mejorar la visualización.

```matlab
B1 = np.maximum(B1, 0)  
B2 = np.maximum(B2, 0)
```

---

## Paso 7: Definir los vértices de la región factible

Identifica los vértices del problema.

```matlab
vertices_A = [0, 0, 10, 20] 
vertices_B = [0, 25, 20, 0]
```

Estos puntos corresponden a la región factible del modelo.


## Paso 8: Graficar las restricciones

Dibuja las rectas de las restricciones.

```matlab
plt.plot(A, B1, label='2A + B = 40') 
plt.plot(A, B2, label='A + 2B = 50')
```


## Paso 9: Sombrear la región factible

Representa gráficamente la región factible.

```matlab
plt.fill(vertices_A, vertices_B, alpha=0.3, label='Región factible')
```


## Paso 10: Marcar los vértices

Agrega los vértices a la gráfica.

```matlab
plt.scatter(vertices_A, vertices_B)
```

Opcionalmente, puedes etiquetarlos.

```matlab
for a, b in zip(vertices_A, vertices_B):
    plt.text(a + 0.5, b + 0.5, f'({a}, {b})')
```


## Paso 11: Configurar la gráfica

Agrega título, ejes, cuadrícula y leyenda.

```matlab
plt.xlim(0, 30)  
plt.ylim(0, 30) 
plt.xlabel('Producto A') 
plt.ylabel('Producto B')
plt.title('Método gráfico de programación lineal')  
plt.grid(True)
plt.legend()
```


## Paso 12: Mostrar la gráfica

```matlab
plt.show()
```


## Paso 13: Evaluar la función objetivo

Evalúa la función objetivo en cada vértice.

```matlab
print("Evaluación de la función objetivo Z = 40A + 30B")
for a, b in zip(vertices_A, vertices_B):
    z = 40 * a + 30 * b
    print(f"Vértice ({a}, {b}) -> Z = {z}"))
```

## Código completo

```matlab
import numpy as np  
import matplotlib.pyplot as plt

A = np.linspace(0, 50, 400)  

B1 = 40 - 2 * A  
B2 = (50 - A) / 2  

B1 = np.maximum(B1, 0)  
B2 = np.maximum(B2, 0)  

vertices_A = [0, 0, 10, 20] 
vertices_B = [0, 25, 20, 0]   

plt.plot(A, B1, label='2A + B = 40')  
plt.plot(A, B2, label='A + 2B = 50')  

plt.fill(vertices_A, vertices_B, alpha=0.3, label='Región factible')  
plt.scatter(vertices_A, vertices_B)

for a, b in zip(vertices_A, vertices_B):
    plt.text(a + 0.5, b + 0.5, f'({a}, {b})')  

plt.xlim(0, 30)  
plt.ylim(0, 30)  
plt.xlabel('Producto A')  
plt.ylabel('Producto B')  
plt.title('Método gráfico de programación lineal')  
plt.grid(True) 
plt.legend()  
plt.show()  

print("Evaluación de la función objetivo Z = 40A + 30B")
for a, b in zip(vertices_A, vertices_B):
    z = 40 * a + 30 * b
    print(f"Vértice ({a}, {b}) -> Z = {z}")
```

## Resultado esperado

El programa debe mostrar:

- La gráfica de las restricciones
- La región factible
- Los vértices del problema
- El valor de la función objetivo en cada vértice

![Activar Solver](https://raw.githubusercontent.com/peter0226/computacion-matematica/main/programacion-lineal/imagenes/python/grafica.png)


## Interpretación

La solución óptima se encuentra en uno de los vértices de la región factible.  
La evaluación de la función objetivo permite identificar cuál de ellos maximiza la utilidad.


> [!NOTE]
> El método gráfico solo puede aplicarse directamente a problemas con dos variables de decisión.

> [!IMPORTANT]
> Identificar correctamente los vértices es indispensable para encontrar la solución óptima.

> [!WARNING]
> Si se despejan incorrectamente las restricciones o se grafica mal la región factible, la interpretación del modelo será errónea.
