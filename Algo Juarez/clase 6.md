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