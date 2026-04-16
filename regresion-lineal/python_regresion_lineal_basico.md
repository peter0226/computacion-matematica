# Ejemplo: Regresión lineal en Python

## Modelo

Se busca analizar la relación entre dos variables:

- Variable independiente (X): Inversión en publicidad (miles de pesos)  
- Variable dependiente (Y): Ventas semanales (unidades)  


## Paso 1: Instalar librerías

```bash
pip install pandas matplotlib numpy
```


## Paso 2: Importar librerías

```python
import pandas as pd 
import numpy as np  
import matplotlib.pyplot as plt
```


## Paso 3: Crear los datos

```python
datos = pd.DataFrame({
    'x': [2, 4, 5, 7, 8, 10, 12],
    'y': [30, 45, 50, 65, 72, 85, 95]
})
```

## Paso 4: Graficar dispersión

```python
plt.scatter(datos['x'], datos['y'])
plt.xlabel('Inversión en publicidad (miles de pesos)')
plt.ylabel('Ventas semanales')
plt.title('Relación entre inversión y ventas')
plt.grid()
plt.show()
```

## Paso 5: Calcular regresión

```python
pendiente, intercepto = np.polyfit(datos['x'], datos['y'], 1)
```

## Paso 6: Crear recta de regresión

```python
y_pred = pendiente * datos['x'] + intercepto
```


## Paso 7: Graficar modelo completo

```python
plt.scatter(datos['x'], datos['y'], label='Datos')
plt.plot(datos['x'], y_pred, color='red', label='Recta de regresión')

plt.xlabel('Inversión en publicidad (miles de pesos)')
plt.ylabel('Ventas semanales')
plt.title('Regresión lineal')
plt.legend()
plt.grid()
plt.show()
```


## Paso 8: Interpretación

La pendiente indica cuánto aumentan las ventas por cada unidad adicional de inversión en publicidad.

El intercepto representa el valor estimado de ventas cuando la inversión es cero.


## Código completo
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

datos = pd.DataFrame({
    'x': [2, 4, 5, 7, 8, 10, 12],
    'y': [30, 45, 50, 65, 72, 85, 95]
})

plt.scatter(datos['x'], datos['y'])
plt.xlabel('Inversión en publicidad (miles de pesos)')
plt.ylabel('Ventas semanales')
plt.title('Relación entre inversión y ventas')
plt.grid()
plt.show()

pendiente, intercepto = np.polyfit(datos['x'], datos['y'], 1)

print("Pendiente:", pendiente)
print("Intercepto:", intercepto)

y_pred = pendiente * datos['x'] + intercepto

plt.scatter(datos['x'], datos['y'], label='Datos')
plt.plot(datos['x'], y_pred, color='red', label='Recta de regresión')

plt.xlabel('Inversión en publicidad (miles de pesos)')
plt.ylabel('Ventas semanales')
plt.title('Regresión lineal')
plt.legend()
plt.grid()
plt.show()
```

> [!NOTE]
> La regresión lineal permite modelar relaciones entre variables y realizar predicciones a partir de datos observados. 
