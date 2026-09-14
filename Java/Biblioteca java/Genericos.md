## 1. Clases Genéricas

En la definición de la clase, debes agregar `<T>` (o cualquier otra letra, por convención se usa `T` de Type) justo después del nombre. Ese tipo `T` reemplazará a todos los lugares donde antes usabas `Object` o un tipo específico.

```Java
// Se declara <T> al lado del nombre de la clase
public class Caja<T> {
    
    // El atributo ahora es del tipo T
    private T contenido;

    // Los parámetros de entrada reciben T
    public void guardar(T contenido) {
        this.contenido = contenido;
    }

    // El valor de retorno es T
    public T obtener() {
        return this.contenido;
    }
}
```

_Nota: Puedes usar múltiples genéricos si lo necesitas, como en los diccionarios:_ `public class Par<K, V>` _(Key, Value)._


La `T` funciona como un comodín o un espacio en blanco en un contrato. Cuando tú creas el objeto usando `Respuesta<Usuario>`, el compilador va a tu código y mentalmente **reemplaza cada letra `T` que encuentre por la palabra `Usuario`**.

Entonces, para ese objeto en particular, tu clase funciona literalmente como si la hubieras escrito así:


```Java
public class RespuestaUsuario {
    private boolean exito;
    private String mensaje;
    private Usuario datos; // ¡Exacto! T se convierte en el tipo de dato Usuario

    public RespuestaUsuario(boolean exito, String mensaje, Usuario datos) { // Acá también cambia
        this.exito = exito;
        this.mensaje = mensaje;
        this.datos = datos;
    }
}
```

Y lo genial de esto es que si en la línea siguiente usas `Respuesta<String>`, el compilador hace exactamente lo mismo, pero ahora todas las `T` se comportan como `String` (`private String datos;`).

  

Básicamente, escribes el molde genérico una sola vez con la `T`, y Java lo adapta automáticamente al tipo de dato que le pases entre los diamantes `< >` al momento de usarlo.

  






## 2. Instanciación (El Operador Diamante)

Cuando vayas a usar tu clase genérica (por ejemplo, en el `main`), debes especificar qué tipo de dato real va a reemplazar a la `T`. A partir de Java 7, solo necesitas poner el tipo en la declaración y dejar un diamante vacío `<>` en el `new`.


```Java
// Bien: El diamante <> del final infiere que es String
Caja<String> cajaDeTextos = new Caja<>();
cajaDeTextos.guardar("Hola mundo");

// Bien: Se usan clases Envoltorio (Integer, Double, Boolean), NUNCA primitivos (int, double)
Caja<Integer> cajaDeNumeros = new Caja<>();
cajaDeNumeros.guardar(100);
```

## 3. Métodos (Funciones) Genéricos

No necesitas que toda la clase sea genérica para tener una función genérica. Para definir un método genérico, el secreto es **declarar el `<T>` justo antes del tipo de retorno**.


```Java
public class Utilidades {
    
    // El <T> antes de 'void' le dice al compilador que este método es genérico
    public static <T> void imprimirElemento(T elemento) {
        System.out.println("El elemento es: " + elemento);
    }

    // Aquí el método recibe un arreglo de tipo T y devuelve un solo elemento de tipo T
    public static <T> T obtenerPrimerElemento(T[] arreglo) {
        if (arreglo == null || arreglo.length == 0) return null;
        return arreglo[0];
    }
}
```

Para usar estas funciones, normalmente no tienes que hacer nada especial. El compilador de Java es inteligente y adivina el tipo basándose en lo que le pasas:


```Java
// Java infiere automáticamente que T es String
Utilidades.imprimirElemento("Un texto"); 

String[] nombres = {"Ana", "Juan"};
String primero = Utilidades.obtenerPrimerElemento(nombres); 
```

## 4. Restringir Tipos (Bounded Generics)

A veces quieres una función o clase genérica, pero no quieres que acepten _cualquier_ objeto, sino solo una familia de objetos (por ejemplo, solo números). Esto se logra con la palabra `extends`.


```Java
// T puede ser cualquier cosa que herede de Number (Integer, Double, Float...)
public static <T extends Number> double sumar(T num1, T num2) {
    return num1.doubleValue() + num2.doubleValue();
}
```



# 5. Arrays genericos



Aquí te muestro cómo se hace paso a paso:

### 1. Definir el atributo (La Declaración)

Para definir el atributo en tu clase, simplemente usas los corchetes `[]` junto a la `T`. Esto **sí está permitido** porque en este punto solo estás "reservando el nombre", no estás creando memoria real todavía.



```Java
public class Coleccion<T> {
    // Así defines un atributo como array genérico
    private T[] miArreglo;
    private int cantidad;
}
```

### 2. Hacer el `new` del array genérico

Aquí es donde debes usar el truco del casteo (`Object`) que vimos al principio. No puedes hacer `new T[10]` por culpa del Type Erasure. Tienes que inicializarlo en tu constructor (o en un método) creando un arreglo de `Object` y forzando la conversión a `T[]`.


```Java
public class Coleccion<T> {
    private T[] miArreglo;
    private int cantidad;

    // Constructor
    public Coleccion(int capacidad) {
        // Así haces el 'new' de un array genérico
        this.miArreglo = (T[]) new Object[capacidad];
        this.cantidad = 0;
    }
}
```

### 3. ¿Y si quiero hacer un `new` de un objeto genérico normal (no array)?

Si lo que quieres es instanciar una sola variable genérica haciendo algo como `T miObjeto = new T();`, te encontrarás con otra pared: **Está estrictamente prohibido en Java.**

Por el mismo _Type Erasure_, en tiempo de ejecución Java no sabe si `T` es un `String`, un `Scanner` o un `Usuario`. Al no saber qué clase es, no sabe qué constructor llamar ni cuánta memoria reservar.

  
Si necesitas guardar un objeto genérico en un atributo, la forma correcta es **pedirlo ya creado por parámetro**:



```Java
public class Contenedor<T> {
    private T miObjeto; // Atributo genérico simple

    // No hacemos 'new T()'. Obligamos a que nos pasen el objeto ya instanciado
    public Contenedor(T objetoYaCreado) {
        this.miObjeto = objetoYaCreado;
    }
}
```







Vamos a desarmar exactamente qué hace cada parte de esta línea para que veas por qué se escribe así:

`public static <T> T obtenerPrimerElemento(T[] arreglo)`

Imagínate que cada una de esas tres partes tiene un rol distinto:

  

**1. El Anuncio (`<T>`)**

La primera `<T>` (la que está entre símbolos de mayor y menor) es solo un **aviso** para el compilador. Le estás diciendo: _"Oye compilador, inventé una variable para tipos de datos que se llama T, no te asustes si la ves más adelante"_.

Si no pones ese primer `<T>`, Java va a pensar que `T` es el nombre de una clase real (como si fuera `String` o `Scanner`) y te dará error porque no existe.

  

**2. El tipo de Retorno (`T`)**

La segunda `T` le dice a la función qué es lo que va a devolver como resultado. Le dices: _"Cuando termines, devuélveme un único elemento de ese tipo T"_.

  

**3. El Parámetro (`T[] arreglo`)**

La tercera parte le indica lo que va a recibir. Le dices: _"Te voy a mandar un arreglo (`[]`) que por dentro está lleno de elementos de ese tipo T"_.

  

### Cómo ocurre el reemplazo en la práctica

A diferencia de las clases (donde ponías el diamante en el `new Respuesta<String>()`), en las funciones no hace falta que tú escribas de qué tipo son. **Java lo adivina (lo infiere) viendo qué le pasas.**

Si tú en tu código escribes esto:


```Java
String[] misTextos = {"Hola", "Mundo"};
String resultado = Utilidades.obtenerPrimerElemento(misTextos);
```

Cuando Java lee esa línea, dice: _"Ah, me pasó un arreglo de `String`. Entonces voy a reemplazar TODAS las `T` de esa función por `String`"_.

Mentalmente, el compilador transforma tu función genérica para que en ese instante se vea así:

```Java
// Avisa <String> | Devuelve String | Recibe un arreglo String[]
public static <String> String obtenerPrimerElemento(String[] arreglo) {
    if (arreglo == null || arreglo.length == 0) return null;
    return arreglo[0];
}
```

Si en la siguiente línea del código tú le pasas un arreglo de números (`Integer[]`), el compilador vuelve a hacer el mismo proceso, pero reemplazando absolutamente todas las `T` por `Integer`.

  

# YO


# GEMINI

No, no es para que tenga un nombre distinto. Poner el `<T>` al lado del nombre de la clase sirve para establecer la **regla general (o el alcance)** para todo ese objeto.

Cuando declaras el `<T>` arriba de todo en `public class Caja<T>`, le estás diciendo a Java: _"Atención, de ahora en adelante, TODO lo que esté dentro de esta clase va a estar sincronizado y compartirá exactamente el mismo comodín"_.

Vamos a ver tu clase `Caja` para entender por qué es tan importante esta sincronización:


```Java
public class Caja<T> { // 1. Declaramos el comodín para TODA la clase
    
    private T contenido; // 2. El atributo usa ESE mismo T

    public void guardar(T elemento) { // 3. El método recibe ESE mismo T
        this.contenido = elemento;
    }

    public T obtener() { // 4. El método devuelve ESE mismo T
        return contenido;
    }
}
```

### ¿Qué logramos al ponerlo en la clase? **Garantizar la coherencia.**

Al declararlo a nivel de clase, cuando tú en el `main` haces un `new Caja<String>()`, obligas a que **todas** las piezas de esa caja se conviertan en `String` al mismo tiempo. La variable guarda un `String`, el método `guardar` solo acepta `String`, y el método `obtener` te asegura devolver un `String`. Todo el objeto habla exactamente el mismo idioma.

  

### ¿Qué pasaría si no lo hiciéramos así?

Imagina que no ponemos el `<T>` en la clase, y en su lugar declaramos genéricos individuales en cada método (como hicimos antes con `Utilidades`):


```Java

public class CajaRota {
    private Object contenido; // Ya no podemos usar T acá

    // Método genérico independiente
    public <T> void guardar(T elemento) { ... }

    // OTRO método genérico independiente
    public <T> T obtener() { ... } 
}
```

Si hiciéramos eso, los métodos estarían desconectados. Podrías usar el método `guardar` pasándole un `String`, pero luego llamar al método `obtener` pidiendo que te devuelva un `Integer`. ¡Se perdería toda la seguridad que nos dan los genéricos porque la clase ya no garantiza que lo que entra es igual a lo que sale!

  

**En resumen:**

- Se pone en los **métodos (funciones)** cuando solo esa función necesita ser genérica e independiente del resto.
    
   
- Se pone en las **clases** cuando quieres que todo el objeto (sus atributos y sus funciones) trabaje en conjunto con el mismo tipo de dato.
    
 

¿Queda claro cómo el `<T>` en la clase actúa como un contrato que obliga a todas sus partes internas a comportarse igual?