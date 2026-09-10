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






Entendiste perfecto el mecanismo de cambiar los signos y los números, pero ojo con pensar que la ecuación original y su dual son equivalentes entre sí o "dan lo mismo".

Lo que el principio te dice es que **si una regla matemática es verdadera, su versión "espejo" es otra regla que también es verdadera**. Son dos leyes distintas que describen operaciones distintas, pero ambas son válidas dentro del sistema.


Fijate con este ejemplo súper básico:


- **Regla original:** $A + 0 = A$ (Si a cualquier variable le sumás 0, te queda esa misma variable).
    
- **Aplicamos dualidad:** Cambiamos el `+` por `*`, y el `0` por `1`.
    
- **Regla dual:** $A * 1 = A$ (Si a cualquier variable la multiplicás por 1, te queda esa misma variable).
    

Las dos ecuaciones son verdades absolutas, pero una te habla del comportamiento de la suma (unión) y la otra del producto (intersección).

  

La gran ventaja de esto es que funciona como un "2x1" matemático: si el día de mañana lográs demostrar que una ley compleja para reducir circuitos es válida, automáticamente sabés que su versión dual también va a funcionar, ahorrándote el trabajo de tener que demostrarla desde cero.

![[Pasted image 20260909223123.png]]

![[Pasted image 20260909223133.png]]

![[Pasted image 20260909223144.png]]

![[Pasted image 20260909223157.png]]

![[Pasted image 20260909223210.png]]

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