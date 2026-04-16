# Ejemplo: Modelo de transporte con Solver en Excel

En este ejemplo se muestra cómo resolver un problema de transporte utilizando Excel Solver.

---

## Modelo

Minimizar:

Costo total de transporte

Sujeto a:

- Restricciones de oferta (producción)
- Restricciones de demanda
- No negatividad

---

## Paso 1: Construir la tabla de costos

Organiza los datos del problema en una tabla que incluya:

- Costos de transporte
- Oferta (producción)
- Demanda

![Tabla inicial](imagenes/solver/transporte/01_tabla_costos_oferta_demanda.png)
---

## Paso 2: Construir la matriz de variables

Crea una tabla donde se colocarán las variables de decisión.

![Matriz variables](imagenes/solver/transporte/02_matriz_variables_vacia.png)

---

## Paso 3: Definir estructura de la matriz

Organiza filas (orígenes) y columnas (destinos).

![Estructura matriz](imagenes/solver/transporte/03_matriz_variables_con_estructura.png)

---

## Paso 4: Calcular suma por filas (oferta)

Utiliza la función:

[ =SUMA(C12:E12) ]

![Fórmula filas](imagenes/solver/transporte/04_formula_suma_filas.png)

![Resultado filas](imagenes/solver/transporte/05_resultado_suma_filas.png)

---

## Paso 5: Calcular suma por columnas (demanda)

Utiliza la función:

[ =SUMA(C12:C14) ]

![Fórmula columnas](imagenes/solver/transporte/06_formula_suma_columnas.png)

![Resultado columnas](imagenes/solver/transporte/07_resultado_suma_columnas.png)

---

## Paso 6: Definir función objetivo

Utiliza:

[ =SUMAPRODUCTO(C5:E7, C12:E14) ]

![Función objetivo](imagenes/solver/transporte/08_funcion_objetivo_sumaproducto.png)

---

## Paso 7: Abrir Solver

Dirígete a:

**Datos → Solver**

![Abrir solver](imagenes/solver/transporte/09_solver_abrir.png)

---

## Paso 8: Configurar objetivo

- Selecciona la celda del costo total
- Elegir opción **Min**

![Objetivo](imagenes/solver/transporte/10_solver_objetivo_min.png)

---

## Paso 9: Variables de decisión

Selecciona la matriz de variables:

![Variables](imagenes/solver/transporte/11_solver_variables_decision.png)

---

## Paso 10: Restricciones de oferta

Suma de filas = producción 

![Restricción oferta](imagenes/solver/transporte/12_solver_agregar_restricciones.png)

![Restricción oferta](imagenes/solver/transporte/12_solver_agregar_restriccion_oferta.png)

![Restricciones oferta](imagenes/solver/transporte/13_solver_restricciones_oferta.png)

---

## Paso 11: Restricciones de demanda

Suma de columnas = demanda

![Restricción demanda](imagenes/solver/transporte/14_solver_agregar_restriccion_demanda.png)

![Restricciones completas](imagenes/solver/transporte/15_solver_restricciones_completas.png)

---

## Paso 12: Método de solución

Selecciona:

**Simplex LP**

![Método](imagenes/solver/transporte/16_solver_metodo_simplex.png)

---

## Paso 13: Ejecutar Solver

![Ejecutar](imagenes/solver/transporte/17_solver_ejecutar.png)

---

## Paso 14: Resultado

![Resultado solver](imagenes/solver/transporte/18_solver_resultado.png)

---

## Paso 15: Valor óptimo

![Tabla final](imagenes/solver/transporte/19_solucion_tabla_final.png)

---

## Interpretación

La solución indica cuántas unidades deben enviarse desde cada origen hacia cada destino para minimizar el costo total de transporte.

El valor óptimo representa el costo mínimo total.

---

> [!NOTE]
> El modelo de transporte es un caso especial de programación lineal altamente eficiente para problemas de distribución.

> [!IMPORTANT]
> Es necesario que la suma de oferta sea igual a la suma de demanda para garantizar solución factible.

> [!WARNING]
> Errores en las restricciones pueden generar soluciones incorrectas o problemas sin solución.
