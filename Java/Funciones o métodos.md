
En Java, la primera regla que tenés que saber es que **las funciones sueltas no existen**. Todo, absolutamente todo, tiene que vivir dentro de una `class`. Por esta razón, en Java (y en la programación orientada a objetos en general) a las funciones se las llama **métodos**.

Aquí está el desglose completo de cómo funcionan, cómo se estructuran y qué tipos existen.
## 1. La anatomía de un método

La estructura básica de un método en Java tiene varias partes obligatorias y otras opcionales. Se ve así:

```Java
[modificador_acceso] [static?] [tipo_de_retorno] nombreDelMetodo([parámetros]) {
    // Código a ejecutar
    return [valor];
}
```

Tomemos un ejemplo real:

```Java
public static int sumar(int a, int b) {
    return a + b;
}
```

- **`public` (Modificador de acceso):** Define quién puede usar este método. `public` significa que cualquier otra parte del programa puede llamarlo. Si fuera `private`, solo se podría usar internamente dentro de esa misma clase.
    
      
    
- **`static` (Opcional):** Define si el método pertenece a la clase en sí, o a un objeto (una instancia) de esa clase. (Más sobre esto abajo).
    
      
    
- **`int` (Tipo de retorno):** Java es de tipado estricto. Tenés que declarar qué tipo de dato va a devolver el método (`int`, `String`, `boolean`, un objeto como `Estudiante`, etc.). Si el método hace un trabajo pero no devuelve ningún valor, se usa la palabra reservada **`void`**.
    
      
    
- **`sumar` (Nombre):** Por convención en Java, los nombres de los métodos se escriben en `camelCase` (empezando con minúscula y usando mayúsculas para separar palabras, ej: `calcularPromedioTotal`).
    
      
    
- **`int a, int b` (Parámetros):** Las variables que recibe el método. Cada una debe tener su tipo de dato explícitamente declarado.
    
      
    

## 2. Métodos de Instancia vs. Métodos Estáticos (`static`)

Esta es la diferencia más importante al empezar a programar en Java, especialmente si venís de lenguajes estructurados.

### Métodos de Instancia (Sin `static`)

Son comportamientos que le pertenecen a un objeto específico. Para usarlos, primero tenés que crear el objeto en memoria (instanciarlo) usando `new`. Tienen acceso a los atributos internos de ese objeto particular.

  

```Java
public class Perro {
    public String nombre;

    // Método de instancia
    public void ladrar() {
        System.out.println(this.nombre + " dice: ¡Guau!");
    }
}

// Para usarlo en tu Main:
Perro miPerro = new Perro();
miPerro.nombre = "Firulais";
miPerro.ladrar(); // Necesitás el objeto 'miPerro' para llamar al método
```

### Métodos Estáticos (Con `static`)

Pertenecen a la clase en general, no a un objeto individual. Se usan mucho para operaciones genéricas, funciones matemáticas o herramientas de utilidad. No pueden acceder a variables de instancia (como el `nombre` del perro) porque no dependen de un objeto.

  

```Java
public class Calculadora {
    // Método estático
    public static int multiplicar(int x, int y) {
        return x * y;
    }
}

// Para usarlo en tu Main:
int resultado = Calculadora.multiplicar(5, 3); // Llamás directo a la clase, sin usar 'new'
```

## 3. Sobrecarga de Métodos (Overloading)

Java te permite tener **múltiples métodos con el mismo nombre exacto** dentro de la misma clase, siempre y cuando sus parámetros sean diferentes (ya sea en cantidad, en orden, o en tipo de dato). Java se da cuenta automáticamente de cuál método debe ejecutar basándose en lo que le pasás en los paréntesis.

  
```Java
public class Impresora {
    // Opción 1: Recibe un String
    public void imprimir(String texto) {
        System.out.println("Imprimiendo texto: " + texto);
    }

    // Opción 2: Recibe un entero
    public void imprimir(int numero) {
        System.out.println("Imprimiendo número: " + numero);
    }
}
```

## 4. El paso de parámetros: ¿Valor o Referencia?

Este es un detalle técnico crucial sobre cómo Java maneja la memoria debajo del capó: **En Java, todo se pasa por valor, siempre.**

  

1. **Tipos primitivos (`int`, `float`, `boolean`, `char`):** Se pasa una copia exacta del valor. Si modificás el parámetro adentro del método, la variable original que quedó afuera no se ve afectada.
    
      
    
2. **Objetos y Arrays (`String`, `Estudiante`, `int[]`):** Lo que se pasa por valor es **la dirección de memoria** donde vive ese objeto. Esto significa que si le pasás un arreglo a un método y modificás una posición de ese arreglo adentro del método, el arreglo original afuera **sí** se va a modificar.








  
# Metodos estaticos


**1. Un método estático SÍ puede llamar a otro método estático**

Como ambos pertenecen a la clase (y no a un objeto particular), pueden comunicarse directamente, incluso si están en la misma clase.


```Java
public class Utilidades {
    public static void iniciarProceso() {
        System.out.println("Iniciando...");
        verificarDatos(); // Llamada directa permitida
    }
    
    public static void verificarDatos() {
        System.out.println("Datos verificados.");
    }
}
```

**2. Un método estático NO puede llamar a un método de instancia directamente**

Esta es la restricción más común y el típico error cuando intentas llamar a una función desde el `public static void main`. Como el método estático existe antes de que se cree cualquier objeto, no sabe a qué objeto específico le estás pidiendo que ejecute la acción.

  
```Java
public class Sistema {
    public void saludar() { // Método de instancia (NO es estático)
        System.out.println("Hola");
    }

    public static void main(String[] args) {
        // saludar(); // ❌ ERROR: no se puede hacer referencia a un método no estático desde un contexto estático
        
        // ✅ FORMA CORRECTA: Crear el objeto primero
        Sistema miSistema = new Sistema();
        miSistema.saludar(); 
    }
}
```

**3. Un método estático NO puede usar variables de instancia**

Por la misma razón anterior: no puede acceder a variables que nacen solo cuando se hace un `new`. Un método estático solo puede modificar o leer variables que también estén declaradas como `static`.


**4. Un método estático NO puede usar `this` ni `super`**

La palabra clave `this` en Java significa "este objeto en particular". Como los métodos estáticos pertenecen al molde (la clase) y no a los objetos generados, usar `this` dentro de un método `static` da un error de compilación inmediato. Lo mismo aplica para `super` (que hace referencia al objeto de la clase padre).

  
**5. (Bonus) Un método de instancia SÍ puede llamar a un método estático**

La restricción es de un solo lado. Si estás adentro de un método normal (no estático), podés llamar a métodos estáticos sin problema, porque si el objeto ya existe, la clase a la que pertenece obviamente también.



![[Pasted image 20260907004326.png]]

No le pasás parámetros porque `sayHello()` es un **método de instancia** (no tiene la palabra `static`), lo que significa que tiene acceso directo e interno a todos los atributos definidos en su propia clase (`name` y `age`).

En la Programación Orientada a Objetos, los objetos guardan su propio estado. No necesitás enviarle la información por la "puerta" de los paréntesis porque el método simplemente lee lo que el objeto ya tiene guardado en su memoria.

Así es como se vería el uso de esta clase en tu archivo principal:

```java
Person persona = new Person();

// 1. Primero le cargás los datos directamente a los atributos del objeto
persona.name = "Juan";
persona.age = 25;

// 2. Al llamar al método, este lee automáticamente su propia información interna
persona.sayHello(); // Imprime: "Hola, soy Juan y tengo 25 años."
```

Si el método fuera una función aislada o estática que no pertenece a ningún objeto en particular, sí estarías obligado a pasarle `(String name, int age)` por parámetro para que sepa con qué textos y números trabajar. Pero al ser parte de la clase `Person`, ya es dueño de esa información.