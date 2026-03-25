
## Conceptos básicos

Los diccionarios trabajan con key-value pairs, donde cada key puede estar conectada a cualquier cosa: diccionarios, arrays, valores, etc.

```python
alien_0 = {'color': 'green', 'points': 5}

# le paso la key y python me devuelve el value
print(alien_0['color'])
print(alien_0['points'])
```

### Acceder a los datos

```python
alien_0 = {'color': 'green', 'points': 5}

# guarda el valor en una variable para usarlo despues
new_points = alien_0['points']
print(f"You just earned {new_points} points!")

# o directamente
print(f"You just earned {alien_0['points']} points!")
```

---

## Modificar Diccionarios

### Agregar nuevas key-value pairs

```python
alien_0 = {'color': 'green', 'points': 5}

# es como darle una nueva bandera y asignarle un valor
alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)  # se agregan en el mismo orden que los voy agregando
```

### Empezar con un diccionario vacío

```python
alien_0 = {}

alien_0['color'] = 'green'
alien_0['points'] = 5

print(alien_0)
```

### Modificar valores

```python
alien_0 = {'color': 'green'}
print(alien_0['color'])
alien_0['color'] = 'yellow'
print(alien_0['color'])
```

### Modificar valores según una condición

```python
alien_0 = {'x_position': 0, 'y_position': 25, 'speed': 'medium'}
print(f"Original position: {alien_0['x_position']}")

if alien_0['speed'] == 'slow':
    x_increment = 1
elif alien_0['speed'] == 'medium':
    x_increment = 2
else:
    x_increment = 3

# la nueva posicion es la vieja posicion mas el incremento
alien_0['x_position'] = alien_0['x_position'] + x_increment
print(f"New position: {alien_0['x_position']}")
```

### Eliminar key-value pairs

```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

# guardo el valor antes de eliminar la key, para poder usarlo despues
puntos = alien_0['points']

# elimina la key 'points' y su value del diccionario permanentemente
del alien_0['points']

print(alien_0)   # diccionario sin la key 'points'
print(puntos)    # sigue teniendo el valor original aunque la key ya no exista
```

---

## Usando get() para acceder a valores

Se usa cuando buscas una key que puede no existir. Sin get(), python lanza un KeyError.

```python
alien_0 = {'color': 'green', 'speed': 'slow'}

# esto da KeyError porque 'points' no existe
print(alien_0['points'])

# get() devuelve None si la key no existe, en lugar de dar error
print(alien_0.get('points'))

# se puede pasar un valor por defecto como segundo parametro
point_value = alien_0.get('points', 'No point value assigned.')
```

---

## Looping a través de un Diccionario

### Iterar sobre todos los items (keys y values)

```python
user_0 = {
    'username': 'efermi',
    'first': 'enrico',
    'last': 'fermi',
}

# items() devuelve una lista de tuplas (key, value) que se desempaquetan
for key, value in user_0.items():
    print(f"\nKey: {key}")
    print(f"Value: {value}")
```

### Iterar sobre las keys

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# usando keys()
for name in favorite_languages.keys():
    print(name.title())

# es lo mismo que iterar sin metodo: python asume que iteramos sobre las keys
for name in favorite_languages:
    print(name.title())
```

### Usar el value asociado a una key dentro del loop

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}
friends = ['phil', 'sarah']

for name in favorite_languages.keys():
    print(f"Hi {name.title()}.")
    if name in friends:
        # le paso la key al diccionario y obtengo el value asociado
        language = favorite_languages[name].title()
        print(f"\t{name.title()}, I see you love {language}!")
```

### Iterar sobre las keys en orden alfabético

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

# sorted() ordena las keys antes de iterar
for name in sorted(favorite_languages.keys()):
    print(f"{name.title()}, thank you for taking the poll.")
```

### Iterar sobre los values

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

print("The following languages have been mentioned:")
for language in favorite_languages.values():
    print(language.title())
```

### Iterar sobre values sin repetidos con set()

`set` es una colección de elementos únicos sin orden, por lo que no se puede acceder con índices, pero sí iterar con un for loop.

```python
print("The following languages have been mentioned:")

# set() elimina los valores duplicados antes de iterar
for language in set(favorite_languages.values()):
    print(language.title())
```

---

## Nesting

### Lista de diccionarios

```python
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

# cada elemento de la lista es un diccionario con sus propias key-value pairs
aliens = [alien_0, alien_1, alien_2]
for alien in aliens:
    print(alien)
```

### Generar múltiples diccionarios con un loop

```python
aliens = []

# crea 30 aliens y los agrega a la lista
for alien_number in range(30):
    # cada iteracion crea un diccionario nuevo en memoria aunque tenga los mismos valores
    new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
    aliens.append(new_alien)

print(f"Total number of aliens: {len(aliens)}")
```

### Modificar los primeros 3 aliens

```python
# slicing para obtener solo los primeros 3 elementos
for alien in aliens[:3]:
    if alien['color'] == 'green':
        # modifica los valores sin crear un nuevo diccionario
        alien['color'] = 'yellow'
        alien['points'] = 10
        alien['speed'] = 'medium'
```

---

### Lista dentro de un diccionario

```python
pizza = {
    'crust': 'thick',
    # la key 'toppings' tiene como value una lista
    'toppings': ['mushrooms', 'extra cheese'],
}

print(f"You ordered a {pizza['crust']}-crust pizza with the following toppings:")
for topping in pizza['toppings']:
    print(f"\t{topping}")
```

```python
favorite_languages = {
    'jen': ['python', 'ruby'],
    'sarah': ['c'],
    'edward': ['ruby', 'go'],
}

# items() desempaqueta en name (key) y languages (lista de valores)
for name, languages in favorite_languages.items():
    print(f"\n{name.title()}'s favorite languages are:")
    for language in languages:
        print(f"\t{language.title()}")
```

---

### Diccionarios dentro de diccionarios

```python
users = {
    'aeinstein': {
        'first': 'albert',
        'last': 'einstein',
        'location': 'princeton',
    },
    'mcurie': {
        'first': 'marie',
        'last': 'curie',
        'location': 'paris',
    },
}

# username = key externa | user_info = diccionario interno
for username, user_info in users.items():
    print(f"\nUsername: {username}")
    full_name = f"{user_info['first']} {user_info['last']}"
    location = user_info['location']
    print(f"\tFull name: {full_name.title()}")
    print(f"\tLocation: {location.title()}")
```