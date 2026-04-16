# Ejemplo: Modelo de transporte en Python con PuLP

En este ejemplo se muestra cómo resolver un modelo de transporte utilizando Python y la librería PuLP.


## Modelo

Minimizar:

Costo total de transporte

Sujeto a:

- Restricciones de oferta
- Restricciones de demanda
- No negatividad


## Paso 1: Instalar la librería

Abre la terminal y ejecuta:

```bash
pip install pulp
```


## Paso 2: Crear el archivo de código

Crea un archivo con el nombre:

```bash
python_transporte_basico.py
```

## Paso 3: Importar librerías

Importa las herramientas necesarias de PuLP.
```python
from pulp import LpProblem, LpVariable, LpMinimize, lpSum, LpStatus, value
```

## Paso 4: Crear el problema

Define el modelo como un problema de minimización.
```python
modelo = LpProblem("Modelo_de_Transporte", LpMinimize)
```

## Paso 5: Definir costos, oferta y demanda

Representa los datos del problema mediante diccionarios.

```python
costos = {  
    ("Granja1", "Ciudad1"): 24,  
    ("Granja1", "Ciudad2"): 30,  
    ("Granja1", "Ciudad3"): 30,  
    ("Granja2", "Ciudad1"): 32,  
    ("Granja2", "Ciudad2"): 26,  
    ("Granja2", "Ciudad3"): 25,  
    ("Granja3", "Ciudad1"): 31,  
    ("Granja3", "Ciudad2"): 32,  
    ("Granja3", "Ciudad3"): 31,  
}  

oferta = {  
    "Granja1": 200,  
    "Granja2": 250,  
    "Granja3": 450,  
}  

demanda = {  
    "Ciudad1": 150,  
    "Ciudad2": 350,  
    "Ciudad3": 400,  
}  
```

Estos diccionarios almacenan:

- Costos de transporte
- Oferta por origen
- Demanda por destino

---

## Paso 6: Definir orígenes y destinos

Obtén la lista de orígenes y destinos a partir de los diccionarios.

```python
origenes = list(oferta.keys())  
destinos = list(demanda.keys())  
```

## Paso 7: Crear variables de decisión

Define una variable para cada posible envío entre origen y destino.

Cada variable representa la cantidad de unidades transportadas desde un origen hacia un destino.

```python 
x = LpVariable.dicts("x", [(i, j) for i in origenes for j in destinos], lowBound=0)  
```

## Paso 8: Definir la función objetivo

Construye la función objetivo para minimizar el costo total de transporte.

Se utiliza la suma del costo unitario multiplicado por la cantidad enviada en cada ruta.

```python
modelo += lpSum(costos[(i, j)] * x[(i, j)] for i in origenes for j in destinos), "Costo_Total"  
```

## Paso 9: Agregar restricciones de oferta

Para cada origen, la suma de los envíos debe ser igual a la oferta disponible.

```python
for i in origenes:  
    modelo += lpSum(x[(i, j)] for j in destinos) == oferta[i], f"Oferta_{i}"  
```

## Paso 10: Agregar restricciones de demanda

Para cada destino, la suma de los envíos recibidos debe ser igual a la demanda requerida.

```python
for j in destinos:  
    modelo += lpSum(x[(i, j)] for i in origenes) == demanda[j], f"Demanda_{j}"  
```

## Paso 11: Resolver el modelo

Ejecuta el modelo para encontrar la solución óptima.

```python
modelo.solve()
```

## Paso 12: Mostrar resultados

Imprime:

- Estado de la solución
- Costo mínimo total
- Cantidades enviadas de cada origen a cada destino

```python
print("Estado:", LpStatus[modelo.status])  
print("Costo mínimo total =", value(modelo.objective))  
print("\nAsignaciones óptimas:")  

for i in origenes:  
    for j in destinos:  
        print(f"{i} -> {j} = {x[(i, j)].varValue}")  
```

## Código completo

```python 
from pulp import LpProblem, LpVariable, LpMinimize, lpSum, LpStatus, value  

# Crear el problema  
modelo = LpProblem("Modelo_de_Transporte", LpMinimize)  

# Costos de transporte  
costos = {  
    ("Granja1", "Ciudad1"): 24,  
    ("Granja1", "Ciudad2"): 30,  
    ("Granja1", "Ciudad3"): 30,  
    ("Granja2", "Ciudad1"): 32,  
    ("Granja2", "Ciudad2"): 26,  
    ("Granja2", "Ciudad3"): 25,  
    ("Granja3", "Ciudad1"): 31,  
    ("Granja3", "Ciudad2"): 32,  
    ("Granja3", "Ciudad3"): 31,  
}  

# Oferta  
oferta = {  
    "Granja1": 200,  
    "Granja2": 250,  
    "Granja3": 450,  
}  

# Demanda  
demanda = {  
    "Ciudad1": 150,  
    "Ciudad2": 350,  
    "Ciudad3": 400,  
}  

origenes = list(oferta.keys())  
destinos = list(demanda.keys())  

# Variables de decisión  
x = LpVariable.dicts("x", [(i, j) for i in origenes for j in destinos], lowBound=0)  

# Función objetivo  
modelo += lpSum(costos[(i, j)] * x[(i, j)] for i in origenes for j in destinos), "Costo_Total"  

# Restricciones de oferta  
for i in origenes:  
    modelo += lpSum(x[(i, j)] for j in destinos) == oferta[i], f"Oferta_{i}"  

# Restricciones de demanda  
for j in destinos:  
    modelo += lpSum(x[(i, j)] for i in origenes) == demanda[j], f"Demanda_{j}"  

# Resolver  
modelo.solve()  

# Mostrar resultados  
print("Estado:", LpStatus[modelo.status])  
print("Costo mínimo total =", value(modelo.objective))  
print("\nAsignaciones óptimas:")  

for i in origenes:  
    for j in destinos:  
        print(f"{i} -> {j} = {x[(i, j)].varValue}")  
```

## Resultado esperado

El programa debe mostrar una solución factible con el costo mínimo total y las asignaciones óptimas para cada ruta.

## Interpretación

La solución indica cuántas unidades deben enviarse desde cada origen hacia cada destino para satisfacer la demanda sin exceder la oferta, minimizando el costo total de transporte.

> [!NOTE]
> PuLP permite modelar problemas de transporte de manera estructurada y clara, utilizando programación lineal.

> [!IMPORTANT]
> Para que el modelo tenga solución factible, la suma total de la oferta debe ser igual a la suma total de la demanda.

> [!WARNING]
> Un error en la definición de costos, oferta o demanda puede alterar completamente la solución del problema.
