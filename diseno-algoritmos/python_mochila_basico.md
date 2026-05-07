# Ejemplo: Problema de la mochila en Python

## Modelo

Se busca seleccionar un conjunto de objetos que maximice el valor total sin exceder una capacidad máxima.

El problema de la mochila consiste en:

- Tener un conjunto de objetos disponibles  
- Cada objeto tiene un peso y un valor  
- Existe una capacidad máxima  
- Se busca maximizar el valor total seleccionado sin exceder la capacidad  

## Datos del problema

Una persona desea preparar una mochila para una excursión. Tiene varios objetos disponibles, pero la mochila solo soporta una capacidad máxima de 15 unidades de peso.

| Objeto | Peso | Valor |
|---|---:|---:|
| Linterna | 3 | 25 |
| Botiquín | 4 | 40 |
| Agua | 5 | 45 |
| Comida | 6 | 55 |
| Manta | 7 | 60 |

Capacidad máxima: 15 unidades de peso

## Paso 1: Importar librerías

```python
import itertools
```

## Paso 2: Definir objetos

```python
objetos = [
    {"nombre": "Linterna", "peso": 3, "valor": 25},
    {"nombre": "Botiquín", "peso": 4, "valor": 40},
    {"nombre": "Agua", "peso": 5, "valor": 45},
    {"nombre": "Comida", "peso": 6, "valor": 55},
    {"nombre": "Manta", "peso": 7, "valor": 60}
]

capacidad = 15
```

## Paso 3: Generar combinaciones posibles

```python
combinaciones = []

for r in range(1, len(objetos) + 1):

    for combinacion in itertools.combinations(objetos, r):

        combinaciones.append(combinacion)
```

## Paso 4: Evaluar combinaciones

```python
mejor_combinacion = None
mejor_valor = 0
mejor_peso = 0

for combinacion in combinaciones:

    peso_total = sum(objeto["peso"] for objeto in combinacion)
    valor_total = sum(objeto["valor"] for objeto in combinacion)

    nombres = [objeto["nombre"] for objeto in combinacion]

    print(nombres, "Peso:", peso_total, "Valor:", valor_total)

    if peso_total <= capacidad and valor_total > mejor_valor:

        mejor_combinacion = nombres
        mejor_valor = valor_total
        mejor_peso = peso_total
```

## Paso 5: Mostrar solución óptima

```python
print("\nMejor combinación:", mejor_combinacion)
print("Peso total:", mejor_peso)
print("Valor máximo:", mejor_valor)
```

## Interpretación

La mejor combinación representa los objetos seleccionados que generan el mayor valor posible sin exceder la capacidad máxima de la mochila.

Este tipo de problema se utiliza en:

- logística  
- selección de recursos  
- planeación de carga  
- toma de decisiones  
- optimización de beneficios  

## Código completo

```python
import itertools

objetos = [
    {"nombre": "Linterna", "peso": 3, "valor": 25},
    {"nombre": "Botiquín", "peso": 4, "valor": 40},
    {"nombre": "Agua", "peso": 5, "valor": 45},
    {"nombre": "Comida", "peso": 6, "valor": 55},
    {"nombre": "Manta", "peso": 7, "valor": 60}
]

capacidad = 15

combinaciones = []

for r in range(1, len(objetos) + 1):

    for combinacion in itertools.combinations(objetos, r):

        combinaciones.append(combinacion)

mejor_combinacion = None
mejor_valor = 0
mejor_peso = 0

for combinacion in combinaciones:

    peso_total = sum(objeto["peso"] for objeto in combinacion)
    valor_total = sum(objeto["valor"] for objeto in combinacion)

    nombres = [objeto["nombre"] for objeto in combinacion]

    print(nombres, "Peso:", peso_total, "Valor:", valor_total)

    if peso_total <= capacidad and valor_total > mejor_valor:

        mejor_combinacion = nombres
        mejor_valor = valor_total
        mejor_peso = peso_total

print("\nMejor combinación:", mejor_combinacion)
print("Peso total:", mejor_peso)
print("Valor máximo:", mejor_valor)
```

> [!NOTE]
> El problema de la mochila es un problema clásico de optimización que permite seleccionar elementos buscando maximizar un beneficio bajo una restricción de capacidad.

> [!IMPORTANT]
> La combinación óptima no siempre corresponde a elegir los objetos con mayor valor individual, ya que también debe considerarse el peso total.

> [!WARNING]
> Evaluar todas las combinaciones posibles puede ser costoso cuando el número de objetos aumenta, por lo que en problemas grandes se utilizan técnicas más eficientes como programación dinámica o algoritmos heurísticos.
