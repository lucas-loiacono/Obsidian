![[Pasted image 20261102195755.png]]

## A mi en cola me conviene tener dos punteros, uno como Ultimo y otro como primero, esto por mi alta, baja y consulta
# Cola

entra por el final y sale al principio

los nuevos van al final, y se van procesando y consultando los primeros de la cola

![[Pasted image 20260928005525.png]]


Para esto tengo que tener dos referencias, una al primero y otra al ultimo, asi para las funciones del ultimo, por ejemplo procesar o consultar no me tengo que recorrer todo para llevar al ultimo al primer lugar

![[Pasted image 20260928005843.png]]

![[Pasted image 20260928010916.png]]

![[Pasted image 20260928011208.png]]

```java
package estructuras;

public class Cola<T> {
	// Atributos
	private Nodo<T> primero; // usa en la consulta y la baja
	private Nodo<T> ultimo;  // usa en el alta
	
	// Metodos
	// Constructor
	// PRE: - 
	// POS: crea una cola vacia
	public Cola() {
		primero = null;
		ultimo = null;
	}
	
	// Alta
	// PRE: la Pila no tiene que estar llena --> llena() -> false
	// POS: agrega el elemento al final de la Pila e incrementa el tamanio logico
	public void alta(T elem) {
		Nodo<T> nuevo = new Nodo<>(elem); // paso 1
		if (vacia()) {			// paso 2A
			primero = nuevo;
		}
		else {					// paso 2B
			ultimo.asignarSiguiente(nuevo);
		}
		ultimo = nuevo;			// paso 3
	}
	
	// Consulta
	// PRE: la Cola no tiene que estar vacia: --> vacia() -> false
	// POS: devuelve el primer elemento
	public T consulta() {
		return primero.obtenerDato();
	}

	// PRE: -
	// POS: devuelve true si la cola esta vacia, false de lo contrario
	public boolean vacia() {
		return (primero == null);
	}

	// Baja
	// PRE: la Cola no tiene que estar vacia: --> vacia() -> false
	// POS: da de baja al primer elemento
	public void baja() {
		primero = primero.obtenerSiguiente();
		if (primero == null)
			ultimo = null;
	}
}
```


![[Pasted image 20260928011547.png]]

![[Pasted image 20260929231823.png]]

Cuando me queda un elemento los dos me apuntan a ese, el siguiente se simboliza con la pata de la derecha

por lo cual al tener doble referencia y yo quiero dar de baja para que pasa el recolector de basura voy a tener que eliminar las dos

ya que cuando doy de baja se mueve solo el primero, ósea primero deja de apuntar al siguiente elemento, como no hay apunta a null, pero yo no muevo a ultimo, entonces siempre queda referenciándolo, por lo cual no lo puedo borrar de la memoria, para esto tengo que los dos apunten a null

![[Pasted image 20260928012122.png]]

Baja

![[Pasted image 20260929231108.png]]


![[Pasted image 20260928012008.png]]

para el alta, mi ultimo si esta la cola vacía va a estar apuntando a null, entonces al hacer el movimiento de apuntar al nuevo no lo puedo hacer

![[Pasted image 20260928012353.png]]