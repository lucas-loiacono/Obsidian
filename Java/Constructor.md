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