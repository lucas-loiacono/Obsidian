
# Conditional Tests en Python

## If Statements

Son estructuras de control que permiten ejecutar un bloque de código solo si se cumple una condición.

```python
cars = ['audi', 'bmw', 'subaru', 'toyota']  
for car in cars:
    # si la condicion se cumple, imprime el nombre en mayuscula
    if car == 'bmw':
        print(car.upper()) 
    # si la condicion no se cumple, imprime con la primera letra en mayuscula
    else: 
        print(car.title())
```

---

## True or False Values

```python
car = 'bmw'
car == 'bmw'  # True

car = 'audi'
car == 'bmw'  # False
```

### Case insensitive comparison

```python
car = 'Audi'
car == 'audi'         # False
car.lower() == 'audi' # True
print(car)            # Imprime 'Audi', lower() no modifica la variable original
```

---

## Operadores de Comparación

### Desigualdad (`!=`)

```python
request_topping = 'mushrooms'

# retorna True, por lo cual sigue con el codigo
if request_topping != 'anchoives':
    print("hold the anchoives")

answer = 17
if answer != 42:
    print("that is not the correct answer. please try again")
```

### Comparaciones numéricas (`<`, `>`, `<=`, `>=`)

```python
age = 18
age < 21  # True
```

---

## Múltiples Condiciones: `and` y `or`

```python
age_0 = 22
age_1 = 18
# and: las dos condiciones deben cumplirse
age_0 >= 21 and age_1 >= 21  # False

age_1 = 22
age_0 >= 21 and age_1 >= 21  # True

# or: basta con que una condicion se cumpla
age_0 = 22
age_1 = 18
age_0 >= 21 or age_1 >= 21   # True

age_0 = 18
age_0 >= 21 or age_1 >= 21   # False
```

---

## Checking Values in a List

```python
request_toppings = ['mushrooms', 'onions', 'pineapple']
'mushrooms' in request_toppings   # True
'pepperoni' in request_toppings   # False

# chequear valores que NO estan dentro de una lista
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'
if user not in banned_users:
    print(f"{user.title()}, you can post a response if you wish")
```

---

## Estructuras If

### If simple

```python
age = 19 
if age >= 18:
    print("you are old enough to vote!")
```

### If-Else

```python
# si no pasa el bloque del if, pasa al else. Hay dos opciones posibles.
age = 17
if age >= 18:
    print("sos mayor de edad")
else:
    print("sos menor de edad")
```

### If-Elif-Else

```python
age = 12
if age < 4:
    print("your admission cost is $0")
elif age < 18:
    print("your admission cost is $25")
else:
    print("your admission cost is $40")
```

> 💡 Casi siempre se usa el `else` para catchear errores. Se puede omitir y dejar solo `elif`.

### Solo con Elif (sin else)

```python
price = 0 
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 25
elif age < 65:
    price = 40
elif age >= 65:
    price = 20
```

---

## If vs Elif: Diferencia clave

- **Varios `if` separados** → se evalúan **todos**, pueden ejecutarse varios bloques.
- **`if-elif`** → en cuanto uno se cumple, **se ignoran los demás**.

```python
# Varios if separados: pueden ejecutarse multiples bloques
request_toppings = ['mushrooms', 'extra cheese']
if 'mushrooms' in request_toppings:
    print("adding mushrooms")
if 'extra cheese' in request_toppings:
    print("adding extra cheese")
if 'pepperoni' in request_toppings:
    print('adding pepperoni')
```

```python
# if-elif: solo se ejecuta el primer bloque que se cumpla, los demas se ignoran
if 'mushrooms' in request_toppings:
    print("adding mushrooms")   
elif 'extra cheese' in request_toppings:
    print("adding extra cheese")
elif 'pepperoni' in request_toppings:
    print('adding pepperoni')
```

---

## If Statements con Listas

```python
requested_toppings = ['mushrooms', 'onions', 'pineapple']
for requested_topping in requested_toppings:
    if requested_topping == 'green peppers':
        print("sorry, we are out of green peppers right now.")
    else:
        print(f"adding {requested_topping}.")
print("\nFinished making your pizza!")
```

### Verificar que una lista no esté vacía

```python
# lista vacia → evalua como False | lista con elementos → evalua como True
requested_toppings = []
if requested_toppings:
    for requested_topping in requested_toppings:
        print(f"adding {requested_topping}.")
    print("\nFinished making your pizza!")
else:
    print("Are you sure you want a plain pizza?")
```

### Usando múltiples listas

```python
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print(f"adding {requested_topping}.")
    else:
        print(f"sorry, we don't have {requested_topping}.")
        
print("\nFinished making your pizza!")
```