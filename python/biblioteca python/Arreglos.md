# Encontrar máximo valor

Siempre dejo el ultimo que cicla hacia afuera como ancla

Nosotros siempre que queramos encontrar algún valor máximo o mínimo y el numero del índice, siempre tenemos que declarar afuera del bucle, ya que adentro se tendrá que comparar con algo para que pase a ser el nuevo valor

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


# 3 Dimensiones

1. **Países (Capa $k$)**: Argentina, Chile, Uruguay.
    
2. **Meses (Fila $i$)**: Enero, Febrero, Marzo.
    
3. **Años (Columna $j$)**: 2023, 2024.
    

La estructura sería: `ventas[pais][mes][anio]`

---

### 1. Recorrido por Capas (Total por País)

Aquí queremos saber cuánto vendió cada país sumando todos sus meses y años. El ciclo de **países** va afuera.


``` python
# k = países, i = meses, j = años
for k in range(len(paises)):
    total_pais = 0
    for i in range(len(meses)):
        for j in range(len(anios)):
            total_pais += ventas[k][i][j]
    print(f"Total vendido en el país {k}: {total_pais}")
```

- **Qué hace:** Entra al "archivador" de Argentina, suma todas sus hojas y filas, luego pasa al "archivador" de Chile.
    

---

### 2. Recorrido por Filas (Total por Mes Global)

Queremos saber cuánto se vendió en "Enero" sumando todos los países y todos los años. El ciclo de **meses** va afuera.


```Python
for i in range(len(meses)):
    total_mes_global = 0
    for k in range(len(paises)):
        for j in range(len(anios)):
            total_mes_global += ventas[k][i][j]
    print(f"Venta total global del mes {i}: {total_mes_global}")
```

- **Qué hace:** Busca la fila "Enero" en el país 1, luego la fila "Enero" en el país 2... termina y pasa a "Febrero".
    

---

### 3. Recorrido por Columnas (Total por Año Global)

Queremos saber cuánto se vendió en el "2024" en todo el mundo y en todos los meses. El ciclo de **años** va afuera.


```Python
for j in range(len(anios)):
    total_anio_global = 0
    for k in range(len(paises)):
        for i in range(len(meses)):
            total_anio_global += ventas[k][i][j]
    print(f"Venta total del año {j} en todos los países: {total_anio_global}")
```

- **Qué hace:** Se "clava" en la columna del año 2024 y recorre todos los países y meses solo para esa columna.
    

---

### 4. Recorrido "Capa-Fila" (Total de un Mes en un País específico)

Si quisieras ver el comportamiento de los meses dentro de cada país (promedio mensual por país), dejas **país** y **mes** en los dos ciclos externos.


```Python
for k in range(len(paises)):
    for i in range(len(meses)):
        suma_mes_pais = 0
        for j in range(len(anios)):
            suma_mes_pais += ventas[k][i][j]
        print(f"País {k}, Mes {i} sumó: {suma_mes_pais}")
```