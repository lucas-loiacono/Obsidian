![[Pasted image 20260915180609.png]]

![[Pasted image 20260915180639.png]]

 heredan los atributos y métodos de la clase padre, pero por ejemplo mostrar cambia el método, ya que es distinto al de la clase rodado

sobreescritura:(override) es un método que se llama igual y que tiene los mismos parámetros que la clase base, 
sobrecarga(overloading): es un método que se llama igual pero tiene distintos parámetros


![[Pasted image 20260920191405.png]]


![[Pasted image 20260920191536.png]]

![[Pasted image 20260920191622.png]]

![[Pasted image 20260920191752.png]]

Acá mi clase perro tendría el método ladrar y comer

![[Pasted image 20260920191906.png]]

si yo quiero usar para el gato el mismo constructor que para animal, esto lo hago llamando al método super() y le agrega el mensaje al constructor

Prácticamente copia  y pega el constructor de animal y sigue con el constructor líneas abajo


![[Pasted image 20260920192151.png]]

![[Pasted image 20260920192356.png]]

como se comportan los animales

![[Pasted image 20260920192621.png]]

Poder modelar para cada tipo de objeto distintos comportamientos


![[Pasted image 20260920192800.png]]

En este caso el polimorfismo dinámico, ya que se llaman igual y tienen los mismos parámetros.
Esto se resuelve dentro de los métodos de las subclases

![[Pasted image 20260920193026.png]]

Es una clase que no se instancia, es como que instancie la clase animal, y de ahí saque dos subclases como por ejemplo perro y gato, pero nunca instancio la clase animal. sirve para guardar todo dentro de una misma bolsa

También se puede definir métodos abstractos, en el cual lo que hago es definirlo pero no implementarlo. Es como dejar un molde para que las subclases luego las modifiquen

![[Pasted image 20260920193347.png]]\

![[Pasted image 20260920194314.png]]

yo al poner el override le estoy avisando al compilador como actúa ese método

![[Pasted image 20260920194633.png]]

Una interfaz lo que tiene que hacer es la firma de los métodos de una clase, que métodos debería tener

![[Pasted image 20260920195304.png]]

![[Pasted image 20260920200004.png]]