
## input()

Siempre se le asigna una variable a `input()` para guardar el valor ingresado y poder usarlo después.

```python
# muestra el mensaje, espera que el usuario ingrese algo y lo guarda
message = input("Tell me something, and I will repeat it back to you: ")
print(message)
```

### Prompt en múltiples líneas

```python
# += concatena un nuevo string al final del string original
prompt = "if you share your name with me, I can personalize the messages you see."
prompt += "\nWhat is your name? "

name = input(prompt)
print(f"\nHello, {name}!")
```

---

## input() con números

`input()` interpreta todo como string, por lo que no se puede usar para comparaciones numéricas directamente.

```python
age = input("how old are you? ")
# >>> '21'  → sale como string, no se puede usar con >=, <=, etc.
```

### Convertir con int()

```python
age = input("how old are you? ")
age = int(age)  # convierte el string a entero

height = input("how tall are you, in inches? ")
height = int(height)

if height >= 48:
    print("\nyou are tall")
else:
    print("\nyou are small")
```

---

## Módulo Operator (resto)

```python
# 4%3 = 1
# 5%3 = 2
# 6%3 = 0

# sirve para saber si un numero es par o impar
number = input("Enter a number, and I'll tell you if it's even or odd: ")
number = int(number)

if number % 2 == 0:
    print(f"\nThe number {number} is even.")
else:
    print(f"\nThe number {number} is odd.")
```

---

## While Loops

El bucle sigue iterando mientras la condición sea `True`.

```python
current_number = 5

while current_number <= 5:
    print(current_number)
    current_number += 1
```

### El usuario decide cuándo salir

```python
prompt = "\nTell me something, and I will repeat it back to you"
prompt += "\nEnter 'quit' to end the program. "

message = ''

# version simple: imprime 'quit' antes de salir
while message != 'quit':
    message = input(prompt)
    print(message)

# version mejorada: no imprime 'quit'
while message != 'quit':
    message = input(prompt)
    if message != 'quit':
        print(message)
```

### Usando un flag

Se usa cuando hay varias condiciones por las que el bucle puede parar.

```python
prompt = "\nTell me something, and I will repeat it back to you"
prompt += "\nEnter 'quit' to end the program. "

active = True
while active:
    message = input(prompt)

    if message == 'quit':
        active = False  # detiene el bucle
    else:
        print(message)
```

### Usando break

Sale del loop inmediatamente sin ejecutar más código.

```python
prompt = "\nPlease enter the name of a city you have visited: "
prompt += "\n(Enter 'quit' when you are finished.) "

while True:
    city = input(prompt)

    if city == 'quit':
        break  # sale del loop sin ejecutar el else
    else:
        print(f"I'd love to go to {city.title()}!")
```

### Usando continue

Vuelve al inicio del loop salteándose el resto del código para ese caso.

```python
current_number = 0
while current_number < 10:
    current_number += 1
    if current_number % 2 == 0:
        continue  # ignora el resto y vuelve al inicio del bucle
    print(current_number)  # solo imprime numeros impares
```

---

## While Loops con Listas y Diccionarios

### Mover elementos entre listas

```python
uncomfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

# mientras la lista no este vacia, el bucle sigue iterando
while uncomfirmed_users:
    # pop() saca el ultimo elemento y lo guarda en current_user
    current_user = uncomfirmed_users.pop()
    print(f"Verifying user: {current_user.title()}")
    confirmed_users.append(current_user)

print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
    print(confirmed_user.title())
```

### Eliminar todas las ocurrencias de un valor en una lista

```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

# remove() solo elimina la primera ocurrencia, por eso se usa while
# el bucle se repite hasta que no quede ninguna ocurrencia de 'cat'
while 'cat' in pets:
    pets.remove('cat')

print(pets)
```

### Llenar un diccionario con input del usuario

```python
responses = {}
polling_active = True

while polling_active:
    name = input("\nWhat is your name? ")
    response = input("Which mountain would you like to climb someday? ")

    # agrega una nueva key-value pair con el nombre y la respuesta del usuario
    responses[name] = response

    repeat = input("Would you like to let another person respond? (yes/no) ")
    if repeat == 'no':
        polling_active = False  # detiene el bucle

for name, response in responses.items():
    print(f"{name} would like to climb {response}.")
```