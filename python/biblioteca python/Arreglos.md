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

# Para hacer un intercambio de valores
Siempre que yo quiera intercambiar valores entre si voy a tener que llamar a un auxiliar 

```python
for i in range(tope):
    for j in range(i+1, tope): #esto hace que cuente el triangulo superior o inferior, asi no volvemos a modificar las que ya modificamos

        aux = matriz[i][j]
        matriz[i][j] = matriz[j][i]
        matriz[j][i] = aux
```