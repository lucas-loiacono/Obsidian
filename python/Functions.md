
## Definir y llamar una función

Se usa `def` para declarar una función. El docstring (triple comillas) describe qué hace.

```python
def greet_user():
    """Display a simple greeting."""
    print("Hello!")

greet_user()  # llama a la funcion
```

---

## Pasar información a una función

```python
# parametro: lo que se declara en la definicion de la funcion
# argumento: lo que se le pasa cuando se la llama
def greet_user(username):
    """Display a simple greeting."""
    print(f"Hello, {username.title()}!")

greet_user('jesus')  # 'jesus' es el argumento
```

---

## Tipos de Argumentos

### Positional arguments

Se asignan en el mismo orden en que están declarados los parámetros.

```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print(f"\nI have a {animal_type}.")
    print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')
```

### Keyword arguments

No hace falta acordarse del orden, se especifica a qué parámetro va cada argumento.

```python
describe_pet(animal_type='hamster', pet_name='harry')
```

### Default values

El parámetro con default value tiene que ir al final. Si no se le pasa un argumento, usa el valor predeterminado.

```python
def describe_pet(pet_name, animal_type='dog'):
    """Display information about a pet."""
    print(f"\nI have a {animal_type}.")
    print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('willie')          # usa el default: 'dog'
describe_pet('willie', 'cat')   # sobreescribe el default con 'cat'
```

### Combinando obligatorios y opcionales

```python
# los parametros sin default van primero, los con default al final
def describe_pet(pet_name, edad, altura, animal_type='dog', comida_favorita='croquetas'):
    print(f"\nI have a {animal_type}.")
    print(f"My {animal_type}'s name is {pet_name.title()}.")
    print(f"My {animal_type} is {edad} years old.")
    print(f"My {animal_type} is {altura} cm tall.")
    print(f"My {animal_type}'s favorite food is {comida_favorita}.")

describe_pet('willie', 5, 30)                            # usa ambos defaults
describe_pet('willie', 5, 30, 'cat')                     # sobreescribe animal_type
describe_pet('willie', 5, 30, comida_favorita='pollo')   # saltea animal_type con keyword
```

---

## Return Values

`return` saca un valor de dentro de la función para poder usarlo afuera.

```python
def get_formatted_name(first_name, last_name):
    """Return a full name, neatly formatted."""
    full_name = f"{first_name} {last_name}"
    return full_name.title()

# siempre guardar el valor devuelto en una variable para usarlo despues
musician = get_formatted_name('jimi', 'hendrix')
print(musician)
```

### Argumento opcional

```python
# middle_name='' hace que sea opcional
def get_formatted_name(first_name, last_name, middle_name=''):
    """Return a full name, neatly formatted."""
    if middle_name:  # cadena vacia se evalua como False
        full_name = f"{first_name} {middle_name} {last_name}"
    else:
        full_name = f"{first_name} {last_name}"
    return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician)

musician = get_formatted_name('john', 'hooker', 'lee')
print(musician)
```

### Retornar un diccionario

```python
def build_person(first_name, last_name, age=None):
    """Return a dictionary of information about a person."""
    person = {'first': first_name, 'last': last_name}
    if age:  # None se evalua como False, no agrega la key si no se paso edad
        person['age'] = age
    return person

musician = build_person('jimi', 'hendrix', age=27)
print(musician)
```

---

## Pasar una Lista a una Función

```python
def greet_users(names):
    """Print a simple greeting to each user in the list."""
    for name in names:
        msg = f"Hello, {name.title()}!"
        print(msg)

usernames = ['hannah', 'ty', 'margot']
greet_users(usernames)
```

---

## Modificar una Lista dentro de una Función

```python
# version sin funciones
unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
completed_models = []

while unprinted_designs:
    current_design = unprinted_designs.pop()
    print(f"Printing model: {current_design}")
    completed_models.append(current_design)

print("\nThe following models have been printed:")
for completed_model in completed_models:
    print(completed_model)
```

```python
# version con funciones: mas organizada y reutilizable
def print_models(unprinted_designs, completed_models):
    """Simulate printing each design, until none are left."""
    while unprinted_designs:
        current_design = unprinted_designs.pop()
        print(f"Printing model: {current_design}")
        completed_models.append(current_design)

def show_completed_models(completed_models):
    """Show all the models that were printed."""
    print("\nThe following models have been printed:")
    for completed_model in completed_models:
        print(completed_model)

unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
completed_models = []
print_models(unprinted_designs, completed_models)
show_completed_models(completed_models)
```

### Evitar que una función modifique la lista original

```python
# unprinted_designs[:] pasa una copia, la lista original no se modifica
print_models(unprinted_designs[:], completed_models)
```

---

## Arbitrary Arguments

### `*args` — número arbitrario de argumentos

Los argumentos se guardan en una **tupla**.

```python
def make_pizza(*toppings):
    """Print the list of toppings that have been requested."""
    print("\nMaking a pizza with the following toppings:")
    for topping in toppings:
        print(f"- {topping}")

make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')
```

### Combinando posicional con `*args`

Los parámetros posicionales siempre van antes del `*`.

```python
def make_pizza(size, *toppings):
    """Summarize the pizza we are about to make."""
    print(f"\nMaking a {size}-inch pizza with the following toppings:")
    for topping in toppings:
        print(f"- {topping}")

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```

### `**kwargs` — número arbitrario de keyword arguments

Los argumentos se guardan en un **diccionario**.

```python
def build_profile(first, last, **user_info):
    """Build a dictionary containing everything we know about a user."""
    profile = {}
    profile['first_name'] = first
    profile['last_name'] = last
    return profile

# los keyword arguments extra se guardan en user_info como diccionario
user_profile = build_profile('albert', 'einstein', location='princeton', field='physics')
```