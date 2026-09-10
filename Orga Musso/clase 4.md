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

Estas diapositivas detallan los métodos algebraicos para obtener las funciones canónicas (o normales) a partir de una expresión lógica, sin necesidad de construir la tabla de verdad.

  

**Desarrollo de la Forma Normal Disyuntiva (Suma de Minitérminos)**

La primera imagen muestra el proceso para expandir la función $f1(A, B, C) = A + B + C$ y convertirla en su forma canónica.

  

- El objetivo algebraico es rellenar la ecuación para que en cada término aparezcan todas las variables del sistema.
    
      
    
- Para lograrlo, se multiplica cada variable original por la suma de las variables faltantes y sus respectivas negaciones; por ejemplo, la variable $A$ se multiplica por $(B + \bar{B})(C + \bar{C})$.
    
      
    
- Luego de aplicar la propiedad distributiva, se genera una sumatoria extensa que contiene todos los minitérminos resultantes.
    
      
    
- Finalmente, se tachan y eliminan todos los minitérminos que quedaron duplicados en el medio de la ecuación para obtener la expresión final.
    
      
    

**Obtención de la Forma Normal Conjuntiva (Producto de Maxitérminos)**

La segunda imagen enumera los pasos teóricos para armar la función equivalente utilizando maxitérminos.

  

- **Paso 1:** Se debe desarrollar primero la función como una suma de minitérminos.
    
      
    
- **Paso 2:** Se identifican los minitérminos específicos para los cuales la función vale '0'.
    
      
    
- **Paso 3:** Se toman esos minitérminos encontrados en el paso 2 y se suman, formando así la Función Negada. A esta suma se le debe aplicar la ley de D'Morgan, lo cual obliga a intercambiar las sumas por multiplicaciones y negar absolutamente todas las variables de los minitérminos para los cuales la función valía cero.
    
      
    

¿Hay algún paso específico del álgebra o de la aplicación de D'Morgan en estas diapositivas que te resulte confuso?

# En este ejercicio seria

![[Pasted image 20260910150253.png]]

¡Ah, excelente pregunta! Entendí a qué apuntás. Querés ver cómo llegar a esa misma ecuación gigante pero **sin mirar la tabla**, usando el método algebraico de "rellenar" las variables que faltan (como vimos en las diapositivas anteriores).

Sabemos por las primeras diapositivas que la función simplificada para esa tabla exacta de la lámpara es:

**$Z = A + B \cdot C$**

El objetivo es que en cada término aparezcan las tres variables ($A, B$ y $C$). Vamos a hacerlo paso a paso:


**Paso 1: Identificar qué le falta a cada término**


- Al primer término ($A$) le faltan la $B$ y la $C$.
    
- Al segundo término ($B \cdot C$) le falta la $A$.

**Paso 2: Rellenar multiplicando por 1**

Recordemos la regla de oro: una variable sumada a su negada siempre da 1 ($X + \bar{X} = 1$). Multiplicar por 1 no altera la ecuación, así que lo usamos para inyectar las letras faltantes.

  

- Al término $A$ lo multiplicamos por $(B + \bar{B})$ y por $(C + \bar{C})$.

- Al término $BC$ lo multiplicamos por $(A + \bar{A})$.

La ecuación nos queda así:

$Z = [A \cdot (B + \bar{B}) \cdot (C + \bar{C})] + [B \cdot C \cdot (A + \bar{A})]$

  

**Paso 3: Aplicar propiedad distributiva (desarmar los paréntesis)**

Hacemos la distributiva clásica.

Primero resolvamos el bloque de la izquierda (la $A$):

$A \cdot (B + \bar{B}) = AB + A\bar{B}$

Ahora multiplicamos eso por la $C$:

$(AB + A\bar{B}) \cdot (C + \bar{C}) = ABC + AB\bar{C} + A\bar{B}C + A\bar{B}\bar{C}$

  

Ahora resolvamos el bloque de la derecha (el $BC$):

$BC \cdot (A + \bar{A}) = ABC + \bar{A}BC$

  

**Paso 4: Unir todo y eliminar redundancias**

Juntamos todos los minitérminos que acabamos de generar en una sola suma gigante:

$Z = ABC + AB\bar{C} + A\bar{B}C + A\bar{B}\bar{C} + ABC + \bar{A}BC$

  

Si te fijás bien, el término **$ABC$ está repetido dos veces**. Por el teorema de Idempotencia ($X + X = X$), sumar lo mismo dos veces es redundante, así que tachamos uno.

  

La ecuación final (ordenando un poco los términos) nos queda:

**$Z = \bar{A}BC + A\bar{B}\bar{C} + A\bar{B}C + AB\bar{C} + ABC$**

  




![[Pasted image 20260909223355.png]]



![[Pasted image 20260909223405.png]]

### Obtención de Función Canónica: Producto de Maxitérminos (FNC)

Este procedimiento detalla los pasos para obtener una expresión canónica de una función booleana como Producto de Maxitérminos, también conocida como Forma Normal Conjuntiva.


**Paso 1: Desarrollo inicial**

- Se debe desarrollar la función original como suma de minitérminos.

- En el ejemplo con la función $F(A, B, C) = A \cdot B + B \cdot C$, la expansión da como resultado los minitérminos $A \cdot B \cdot C$, $A \cdot B \cdot \text{Not}(C)$ y $\text{Not}(A) \cdot B \cdot C$.
    

**Paso 2: Identificación de ceros**

  

- A continuación, se deben identificar los minitérminos para los cuales la función vale '0'.

- En el ejemplo analizado, los minitérminos que cumplen esta condición son $\text{Not}(A) \cdot \text{Not}(B) \cdot \text{Not}(C)$, $\text{Not}(A) \cdot \text{Not}(B) \cdot C$, $\text{Not}(A) \cdot B \cdot \text{Not}(C)$, $A \cdot \text{Not}(B) \cdot \text{Not}(C)$ y $A \cdot \text{Not}(B) \cdot C$.

**Paso 3: Aplicación de De Morgan**

  

- Se toma la suma de los minitérminos encontrados en el paso anterior, lo cual conforma la Función Negada.

- En el ejemplo de aplicación, esta función negada se denomina $G(A, B, C)$.
   
- A esta función se le debe aplicar la ley de D'Morgan.
   
- La aplicación de esta ley requiere intercambiar sumas por multiplicaciones.

- Adicionalmente, se deben negar todas las variables de los minitérminos para los cuales la función vale cero.

- Como resultado en el ejemplo, el término original $\text{Not}(A) \cdot \text{Not}(B) \cdot \text{Not}(C)$ se transforma en el maxitérmino $(A + B + C)$, y al agrupar todos los términos mediante multiplicación, se obtiene la Forma Canónica Normal Conjuntiva final.


# Hago el ejemplo que hicimos con conjuntiva

![[Pasted image 20260910151804.png]]

¡Me encanta el desafío! Vamos a hacer exactamente el mismo proceso de "rellenar" algebraicamente para llegar a la Forma Normal Conjuntiva (FNC) de la función $Z = A + B \cdot C$, pero aplicando el Principio de Dualidad.

  

Como ahora buscamos un **Producto de Sumas**, las reglas se invierten: en vez de multiplicar por $1$, vamos a **sumar $0$**.

  

**Paso 1: Convertir la ecuación a multiplicaciones**

Nuestra ecuación original es una suma ($A + BC$). Para empezar a trabajar con maxitérminos, necesitamos que sea una multiplicación.

¿Te acordás de la "distributiva rara" (Postulado P2b) que vimos al principio? Esa regla decía que $X + Y \cdot Z = (X + Y) \cdot (X + Z)$.

Si le aplicamos eso a nuestra función, nos queda:

$Z = (A + B) \cdot (A + C)$

  

**Paso 2: Identificar faltantes y rellenar sumando $0$**

A nuestro primer bloque $(A + B)$ le falta la $C$. Al segundo bloque $(A + C)$ le falta la $B$.

La regla de oro acá es que multiplicar una variable por su negada siempre da $0$ ($X \cdot \bar{X} = 0$). Como sumar $0$ no afecta a la ecuación, lo inyectamos:

  

- Al primer bloque le sumamos $(C \cdot \bar{C})$. Nos queda: $(A + B) + (C \cdot \bar{C})$
    
      
    
- Al segundo bloque le sumamos $(B \cdot \bar{B})$. Nos queda: $(A + C) + (B \cdot \bar{B})$
    
      
    

**Paso 3: Distribuir para desarmar los bloques**

Volvemos a aplicar esa "distributiva rara" en cada bloque para separar la letra normal de la negada:

  

- El bloque de la izquierda se desarma en: $(A + B + C) \cdot (A + B + \bar{C})$
    
      
    
- El bloque de la derecha se desarma en: $(A + C + B) \cdot (A + C + \bar{B})$. Si ordenamos las letras alfabéticamente, es $(A + B + C) \cdot (A + \bar{B} + C)$
    
      
    

**Paso 4: Unir todo y eliminar redundancias**

Juntamos todos los maxitérminos que acabamos de generar en una sola multiplicación gigante:

$Z = (A + B + C) \cdot (A + B + \bar{C}) \cdot (A + B + C) \cdot (A + \bar{B} + C)$

  

Si te fijás, **el término $(A + B + C)$ está repetido dos veces**. Por el teorema de Idempotencia ($X \cdot X = X$), multiplicar lo mismo dos veces es redundante, así que tachamos uno.

  

La ecuación final nos queda:

**$Z = (A + B + C) \cdot (A + B + \bar{C}) \cdot (A + \bar{B} + C)$**

  

¡Listo! Llegamos por puro método algebraico exactamente a la misma Forma Normal Conjuntiva que habíamos sacado antes mirando las 3 filas de ceros en la tabla de verdad.



![[Pasted image 20260909223414.png]]


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