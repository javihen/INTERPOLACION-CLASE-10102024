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

Utilizando el polinomio construido, se estima la temperatura para **11,942 ft** que corresponde a la Ciudad de La Paz. El resultado aproximado es:

\[
T(11,942 \text{ ft}) \approx 188.78 \, ^\circ F
\]

Utilizando el polinomio construido, se estima la temperatura para **13,615 ft** que corresponde a la Ciudad de El Alto. El resultado aproximado es:

\[
T(13,615 \text{ ft}) \approx 186.15 \, ^\circ F
\]

Esto se lo puede observar el archivo adjunto con extension XLS (excel)

## 5. Conclusión
Esta técnica es útil para realizar aproximaciones precisas cuando los datos exactos no están disponibles en el conjunto original de mediciones.
La comparación entre los métodos de Newton y Lagrange para interpolación depende de varios factores, como la facilidad de uso, la estabilidad numérica y la precisión.

¿Cuál es mejor en este caso?
Para el problema específico de encontrar 

T(5.000), T(11.942) y T(13,615) usando los datos de la tabla:

Ambos métodos producen el mismo resultado ya que los puntos de interpolación son los mismos.
Si no necesitas recalcular con frecuencia o añadir más datos, el método de Lagrange es probablemente más sencillo de implementar.
Si estás interesado en la eficiencia y quieres ir agregando más puntos al conjunto de datos, el método de Newton sería más adecuado.

Para un conjunto fijo de datos y un solo cálculo, ambos métodos son equivalentes en términos de error. Elige el método que te resulte más cómodo: Lagrange para simplicidad, Newton para eficiencia en modificaciones.
