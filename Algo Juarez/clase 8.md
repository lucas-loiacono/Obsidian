
![[Pasted image 20260912182921.png]]

si yo quiero guardar datos, lo tengo que hacer de esta forma, me tengo que crear una clase para cada tipo repitiendo el mismo codigo

![[Pasted image 20260912183312.png]]

![[Pasted image 20260912184301.png]]


Esto esta mal
![[Pasted image 20260912184604.png]]

Casteo todo a clase object, el tema es que cuando quiero sacar un elemento de la caja, se olvida de lo que es y lo tengo que castear de nuevo a la fuerza


Para esto se crearon lo genéricos

![[Pasted image 20260912190022.png]]

declaro entre <> una variable que todavia no se sabe el tipo de dato que va a contener

![[Pasted image 20260912190714.png]]

acá guardo el dato, pero a la hora que lo quiero mostrar si lo casteo mal el archivo se rompe en tiempo de ejecución

## Solución

![[Pasted image 20260912191328.png]]

Acá le tengo que pasar de que tipo es la caja entre los <>, pero si a la de string le paso in interger lo que hace es que se no deja compilar desde el principio




![[Pasted image 20260912193004.png]]

java acá con los métodos java es mas inteligente, ya que le pasamos los argumentos y java ya lee el tipo que son compilando normal



![[Pasted image 20260912195741.png]]

Contrato: te obliga a programar ciertos métodos
En este caso el contrato que me debe dar dos métodos, k y v getclave y getvalor


![[Pasted image 20260912200143.png]]

A lo genéricos los restrinjo para que no me pueda tomar ciertos tipos de datos, por ejemplo si yo tengo una calculadora puedo hacer que me tome tipos de datos como int, float, doble, pero no quiero que me tome un string
De todos los datos que puede tomar el genérico lo restrinjo a unos pocos

En el caso es acepta cualquier tipo t, pero que sea heredado de la clase Numbers
Es como "t se extiende de Numbers" ósea que t extiende una rama de la clase Numbers

![[Pasted image 20260912200735.png]]

Ese es el "truco de magia" completo. Básicamente el proceso es así:

1. **El Guardián (Tiempo de Compilación):** Tú declaras la caja como `<String>`. El compilador se pone estricto y vigila que solo entren textos. Si intentas meter un número, te detiene y te marca un error en rojo en tu código.
    
      
    
2. **La Amnesia (Type Erasure):** Una vez que el compilador aprueba todo y te asegura que no hay errores, borra la etiqueta `<String>` para crear el código final. En la memoria real de Java (cuando el programa ya está corriendo), tu dato se guarda en un arreglo o variable de tipo `Object`.
    
      
    
3. **El Rescate Automático (Tiempo de Ejecución):** Cuando vas a sacar el dato usando tu método `.obtener()`, como el compilador _ya garantizó_ que nadie metió nada incorrecto en el paso 1, él mismo escribe ese casteo `(String)` por ti de forma oculta e invisible.
    
      
    

Por eso decimos que los genéricos son una herramienta **para el programador y para el compilador**, no para la memoria de la máquina. Te dan la seguridad de que tu programa no va a explotar y te ahorran el trabajo pesado de tener que hacer casteos manuales o escribir 50 clases distintas.




![[Pasted image 20260912201626.png]]

Es un tema muy común para confundirse. El problema fundamental es que **los arreglos y los genéricos en Java fueron diseñados con reglas opuestas** sobre cómo recuerdan los tipos de datos.


Aquí te lo explico paso a paso basándome en lo que muestra tu imagen ("image_9d904a.png"):

**1. Cómo funcionan los Arreglos (Arrays)**

Los arreglos en Java son estrictos en tiempo de ejecución. Si creas un arreglo de `String[]`, Java sabe en todo momento que es exclusivo para textos. Si intentas meter un `Integer` ahí mientras el programa corre, Java se da cuenta inmediatamente y lanza un error para protegerte (`ArrayStoreException`).

**2. Cómo funcionan los Genéricos (`<T>`)**

Los genéricos sufren de algo llamado **Type Erasure** (Borrado de Tipos). Para hacer que los genéricos fueran compatibles con versiones muy antiguas de Java, el compilador "borra" la letra `T` después de revisar que tu código esté bien escrito y la reemplaza por `Object`. Es decir, al momento de ejecutar el programa, la `T` desaparece; Java tiene "amnesia" sobre qué tipo exacto de dato era.

**El Choque (Por qué `new T[10]` NO compila)**

Aquí ocurre el problema que menciona la advertencia de tu imagen. El arreglo necesita saber _exactamente_ su tipo al ejecutarse para crear el espacio correcto en memoria y evitar datos inválidos. Pero como el genérico `T` sufre borrado y pierde su tipo real, Java no sabe de qué tamaño o tipo construir el arreglo. Al no saber qué es `T` en tiempo de ejecución, te prohíbe instanciarlo directamente.

**La Solución (El "Truco" del Casteo)**

La solución que muestra la imagen es básicamente un trato que haces con el compilador:


1. **Creas un arreglo de `Object`**: `new Object[10]`. Java sí sabe qué es un `Object` y cómo construir un arreglo de este tipo en memoria.
    
2. **Haces un "Casteo" (Conversión)**: `(T[])`. Le dices al compilador: _"Crea este arreglo genérico de objetos, yo me hago responsable por código de que solo entren elementos del tipo T"_.
    
La línea final queda así:

`T[] miArreglo = (T[]) new Object[10];`

**Un detalle para la práctica:**

Cuando hagas esto, tu IDE (como IntelliJ o Eclipse) te va a marcar una advertencia amarilla de _"Unchecked cast"_ (Casteo no verificado). Es completamente normal. Solo asegúrate de que tu clase controle bien qué datos se guardan ahí. Por esta misma limitación, en Java casi siempre es más fácil y seguro usar colecciones como `ArrayList<T>` en lugar de crear arreglos genéricos desde cero.


# Type erasure

El **Type Erasure** (Borrado de Tipos) es un proceso del compilador de Java que elimina toda la información sobre los tipos genéricos (como `<T>`, `<String>` o `<Integer>`) justo antes de generar el código que se va a ejecutar.

Básicamente, los genéricos en Java son una ilusión óptica para el programador. Existen en tu código fuente para que el compilador te obligue a respetar los tipos de datos y evitar errores, pero desaparecen cuando el programa corre.

Así es como funciona en la práctica:


**1. Lo que tú escribes (Código Fuente):**


```java
List<String> nombres = new ArrayList<String>();
nombres.add("Juan");
String unNombre = nombres.get(0);
```

**2. Lo que hace el Type Erasure (Lo que se ejecuta):**

```java
// El tipo <String> desaparece y se reemplaza por Object
List nombres = new ArrayList(); 
nombres.add("Juan");
// El compilador agrega un casteo oculto automáticamente
String unNombre = (String) nombres.get(0); 
```

**¿Por qué Java hace esto?**

Todo se resume a **compatibilidad hacia atrás**. Los genéricos se introdujeron en Java 5 (año 2004). Los creadores de Java necesitaban que los programas nuevos, escritos con genéricos, pudieran ejecutarse sin problemas en servidores y máquinas virtuales antiguas que no tenían idea de qué era un `<T>`. Al "borrar" los tipos, el código resultante era idéntico al código de las versiones viejas de Java.

  
**¿Qué consecuencias tiene?**

La consecuencia principal es la "amnesia" en tiempo de ejecución. Mientras tu programa se está ejecutando, una `List<String>` y una `List<Integer>` son exactamente la misma cosa para la memoria de Java: ambas son simplemente una `List` que guarda `Objects`. Por esta pérdida de identidad es que no puedes crear arreglos genéricos directos (`new T[10]`) o preguntar si un objeto es de un tipo genérico específico (`if (obj instanceof List<String>)`).




  


### 1. Aclaración: Un genérico NO es para meter "cualquier cosa mezclada"

Cuando usas un genérico (`<T>`), no estás creando una caja donde puedes tirar un `String` y luego un `int` mezclados. Más bien, estás creando una **"plantilla"**.

  

Cuando tú vas a usar esa clase en tu código (por ejemplo en el `main`), el compilador te obliga a **elegir un tipo de dato único** para esa instancia en particular:

`Caja<String> miCajaDeTextos = new Caja<String>();`

  

A partir de esa línea, el compilador **se vuelve estricto**: solo te dejará meter `Strings` en _esa_ caja. Si intentas meter un `100` (int), el programa ni siquiera va a compilar. Te dará error antes de ejecutar.

  

### 2. ¿Cómo sabe qué devolverte si ocurre el "Type Erasure"?

Como tú le dijiste al compilador desde el principio que esa caja era de `<String>`, el compilador **ya verificó** que nunca entró un número ahí.

  

Entonces, cuando ocurre el _Type Erasure_ y reemplaza todo por `Object`, el compilador **escribe el casteo por ti de forma invisible y segura**.

Tú escribes esto:

`String texto = miCajaDeTextos.obtener();`

Y el compilador por debajo lo transforma a esto:

`String texto = (String) miCajaDeTextos.obtener();`

  

Lo hace con total seguridad porque él mismo se aseguró de que nadie metiera nada que no fuera un String.

  

### 3. La diferencia con la foto ("image_9d9fea.jpg")

Tu foto muestra exactamente **el infierno que era programar en Java antes de que existieran los genéricos** (antes del 2004). Muestra los dos problemas que los genéricos vinieron a solucionar:

  

**El problema 1: "CÓDIGO DUPLICADO" (Líneas 8 a 15)**

Para tener cajas seguras que no mezclen datos, tenías que crear una clase entera distinta para cada tipo de dato. Tenías que programar una `CajaString.java`, luego una `CajaInteger.java`, luego una `CajaPerro.java`... Imagina hacer eso para 50 tipos de datos distintos. Es insostenible.

  

**El problema 2: "LA FALSA SOLUCIÓN (Object)" - La clase `CajaMal` (Líneas 19 a 27)**

Para evitar crear 50 clases, los programadores hacían una sola caja que recibía y devolvía `Object` (la clase de la que heredan todos en Java).

Aquí **SÍ** podías meter cualquier cosa. Pero mira los problemas que generaba (y que están explicados en los comentarios de tu imagen):

  

1. **Te obliga a hacer el casteo a mano:** Tienes que escribir explícitamente `(String) cajaMal.obtener()`.
    
      
    
2. **Es peligroso (No avisa):** Como dice el comentario en la línea 26, si tú te equivocas y escribes `(Integer) cajaMal.obtener()` intentando sacar un número cuando en realidad habías guardado un texto, **el compilador no te avisa**. El programa compila perfecto, pero cuando lo ejecutes y llegue a esa línea, **tu programa va a explotar** (lanzará un `ClassCastException`) y se cerrará.
    
      
    

### En resumen:

La diferencia entre la `CajaMal` de tu foto y usar Genéricos (`Caja<T>`) es que **el genérico hace el trabajo sucio por ti de forma segura:**

  

- **Con `CajaMal` (Object):** El compilador no sabe qué hay adentro. Tú asumes el riesgo, tú haces el casteo a mano, y si te equivocas, el programa explota al ejecutarse.
    
      
    
- **Con Genéricos (`Caja<T>`):** Escribes la clase una sola vez (adiós código duplicado). El compilador vigila estrictamente qué metes, él mismo hace el casteo invisible al sacar el dato, y te garantiza al 100% que el programa nunca va a explotar por un error de tipos.