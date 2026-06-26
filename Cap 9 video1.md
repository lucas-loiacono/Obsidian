Me dan datos y busco las distribuciones de los resultados

Inferencia: construir un modelo sobre la base de datos experimentales y extraer concluciones 
Poblacion: totalidad de los resultados experimentales posibles
Muestra: conjunto de datos que se obtiene al realizar el experimento una cierta candtidad de veces





![[Pasted image 20260625205902.png]]




![[Pasted image 20260625211538.png]]




### 1. La Muestra Aleatoria Teórica ($\underline{X}$)

$$\underline{X} = (X_1, \dots, X_n)$$

- **¿Qué es?** Es el vector que representa tu **plan de experimentación**, antes de ejecutarlo.
    
- **Sus componentes:** Cada $X_i$ es una Variable Aleatoria ("Observable"). Como el experimento todavía no se hizo, no sabés qué valor van a tomar, por eso son incógnitas (mayúsculas).
    
- **La regla fundamental ($iid \sim X$):** Significa que todas las variables $X_1 \dots X_n$ son **Independientes** entre sí e **Idénticamente Distribuidas** respecto a la variable poblacional $X$. Básicamente, todas siguen las mismas reglas matemáticas que el fenómeno original que estás estudiando.
    
- **Analogía en código:** Es como declarar un arreglo de $n$ posiciones donde cada elemento es la llamada a una función, pero **antes** de correr el script. Sabés qué tipo de dato va a devolver, pero aún no tenés los valores empíricos.
    


```Python
   # Muestra teórica (Variables)
   X = [ejecutar_query(), ejecutar_query(), ejecutar_query()]
```
   

### 2. La Muestra Observada ($\underline{x}$)

$$\underline{x} = (x_1, \dots, x_n)$$

- **¿Qué es?** Son las $n$ **observaciones reales** obtenidas luego de realizar las $n$ repeticiones independientes del experimento.
    
- **Sus componentes:** Al pasar a minúsculas ($x_i$), la matemática te indica que la aleatoriedad desapareció. Ya no son variables, son **datos concretos y constantes** (números reales).
    
- **Analogía en código:** Es el estado de la memoria una vez que el script terminó de ejecutarse. Las funciones ya devolvieron sus resultados y ahora tenés un arreglo de números (enteros o flotantes) fijos.





```Python
  # Muestra observada (Datos reales)
   x = [15.2, 12.8, 14.1]
```


### Ejemplo Práctico: Lanzamiento de Dados ($n = 6$)

Si decidís tirar un dado 6 veces, tu muestra tiene un tamaño de $n = 6$. Así se diferencian los dos vectores de la teoría:

#### 1. La Muestra Teórica ($\underline{X}$)

Es tu plan **antes de tirar los dados**. Sabés que vas a hacer 6 repeticiones independientes, pero no sabés qué va a salir.

$$\underline{X} = (X_1, X_2, X_3, X_4, X_5, X_6)$$

- Cada $X_i$ representa "el número que **va a salir** en la tirada $i$".
    
- Son **Variables Aleatorias** (por eso van en mayúscula). Siguen siendo una incógnita.
    

#### 2. La Muestra Observada ($\underline{x}$)

Agarrás los dados, los tirás y anotás los resultados concretos. Supongamos que salió: 5, 2, 6, 1, 4, 2.

$$\underline{x} = (x_1, x_2, x_3, x_4, x_5, x_6) = (5, 2, 6, 1, 4, 2)$$

- Al pasar a minúsculas, se convierten en tus **observaciones reales**.
    
- Cada $x_i$ es el número que **efectivamente salió**. La aleatoriedad desapareció; ahora son constantes empíricas listas para ser analizadas.



## La Distribución Conjunta: De la Intersección a la Multiplicación

Cuando tomamos una muestra aleatoria de tamaño $n$, no nos importa solo lo que pasa con un elemento aislado, sino que queremos saber **la probabilidad de que toda la muestra ocurra exactamente como ocurrió**.

Para eso usamos la Función de Distribución Conjunta.

### 1. Las Comas son Intersecciones (El "AND" lógico)

En la fórmula, vas a ver que las probabilidades están separadas por comas:

$$P(X_1 \le x_1, \dots, X_n \le x_n)$$

- **¿Qué significa?** Esas comas representan la **intersección** ($\cap$) de eventos.
    
- Así como en la lógica de programación un `and` requiere que _todas_ las condiciones se cumplan simultáneamente para que el resultado sea verdadero, acá estamos calculando la probabilidad de que el primer dato sea menor a $x_1$ **Y** el segundo sea menor a $x_2$ **Y** el tercero a $x_3$, todo al mismo tiempo.
    

### 2. La Magia de la Independencia (iid)

Calcular la probabilidad de intersecciones gigantes es matemáticamente un infierno... a menos que los eventos sean **independientes**.

Acá entra en juego la regla de oro de tu muestra: como sabemos que cada repetición del experimento es independiente de las demás (por ser **iid**), la teoría de probabilidades nos da un atajo. **La probabilidad de la intersección de eventos independientes es igual a la multiplicación de sus probabilidades individuales.**

- _Recordatorio:_ $P(A \cap B) = P(A) \cdot P(B)$
    

### 3. La Productoria Final (La fórmula de tu apunte)

Como todas tus variables $X_i$ siguen exactamente la misma distribución que tu población original $X$, podés reemplazar la probabilidad de cada una por la función $F_X(x_i)$ y multiplicarlas todas juntas usando el símbolo de la productoria ($\prod$):

$$F_{X_1, \dots, X_n}(x_1, \dots, x_n) = P(X_1 \le x_1, \dots, X_n \le x_n) = \prod_{i=1}^n F_X(x_i), \quad \forall n \in \mathbb{N}$$


![[Pasted image 20260625214900.png]]

![[Pasted image 20260625220745.png]]