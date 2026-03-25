Esto imprime la lista completa con los corchetes y las comillas, es la representación de la lista en Python.

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
```

### Acceder a los elementos de la lista
Esto imprime el primer elemento, pero como le estoy pidiendo 1 solo elemento me lo imprime sin corchetes ni comillas.

```python
print(bicycles[0])
print(bicycles[0].title())
```

Si quiero acceder al último ítem de una lista, esto también se puede hacer con el `-2`, `-3`, etc., devolviendo los anteúltimos y así.

```python
print(bicycles[-1])
```

### Usar f-strings con valores de las listas

```python
message = f"My first bicycle was a {bicycles[0].title()}."
print(message)
```

### Modificando elementos de una lista
Cambio el valor de un elemento en una posición específica.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

motorcycles[0] = 'ducati'
print(motorcycles)
```

### Agregar elementos a listas al final

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.append('ducati')
print(motorcycles)

motorcycles = []
motorcycles.append('honda')
motorcycles.append('yamaha')
motorcycles.append('suzuki')
print(motorcycles)
```

### Agregar elementos a listas en distintas posiciones
Esto toma la posición 0 y reemplaza el valor de ese lugar por el nuevo, desplaza todos los demás a los siguientes lugares en adelante.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.insert(0, 'ducati') 
print(motorcycles) # esto devuelve ['ducati', 'honda', 'yamaha', 'suzuki']
```

### Remover elementos de la lista
Usando `del` esto elimina el elemento de la primera posición y no se puede acceder al valor una vez borrado.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
del motorcycles[0] 
print(motorcycles)
```

Acá popeo (extraigo) el valor, y de paso lo guardo en una variable. Esto imprime el ultimo elemento de la lista, pero a diferencia de del, el valor del elemento eliminado se guarda en la variable popped_motorcycles, por lo que se puede acceder al valor eliminado después de eliminarlo

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
popped_motorcycles = motorcycles.pop() 
print(motorcycles)
print(popped_motorcycles)
```

Acá popeo el valor, lo guardo en una variable, y luego lo vuelvo a agregar a la lista, pero con la primera letra en mayúscula.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
last_owned = motorcycles.pop() 
print(f"The last motorcycle I owned was a {last_owned.title()}.")
motorcycles.append(f"{last_owned.title()}") 
print(motorcycles)
```

Popear un valor de una posición específica, y de paso guardarlo en una variable.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
first_owned = motorcycles.pop(0) 
print(f"The first motorcycle I owned was a {first_owned.title()}.")
```

### Remover un valor por su valor
Para cuando no se sabe la posición del valor, pero sí se sabe el valor. Esto elimina el valor de la lista, pero no se puede acceder al valor una vez borrado, y si el valor no está en la lista da un error.

```python
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
motorcycles.remove('ducati') 
print(motorcycles)
```

Remover un valor por su valor, pero antes guardar el valor en una variable para poder usarlo después. `remove` solo elimina la primera ocurrencia del valor; si hay más de un valor igual en la lista, solo se elimina el primero, y los demás quedan en la lista.

```python
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
too_expensive = 'ducati' 
motorcycles.remove(too_expensive) 
print(motorcycles)
print(f"A {too_expensive.title()} is too expensive for me.")
```

### Ordenar listas de forma permanente
Alfabéticamente o en orden inverso. `sort()` ordena la lista de forma permanente, es decir, cambia el orden de los elementos en la lista, y no se puede volver al orden original a menos que se vuelva a ordenar la lista. Se pone reverse true para que sea al revés 

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort() 
print(cars)

cars.sort(reverse=True) 
print(cars)
```

### Ordenar listas de forma temporal
Alfabéticamente o en orden inverso. `sorted()` no cambia el orden de los elementos en la memoria, y se puede volver al orden original simplemente imprimiendo la lista sin ordenar.
*(Nota: Ordenar es más complicado con letras mayúsculas y minúsculas mezcladas, ya que las mayúsculas se ordenan antes. Es recomendable usar solo minúsculas o solo mayúsculas para evitar confusiones).*

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print("Here is the original list:")
print(cars)

print("\nHere is the sorted list:")
print(sorted(cars)) 

print("\nHere is the original list again:")
print(cars)

print("\nHere is the sorted list in reverse:")
print(sorted(cars, reverse=True)) 

print("\nHere is the original list again:")
print(cars)
```

Esto cambia el display de la lista, pero no se cambia el orden en la memoria, por lo que si se vuelve a imprimir la lista sin ordenar, se muestra el orden original, y si se vuelve a imprimir la lista ordenada, se muestra el orden ordenado, pero el orden en la memoria sigue siendo el mismo, es decir, el orden original.

Ordenar es mas complicado con letras mayúsculas y minúsculas, porque las mayúsculas se ordenan antes que las minúsculas, por lo que si hay una mezcla de mayúsculas y minúsculas en la lista, el orden puede ser diferente al esperado, por eso es recomendable usar solo minúsculas o solo mayúsculas en las listas para evitar confusiones.

### Imprimir una lista al revés
`reverse()` invierte el orden de los elementos en la lista, es decir, cambia el orden de los elementos permanentemente, y no se puede volver al orden original a menos que se vuelva a invertir la lista.

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)

cars.reverse() 
print(cars)

cars.reverse() # esto vuelve a invertir el orden de los elementos, osea a su forma original.
print(cars)
```

### Longitud de una lista
`len()` devuelve la longitud de la lista, es decir, el número de elementos. Aunque el índice del último elemento sea `len(cars)-1` (porque empieza en 0). Como guardamos la longitud de la lista en una variable, podemos usar esa variable para acceder al último elemento, aunque la variable no se actualiza automáticamente con los cambios en la lista.

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']

print(len(cars)) #esto devuelve la longitud de la lista, es decir, el numero de elementos en la lista, en este caso 4, porque hay 4 elementos en la lista, aunque el indice del ultimo elemento sea 3, porque el indice empieza en 0.

longitud = len(cars) #esto guarda la longitud de la lista en una variable, para poder usarla despues

cars.insert(len(cars), 'mercedes') #esto inserta un nuevo elemento al final de la lista, porque el indice del ultimo elemento es len(cars)-1, entonces el indice del nuevo elemento es len(cars), que es el siguiente indice disponible, y no se puede usar un indice mayor a len(cars) porque da un error, pero si se puede usar un indice igual a len(cars) para insertar un nuevo elemento al final de la lista.

print(cars)

print(cars[longitud-1]) # esto imprime el ultimo elemento de la lista, porque el indice del ultimo elemento es len(cars)-1, y como guardamos la longitud de la lista en una variable, podemos usar esa variable para acceder al ultimo elemento de la lista, aunque se agreguen nuevos elementos a la lista despues de guardar la longitud, porque la variable longitud sigue teniendo el valor original de la longitud de la lista, y no se actualiza automaticamente con los cambios en la lista.
```

### Trabajando con listas: Looping (Bucles)
El bucle `for` itera sobre cada elemento de la lista y ejecuta el bloque de código. El nombre del mago se guarda en la variable `magician`, que cambia su valor en cada iteración del bucle.
En Python no necesito indicar el límite del bucle, este se detiene al final de la lista.

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians: 
    print(magician) # esto imprime el nombre del mago 
```

Si imprimo la variable fuera del bucle, mostrará el último elemento de la lista, porque al final del bucle, `magician` tiene el valor de la última iteración ('carolina').
*(En C sería algo así como: `for(int i=0; i<sizeof(magicians); i++){ magician = magicians[i]; printf("%s", magician); }`)*

```python
print(magician) 
```

Se puede personalizar usando f-strings:
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(f"{magician.title()}, that was a great trick!") 
```

**Cuando termina el loop e indentación:**
En Python, la indentación es muy importante porque indica el bloque de código que se ejecuta en cada iteración. Lo que no está indentado se imprime al final del bucle, una sola vez.

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(f"{magician.title()}, that was a great trick!")
print("Thank you everyone, that was a great magic show!") 
```

### Creando listas numéricas (Range)
Para imprimir rangos de números, puedo usar `range()`. El límite superior no se incluye en la secuencia (del 1 hasta el 4). También se puede pasar `range(6)`, que genera del 0 al 5.

```python
for value in range(1,5): 
    print(value) 
```

Puedo usar los valores generados por `range()` para crear listas de números, usando la función `list()`.

```python
numbers = list(range(1,6)) 
print(numbers) # esto imprime [1, 2, 3, 4, 5]
```

Puedo saltear números en la secuencia usando un tercer parámetro, que es el paso. Ejemplo para números pares desde el 0 hasta el 10:

```python
even_numbers = list(range(0,11,2)) 
print(even_numbers) # esto imprime [0, 2, 4, 6, 8, 10]
```

Puedo crear sets de números, como calcular el cuadrado de cada número:

```python
squares = []
for value in range(1,11):
    square = value**2 
    squares.append(square) 
print(squares) # esto imprime [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Estadísticas con listas
Encontrar el valor mínimo, máximo y la suma de todos los valores de una lista.

```python
digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
print(min(digits)) 
print(max(digits)) 
print(sum(digits)) 
```

### List Comprehensions
Esto es una forma más compacta de crear listas a partir de una secuencia de números, usando una sintaxis especial que combina un bucle `for` con la creación de la lista.

```python
squares = [value**2 for value in range(1,11)] 
print(squares) 
```

### Slices (Rebanadas)
Las slices sirven para obtener una parte de la lista usando `[inicio:fin]`. El índice de la izquierda es inclusivo, y el de la derecha es exclusivo.
* Si no se especifica inicio, asume 0.
* Si no se especifica fin, asume el final de la lista.
* Si se especifica un índice negativo, se cuenta desde el final hacia el principio.

```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[0:3]) 
print(players[1:4]) 
print(players[:4]) 
print(players[2:]) 
print(players[-3:]) 
```

### Looping a través de un Slice

```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print("Here are the first three players on my team:")
for player in players[:3]:
    print(player.title())   
```

### Copiando una lista
Usando `[:]` se crea una copia independiente de la lista. Cualquier cambio que se haga en una no afecta a la otra porque son dos listas diferentes en la memoria.

```python
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods[:] 

print("My favorite foods are:")
print(my_foods)
print("\nMy friend's favorite foods are:")
print(friend_foods)

my_foods.append('cannoli') 
friend_foods.append('ice cream') 

print(friend_foods)
print(my_foods) 
```

*(Nota: Si yo hago `friend_foods = my_foods` sin los corchetes, esto no crea una copia. Ambas variables apuntan a la misma lista en la memoria, por lo que cambiar una, cambiaría la otra).*

### Tuplas
Las tuplas son listas inmutables, es decir, no se pueden cambiar sus elementos una vez creadas. Se indexan de la misma forma que las listas.

```python
dimensions = (200, 50)
```


