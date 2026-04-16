# Ejemplo: Programación lineal básica en MATLAB con linprog

En este ejemplo se muestra cómo resolver un problema de programación lineal en MATLAB utilizando la función `linprog`.

## Modelo matemático

Maximizar:

Z = 10X + 8Y

Sujeto a:

30X + 20Y ≤ 120  
2X + 2Y ≤ 9  
4X + 6Y ≤ 24  

X, Y ≥ 0


## Paso 1: Crear el archivo de código

Crea un archivo con el nombre:

```text
matlab_linprog_basico.m
```

## Paso 2: Definir la función objetivo
En MATLAB, linprog resuelve problemas de minimización.
Por ello, para maximizar la función objetivo, se cambian de signo sus coeficientes.

```matlab
f = [-10 -8];
```

## Paso 3: Definir las restricciones
Las restricciones se escriben en forma matricial como:
A * x ≤ b
```matlab
A = [
    30 20;
    2  2;
    4  6
];

b = [
    120;
    9;
    24
];
```

## Paso 4: Definir la no negatividad
Se indica que las variables no pueden tomar valores negativos.
```matlab
lb = [0 0];
```

## Paso 5: Resolver el modelo
```matlab
[x, fval, exitflag] = linprog(f, A, b, [], [], lb, []);
```

## Paso 6: Mostrar resultados
```matlab
disp('Estado de salida:');
disp(exitflag);

disp('Valores óptimos de las variables:');
disp(['X = ', num2str(x(1))]);
disp(['Y = ', num2str(x(2))]);

disp('Valor óptimo de Z:');
disp(-fval);
```
> [!NOTE]
> MATLAB utiliza el formato matricial para trabajar con programación lineal, lo cual facilita la resolución de modelos más grandes.

> [!IMPORTANT]
> Para resolver problemas de maximización con linprog, recuerda cambiar el signo de la función objetivo.

> [!WARNING]
> Si las restricciones no están en la forma correcta, MATLAB puede devolver una solución errónea o indicar que el problema no es factible.

