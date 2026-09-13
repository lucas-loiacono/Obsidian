
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



![[Pasted image 20260912212158.png]]

![[Pasted image 20260913162438.png]]


### Acá seria que 1 estacionamiento guarda entre 0 y 1 auto,, 0 si esta vacío, 1 si esta ocupado

![[Pasted image 20260913164336.png]]


![[Pasted image 20260913171403.png]]


sino se puede poner así sin flecha pero asignando el vehículo


![[Pasted image 20260913172709.png]]



![[Pasted image 20260913171855.png]]


![[Pasted image 20260913172535.png]]

![[Pasted image 20260913172739.png]]


```java

package org.example;

public class Estacionamiento<T> {

    private T vehiculoGuardado;

    public Estacionamiento() {
        this.vehiculoGuardado = null;
    }

    public void estacionar(T vehiculo) {
        if (vehiculo == null) {
            System.out.println("Error: No se puede estacionar un vehículo nulo.");
        } else if (this.estaOcupado()) {
            System.out.println("Error: El estacionamiento ya está ocupado.");
        } else {
            this.vehiculoGuardado = vehiculo;
        }
    }

    public T retirar() {
        T vehiculoTemporal = null;
        if (this.estaOcupado()) {
            vehiculoTemporal = this.vehiculoGuardado;
            this.vehiculoGuardado = null;
        } else {
            System.out.println("Error: El estacionamiento está vacío.");
        }

        return vehiculoTemporal;
    }
    public boolean estaOcupado() {
        return this.vehiculoGuardado != null;
    }
}
```



```java
package org.example;

public class Auto {
    private final String patente;
    private final String marca;

    public Auto(String patente, String marca) {
        this.patente = patente;
        this.marca = marca;
    }

    public String getPatente() {
        return patente;
    }

    public String getMarca() {
        return marca;
    }
}
```


```java
package org.example;

public class Main {
    public static void main(String[] args) {
        Auto miFitito;
        Auto miFerrari;
        Estacionamiento<Auto> cochera;
        Auto autoRetirado;

        miFitito = new Auto("ABC-123", "Fiat");
        miFerrari = new Auto("ZZZ-999", "Ferrari");

        cochera = new Estacionamiento<>();

        System.out.println("PRUEBA DEL ESTACIONAMIENTO ");
        System.out.println("Cochera ocupada? " + cochera.estaOcupado());

        System.out.println("\nEstacionando el Fiat");
        cochera.estacionar(miFitito);
        System.out.println("Cochera ocupada? " + cochera.estaOcupado());

        System.out.println("\nIntentando estacionar la Ferrari");
        cochera.estacionar(miFerrari);

        System.out.println("\nRetirando vehículo");
        autoRetirado = cochera.retirar();

        System.out.println("Se retiró un auto marca: " + autoRetirado.getMarca() + " con patente: " + autoRetirado.getPatente());

        System.out.println("Cochera ocupada? " + cochera.estaOcupado());
    }
}
```



El diagrama UML se construye dividiendo cada clase en tres compartimentos horizontales: nombre de la clase, atributos (estado) y métodos (comportamiento). Al traducir el enunciado de la **image_34ce62.jpg** a los esquemas, la lógica se desglosa de la siguiente manera:

**1. Clase `Auto` (Entidad concreta)**

- **Atributos (Compartimento medio):** Se definen los datos internos. El símbolo `-` indica que son de visibilidad **privada**, respetando el principio de encapsulamiento. Por eso se modela como `-patente: String` y `-marca: String`.
    
- **Métodos (Compartimento inferior):** Se define cómo interactuar con la clase. El símbolo `+` indica que son **públicos**. Aquí se ubican el constructor `+ Auto(patente: String, marca: String)` y los métodos _getters_ para consultar los atributos privados.
    

**2. Clase `Estacionamiento<T>` (Clase Genérica)** El enunciado exige que la clase guarde un elemento de _cualquier_ tipo, lo que en lenguajes orientados a objetos como Java se resuelve con Tipos Genéricos.

- **Definición del Genérico:** La **image_34ce84.png** representa mejor este concepto que la anterior, ya que incluye la etiqueta `<<T>>` debajo del nombre `Estacionamiento`, indicando explícitamente que es una clase parametrizada.
    
- **Atributo interno:** En esa misma imagen se agrega el atributo `vehiculo: T` (nota: por convención de encapsulamiento, en un diseño formal debería llevar un `-` para ser privado, es decir, `- vehiculo: T`). Esto señala que el espacio de guardado no está atado a la clase `Auto`, sino al tipo genérico `T`.
    
- **Métodos:** Las firmas de los métodos utilizan el parámetro genérico en lugar de clases concretas. `estacionar(vehiculo: T)` recibe el elemento, y `retirar(): T` especifica que devuelve un objeto de ese mismo tipo `T`.
    

**3. La Relación (Asociación y Multiplicidad)** Los números `1` y `0..1` sobre la línea que conecta ambas clases definen la multiplicidad de la asociación, es decir, cuántas instancias de una clase se relacionan con la otra.

- **Significado lógico:** Un objeto `Estacionamiento` (`1`) puede contener cero o un objeto (`0..1`). Esto modela perfectamente la restricción del enunciado de "guardar un único elemento": el estacionamiento puede estar vacío (`0`) o estar ocupado por exactamente un vehículo (`1`).
    

Para armar estos diagramas desde cero, la regla general es extraer los sustantivos del enunciado para crear las clases, buscar las características propias de cada entidad para definir los atributos privados, y localizar las acciones requeridas para plantear los métodos públicos.





Los genéricos (representados con letras como `<T>`, `<E>`, `<K>`, etc.) son esencialmente **plantillas o comodines para los tipos de datos**. Permiten definir una clase, interfaz o método sin especificar de antemano qué tipo de dato exacto va a manejar, delegando esa decisión al momento en que se usa la clase.

  

Para entender por qué se usan y para qué sirven, lo mejor es ver los problemas que resuelven:

  

**1. Reutilización de código (El problema de repetir código)**

Pensá en el concepto de un Tipo de Dato Abstracto (TDA). Si quisieras hacer una estructura, como una Pila, una Lista, o el `Estacionamiento` del ejercicio, y no existieran los genéricos, tendrías que programar una clase distinta para cada cosa que quieras guardar: un `EstacionamientoDeAutos`, un `EstacionamientoDeMotos`, un `EstacionamientoDeCamiones`.

Al usar `<T>`, programás la lógica de guardar y retirar una sola vez. Cuando instancias la clase en el código, le decís qué es esa "T": `Estacionamiento<Auto> miEstacionamiento = new Estacionamiento<>();`.

  

**2. Seguridad de tipos (El problema de usar `Object` o punteros)**

En lenguajes orientados a objetos como Java, la alternativa antigua a los genéricos era usar la clase superpadre `Object` (que acepta cualquier cosa). En lenguajes de más bajo nivel como C, la alternativa para hacer estructuras genéricas es usar punteros vacíos (`void *`).

El gran peligro de esas alternativas es que no hay control estricto. Si tu estacionamiento guarda un `Object` o un `void *`, el compilador te va a dejar guardar un objeto `Gato` adentro de un estacionamiento pensado para vehículos. El programa va a compilar bien, pero cuando intentes sacar ese elemento y llamar al método `getPatente()`, el programa va a fallar (lanzando un error en tiempo de ejecución o problemas de memoria).

Al usar genéricos, el compilador valida todo estrictamente. Si definiste un `Estacionamiento<Auto>`, y le querés pasar un `Gato`, el código directamente no compila. Te avisa del error antes de probar el programa.

  

**3. Eliminación de conversiones forzadas (Casting)**

Siguiendo con el punto anterior, si guardás un dato como un tipo genérico absoluto (como `Object`), al retirarlo el programa no sabe qué es. Para poder usarlo, tendrías que forzar su tipo manualmente:

`Auto miAuto = (Auto) estacionamiento.retirar();`

  

Con los genéricos `<T>`, como el sistema ya sabe de qué tipo es la instancia desde que la creaste, te ahorrás ese paso. El método `retirar(): T` ya devuelve un `Auto` directamente:

`Auto miAuto = estacionamiento.retirar();`

  

En resumen: sirven para escribir código mucho más flexible y reutilizable, manteniendo al mismo tiempo una validación estricta por parte del compilador para evitar errores inesperados mientras el programa está funcionando.


# Genéricos del ejemplo



  

**1. Avisarle a la clase que es genérica (en Estacionamiento.java)**

En tu código pusiste `public class Estacionamiento`, pero luego adentro usás la `T`. Para que Java sepa que esa `T` es un comodín genérico y no una clase real llamada "T", tenés que poner el `<T>` en el encabezado de la clase.


```Java
package org.example;

// ACÁ ESTÁ EL CAMBIO: Se agrega <T> al lado del nombre de la clase
public class Estacionamiento<T> { 

    private T vehiculoGuardado;

    public Estacionamiento() {
        this.vehiculoGuardado = null;
    }

    // El resto de tus métodos quedan exactamente igual
    public void estacionar(T vehiculo) {
        // ...
    }
    
    // ...
}
```

**2. Definir qué es la "T" al crear el objeto (en Main.java)**

Acá es exactamente donde respondo tu duda de "cómo pasar la `<T>`". Cuando declarás la variable `cochera`, es el momento de decirle al compilador: _"Para esta cochera específica, quiero que la `T` sea reemplazada por la clase `Auto`"_.

Tenés que agregarlo en la declaración de la variable:



```Java
package org.example;

public class Main {

    public static void main(String[] args) {

        Auto miFitito;
        Auto miFerrari;
        
        // ACÁ ESTÁ EL CAMBIO: Le decís que la T va a ser un <Auto>
        Estacionamiento<Auto> cochera; 
        
        Auto autoRetirado;

        miFitito = new Auto("ABC-123", "Fiat");
        miFerrari = new Auto("ZZZ-999", "Ferrari");

        // Al instanciar, el <> vacío (operador diamante) ya entiende que es un Auto 
        // porque se lo dijiste en la línea de arriba.
        cochera = new Estacionamiento<>(); 

        // ... resto de tu código ...
```

**¿Qué pasa por detrás una vez que hiciste esto?**

Al escribir `Estacionamiento<Auto> cochera;`, el compilador de Java lee tu clase `Estacionamiento` e imaginariamente reemplaza todas las `T` por `Auto`. Entonces tu método `estacionar(T vehiculo)` internamente se transforma de forma segura en `estacionar(Auto vehiculo)`.

Si el día de mañana creás una clase `Moto`, podrías crear otra variable en el Main que sea `Estacionamiento<Moto> cocheraMotos = new Estacionamiento<>();`, y para esa variable, todas las `T` se comportarán como motos, reutilizando todo tu código sin haber programado la clase dos veces.


## Yo
osea yo como tipo de dato a lo que tenga ahi adentro le paso la clase, y ahi me reemplaza todas las t por mi clase

## Gemini

¡Exactamente, lo entendiste a la perfección!

  

Esa es la forma más fácil y correcta de pensarlo. Cuando vos escribís `Estacionamiento<Auto>`, le estás diciendo a Java: _"Agarrá la plantilla de la clase `Estacionamiento` y, en todos los lugares donde veas una `T`, hacé de cuenta que dice `Auto`"_.

  

Por eso se llama "plantilla" o "comodín". Si mañana decidís hacer un `Estacionamiento<String>`, entonces:

  

- `private T vehiculoGuardado;` pasa a ser `private String vehiculoGuardado;`
    
- `public void estacionar(T vehiculo)` pasa a ser `public void estacionar(String vehiculo)`
    
- `public T retirar()` pasa a ser `public String retirar()`
    


¡Es así de directo! Te ahorra muchísimo tiempo porque te permite programar y probar toda la lógica de guardar y retirar una sola vez, y después reutilizarla con la clase que se te ocurra.

