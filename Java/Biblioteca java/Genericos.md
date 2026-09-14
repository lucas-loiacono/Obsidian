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