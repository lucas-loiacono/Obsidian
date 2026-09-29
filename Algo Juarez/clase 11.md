![[Pasted image 20260927192224.png]]

uno no sabe quien es el primero, pero sabe quien es el ultimo y se tiene de referencia
cada uno tiene lo que tiene que representar y la referencia al de delante suyo, el primero tiene referencia nula al no tener nadie delante suya

para la pila se hace la referencia al anterior y para la cola al posterior

![[Pasted image 20260929180531.png]]

El primero tiene referencia nula

![[Pasted image 20260927193255.png]]

![[Pasted image 20260927195027.png]]

![[Pasted image 20260927195203.png]]

si corto mi cadena, una parte se pierde de la otra, se separan

![[Pasted image 20260929181807.png]]

![[Pasted image 20260929181846.png]]
ya no necesito memoria contigua, puede estar separado dentro de la memoria, pero si corto la cadena pierdo la referencia a los siguientes

![[Pasted image 20260927200442.png]]

para referenciar a otro nodo se le pasa la misma clase a siguiente, ya que es del mismo tipo de dato

![[Pasted image 20260927200502.png]]


```java 
package estructuras;

public class Nodo<T> {
	// atributos
	private T dato;//el tipo de dato que quiero guardar
	private Nodo<T> siguiente; //referencia al siguiente nodo

	// metodos
	// Constructor
	public Nodo(T elem) {
		dato = elem;
		siguiente = null; //lo puedo dejar en null y despues pasarle asignar aparte
	}

	
	public Nodo(T elem, Nodo<T> sig) {
		dato = elem;
		siguiente = sig;
	}
	
	
	// get y set
	public T obtenerDato() {
		return dato;
	}
	
	public void asignarDato(T dato) {
		this.dato = dato;
	}
	
	public Nodo<T> obtenerSiguiente() {
		return siguiente;
	}
	
	public void asignarSiguiente(Nodo<T> siguiente) {
		this.siguiente = siguiente;
	}
```

# Pila dinámica

![[Pasted image 20260927200718.png]]

Lo único que necesito es tener la referencia al ultimo dato, que se encarga de quien le viene delante 
antes metíamos la pila dentro de un vector, ahora como tenemos nodos, podemos no tener un vector y tener referencias enlazadas 

```java
package estructuras;

public class PilaD<T> {
	// Atributos
	private Nodo<T> ultimo; //lo unico que tengo que saber es cual es el ultimo, despues de ahi tengo que ver cuales son los siguientes
	
	
	
	// Metodos
	// Constructor
	// PRE: - 
	// POS: crea una pila vacia
	public PilaD() {
		System.out.println("------------ Pila dinamica ------------------------");
		ultimo = null; //como creo una pila vacia, no tengo elemento, por lo cual                                                es null
	}
	
	// Alta
	// PRE: -
	// POS: agrega el elemento al final de la Pila 
	public void alta(T elem) {
		Nodo<T> nuevo = new Nodo<>(elem, ultimo); // paso 1 y 2
		//nuevo.asignarSiguiente(ultimo);   // paso 2
		ultimo = nuevo;					  // paso 3
	}
	
	// Consulta
	// PRE: la Pila no tiene que estar vacia: --> vacia() -> false
	// POS: devuelve el ultimo elemento
	public T consulta() {
		return ultimo.obtenerDato();
	}

	// PRE: -
	// POS: devuelve true si la pila esta vacia, false de lo contrario
	public boolean vacia() {
		return (ultimo == null);
	}

	// Baja
	// PRE: la Pila no tiene que estar vacia: --> vacia() -> false
	// POS: da de baja al ultimo elemento
	public void baja() {
		ultimo = ultimo.obtenerSiguiente();
	}
}
```


en  una pila siempre se da de baja y consulta el ultimo

![[Pasted image 20260927232404.png]]

Mi ultimo es el A, cuando doy de baja a A mi ultimo pasa a ser mi C

![[Pasted image 20260927232513.png]]

![[Pasted image 20260927235305.png]]

cuando doy de baja al ultimo, mi referencia queda en null




![[Pasted image 20260928000330.png]]

![[Pasted image 20260929194740.png]]

Cuando doy de baja al ultimo, tengo que pasar mi referencia de ultimo a siguiente
Como le saco la referencia de ultimo a mi elemento, pasa el recolector de basura y lo elimina, y le asigno mi ultimo al siguiente elemento




![[Pasted image 20260928000539.png]]

Para dar de alta un dato lo que tengo que hacer es meter el dato en un nodo

1. Primero lo tengo que enganchar al ultimo,
2. Después le paso la referencia de mi ultimo al nuevo

![[Pasted image 20260928001058.png]]





![[Pasted image 20260928003849.png]]

yo cuando creo una pila, mi ultimo no va a estar referenciando a nada

![[Pasted image 20260928004048.png]]

# Cola

entra por el final y sale al principio

los nuevos van al final, y se van procesando y consultando los primeros de la cola

![[Pasted image 20260928005525.png]]


Para esto tengo que tener dos referencias, una al primero y otra al ultimo, asi para las funciones del ultimo, por ejemplo procesar o consultar no me tengo que recorrer todo para llevar al ultimo al primer lugar

![[Pasted image 20260928005843.png]]

![[Pasted image 20260928010916.png]]

![[Pasted image 20260928011208.png]]


![[Pasted image 20260928011547.png]]

Cuando me queda un elemento los dos me apuntan a ese, el siguiente se simboliza con la pata de la derecha

por lo cual al tener doble referencia y yo quiero dar de baja para que pasa el recolector de basura voy a tener que eliminar las dos

![[Pasted image 20260928012122.png]]


![[Pasted image 20260928012008.png]]

para el alta, mi ultimo si esta la cola vacía va a estar apuntando a null, entonces al hacer el movimiento de apuntar al nuevo no lo puedo hacer

![[Pasted image 20260928012353.png]]