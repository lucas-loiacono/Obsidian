
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

![[Pasted image 20260825191520.png]]

![[Pasted image 20260825192759.png]]

![[Pasted image 20260825193340.png]]

TDA

![[Pasted image 20260825193750.png]]

![[Pasted image 20260825194123.png]]

![[Pasted image 20260825194548.png]]