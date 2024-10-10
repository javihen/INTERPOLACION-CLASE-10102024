# Cálculo de \( T(5.000) \) utilizando interpolación de Newton

## Introducción
El objetivo es calcular el valor de \( T \) a una altura de \( h = 5.000 \) metros, usando interpolación de Newton, basada en la siguiente tabla de valores:

| \( h(m) \)  | \( T(F) \)  |
|-------------|-------------|
| -0.305      | 213.9       |
| 0.000       | 212.0       |
| 0.914       | 206.2       |
| 2.438       | 196.2       |
| 4.572       | 184.4       |
| 6.706       | 172.6       |
| 8.534       | 163.1       |

## 1. Concepto de interpolación de Newton
La interpolación de Newton es una técnica que permite estimar el valor de una función en un punto no presente en los datos conocidos, utilizando una serie de términos llamados **diferencias divididas**.

La fórmula general para el polinomio de Newton es:

\[
P(x) = f(x_0) + (x - x_0) f[x_0, x_1] + (x - x_0)(x - x_1) f[x_0, x_1, x_2] + \dots
\]

Donde:
- \( f[x_0, x_1, \dots] \) son las **diferencias divididas**, que representan los coeficientes del polinomio.
  
## 2. Cálculo de las diferencias divididas
Para calcular las diferencias divididas, utilizamos la siguiente fórmula para la primera orden:

\[
f[x_i, x_{i+1}] = \frac{f(x_{i+1}) - f(x_i)}{x_{i+1} - x_i}
\]

Luego, para diferencias de mayor orden:

\[
f[x_i, x_{i+1}, x_{i+2}] = \frac{f[x_{i+1}, x_{i+2}] - f[x_i, x_{i+1}]}{x_{i+2} - x_i}
\]

Se procede de forma iterativa hasta el orden máximo que corresponde al número de puntos en la tabla.

### Tabla de diferencias divididas:

| \( h(m) \)  | \( T(F) \)  | \( f[x_0, x_1] \) | \( f[x_0, x_1, x_2] \) | \( f[x_0, x_1, x_2, x_3] \) | \( f[x_0, x_1, x_2, x_3, x_4] \) | \( f[x_0, x_1, x_2, x_3, x_4, x_5] \) |
|-------------|-------------|-------------------|-------------------------|-----------------------------|-----------------------------------|-------------------------------------|
| -0.305      | 213.9       | -6.2295           | -0.0953                 | 0.0025                      | 0.0161                            | -0.0051                            |
| 0.000       | 212.0       | -6.3457           | -0.0886                 | 0.0811                      | -0.0194                           | 0.00323                            |
| 0.914       | 206.2       | -6.5617           | 0.2822                  | -0.0487                     | 0.00820                           |                                     |
| 2.438       | 196.2       | -5.5295           | -0.0000                 | 0.0138                      |                                   |                                     |
| 4.572       | 184.4       | -5.5295           | 0.0839                  |                             |                                   |                                     |
| 6.706       | 172.6       | -5.1969           |                         |                             |                                   |                                     |
| 8.534       | 163.1       |                   |                         |                             |                                   |                                     |

## 3. Polinomio de interpolación de Newton
Con los coeficientes calculados en la tabla de diferencias divididas, el polinomio de Newton que resulta es:

\[
P(x) = 213.9000 - 6.2295(x + 0.305) - 0.0953(x)(x - 0.914) + 0.0025(x)(x - 0.914)(x - 2.438) 
\]
\[
+ 0.0161(x)(x - 0.914)(x - 2.438)(x - 4.572) - 0.0051(x)(x - 0.914)(x - 2.438)(x - 4.572)(x - 6.706) 
\]
\[
+ 0.0009(x)(x - 0.914)(x - 2.438)(x - 4.572)(x - 6.706)(x - 8.534)
\]

## 4. Evaluación en \( h = 5.000 \)
Finalmente, evaluamos el polinomio en \( h = 5.000 \):

\[
P(5.000) = 182.28 \, \text{F}
\]

## 5. Conclusión
El valor estimado de la temperatura \( T(5.000) \) usando interpolación de Newton es **182.28°F**. Esta técnica es útil para realizar aproximaciones precisas cuando los datos exactos no están disponibles en el conjunto original de mediciones.
