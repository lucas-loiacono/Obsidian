![[Pasted image 20260906163423.png]]

![[Pasted image 20260906163457.png]]

![[Pasted image 20260906163547.png]]

![[Pasted image 20260906165045.png]]

![[Pasted image 20260906180914.png]]

Lo deja como marcado para que cuando vuelva de hacer la ejecución de la función siga con el código, en ese caso con la edad que tenia en ese momento

![[Pasted image 20260906181225.png]]

![[Pasted image 20260906181643.png]]

aca el else no va, ya que es implicito, no esta escrito


![[Pasted image 20260906181930.png]]


indirecta

![[Pasted image 20260906181842.png]]

![[Pasted image 20260906182116.png]]

anidada

![[Pasted image 20260906182331.png]]

![[Pasted image 20260906183229.png]]

![[Pasted image 20260906183327.png]]

![[Pasted image 20260906183510.png]]

![[Pasted image 20260906193753.png]]

![[Pasted image 20260906184716.png]]

![[Pasted image 20260906184845.png]]

![[Pasted image 20260906185404.png]]

![[Pasted image 20260906185216.png]]

![[Pasted image 20260906193836.png]]

![[Pasted image 20260906194438.png]]

Merge sort
![[Pasted image 20260906203602.png]]

![[Pasted image 20260906203656.png]]

# 🧩 Merge Sort (Ordenamiento por Mezcla)

**Paradigma:** Divide y Vencerás (Recursivo).

**Complejidad de Tiempo:** $O(n \log n)$ en todos los casos (Mejor, Peor y Promedio).

**Complejidad de Espacio:** $O(n)$ (Requiere arreglos auxiliares).

**Estabilidad:** Sí, es estable (mantiene el orden relativo de elementos con valores iguales).

  

## ⚙️ Funcionamiento Lógico

El algoritmo divide el problema en subproblemas más pequeños, los resuelve y luego combina las soluciones. Se divide en dos fases:

  

1. **Fase de División (Divide):**
    
      
    - El vector original se parte a la mitad recursivamente.
        
          
        
    - La recursión se detiene al llegar al **caso base**: subvectores de tamaño 1. (Un arreglo de un solo elemento ya está ordenado por definición).
        
          
        
2. **Fase de Fusión (Merge / Vencerás):**
    
      
    - Se toman dos subvectores adyacentes y se combinan en un nuevo arreglo temporal.
        
          
        
    - Para combinarlos ordenadamente, se utilizan punteros al inicio de cada subvector. Se comparan los elementos y se inserta el menor en el arreglo temporal, avanzando el puntero correspondiente.
        
          
        
    - Este proceso se repite, subiendo por el árbol de llamadas recursivas, hasta reconstruir el tamaño del vector original, ahora completamente ordenado.
        
          
        

## 💡 Notas Clave

- **No es _in-place_:** A diferencia de algoritmos como Insertion Sort o Quick Sort, Merge Sort necesita instanciar memoria extra durante la etapa de fusión para los arreglos temporales.
    
      
    
- **Rendimiento predecible:** Como siempre divide el arreglo a la mitad sin importar cómo vengan los datos inicialmente, su tiempo de ejecución está garantizado en $O(n \log n)$, haciéndolo ideal para estructuras de datos grandes donde el peor caso de Quick Sort ($O(n^2)$) sería un riesgo.




**Vector inicial a ordenar:** `[38, 27, 43, 3, 9, 82, 10, 19]`

  

**Fase 1: División**

El vector original se divide exactamente por la mitad de forma sucesiva. En esta etapa no hay comparaciones ni ordenamiento, solo partición.

  

- **1° División (Mitades):**
    
    `[38, 27, 43, 3]` y `[9, 82, 10, 19]`
    
      
    
- **2° División (Cuartos):**
    
    `[38, 27]` , `[43, 3]` , `[9, 82]` , `[10, 19]`
    
      
    
- **3° División (Octavos - Caso base):**
    
    `[38]` , `[27]` , `[43]` , `[3]` , `[9]` , `[82]` , `[10]` , `[19]`
    
      
    

**Fase 2: Fusión (Merge)**

Al llegar a los elementos individuales, el algoritmo comienza a retroceder. Toma dos subvectores adyacentes, compara sus elementos uno a uno y los unifica en un nuevo arreglo temporal ordenado.

  

- **1° Fusión (Subvectores de 2 elementos):**
    
    El `38` y el `27` se comparan y se invierten. Lo mismo con el `43` y el `3`.
    
    `[27, 38]` , `[3, 43]` , `[9, 82]` , `[10, 19]`
    
      
    
- **2° Fusión (Subvectores de 4 elementos):**
    
    Se comparan los subvectores `[27, 38]` y `[3, 43]`. El `3` es el menor de todos, luego el `27`, luego el `38` y por último el `43`.
    
    `[3, 27, 38, 43]` , `[9, 10, 19, 82]`
    
      
    
- **3° Fusión (Vector final de 8 elementos):**
    
    Se comparan los dos bloques restantes agrupándolos secuencialmente de menor a mayor.
    
    `[3, 9, 10, 19, 27, 38, 43, 82]`



![[Pasted image 20260906204510.png]]

![[Pasted image 20260906204526.png]]

![[Pasted image 20260906204635.png]]

![[Pasted image 20260906205432.png]]


![[Pasted image 20260906205652.png]]


La imagen **image_25241c.jpg** es un ejemplo perfecto para contrastar diferentes algoritmos que resuelven un mismo problema (calcular $2^{64}$) y demuestra el impacto masivo que tiene aplicar el paradigma de "Divide y Vencerás" que vimos recién con Merge Sort.

  

Aquí tienes el desglose de los tres enfoques que muestra la diapositiva:

  

- **Enfoque Iterativo (Arriba a la izquierda):**
    
    Utiliza un bucle `for` clásico que multiplica la base por sí misma paso a paso. Para llegar a $2^{64}$, el ciclo se ejecuta **64 veces**. Su tiempo de ejecución crece a la misma velocidad que el exponente (complejidad lineal $O(n)$).
    
      
    
- **Enfoque Recursivo Simple (Arriba a la derecha):**
    
    Plantea la solución llamándose a sí mismo restando de a 1 (`exponente - 1`). Aunque evita el ciclo `for`, requiere apilar **64 llamadas recursivas** en memoria hasta llegar al caso base. Es tan ineficiente en tiempo como el iterativo ($O(n)$), pero con el riesgo adicional de desbordar la pila de llamadas (Stack Overflow) con números muy grandes.
    
      
    
- **Enfoque Divide y Vencerás / Exponenciación Rápida (Abajo):**
    
    Aquí entra la optimización logarítmica. En lugar de restar 1, el algoritmo **divide el problema a la mitad** en cada paso (`exponente / 2`). Al calcular la potencia de la mitad y luego multiplicarla por sí misma (`resultado *= resultado`), el número de operaciones se desploma. Como muestra el gráfico, para llegar a $64$, solo necesita **6 llamadas recursivas** ($32 \rightarrow 16 \rightarrow 8 \rightarrow 4 \rightarrow 2 \rightarrow 1$).
    
      
    

Este último algoritmo reduce drásticamente el costo computacional llevándolo a $O(\log n)$, demostrando que pensar el problema fraccionándolo en mitades es inmensamente superior a procesarlo de forma secuencial.








![[Pasted image 20260906211630.png]]

![[Pasted image 20260906211642.png]]


Imagina que tienes que calcular $2^8$.

  

El enfoque tradicional haría $2 \times 2 \times 2 \times 2 \times 2 \times 2 \times 2 \times 2$ (siete operaciones). El enfoque de "Divide y Vencerás" (Exponenciación Rápida) usa la lógica de que $2^8$ es exactamente lo mismo que $(2^4) \times (2^4)$. Si calculas $2^4$ una sola vez, solo tienes que multiplicar ese resultado por sí mismo. Te ahorraste procesar la otra mitad por completo.

  

Así es como avanza paso a paso el código de la tercera imagen para calcular **$2^8$**:

  

- **Fase 1: Dividir hacia abajo (Llamadas recursivas)**
    
    El algoritmo busca achicar el problema dividiendo el exponente por la mitad (`exponente / 2`) antes de hacer cualquier cuenta.
    
      
    - Para calcular `potencia(2, 8)`, pausa y llama a `potencia(2, 4)`.
        
          
        
    - Para calcular `potencia(2, 4)`, pausa y llama a `potencia(2, 2)`.
        
          
        
    - Para calcular `potencia(2, 2)`, pausa y llama a `potencia(2, 1)`.
        
          
        
    - Al llegar a `potencia(2, 1)`, el código detecta el caso base (`else if (exponente == 1)`) y directamente devuelve un **2**. No divide más.
        
          
        
- **Fase 2: Vencer hacia arriba (Reconstrucción)**
    
    Ahora el algoritmo desanda el camino, usando la instrucción `resultado *= resultado` (multiplicar el resultado por sí mismo).
    
      
    - **Vuelve a `potencia(2, 2)`:** Toma el **2** que recibió de abajo y lo eleva al cuadrado ($2 \times 2 = 4$). Devuelve **4**.
        
          
        
    - **Vuelve a `potencia(2, 4)`:** Toma el **4** que recibió de abajo y lo eleva al cuadrado ($4 \times 4 = 16$). Devuelve **16**.
        
          
        
    - **Vuelve a `potencia(2, 8)`:** Toma el **16** que recibió de abajo y lo eleva al cuadrado ($16 \times 16 = 256$). Devuelve el resultado final: **256**.
        
          
        

**El caso de los exponentes impares**

Si quisieras calcular **$2^5$**, el código divide $5 / 2$, lo que en programación da $2$ (división entera). El algoritmo calcula $2^2$ (que da $4$) y luego lo multiplica por sí mismo dando $16$ ($2^4$).

Para que no falte ese último "por dos", el código tiene una validación final: `if ((exponente % 2) == 1)`. Al detectar que el 5 era impar, hace una multiplicación extra por la base original: $16 \times 2 = 32$.

  

En resumen, resolver el problema dividiéndolo te permite reciclar los resultados anteriores en lugar de calcular todo desde cero una y otra vez. Por eso en la imagen, calcular $2^{64}$ solo toma 6 llamadas en lugar de 64.



![[Pasted image 20260906211708.png]]

![[Pasted image 20260906211725.png]]


El fragmento de código de la **image_2f2f28.png** intenta ser la versión **iterativa** del algoritmo de exponenciación rápida (Divide y Vencerás). Su objetivo es alcanzar una eficiencia de $O(\log n)$ sin apilar llamadas recursivas, dividiendo el contador de operaciones a la mitad en cada ciclo (`i /= 2`) mediante un bucle `for`.

  

Para entender cómo avanza la lógica planteada, hagamos una prueba de escritorio calculando $2^4$ (`base = 2`, `exponente = 4`):

  

1. Se inicializa `resultado = 2`.
    
      
    
2. El bucle `for` arranca la variable de control con `i = 3` (exponente - 1).
    
      
    
3. **Primera iteración (`i = 3`):** Se evalúa la condición `(exponente % 2) == 1`. Como `4 % 2` da como resto `0` (falso), ignora el `if`. Luego hace `resultado *= resultado` (calcula $2 \times 2 = 4$).
    
      
    
4. El bucle actualiza `i /= 2` (división entera: $3 / 2 = 1$).
    
      
    
5. **Segunda iteración (`i = 1`):** La condición `4 % 2 == 1` sigue siendo falsa. El algoritmo hace `resultado *= resultado` (calcula $4 \times 4 = 16$).
    
      
    
6. El bucle actualiza `i /= 2` ($1 / 2 = 0$). Como la condición `i > 0` ya no se cumple, el ciclo se rompe.
    
      
    
7. Devuelve `16`.
    
      
    

Para potencias pares, el avance fraccionado funciona y devuelve el resultado esperado. Ahora veamos qué ocurre con el avance para una potencia impar, por ejemplo $2^3$ (`base = 2`, `exponente = 3`):

  

1. Se inicializa `resultado = 2`.
    
      
    
2. El bucle arranca con `i = 2` (exponente - 1).
    
      
    
3. **Primera iteración (`i = 2`):** Se evalúa la condición `(exponente % 2) == 1`. Como `3 % 2` es `1` (verdadero), entra al `if` y multiplica `resultado *= base` ($2 \times 2 = 4$). Inmediatamente después, fuera del `if`, el código hace `resultado *= resultado` ($4 \times 4 = 16$).
    
      
    
4. El bucle actualiza `i /= 2` ($2 / 2 = 1$).
    
      
    
5. **Segunda iteración (`i = 1`):** Vuelve a evaluar `(exponente % 2) == 1`. Como la variable `exponente` es estática y nunca se modificó en el bucle, **sigue valiendo 3, por lo que la condición vuelve a dar verdadero**. Entra al `if`, hace `resultado *= base` ($16 \times 2 = 32$) y luego `resultado *= resultado` ($32 \times 32 = 1024$).
    
      
    
6. El bucle actualiza `i = 0`, termina y devuelve `1024`.
    
      
    

Como demuestra el cálculo paso a paso, el algoritmo contiene un error lógico grave (bug). Al evaluar el `exponente` original en el `if` en lugar de verificar el bit correspondiente o actualizar la variable en cada iteración, cualquier cálculo con un exponente impar provocará que el resultado se dispare descontroladamente, arrojando valores completamente erróneos.

![[Pasted image 20260906212355.png]]

ordenamiento por pivote


![[Pasted image 20260906214045.png]]


![[Pasted image 20260906214014.png]]

y después uno por pivote