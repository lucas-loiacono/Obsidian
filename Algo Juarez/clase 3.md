
![[Pasted image 20260825182208.png]]

POO: hay que pensar el sistema como objetos que interactúan entre si, no se piensa como c o python, donde tengo que desarrollar un sistema, tengo que mirar el scope de hasta donde abarca el sistema. yo cuando pienso en objeto tengo que pensar en un objeto medico, otro objeto paciente, otro que sea turno y así, y los tengo que relacionar entre si.

los objetos son aquellos que pueden ser reutilizables y que tenga varias instancias, por ejemplo paciente, yo voy a tener varios pacientes en la clínica, en el cual tiene información, como por ejemplo el DNI, lo tengo que pensar como molde para poder crear muchos, por ejemplo paciente puede ser un molde y cada uno tiene sus atributos



![[Pasted image 20260825184203.png]]


Cada objeto tiene sus atributos (guardo características del objeto) y métodos (su comportamiento con el sistema)

Se le dice instancia a un objeto especifico

![[Pasted image 20260825184443.png]]

S: única responsabilidad, pensar una clase que cumpla un solo rol, que tenga una sola responsabilidad, por ejemplo no podría poner una clase hospital que cumpla los roles de turnos, médicos

O: open close, el código tiene que ser abierto a la extensión, pero cerrado a la modificación (encapsulación). se tiene que poder aumentar el comportamiento, pero cuidando la salud de mi objeto, cuidando la variante de representación del objeto, ya que si se lo paso a una persona le puede cambiar cosas que quiero y cosas que no quiero, entonces se encapsula lo que no se puede cambiar, mientras que le dejo al usuario que se pueda expandir pero le pongo ese limite. para esto pongo los atributos del objeto en privado


![[Pasted image 20260825190502.png]]

![[Pasted image 20260825190803.png]]

También para que no me puedan cambiar los atributos de mi objeto para que no me lo rompan, ósea que deje de ser lo mas parecido al objeto que quiero representar


En la imagen **image_e81ba4.jpg** se muestran los principios **SOLID**, un conjunto de reglas fundamentales en la Programación Orientada a Objetos (POO) diseñadas para crear software más fácil de mantener, entender y escalar.

El significado de cada sigla es el siguiente:

- **S - Single Responsibility Principle (Principio de Responsabilidad Única):** Una clase debe tener un solo propósito o responsabilidad. Como indica la diapositiva, cada clase debe respetar su "razón de existir". Si una clase hace demasiadas cosas distintas, cualquier pequeño cambio en el sistema obligará a modificarla constantemente.
    
- **O - Open-Closed Principle (Principio de Abierto/Cerrado):** Las clases deben estar _abiertas a la extensión_, pero _cerradas a la modificación_. Esto significa que debes poder agregar nuevas funcionalidades (por ejemplo, creando nuevas clases hijas o implementando interfaces) sin necesidad de tocar o alterar el código fuente original que ya funciona.
    
- **L - Liskov Substitution Principle (Principio de Sustitución de Liskov):** Las clases derivadas (hijas) deben poder sustituir a sus clases base (padres) sin alterar el correcto funcionamiento del programa. Si el sistema espera usar la clase padre, pasarle una clase hija no debería romper nada.
    
- **I - Interface Segregation Principle (Principio de Segregación de Interfaces):** Es mejor crear muchas interfaces pequeñas y muy específicas en lugar de una sola interfaz gigante y de propósito general. Ninguna clase debería verse obligada a depender de o implementar métodos que no va a utilizar.
    
- **D - Dependency Inversion Principle (Principio de Inversión de Dependencias):** Los módulos de alto nivel no deben depender de los módulos de bajo nivel; ambos deben depender de abstracciones (interfaces). Esto asegura que tu código dependa de "contratos" generales en lugar de implementaciones concretas, facilitando los cambios a futuro.
    

**¿Qué es el encapsulamiento?** Es uno de los pilares de la POO. Consiste en **ocultar el estado interno** (los datos, atributos o variables) de un objeto para que no pueda ser leído ni alterado directamente por otras clases (lo que tu diapositiva llama "no exponerse a otras clases"). En lugar de dejar los datos públicos, se los declara como privados y se interactúa con ellos a través de métodos controlados. Esto protege la lógica interna y asegura que los datos no se corrompan desde afuera.

**¿Por qué el encapsulamiento se relaciona fuertemente con la 'O' (Open-Closed)?** El encapsulamiento es la herramienta principal que te permite cumplir con la parte de **"cerrado a la modificación"**.

Si no encapsulas tu código (dejando todo público), cualquier otra parte del sistema podría entrar y modificar el estado de esa clase directamente. Al encapsular, blindas la estructura interna de la clase. De este modo, garantizas que la única forma de añadirle nuevo comportamiento al sistema sea extendiéndolo (creando nuevas clases que hereden o interactúen con la base) y no abriendo la clase original para modificar su código interno, cumpliendo exactamente con el Principio de Abierto-Cerrado.

![[Pasted image 20260825191405.png]]


![[Pasted image 20260830230236.png]]

![[Pasted image 20260825191520.png]]

![[Pasted image 20260825192759.png]]




``` java
class Persona {
    private String nombre;
    private Integer edad;

    // Constructor de Personas
    Persona(String n, Integer e) {
        nombre = n;
        if (e > 0) { // <-- Se completa la condición vacía de la imagen
            edad = e;
        } else {
            System.out.println("ingresa una edad valida!"); // Sysout
        }
    }

    // Método para modificar los datos (Setter)
    void setPersona(String n, Integer e) {
        nombre = n;
        if (e > 0) {
            edad = e;
        } else {
            System.out.println("ingresa una edad valida!");
        }
    }
}
```



En el código de la imagen **image_f3788a.png**, el encapsulamiento se aplica declarando los atributos como `private` y usando los métodos (como el constructor y `setPersona`) como "filtros" obligatorios para validar los datos antes de guardarlos.

Funciona de la siguiente manera:

- **Ocultamiento (`private`):** Al definir `private Integer edad;`, bloqueas el acceso directo a la variable. Esto impide que desde la función `main` alguien haga algo como `p1.edad = -10;` y corrompa los datos.
    
- **Control y Validación:** Como el exterior no puede tocar `edad` directamente, la única forma de modificar ese dato es pidiéndoselo a la clase a través de `setPersona(n, e)`. Al hacerlo, la clase ejecuta su regla de negocio: `if (e > 0)`. Esto garantiza que la edad asignada tenga sentido lógico. Si el valor es negativo o cero, la variable interna se protege, no se modifica y se rechaza la operación con el mensaje "ingresa una edad valida!".


![[Pasted image 20260825193340.png]]

TDA

![[Pasted image 20260825193750.png]]

Un **TDA** (Tipo de Dato Abstracto o _Abstract Data Type_) es un modelo conceptual o un "contrato" que define **qué datos almacena y qué operaciones se pueden realizar con ellos**, sin importar **cómo** está programado por dentro.

### La idea central: El _Qué_ vs. El _Cómo_

- **El TDA define el _QUÉ_:** Especifica las acciones disponibles (la interfaz o comportamiento público).
    
- **La implementación define el _CÓMO_:** Es el código real (la clase, los punteros, los arreglos o la memoria) que hace que esas operaciones funcionen.
    

### Una analogía simple: La Cafetera

Piensa en una cafetera como un TDA:

- **Operaciones (TDA):** `encender()`, `cargarAgua()`, `prepararCafe()`. A ti solo te interesa saber que al apretar `prepararCafe()` obtienes un café.
    
- **Implementación interna:** Si por dentro usa una bomba de presión, resistencias térmicas o válvulas mecánicas, al usuario le da igual. Si el fabricante cambia el circuito interno pero mantiene los mismos botones, la cafetera sigue funcionando igual para quien la usa.
    

### Desglosando los puntos de la diapositiva

1. **"Es un mecanismo de descripción de alto nivel que, al implementarse, genera una clase":**
    
    El TDA es el diseño teórico (en papel o en abstracción). Cuando tomas ese diseño y lo programas en un lenguaje como Java, C++ o Python, escribes una **clase** con sus atributos y métodos.
    
2. **"Es una estructura de datos definida por las operaciones que puede hacer y no por cómo hacerlas":**
    
    Por ejemplo, el TDA **Pila (Stack)** se define únicamente por dos operaciones:
    
    - `apilar(elemento)` (push)
        
    - `desapilar()` (pop)
        
    
    No importa si por dentro se implementó usando un arreglo estático (`int[]`) o una lista enlazada con punteros (`Node*`). Mientras cumpla con esas operaciones, sigue siendo una Pila.
    

### Resumen de la diferencia clave

| **Concepto**           | **Rol**                            | **Enfoque**                                    |
| ---------------------- | ---------------------------------- | ---------------------------------------------- |
| **TDA**                | Modelo conceptual / Especificación | Qué hace (operaciones y comportamiento)        |
| **Estructura / Clase** | Código real en memoria             | Cómo lo hace (variables, algoritmos, punteros) |







Te lo tienes que imaginar como el **boceto o contrato de todas las acciones válidas** que definen a esa entidad, no solo de una acción principal aislada.

Un TDA representa el **paquete completo de comportamiento**: define qué información representa y el conjunto exacto de operaciones que se le pueden pedir desde afuera.

### ¿Por qué el conjunto de acciones y no solo la principal?

Tomemos como ejemplo una **Cuenta Bancaria**:

- Si piensas solo en la "acción principal", podrías pensar únicamente en `transferirDinero()`.
    
- Sin embargo, el **TDA Cuenta Bancaria** es el conjunto completo de reglas y operaciones permitidas:
    
    - `depositar(monto)`
        
    - `extraer(monto)`
        
    - `consultarSaldo()`
        

El TDA define **todas las formas posibles en que el mundo exterior puede interactuar con los datos**. Todo lo que esté fuera de ese boceto simplemente no existe para quien usa el TDA.

### La relación exacta entre TDA e Interfaces / Clases

Para visualizarlo de forma práctica en código:

1. **El TDA es el plano / contrato (en Java sería una `interface`):**
    
    Dice qué métodos existen, qué parámetros reciben y qué devuelven, sin una sola línea de código real dentro.
    
2. **La Clase es la implementación real:**
    
    Es donde escribes las variables (`private double saldo;`) y el código que hace funcionar cada una de esas acciones.




![[Pasted image 20260825194123.png]]

![[Pasted image 20260825194548.png]]

![[Pasted image 20260831004334.png]]

![[Pasted image 20260831004553.png]]

![[Pasted image 20260831004902.png]]

El **UML** (Lenguaje Unificado de Modelado, por sus siglas en inglés) es un lenguaje visual gráfico y estandarizado que se utiliza en ingeniería de software para diseñar, documentar y planificar la estructura de un sistema antes de escribir el código.

  

Así como un arquitecto hace un plano antes de construir una casa, un programador usa UML para dibujar la arquitectura de su programa.

  

En el contexto de la Programación Orientada a Objetos y los TDAs que venías viendo, la herramienta principal del UML es el **Diagrama de Clases**, que sirve para representar visualmente tus "bocetos":

  

- **Estructura del diagrama:** Cada clase se dibuja como un rectángulo dividido horizontalmente en tres bloques:
    
      
    1. El nombre de la clase (ej. `Complejo`).
        
          
        
    2. Los atributos o variables (el dominio).
        
          
        
    3. Los métodos u operaciones (el comportamiento).
        
          
        
- **Simbología de Encapsulamiento:** El UML usa símbolos específicos para indicar qué es visible y qué está oculto, mapeando exactamente los conceptos de público y privado:
    
      
    - `-` (Signo menos): Indica que el atributo o método es **private** (ej. `- real: double`).
        
          
        
    - `+` (Signo más): Indica que es **public** (ej. `+ sumar(otro: Complejo)`).
        
          
        
    - `#` (Numeral): Indica que es **protected** (se usa cuando hay herencia).
        
          
        
- **Relaciones y Dependencias:** Permite dibujar distintos tipos de líneas y flechas conectando los rectángulos para mostrar cómo interactúan las clases entre sí (quién hereda de quién, quién depende de quién, etc.).
    
      
    

Básicamente, el UML es el estándar universal que te permite agarrar la definición teórica de un TDA y plasmarla en un gráfico que cualquier otro programador del mundo pueda entender rápidamente, sin importar si luego lo van a programar en Java, Python, C o cualquier otro lenguaje.


![[Pasted image 20260831005523.png]]

La imagen **image_f63a28.png** es tu "diccionario" visual de UML. Como puedes ver, el lado izquierdo confirma exactamente lo que acabamos de hablar: el rectángulo dividido en tres partes (Nombre, Atributos, Métodos) y los signos de visibilidad (`+`, `-`, `#`) que te permiten graficar el encapsulamiento.

  

La parte nueva de esta diapositiva son las herramientas para conectar tus clases (TDAs) entre sí:

  

**1. Relaciones básicas (Las flechas)**

En un programa real, las clases no están aisladas; interactúan.

  

- **Herencia (flecha con triángulo vacío):** Representa una relación de "es un tipo de". Por ejemplo, si tienes una clase `Perro`, usarías esta flecha apuntando hacia una clase padre llamada `Animal`.
    
      
    
- **Asociación (flecha simple):** Representa una relación de "tiene un", "conoce a" o "usa un". Por ejemplo, una clase `Cliente` tendría una flecha de asociación apuntando hacia una clase `CuentaBancaria`.
    
      
    

**2. Multiplicidad**

Estos números se escriben en los extremos de la flecha de Asociación para definir las reglas de cantidad en esa relación:

  

- **`1` (Exactamente 1):** Un país tiene _exactamente 1_ ciudad capital.
    
      
    
- **`0..1` (Cero a uno):** Un conductor puede tener _0 o 1_ auto asignado en este momento.
    
      
    
- **`0..*` o `*` (Cero a muchos / Muchos):** Un profesor puede tener _0 o muchos_ alumnos en su clase.
    
      
    

Con estos elementos ya tienes lo necesario para dibujar el plano arquitectónico de cualquier sistema orientado a objetos antes de escribir la primera línea de código.



![[Pasted image 20260831011445.png]]

La dirección de la flecha en una asociación (la punta que señala desde `Persona` hacia `Coche`) indica la **navegabilidad** de la relación. Básicamente, define "quién conoce a quién".

  

- **Por qué apunta hacia Coche:** Significa que la clase `Persona` conoce y tiene acceso a sus coches, pero el `Coche` no tiene idea de quién es su dueño (la relación es unidireccional).
    
      
    
- **Cómo se traduce al código:** Esto implica que dentro de la clase `Persona` existirá un atributo oculto (por ejemplo, una lista o un arreglo) para guardar objetos de tipo `Coche`. Por el contrario, dentro de la clase `Coche` no habrá ninguna variable que guarde a la `Persona`.
    
      
    

**Explicación general de la imagen:**

  

La imagen **image_f641ea.jpg** es un ejemplo integrador que une los conceptos de TDA, encapsulamiento y UML. Destaca reglas prácticas para armar estos diagramas:

  

- **Aplicación del Encapsulamiento:** Muestra gráficamente cómo los datos (`modelo`, `marca`, `nombre`, `edad`) llevan un `-` por ser privados, mientras que las acciones (`requiereMecanico()`, `mostrarDatos()`) llevan un `+` por ser públicas. También muestra la sintaxis estandarizada para definir los parámetros y lo que devuelve un método (ej. `: Boolean`).
    
      
    
- **La regla de oro de la Asociación:** El texto a la derecha aclara un error muy común al dibujar UML: _"no se pone el atributo si se dibuja la relación"_. Como ya dibujaste la flecha que indica que la Persona tiene Coches, **está mal** escribir un atributo llamado `- misCoches: Coche[]` dentro de la caja de `Persona`. La flecha es la representación gráfica de ese atributo.
    
      
    
- **Lectura de la Multiplicidad:** Los números te dictan las reglas del negocio. Se lee combinando ambos extremos de la flecha: "Exactamente **1** `Persona` puede tener entre **0 y muchos** (`0..*`) objetos de tipo `Coche`".



La multiplicidad en UML siempre se lee en ambas direcciones cruzadas para entender la regla de negocio completa que estás modelando:

- **De Persona a Coche:** Te paras en la clase `Persona`, sigues la línea y miras el número que está del lado opuesto (`0..*`). Esto significa que **1 Persona puede tener de 0 a muchos Coches**.
    
- **De Coche a Persona:** Te paras en la clase `Coche`, haces el camino inverso y miras el número que está del lado de la clase Persona (`1`). Esto significa que **1 Coche le pertenece a exactamente 1 Persona** (es decir, en este sistema un coche no puede estar sin dueño, ni ser propiedad compartida de dos personas a la vez).
    

Es tal cual lo dedujiste. Esas anotaciones (`1` y `0..*`) son fundamentales porque te dictan exactamente cómo vas a tener que estructurar el código y tu base de datos cuando pases del diseño a la programación real.





![[Pasted image 20260831012222.png]]

![[Pasted image 20260831012233.png]]

![[Pasted image 20260831012540.png]]


![[Pasted image 20260831013408.png]]

![[Pasted image 20260831013643.png]]ahi recien active las teclas rapidas para ver como funciona este teclado con el punto de activacion en 0.001