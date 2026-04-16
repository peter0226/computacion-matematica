# Ejemplo: Modelo de transporte en MATLAB con linprog

En este ejemplo se muestra cómo resolver un modelo de transporte utilizando MATLAB y la función `linprog`.

## Modelo

Minimizar:

Z = 24x11 + 30x12 + 30x13 + 32x21 + 26x22 + 25x23 + 31x31 + 32x32 + 31x33

Sujeto a:

### Restricciones de oferta

x11 + x12 + x13 = 200  
x21 + x22 + x23 = 250  
x31 + x32 + x33 = 450  

### Restricciones de demanda

x11 + x21 + x31 = 150  
x12 + x22 + x32 = 350  
x13 + x23 + x33 = 400  

### Restricciones de no negatividad

xij ≥ 0


## Datos del problema

### Costos de transporte por unidad

| Origen / Destino | Ciudad 1 | Ciudad 2 | Ciudad 3 |
|------------------|----------|----------|----------|
| Granja 1         | 24       | 30       | 30       |
| Granja 2         | 32       | 26       | 25       |
| Granja 3         | 31       | 32       | 31       |

### Oferta

- Granja 1: 200
- Granja 2: 250
- Granja 3: 450

### Demanda

- Ciudad 1: 150
- Ciudad 2: 350
- Ciudad 3: 400

## Paso 1: Crear el archivo de código

Crea un archivo con el nombre:

```bash
matlab_transporte_basico.m
```


## Paso 2: Definir la función objetivo

En MATLAB, la función objetivo se representa mediante un vector con los costos de transporte.

```python
f = [24 30 30 32 26 25 31 32 31];
```

Cada posición corresponde a una variable de decisión:

- x11, x12, x13
- x21, x22, x23
- x31, x32, x33


## Paso 3: Definir las restricciones de oferta

Las restricciones de oferta indican que cada origen debe enviar exactamente la cantidad disponible.

```python 
Aeq_oferta = [  
    1 1 1 0 0 0 0 0 0;  
    0 0 0 1 1 1 0 0 0;  
    0 0 0 0 0 0 1 1 1  
];  

beq_oferta = [  
    200;  
    250;  
    450  
];  
```

## Paso 4: Definir las restricciones de demanda

Las restricciones de demanda indican que cada destino debe recibir exactamente la cantidad requerida.

```python 
Aeq_demanda = [  
    1 0 0 1 0 0 1 0 0;  
    0 1 0 0 1 0 0 1 0;  
    0 0 1 0 0 1 0 0 1  
];  

beq_demanda = [  
    150;  
    350;  
    400  
];  
```

## Paso 5: Unir las restricciones de igualdad

Se integran las restricciones de oferta y demanda en una sola matriz.

```python  
Aeq = [Aeq_oferta; Aeq_demanda];  
beq = [beq_oferta; beq_demanda];  
```

## Paso 6: Definir no negatividad

Se establece que las variables no pueden tomar valores negativos.

```python
lb = zeros(9,1);
```

## Paso 7: Resolver el modelo

En MATLAB, `linprog` se utiliza para resolver problemas de minimización.

```python
x, fval, exitflag = linprog(f, [], [], Aeq, beq, lb, []);
```

## Paso 8: Mostrar resultados

Imprime:

- Estado de salida
- Valor óptimo de Z
- Valores de las variables

```python  
disp('Estado de salida:');  
disp(exitflag);  

disp('Valor óptimo de Z:');  
disp(fval);  

disp('Valores de las variables:');  
disp(['x11 = ', num2str(x(1))]);  
disp(['x12 = ', num2str(x(2))]);  
disp(['x13 = ', num2str(x(3))]);  
disp(['x21 = ', num2str(x(4))]);  
disp(['x22 = ', num2str(x(5))]);  
disp(['x23 = ', num2str(x(6))]);  
disp(['x31 = ', num2str(x(7))]);  
disp(['x32 = ', num2str(x(8))]);  
disp(['x33 = ', num2str(x(9))]);  
```

## Código completo

```python
clc;  
clear;  

% Coeficientes de la función objetivo  
f = [24 30 30 32 26 25 31 32 31];  

% Restricciones de oferta  
Aeq_oferta = [  
    1 1 1 0 0 0 0 0 0;  
    0 0 0 1 1 1 0 0 0;  
    0 0 0 0 0 0 1 1 1  
];  

beq_oferta = [  
    200;  
    250;  
    450  
];  

% Restricciones de demanda  
Aeq_demanda = [  
    1 0 0 1 0 0 1 0 0;  
    0 1 0 0 1 0 0 1 0;  
    0 0 1 0 0 1 0 0 1  
];  

beq_demanda = [  
    150;  
    350;  
    400  
];  

% Unir restricciones de igualdad  
Aeq = [Aeq_oferta; Aeq_demanda];  
beq = [beq_oferta; beq_demanda];  

% No negatividad  
lb = zeros(9,1);  

% Resolver  
[x, fval, exitflag] = linprog(f, [], [], Aeq, beq, lb, []);  

% Mostrar resultados  
disp('Estado de salida:');  
disp(exitflag);  

disp('Valor óptimo de Z:');  
disp(fval);  

disp('Valores de las variables:');  
disp(['x11 = ', num2str(x(1))]);  
disp(['x12 = ', num2str(x(2))]);  
disp(['x13 = ', num2str(x(3))]);  
disp(['x21 = ', num2str(x(4))]);  
disp(['x22 = ', num2str(x(5))]);  
disp(['x23 = ', num2str(x(6))]);  
disp(['x31 = ', num2str(x(7))]);  
disp(['x32 = ', num2str(x(8))]);  
disp(['x33 = ', num2str(x(9))]);  
```

## Resultado esperado

El programa debe mostrar una solución factible con el costo mínimo total y las asignaciones óptimas para cada ruta.


## Interpretación

La solución indica cuántas unidades deben enviarse desde cada origen hacia cada destino para satisfacer la demanda sin exceder la oferta, minimizando el costo total de transporte.


> [!NOTE]
> MATLAB representa este tipo de problemas en forma matricial, lo que facilita trabajar con modelos más grandes.

> [!IMPORTANT]
> Para este tipo de modelo balanceado, las restricciones de oferta y demanda se expresan como igualdades.

> [!WARNING]
> Un error en el orden de las variables dentro del vector de decisión puede alterar completamente la interpretación de la solución.
