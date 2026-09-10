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

![[Pasted image 20260909223317.png]]

![[Pasted image 20260909223335.png]]

![[Pasted image 20260909223346.png]]

![[Pasted image 20260909223355.png]]

![[Pasted image 20260909223405.png]]

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