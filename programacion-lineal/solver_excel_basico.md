# Ejemplo: Programación lineal con Solver en Excel

En este ejemplo se muestra cómo resolver un problema de programación lineal utilizando Excel Solver.

## Modelo matemático

Maximizar:

Z = 10X + 8Y

Sujeto a:

30X + 20Y ≤ 120  
2X + 2Y ≤ 9  
4X + 6Y ≤ 24  


## Paso 1: Construir la tabla en Excel

Organiza los datos del problema en una tabla que incluya:

- Coeficientes de la función objetivo
- Variables de decisión
- Restricciones

![Tabla inicial](imagenes/solver/ejemplo/01_tabla_inicial.png)



## Paso 2: Definir las restricciones

Para cada restricción, utiliza la función `SUMAPRODUCTO` para calcular el lado izquierdo de la expresión.

```excel
=SUMAPRODUCTO($C$7:$D$7,C8:D8)
```

Esta fórmula multiplica los coeficientes de cada restricción por las variables de decisión.

Aplica este mismo procedimiento para cada una de las restricciones del modelo.

![Restricción 1](imagenes/solver/ejemplo/02_restriccion_formula.png)

![Restricción 2 y 3](imagenes/solver/ejemplo/03_arrastre_formula.png)



## Paso 3: Definir la función objetivo

Utiliza la función `SUMAPRODUCTO` para calcular el valor de la función objetivo.

```excel
=SUMAPRODUCTO($C$7:$D$7,C12:D12)
```
Esta fórmula multiplica los coeficientes de la función objetivo por las variables de decisión.

![Función objetivo](imagenes/solver/ejemplo/04_funcion_objetivo_formula.png)




## Paso 4: Abrir Solver

Dirígete a:

**Datos → Solver**

![Abrir Solver](imagenes/solver/ejemplo/05_solver_abrir.png)



## Paso 5: Configurar la función objetivo

En Solver:

- Selecciona la celda donde se calcula Z  
- Define el objetivo como **Máx**

![Definir objetivo](imagenes/solver/ejemplo/06_solver_objetivo.png)



## Paso 6: Seleccionar variables de decisión

Selecciona las celdas correspondientes a las variables X y Y.

![Seleccionar variables](imagenes/solver/ejemplo/07_solver_variables.png)



## Paso 7: Agregar restricciones

Agrega cada una de las restricciones del modelo en Solver.

![Agregar restricción 1](imagenes/solver/ejemplo/08_solver_restriccion.png)

![Agregar restricción 2](imagenes/solver/ejemplo/09_solver_restriccion_1.png)
![Agregar restricción 2](imagenes/solver/ejemplo/10_solver_restriccion_1_1.png)

![Agregar restricción 2](imagenes/solver/ejemplo/11_solver_restriccion_2.png)
![Agregar restricción 2](imagenes/solver/ejemplo/12_solver_restriccion_2_1.png)

![Agregar restricción 2](imagenes/solver/ejemplo/13_solver_restriccion_3.png)
![Agregar restricción 2](imagenes/solver/ejemplo/14_solver_restriccion_3_1.png)



## Paso 8: Seleccionar método de resolución

Selecciona el método:

**Simplex LP**

![Método Simplex](imagenes/solver/ejemplo/15_solver_metodo_simplex.png)



## Paso 9: Ejecutar Solver

Haz clic en **Resolver** para obtener la solución óptima.

![Ejecutar Solver](imagenes/solver/ejemplo/16_solver_resolver.png)
![Ejecutar Solver](imagenes/solver/ejemplo/17_solver_resolver_1.png)



## Paso 10: Analizar resultados

> Observa los valores obtenidos para las variables de decisión.
> Analiza el valor óptimo de la función objetivo.
> Confirma que Solver encontró una solución válida.

![Resultado Solver](imagenes/solver/ejemplo/18_resultado_solver.png)



> [!NOTE]
> Las variables de decisión pueden inicializarse en cero o dejarse vacias, ya que Solver ajusta automáticamente sus valores para encontrar la solución óptima.

> [!IMPORTANT]
> Este procedimiento permite resolver modelos de programación lineal de forma eficiente utilizando herramientas computacionales.

> [!WARNING]
> Un error en la formulación de restricciones puede generar resultados incorrectos, por lo que deben verificarse cuidadosamente.
