# Encontrar máximo valor

nosotros siempre que querramos encontrar algun valor maximo o minimo y el numero del indice, siempre tenemos que declarar afuera del bucle, ya que adentro se tendra que comparar con algo para que pase a ser el nuevo valor

``` python
arreglo = [0 for _ in range(10)]

suma = 0 #para declarar una suma, esto lo tengo que hacer porque si lo hago adentro del bucle se va a resetear el valor cada vez que se repita

max_val = arreglo[0]
indice_max_val = 0 

for i in range():
	if arreglo[i] > max_val:  #aca uso la comparacion para quedarme con algo
		max_val = arreglo[i]  
		indice_max_val = i
	
	suma += arreglo[i]

```