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

# Como recorrer una matriz

Para recorrer una matriz tengo que entender que quiero recorrer, si filas o columnas, ósea que es lo que quiero hacer que cicle o cambie mas tarde, si quiero hacer el promedio de meses a través de los años voy a tener que rotar mas rápido los años que los meses

```python

# Supongamos: datos[mes][anio]
suma_anio_mayor = -1
anio_mayor = 0

# 1. Encontrar el año con la mayor suma
for j in range(len(anios)):
    suma_anio = 0
    for i in range(len(meses)):
        suma_anio += datos[i][j]
    
    if suma_anio > suma_anio_mayor:
        suma_anio_mayor = suma_anio
        anio_mayor = j

# 2. Encontrar el mes con la mayor suma a través de los años
suma_mes_mayor = -1
mes_mayor = 0

for i in range(len(meses)):
    suma_en_anios = 0
    for j in range(len(anios)):
        suma_en_anios += datos[i][j]
        
    if suma_en_anios > suma_mes_mayor:
        suma_en_anios_mayor = suma_en_anios # Aquí corriges el nombre
        mes_mayor = i
```

La estructura `matriz[i][j]` (donde `i` es fila y `j` es columna) se mantiene estática como un mapa de coordenadas. Lo que determina qué estás analizando es **cuál ciclo pones afuera**.

### 1. Para analizar FILA por FILA (Análisis de Meses)

Si quieres saber cuánto se sumó en "Enero" a través de todos los años, dejas la **i (fila)** fija en el ciclo externo y mueves la **j (columna)** en el interno.

```Python
for i in range(len(meses)): # Me quedo parado en una fila (Mes)
    suma_del_mes = 0
    for j in range(len(anios)): # Recorro todas las columnas de esa fila
        suma_del_mes += matriz[i][j]
    # Aquí ya tengo el total de ese mes
```
### 2. Para analizar COLUMNA por COLUMNA (Análisis de Años)

Si quieres saber cuánto se sumó en el "Año 2024" sumando todos sus meses, dejas la **j (columna)** fija en el ciclo externo y mueves la **i (fila)** en el interno.

```Python
for j in range(len(anios)): # Me quedo parado en una columna (Año)
    suma_del_anio = 0
    for i in range(len(meses)): # Recorro todas las filas de esa columna
        suma_del_anio += matriz[i][j]
    # Aquí ya tengo el total de ese año
```