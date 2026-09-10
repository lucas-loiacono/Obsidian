![[Pasted image 20260909223042.png]]

![[Pasted image 20260909223059.png]]

![[Pasted image 20260909223112.png]]

El álgebra de Boole es la base matemática que permite que funcionen las computadoras y los sistemas digitales. A diferencia del álgebra tradicional donde utilizás infinitos números, en este sistema **solo existen dos valores: el 0 y el 1** (que representan estados como apagado/encendido o falso/verdadero).


Como se detalla en `image_ed6d0c.png`, esta álgebra se construye sobre un conjunto muy reducido de elementos y tres operadores fundamentales que luego vas a traducir físicamente en circuitos:


- **Producto Lógico (AND / `*`):** Funciona como una conjunción o intersección. Para que el resultado sea 1, **todos** los elementos operados deben ser 1. Si hay un solo 0, todo el resultado es 0.
    
- **Suma Lógica (OR / `+`):** Funciona como una disyunción o unión. Para que el resultado sea 1, alcanza con que **al menos uno** de los elementos sea 1. Solo da 0 si absolutamente todos los valores son 0.
    
- **Complemento (NOT / `~` o `'`):** Es la inversión o negación. Simplemente da vuelta el estado actual: lo que es 0 pasa a ser 1, y lo que es 1 pasa a ser 0.

Un concepto central que te va a ahorrar mucho trabajo es el **Principio de Dualidad**. Esta regla establece que cualquier ecuación, identidad o ley que demuestres en este sistema tiene una versión "espejo" que también es matemáticamente válida. Para obtener esa ley dual, simplemente tenés que intercambiar todas las sumas (`+`) por multiplicaciones (`*`) y todos los ceros (`0`) por unos (`1`), y viceversa.


El motivo por el cual estudiás esto, tal como marcan los objetivos en `image_ed6d46.png`, es porque estas funciones lógicas abstractas son la herramienta principal para describir cómo se comportan los circuitos elementales (las compuertas lógicas). Al dominar esta matemática, vas a poder analizar, diseñar y simplificar los bloques que construyen la arquitectura de cualquier computadora.




Lo que el principio te dice es que **si una regla matemática es verdadera, su versión "espejo" es otra regla que también es verdadera**. Son dos leyes distintas que describen operaciones distintas, pero ambas son válidas dentro del sistema.


Fijate con este ejemplo súper básico:


- **Regla original:** $A + 0 = A$ (Si a cualquier variable le sumás 0, te queda esa misma variable).
    
- **Aplicamos dualidad:** Cambiamos el `+` por `*`, y el `0` por `1`.
    
- **Regla dual:** $A * 1 = A$ (Si a cualquier variable la multiplicás por 1, te queda esa misma variable).
    

Las dos ecuaciones son verdades absolutas, pero una te habla del comportamiento de la suma (unión) y la otra del producto (intersección).

  

La gran ventaja de esto es que funciona como un "2x1" matemático: si el día de mañana lográs demostrar que una ley compleja para reducir circuitos es válida, automáticamente sabés que su versión dual también va a funcionar, ahorrándote el trabajo de tener que demostrarla desde cero.




## Yo

osea si es verdadera la primera, tengo que comprobar que la dual tambien sea

## Gemini


No, ¡justamente al revés! La magia de este principio es que **no tenés que comprobar la segunda**.

Si vos ya sabés (o ya demostraste paso a paso) que la primera ecuación es verdadera, el Principio de Dualidad te garantiza que su versión "espejo" es **automáticamente verdadera**.

No hace falta hacer ninguna demostración matemática extra para validar la dual. Por eso funciona como un "2x1": te matás demostrando una sola ecuación y, de regalo, te llevás otra ley totalmente válida para usar en tus circuitos.

![[Pasted image 20260909223123.png]]

**1. El Vocabulario (Diapositiva 4)**

- **Magnitud y Variable:** La magnitud es el estado real (`0` o `1`), y la variable es la letra abstracta que usás para representarlo (como $A$, $B$, $C$).
    
- **Complemento:** Es la negación (el NOT). Acá te introducen la notación más común que vas a usar al diseñar circuitos: en vez de un apóstrofo, se le pone una línea arriba a la variable ($\bar{A}$).
    
- **Literal:** Esta es una distinción importante. Una "variable" es la letra base (por ejemplo, $A$). Un "literal" es cualquier aparición de esa variable en una ecuación, ya sea en su forma normal ($A$) o complementada ($\bar{A}$).

![[Pasted image 20260909223133.png]]

![[Pasted image 20260909223144.png]]

![[Pasted image 20260909223157.png]]

![[Pasted image 20260909223210.png]]

Para entender estos teoremas sin memorizarlos de memoria, lo mejor es pensarlos como condiciones lógicas puras (imaginate que estás evaluando condiciones dentro de un `if` al programar, donde `1` es `True` y `0` es `False`):

  

- **T2) Existencia de elementos nulos:**
    
      
    - **Suma ($A + 1 = 1$):** El operador OR (`+`) busca que _al menos una_ condición sea verdadera. Si yo te digo "Te apruebo la materia si hacés el trabajo práctico ($A$) **O** si me llamo Guillermo ($1$, una verdad absoluta)", la condición entera ya es verdadera. No me importa qué valor tenga $A$ (si hiciste el trabajo o no), porque el $1$ ya forzó que toda la suma sea `True`.
        
          
        
    - **Producto ($A \bullet 0 = 0$):** El operador AND (`*`) es estricto y exige que _todas_ las condiciones se cumplan. Si te digo "Te apruebo si hacés el trabajo ($A$) **Y** si los cerdos vuelan ($0$, falso)", es imposible que apruebes. La presencia de un solo $0$ destruye cualquier cadena de multiplicaciones.
        
          
        
- **T3) Involución ($\bar{\bar{A}} = A$):**
    
    Es la lógica pura de la doble negación que usamos al hablar. Si yo digo "No es cierto que no tengo hambre", lógicamente significa que sí tengo hambre. Si a un valor `True` le aplicás un `not` pasa a `False`, y si le aplicás otro `not`, vuelve a `True`.
    
      
    
- **T4) Absorción:** Esta es la regla dorada para eliminar código o compuertas redundantes.
    
      
    - **$A + A \bullet B = A$:** Imaginate este requisito: "Podés entrar al recital si traés tu entrada ($A$) **O** si (traés tu entrada ($A$) **Y** venís con un amigo ($B$))". Analizalo lógicamente: si tenés la entrada ($A=1$), entrás por la primera regla. Si no tenés la entrada ($A=0$), la segunda regla tampoco te sirve porque te exige la entrada. En definitiva, que vengas con el amigo ($B$) es un dato completamente inútil. La ecuación "absorbe" a $B$ y la descarta, porque todo depende exclusivamente de $A$.
        
          
        
- **T5) Asociatividad:**
    
    Significa que el orden en que agrupás evaluaciones lógicas idénticas no cambia el resultado. Si para un alta de usuario exijo "Mail válido ($A$) Y Contraseña fuerte ($B$) Y Mayor de edad ($C$)", da exactamente lo mismo si mi sistema primero verifica $(A \bullet B)$ y luego $C$, o si arranca por $(B \bullet C)$ y luego $A$. El rigor es el mismo. _Ojo: esto solo vale si todos los operadores son exactamente iguales (todas sumas o todos productos)._
    
      
    
- **T6) Leyes de De Morgan:**
    
    Llevémoslo a sentencias de la vida cotidiana para entender por qué los operadores se invierten.
    
      
    - **T6a ($\overline{A + B} = \bar{A} * \bar{B}$):** Imaginate que afirmo: _"Es mentira que voy a comer pizza o hamburguesa"_ ($\overline{A+B}$). ¿Qué significa esto lógicamente? Significa que _"NO voy a comer pizza"_ **Y** _"NO voy a comer hamburguesa"_ ($\bar{A} * \bar{B}$).
        
          
        
    - **T6b ($\overline{A * B} = \bar{A} + \bar{B}$):** Ahora imaginate que afirmo: _"Es mentira que tengo un auto y una moto"_ ($\overline{A*B}$). Para que mi mentira sea cierta, no hace falta que no tenga ninguno de los dos; simplemente alcanza con que _"NO tenga auto"_ **O** _"NO tenga moto"_ ($\bar{A} + \bar{B}$). Al fallar uno solo, la afirmación original ya era mentira.


![[Pasted image 20260909223228.png]]

![[Pasted image 20260909223245.png]]

![[Pasted image 20260909223255.png]]

![[Pasted image 20260909223307.png]]

Esta imagen (`image_f9afc9.png`) aísla la parte teórica de la diapositiva que vimos recién, definiendo las reglas de juego para empezar a diseñar circuitos reales a partir de ecuaciones.

  

Vamos a desglosar los cuatro conceptos:

  

- **Función Lógica:** Es simplemente la ecuación matemática que describe qué va a hacer tu circuito. Representa el resultado final (la salida) basándose en las variables de entrada que le des.
    
      
    
- **Equivalencia de Funciones Lógicas:** Este es el motivo por el cual estudiaste todos los teoremas anteriores. Podés tener un circuito con 50 compuertas y otro con solo 3; si al probar todas las combinaciones posibles de ceros y unos en sus entradas ambos devuelven exactamente los mismos resultados, **tienen la misma tabla de verdad**. Por lo tanto, son funciones equivalentes. El objetivo siempre va a ser encontrar la función equivalente más barata y chica posible.
    
      
    
- **Minitérmino y Maxitérmino:** La regla de oro acá es que en estos términos **tienen que aparecer absolutamente todas las variables** del sistema. Si tu circuito depende de $A$, $B$ y $C$:
    
      
    - Un **minitérmino** es una multiplicación que incluye a las tres (ej: $A \cdot \bar{B} \cdot C$).
        
          
        
    - Un **maxitérmino** es una suma que incluye a las tres (ej: $A + \bar{B} + C$).
        
        Como cada variable tiene solo 2 estados posibles ($0$ o $1$), la cantidad de combinaciones (y por ende, la cantidad máxima de minitérminos o maxitérminos que vas a tener en tu tabla) siempre se calcula como $2^n$, donde $n$ es la cantidad de variables.
        
          
        
- **Redundancia (Condiciones "No importa"):** Este es un concepto que te va a salvar la vida cuando quieras simplificar circuitos complejos. A veces, hay combinaciones de entrada que son imposibles en el mundo real. Por ejemplo, si un sensor mide el estado de una puerta, la puerta no puede estar "abierta" y "cerrada" exactamente al mismo tiempo. Como esa combinación nunca va a ocurrir, el valor que devuelva tu circuito para ese caso específico **no está definido ni nos interesa**. Estas redundancias (conocidas en la bibliografía como _Don't Cares_) se usan como comodines a tu favor para achicar aún más las ecuaciones.

![[Pasted image 20260909223317.png]]

Esta diapositiva (`image_f9b70d.png`) te muestra exactamente cómo pasar del comportamiento deseado (la tabla de verdad) a una ecuación matemática concreta para armar el circuito.

  

Para lograr esto, se usan las **Funciones Canónicas**, que son formas universales y estandarizadas de escribir la ecuación basándote directamente en los resultados de la tabla. Tenés dos caminos para hacerlo:

  

- **Forma Normal Disyuntiva (Suma de Productos - SPm):** Vas a la columna de salida ($Z$) y te fijás **únicamente en las filas que dan $1$**. Para cada una de esas filas armás un minitérmino (multiplicando las entradas) y al final sumás todos esos bloques.
    
      
    
- **Forma Normal Conjuntiva (Producto de Sumas - PSM):** Hacés el proceso inverso. Buscás las filas donde **$Z$ da $0$**. Armás un maxitérmino para cada una (sumando las entradas) y al final multiplicás todos los bloques entre sí.
    
      
    

**El ejemplo de la lámpara paso a paso**

Tenés 3 variables: Llave $A$, Puerta $B$ y Ventana $C$. Como la fórmula para saber la cantidad de combinaciones es $2^n$, el cuadro se arma con $2^3 = 8$ filas.

  

La regla lógica que te dan es $Z = A + B \cdot C$. Si mirás la columna $Z$, el resultado es $1$ (lámpara encendida) en estos casos específicos:

  

1. Cuando $B$ y $C$ valen $1$ al mismo tiempo (fila 011).
    
      
    
2. Cuando $A$ vale $1$, sin importar qué pase con el resto (las últimas 4 filas de la tabla: 100, 101, 110, 111).
    
      
    

**¿Por qué está resaltado en amarillo "(¿pero es la mínima?)"?**

Esta es la pregunta que define el resto de la materia. Si vos armás la función canónica guiándote por los cinco $1$s de esa tabla, te va a quedar una ecuación original gigantesca con 5 minitérminos sumados. Construir un circuito literal con esa ecuación enorme es carísimo y ocupa muchísimo espacio físico.

  

Justamente por eso aprendiste todos los postulados y teoremas anteriores (y los mapas de Karnaugh que seguro vas a ver pronto): el objetivo es agarrar esa función canónica monstruosa y simplificarla algebraicamente hasta llegar a su mínima expresión posible, que en este caso es el simple y elegante $Z = A + B \cdot C$.


Vamos a armar las dos ecuaciones paso a paso usando la tabla de verdad de la diapositiva para que veas cómo se construyen en la práctica.

  

La regla de oro antes de empezar:

  

- Para los **minitérminos** (buscando los `1`), la variable normal vale `1` y la negada vale `0`.
    
      
    
- Para los **maxitérminos** (buscando los `0`), la lógica se invierte: la variable normal vale `0` y la negada vale `1`.
    
      
    

### 1. Forma Normal Disyuntiva (Suma de Productos / SPm)

Acá nos interesan **únicamente las filas donde $Z = 1$**. Si mirás la tabla, son las últimas 5 filas. Para cada una, armamos un minitérmino multiplicando las variables ($A \cdot B \cdot C$):

  

- Fila (0, 1, 1) $\rightarrow$ La $A$ es $0$, así que va negada. Queda: **$\bar{A} \cdot B \cdot C$**
    
      
    
- Fila (1, 0, 0) $\rightarrow$ La $B$ y la $C$ son $0$, van negadas. Queda: **$A \cdot \bar{B} \cdot \bar{C}$**
    
      
    
- Fila (1, 0, 1) $\rightarrow$ La $B$ es $0$, va negada. Queda: **$A \cdot \bar{B} \cdot C$**
    
      
    
- Fila (1, 1, 0) $\rightarrow$ La $C$ es $0$, va negada. Queda: **$A \cdot B \cdot \bar{C}$**
    
      
    
- Fila (1, 1, 1) $\rightarrow$ Todas son $1$, ninguna va negada. Queda: **$A \cdot B \cdot C$**
    
      
    

Ahora, la "Forma Normal Disyuntiva" se arma sumando todos esos bloquecitos que acabamos de conseguir:

**$Z = (\bar{A} \cdot B \cdot C) + (A \cdot \bar{B} \cdot \bar{C}) + (A \cdot \bar{B} \cdot C) + (A \cdot B \cdot \bar{C}) + (A \cdot B \cdot C)$**

  

### 2. Forma Normal Conjuntiva (Producto de Sumas / PSM)

Acá hacemos lo contrario: nos interesan **únicamente las filas donde $Z = 0$**. Si mirás la tabla, son las primeras 3 filas. Para cada una, armamos un maxitérmino sumando las variables ($A + B + C$), recordando que **acá el $1$ es el que se niega**:

  

- Fila (0, 0, 0) $\rightarrow$ Todas son $0$, ninguna se niega. Queda: **$(A + B + C)$**
    
      
    
- Fila (0, 0, 1) $\rightarrow$ La $C$ es $1$, así que va negada. Queda: **$(A + B + \bar{C})$**
    
      
    
- Fila (0, 1, 0) $\rightarrow$ La $B$ es $1$, así que va negada. Queda: **$(A + \bar{B} + C)$**
    
      
    

La "Forma Normal Conjuntiva" se arma multiplicando todos esos bloquecitos:

**$Z = (A + B + C) \cdot (A + B + \bar{C}) \cdot (A + \bar{B} + C)$**

  

**Conclusión:**

Tanto la ecuación gigante de sumas (SPm) como la ecuación de multiplicaciones (PSM) son matemáticamente **equivalentes**. Si construís un circuito con cualquiera de las dos, la lámpara se va a encender y apagar exactamente en los mismos momentos.

  

El problema es que construir un circuito con 5 sumas y multiplicaciones de a 3 variables es un desperdicio físico y económico. Ahí es donde entran los teoremas del álgebra de Boole que viste antes: para agarrar cualquiera de esas dos ecuaciones monstruosas, factorizarlas y reducirlas hasta llegar a la expresión mínima que te dio el profesor al principio: $Z = A + B \cdot C$.

![[Pasted image 20260909223335.png]]

¡Justamente esta diapositiva, `image_fa3008.png`, es la resolución oficial del ejercicio que acabamos de hacer a mano en el mensaje anterior!

Acá el profesor te formaliza en limpio cómo se construyen esas dos ecuaciones:

- **Lado izquierdo (FND / SPm):** Te escribe la regla teórica exacta que aplicamos: buscar los $1$ de la salida, reemplazar los $0$ de la entrada por variables negadas y los $1$ por variables normales. Al lado de la tabla podés ver listados exactamente los mismos cinco minitérminos que armamos recién, y abajo de todo, la sumatoria final gigante.
    
- **Lado derecho (FNC / PSM):** Te muestra directamente el resultado final del producto de sumas (los tres maxitérminos multiplicados) correspondiente a las filas donde la $Z$ vale $0$.
    

El detalle interesante acá es que en el lado derecho menciona que esto se obtiene teniendo en cuenta el **Principio de Dualidad**. Como charlamos al principio, esto es porque para pasar de la técnica de minitérminos a maxitérminos estás invirtiendo todas las reglas del juego: pasás de buscar unos a buscar ceros, pasás de multiplicar a sumar, y pasás de negar los ceros a negar los unos. Todo es el "espejo" lógico de lo anterior.

¿Querés que veamos cómo usar el álgebra de Boole para empezar a simplificar este choclazo de ecuación, o pasamos a la siguiente diapositiva que tengas?


Estás muy cerca con la idea, pero hay una pequeña confusión con la estructura del maxitérmino. Vamos a separar el "ladrillo" (el término individual) de la "pared" (la ecuación completa).

  

**1. Los ladrillos (Términos individuales)**

Tanto el minitérmino como el maxitérmino son un solo bloque individual que contiene a todas las variables ($A, B, C$) una sola vez:

  

- **Minitérmino:** Es una **multiplicación** interna de las variables. Ejemplo: $A \cdot B \cdot C$
    
      
    
- **Maxitérmino:** Es una **suma** interna de las variables. Ejemplo: $A + B + C$ (no es $ABC + ABC$, sino las letras separadas por signos de suma).
    
      
    

**2. La pared (Las Funciones Normales)**

Acá es donde unimos varios ladrillos para armar el circuito final, y creo que a esto apuntabas con tu ejemplo:

  

- **Forma Normal Disyuntiva (SPm):** Agarrás varios minitérminos y los sumás entre sí. Te queda: $(A \cdot B \cdot C) + (\bar{A} \cdot B \cdot \bar{C}) + (A \cdot \bar{B} \cdot C)$.
    
      
    
- **Forma Normal Conjuntiva (PSM):** Agarrás varios maxitérminos y los multiplicás entre sí. Te queda: $(A + B + C) \cdot (\bar{A} + B + \bar{C}) \cdot (A + \bar{B} + C)$.
    
      
    

En resumen: el minitérmino es el grupito donde las letras se multiplican, y el maxitérmino es el grupito donde las letras se suman. ¿Se ve más clara ahí la diferencia visual?

![[Pasted image 20260909223346.png]]

Estas diapositivas detallan los métodos algebraicos para construir ambas funciones canónicas a partir de una ecuación, sin depender visualmente de la tabla de verdad.

**Armando los Minitérminos (Forma Normal Disyuntiva)**

En `image_fb0cc9.png`, se muestra el desarrollo para expandir la función original $f1(A, B, C) = A + B + C$.

- El objetivo es asegurar que en cada término aparezcan todas las variables del sistema.
    
- Se rellenan las variables faltantes multiplicando el término original por la suma de la variable que falta y su negación, tal como se hace al multiplicar $A$ por $(B + \bar{B})(C + \bar{C})$.
    
- Tras aplicar la propiedad distributiva, se obtiene una sumatoria larga que contiene múltiples minitérminos.
    
- Para obtener el resultado limpio, se tachan todos los minitérminos duplicados en el medio de la ecuación.

![[Pasted image 20260909223355.png]]

**Armando los Maxitérminos (Forma Normal Conjuntiva)** En `image_fb0ce6.png`, se enumeran los tres pasos teóricos exactos para obtener la expresión canónica como Producto de Maxitérminos.

- **Paso 1:** Primero se debe desarrollar la función como una suma de minitérminos.
    
- **Paso 2:** Luego, se deben identificar los minitérminos en los que la función original vale '0'.
    
- **Paso 3:** Esos minitérminos identificados que valen cero se suman, lo cual conforma la Función Negada.
    
- Sobre esa suma de minitérminos se debe usar la ley D'Morgan.
    
- La aplicación de esta ley consiste en intercambiar las sumas por multiplicaciones.
    
- En este mismo paso, se deben negar todas las variables que componen los minitérminos para los cuales la función valía cero.

![[Pasted image 20260909223405.png]]

![[Pasted image 20260909223414.png]]

Las Formas Normales (o Canónicas) son dos maneras universales y estandarizadas de escribir exactamente la misma ecuación lógica. Sí, podés expresar el comportamiento de un mismo circuito de estas dos formas distintas, y ambas son matemáticamente equivalentes.

  

La diferencia radica en qué parte del comportamiento del circuito elegís mirar:

  

- **Forma Normal Disyuntiva (FND / Suma de Productos):** Se enfoca exclusivamente en los casos donde tu circuito tiene que dar `1` (encendido). Agrupa las variables multiplicándolas (minitérminos) y luego **suma** todos esos grupos.
    
      
    
- **Forma Normal Conjuntiva (FNC / Producto de Sumas):** Se enfoca exclusivamente en los casos donde tu circuito tiene que dar `0` (apagado). Agrupa las variables sumándolas (maxitérminos) y luego **multiplica** todos esos grupos.
    
      
    

Para verlo en la práctica, imaginá un circuito muy simple con dos variables ($A$ y $B$) y su salida ($Z$):

  

|**A**|**B**|**Z (Salida)**|
|---|---|---|
|0|0|**0**|
|0|1|**1**|
|1|0|**0**|
|1|1|**1**|

**1. Expresándolo como FND (Mirando los unos)**

Buscamos las filas donde $Z=1$, que son la segunda y la cuarta.

  

- Fila (0, 1): La $A$ vale $0$, así que va negada. El minitérmino es $\bar{A} \cdot B$.
    
      
    
- Fila (1, 1): Ambas valen $1$. El minitérmino es $A \cdot B$.
    
      
    
- **Ecuación FND:** Sumás los bloques $\rightarrow$ $Z = (\bar{A} \cdot B) + (A \cdot B)$
    
      
    

**2. Expresándolo como FNC (Mirando los ceros)**

Buscamos las filas donde $Z=0$, que son la primera y la tercera. Recordá que para los maxitérminos, la regla se invierte (el $1$ se niega).

  

- Fila (0, 0): Ambas valen $0$, ninguna se niega. El maxitérmino es $(A + B)$.
    
      
    
- Fila (1, 0): La $A$ vale $1$, así que va negada. El maxitérmino es $(\bar{A} + B)$.
    
      
    
- **Ecuación FNC:** Multiplicás los bloques $\rightarrow$ $Z = (A + B) \cdot (\bar{A} + B)$
    
      
    

Si aplicás los teoremas del álgebra de Boole que viste antes para simplificar cualquiera de esas dos ecuaciones, ambas se reducen a $Z = B$. Esto demuestra que tanto la FND como la FNC son dos caminos distintos para describir exactamente la misma realidad lógica.


![[Pasted image 20260909223723.png]]

![[Pasted image 20260909223732.png]]

![[Pasted image 20260909223740.png]]

![[Pasted image 20260909223750.png]]

![[Pasted image 20260909223759.png]]

![[Pasted image 20260909223808.png]]

![[Pasted image 20260909223819.png]]

![[Pasted image 20260909223829.png]]

![[Pasted image 20260909223840.png]]

![[Pasted image 20260909223852.png]]

![[Pasted image 20260909223903.png]]

![[Pasted image 20260909223912.png]]

![[Pasted image 20260909223923.png]]

![[Pasted image 20260909223940.png]]