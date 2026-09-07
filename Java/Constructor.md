El constructor es un método especial que se ejecuta automáticamente en el instante exacto en que creás un objeto usando la palabra **`new`**. Su trabajo principal es inicializar los atributos de la clase para que el objeto nazca con datos válidos desde el primer segundo.

Para crearlo, tiene **dos reglas estrictas**:

1. Tiene que llamarse **exactamente igual** que la clase (respetando mayúsculas).
    
      
    
2. **No tiene tipo de retorno** (ni `int`, ni `String`, ni siquiera `void`).
    
      
    
Tomando el mismo código de la clase `Person` que mostraste recién, así es como se le agrega su constructor:


```java
public class Person {
    
    // Atributos
    String name;
    int age;

    // ---> ESTE ES EL CONSTRUCTOR <---
    public Person(String name, int age) {
        this.name = name; // Guarda el nombre que entra por parámetro en el atributo de la clase
        this.age = age;   // Guarda la edad
    }

    // Métodos
    public void sayHello() {
        System.out.println("Hola, soy " + name + " y tengo " + age + " años.");
    }
}
```

### ¿Cómo cambia esto la forma de usar la clase?

Antes, para darle datos a la persona, tenías que hacerlo en tres pasos (crear, asignar nombre, asignar edad). Ahora, el constructor te obliga a pasarle los datos por paréntesis en la misma línea que hacés el `new`:

  

```Java
// Se ejecuta el constructor automáticamente y le pasa "Juan" y 25
Person persona = new Person("Juan", 25); 

// El objeto ya nace listo para usar
persona.sayHello(); 
```

### El uso de la palabra `this`

Habrás notado que adentro del constructor dice `this.name = name;`.

  
- El `name` que está a la derecha del igual es el **parámetro** (el que viene de afuera, "Juan").
    
      
- El `this.name` que está a la izquierda es el **atributo** de la clase (la variable que está declarada arriba de todo).
    
    Usamos `this.` para decirle a Java: _"Agarrá el dato que me acaban de pasar y guardalo en MI memoria interna, no lo pierdas"_.


### ¿Y por qué tu código anterior funcionaba sin constructor?

Si vos no escribís ningún constructor en tu clase, Java, de forma invisible, inyecta un **"constructor por defecto"** que está completamente vacío (`public Person() {}`). Por eso antes podías hacer `new Person()` sin pasarle nada. Pero apenas vos escribís tu propio constructor con parámetros, Java borra el suyo por defecto y te obliga a usar el que vos inventaste.


![[Pasted image 20260907010645.png]]


![[Pasted image 20260907010551.png]]


La diferencia exacta radica en el **Encapsulamiento** (uno de los pilares de la POO). En la imagen que enviaste estás viendo una **asignación directa**, un enfoque súper común y válido en tutoriales iniciales para no marear con tantos conceptos a la vez, pero que en un entorno universitario o profesional se considera una mala práctica arquitectónica.

Acá está el desglose de lo que pasa en tu captura frente a la estructura con Setters que armaste para tus notas:

**1. El código de la imagen (Acceso Directo)** Fijate que en la clase `Person`, los atributos `String name;` e `int age;` no tienen la palabra `private` adelante. Al estar desprotegidos, cualquier otra clase (como tu `main`) puede agarrar el objeto y modificarle las variables a la fuerza usando el punto: `person.age = 38;`.

**2. El código con Setters (Encapsulamiento)** Si a esos atributos les pusieras `private String name;`, Java automáticamente cerraría esa puerta con llave. Si alguien intentara hacer `person.age = 38;` en el `main`, IntelliJ te marcaría todo el renglón en rojo con un error de compilación. Para poder inyectarle la información, el `main` estaría obligado a usar el método oficial que provee la clase: `person.setAge(38);`.

### ¿Por qué te van a exigir usar Setters en vez de hacerlo como en la imagen?

La respuesta es **control y validación del estado del objeto**.

Si dejás los atributos abiertos para que el `main` los modifique directamente, como se ve en la captura, el día de mañana un error en el código podría mandar `person.age = -1500;` y el objeto `Person` se lo tragaría sin chistar. Tendrías una persona con edad negativa en tu sistema.

Si usás un Setter, el objeto `Person` recupera el control sobre sus propios datos, porque podés ponerle un filtro:


```Java
public void setAge(int age) {
    if (age >= 0) {
        this.age = age; // Solo se guarda si el dato tiene sentido
    } else {
        System.out.println("Error: Una persona no puede tener edad negativa.");
    }
}
```

En resumen: el enfoque de la imagen funciona perfecto para practicar la sintaxis inicial, pero a medida que empieces a diseñar sistemas más complejos aplicando reglas sólidas de diseño de clases, vas a necesitar blindar todos tus atributos con `private` y usar constructores o Setters.












# 📌 Apunte Definitivo: Estado de Objetos y Encapsulamiento en Java

En la Programación Orientada a Objetos (POO), la forma en que le damos estado (datos) a un objeto define la robustez de todo el sistema. A continuación, la evolución desde el enfoque básico hasta el estándar profesional.

---

## 1. Asignación Directa (El Anti-patrón)
Es el método más permisivo, común en tutoriales iniciales pero **fuertemente penalizado en entornos universitarios y profesionales**. 

*   **Cómo funciona:** Los atributos se declaran sin modificador de acceso (o como `public`).
*   **Implementación:** Se accede a la variable directamente desde afuera usando un punto (`.`).
*   **El Problema Crítico:** Rompe el principio de seguridad. Cualquier parte del programa puede inyectar datos inválidos (ej: una edad de `-500` o un `null`) y el objeto no tiene forma de defenderse ni de validarlos.

```java
// CLASE
public class Person {
    String name; // Desprotegido
    int age;     // Desprotegido
}

// MAIN
Person persona = new Person();
persona.age = 38; // Inyección directa sin control
```

## 2. El Estándar POO: Encapsulamiento (`private`)

Para solucionar el problema anterior, la POO exige que **todos los atributos de una clase sean privados**.

Al poner la palabra `private` adelante de la variable, esta queda blindada. Nadie fuera del propio archivo puede verla, leerla ni modificarla. El objeto recupera el control absoluto de su memoria.


Al cerrar esta puerta, Java nos obliga a usar métodos controlados (Constructores y Setters) para dejar entrar la información.

  

## 3. Inicialización mediante Constructor (Datos Obligatorios)

El constructor es el mecanismo para **cargar datos en el instante exacto en que el objeto nace**. Es ideal para los atributos vitales sin los cuales el objeto no tiene sentido que exista (ej: no podés crear un alumno sin DNI o Padrón).

  

- **Reglas:** Se llama exactamente igual que la clase y no tiene tipo de retorno (ni siquiera `void`).
    
      
- **Uso de `this`:** Se usa `this.atributo` para diferenciar la variable interna de la clase del parámetro que viene de afuera.
    


```java
// CLASE
public class Person {
    private String name;
    private int age;

    // CONSTRUCTOR
    public Person(String name, int age) {
        this.name = name; 
        this.age = age;   
    }
}

// MAIN
// El objeto nace 100% completo y listo para usarse
Person persona = new Person("Brais", 38); 
```

## 4. Modificación mediante Setters (Datos Dinámicos / Opcionales)

Si un dato cambia a lo largo del tiempo (como la edad o el domicilio) o no era obligatorio al momento de crear el objeto, se utilizan los **Setters**. Son métodos públicos dedicados exclusivamente a modificar un único atributo privado.

  
- **La gran ventaja:** Como la información tiene que pasar por este método antes de guardarse en el atributo, **podés agregar lógica de validación (ifs)**.
    


```java
// CLASE
public class Person {
    private int age;

    // SETTER CON VALIDACIÓN
    public void setAge(int age) {
        if (age >= 0 && age <= 120) {
            this.age = age; // El dato es válido, se guarda.
        } else {
            System.out.println("Error: Edad inválida.");
        }
    }
}

// MAIN
Person persona = new Person();
persona.setAge(38); // Pasa por el filtro de seguridad y luego se guarda
```

## 5. Lectura mediante Getters

Al ser los atributos `private`, el `main` tampoco puede imprimirlos con un `System.out.println(persona.name);`. Para extraer la información de forma segura (solo lectura), se crean los métodos **Getters**.

```java
public String getName() {
    return this.name;
}
```

## 💡 Resumen Visual de la Clase Perfecta (Estructura Final)


```java
public class Person {
    
    // 1. Atributos siempre privados
    private String name;
    private int age;

    // 2. Constructor (Nacimiento del objeto)
    public Person(String name, int age) {
        this.name = name;
        this.setAge(age); // Buena práctica: usar el setter interno para aprovechar su validación
    }

    // 3. Getters (Para leer de forma segura)
    public String getName() { return this.name; }
    public int getAge() { return this.age; }

    // 4. Setters (Para modificar de forma segura)
    public void setName(String name) { 
        this.name = name; 
    }
    
    public void setAge(int age) {
        if (age >= 0) {
            this.age = age;
        }
    }
}
```

