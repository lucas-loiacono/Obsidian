# Listas

![[Pasted image 20260929233640.png]]

Puedo agregar en cualquier posición

![[Pasted image 20260929233731.png]]

![[Pasted image 20260929233759.png]]

![[Pasted image 20260929234021.png]]

![[Pasted image 20260929234842.png]]

cuando doy el alta tengo que poner longitud o cantidad + 1, así puede dar de alta también al final


```java
package estructuras;

public class Lista<T> {
	// Atributos
	private Nodo<T> primero;
	private Nodo<T> actual;
	private int cantidad;
	
	// Metodos
	// Constructor
	// PRE: - 
	// POS: crea una lista vacia
	public Lista() {
		primero = null;
		actual = null;
		cantidad = 0;
	}
	
	// Alta
	// PRE: 0 < pos <= obtenerCantidad() + 1
	// POS: agrega el elemento en la posicion "pos" e incrementa su cantidad 
	public void alta(T elem, int pos) {
		Nodo<T> nuevo = new Nodo<>(elem);
		if (pos == 1) {
			nuevo.asignarSiguiente(primero);
			primero = nuevo;
		}
		else {
			Nodo<T> anterior = obtenerNodo(pos - 1);
			Nodo<T> posterior = anterior.obtenerSiguiente();
			nuevo.asignarSiguiente(posterior);
			anterior.asignarSiguiente(nuevo);
		}
		cantidad++;
	}
	
	// Consulta
	// PRE: 0 < pos <= obtenerCantidad()
	// POS: devuelve el elemento que esta en la posicion "pos"
	public T consulta(int pos) {
		Nodo<T> aux = obtenerNodo(pos);
		return aux.obtenerDato();
	}

	// PRE: -
	// POS: devuelve la cantidad de elementos que hay en la lista
	public int obtenerCantidad() {
		return cantidad;
	}

	// Baja
	// PRE: PRE: 0 < pos <= obtenerCantidad()
	// POS: da de baja al elemento que esta en la posicion "pos"
	public void baja(int pos) {
		if (pos == 1) {
			primero = primero.obtenerSiguiente();
		}
		else {
			Nodo<T> anterior = obtenerNodo(pos - 1);
			Nodo<T> eliminar = anterior.obtenerSiguiente();
			anterior.asignarSiguiente(eliminar.obtenerSiguiente());
		}
		cantidad--;
	}
	
	// METODOS PARA EL CURSOR O ACTUAL
	// Hay un siguiente?
	// PRE: -
	// POS: devuelve true si lo hay, false de lo contrario
	public boolean haySiguiente() {
		return (actual != null);
	}
	
	// obtenerSiguiente
	// PRE: haySiguiente() tiene que ser true
	// POS: devuelve el dato actual y avanza el cursor
	public T obtenerSiguiente() {
		T dato = actual.obtenerDato();
		actual = actual.obtenerSiguiente();
		return dato;
	}
	
	// iniciar
	// PRE: -
	// POS: lleva el actual al principio
	public void iniciar() {
		actual = primero;
	}
	
	// PRE: PRE: 0 < pos <= obtenerCantidad()
	// POS: devuelve una referencia al nodo que esta en la posicion "pos"
	private Nodo<T> obtenerNodo(int pos) {
		Nodo<T> aux = primero;
		for (int i = 1; i < pos; i++)
			aux = aux.obtenerSiguiente();
		return aux;
	}
```


Siempre me tengo que ir moviendo entre nodos hasta llegar al nodo que necesito para ejecutar mi accion

como tengo que usar tanto en la baja como en el alta me creo una funcion que me devuelva el nodo
![[Pasted image 20260930001023.png]]

si yo quiero una referencia al numero 3, tengo que hacer 2 saltos, por eso mi for es < pos 

![[Pasted image 20260930155857.png]]

me creo mi auxiliar y lo voy moviendo nodo por nodo hasta llegar al que quiero



Alta

![[Pasted image 20260930000339.png]]

Acá tengo que recorrer todo el nodo hasta el 4to para asociar el 4 con el nuevo

Baja

![[Pasted image 20260930000437.png]]

Acá tengo que recorrer todo el nodo hasta llegar al 4to y cambiar al que esta señalando 

![[Pasted image 20260930161349.png]]

si yo doy de baja al ultimo no pasa nada, ya que pasa a referenciar a null, pero el tema es cuando doy de baja el primero

![[Pasted image 20260930161437.png]]

tengo que cambiar mi referencia del primero y lo tengo que pasar al siguiente

![[Pasted image 20260930164349.png]]


Consulta

![[Pasted image 20260930160105.png]]

Primero tengo que obtener mi nodo con un auxiliar, y después preguntar sobre el auxiliar 

Antes para la consulta en pila o cola teníamos a ultimo, ósea teníamos una variable que referenciaba al nodo, y ahí aplicábamos la consulta, sobre la variable