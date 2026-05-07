# Ejemplo: Problema del agente viajero en Python

## Modelo

Se busca encontrar la ruta de menor distancia total para recorrer varias ciudades y regresar al punto de origen.

El problema del agente viajero consiste en:

- Visitar cada ciudad una sola vez  
- Regresar al punto inicial  
- Minimizar la distancia total recorrida  

## Datos del problema

La siguiente matriz representa las distancias entre ciudades:

| Ciudad | P | Q | R | S | T |
|---|---|---|---|---|---|
| P | 0 | 12 | 18 | 30 | 25 |
| Q | 12 | 0 | 14 | 22 | 28 |
| R | 18 | 14 | 0 | 16 | 20 |
| S | 30 | 22 | 16 | 0 | 10 |
| T | 25 | 28 | 20 | 10 | 0 |

## Paso 1: Instalar bibliotecas

```bash
pip install matplotlib networkx
```

## Paso 2: Importar librerías

```python
import itertools
import networkx as nx
import matplotlib.pyplot as plt
```

## Paso 3: Definir ciudades y distancias

```python
ciudades = ['P', 'Q', 'R', 'S', 'T']

distancias = {
    ('P', 'Q'): 12,
    ('P', 'R'): 18,
    ('P', 'S'): 30,
    ('P', 'T'): 25,
    ('Q', 'R'): 14,
    ('Q', 'S'): 22,
    ('Q', 'T'): 28,
    ('R', 'S'): 16,
    ('R', 'T'): 20,
    ('S', 'T'): 10
}
```

## Paso 4: Crear función de distancia

```python
def obtener_distancia(origen, destino):

    if origen == destino:
        return 0

    if (origen, destino) in distancias:
        return distancias[(origen, destino)]

    return distancias[(destino, origen)]
```

## Paso 5: Generar rutas posibles

```python
rutas = list(itertools.permutations(ciudades[1:]))
```

## Paso 6: Calcular distancia total

```python
mejor_ruta = None
menor_distancia = float('inf')

for ruta in rutas:

    ruta_completa = ['P'] + list(ruta) + ['P']

    distancia_total = 0

    for i in range(len(ruta_completa) - 1):

        distancia_total += obtener_distancia(
            ruta_completa[i],
            ruta_completa[i + 1]
        )

    print(ruta_completa, "=", distancia_total)

    if distancia_total < menor_distancia:

        menor_distancia = distancia_total
        mejor_ruta = ruta_completa
```

## Paso 7: Mostrar mejor ruta

```python
print("\nRuta óptima:", mejor_ruta)
print("Distancia mínima:", menor_distancia)
```

## Paso 8: Representar el grafo

```python
G = nx.Graph()

for ciudad in ciudades:
    G.add_node(ciudad)

for (origen, destino), distancia in distancias.items():

    G.add_edge(
        origen,
        destino,
        weight=distancia
    )

pos = nx.spring_layout(G)

etiquetas = nx.get_edge_attributes(G, 'weight')

nx.draw(
    G,
    pos,
    with_labels=True,
    node_color='lightblue',
    node_size=2000,
    font_size=12
)

nx.draw_networkx_edge_labels(
    G,
    pos,
    edge_labels=etiquetas
)

plt.title("Problema del Agente Viajero")
plt.show()
```

## Interpretación

La ruta óptima representa el recorrido con menor distancia total posible.

Este tipo de problemas se utiliza en:

- logística  
- distribución  
- planeación de rutas  
- transporte  
- optimización de recorridos  

## Código completo

```python
import itertools
import networkx as nx
import matplotlib.pyplot as plt

ciudades = ['P', 'Q', 'R', 'S', 'T']

distancias = {
    ('P', 'Q'): 12,
    ('P', 'R'): 18,
    ('P', 'S'): 30,
    ('P', 'T'): 25,
    ('Q', 'R'): 14,
    ('Q', 'S'): 22,
    ('Q', 'T'): 28,
    ('R', 'S'): 16,
    ('R', 'T'): 20,
    ('S', 'T'): 10
}

def obtener_distancia(origen, destino):

    if origen == destino:
        return 0

    if (origen, destino) in distancias:
        return distancias[(origen, destino)]

    return distancias[(destino, origen)]

rutas = list(itertools.permutations(ciudades[1:]))

mejor_ruta = None
menor_distancia = float('inf')

for ruta in rutas:

    ruta_completa = ['P'] + list(ruta) + ['P']

    distancia_total = 0

    for i in range(len(ruta_completa) - 1):

        distancia_total += obtener_distancia(
            ruta_completa[i],
            ruta_completa[i + 1]
        )

    print(ruta_completa, "=", distancia_total)

    if distancia_total < menor_distancia:

        menor_distancia = distancia_total
        mejor_ruta = ruta_completa

print("\nRuta óptima:", mejor_ruta)
print("Distancia mínima:", menor_distancia)

G = nx.Graph()

for ciudad in ciudades:
    G.add_node(ciudad)

for (origen, destino), distancia in distancias.items():

    G.add_edge(
        origen,
        destino,
        weight=distancia
    )

pos = nx.spring_layout(G)

etiquetas = nx.get_edge_attributes(G, 'weight')

nx.draw(
    G,
    pos,
    with_labels=True,
    node_color='lightblue',
    node_size=2000,
    font_size=12
)

nx.draw_networkx_edge_labels(
    G,
    pos,
    edge_labels=etiquetas
)

plt.title("Problema del Agente Viajero")
plt.show()
```

> [!NOTE]
> El problema del agente viajero es un problema clásico de optimización combinatoria utilizado en logística, rutas y distribución.

> [!IMPORTANT]
> Conforme aumenta el número de ciudades, el número de rutas posibles crece rápidamente, aumentando la complejidad computacional del problema.

> [!WARNING]
> Evaluar todas las rutas posibles puede ser costoso en problemas grandes, por lo que en aplicaciones reales suelen utilizarse algoritmos heurísticos o aproximados.
