#conditional tests
#if statements son estructuras de control que permiten ejecutar un bloque de codigo solo si se cumple una condicion, por ejemplo:
cars = ['audi', 'bmw', 'subaru', 'toyota']  
for car in cars:
    if car == 'bmw': #esto es una condicion, que se evalua en cada iteracion del bucle, y si la condicion se cumple, se ejecuta el bloque de codigo indentado debajo de la condicion, que en este caso es imprimir el nombre del coche en mayuscula, y si la condicion no se cumple, no se ejecuta el bloque de codigo indentado debajo de la condicion, y se pasa a la siguiente iteracion del bucle.
        print(car.upper()) 
    else: 
        print(car.title()) #esto se ejecuta si la condicion no se cumple, es decir, si el coche no es 'bmw', entonces se ejecuta el bloque de codigo indentado debajo del else, que en este caso es imprimir el nombre del coche con la primera letra en mayuscula, y el resto en minuscula, usando el metodo title() para formatear el nombre del coche.
        
#true or false values
car = 'bmw'
car == 'bmw' #esto devuelve True, porque la condicion se cumple, es decir, el valor de car es igual a 'bmw', por lo que la condicion se evalua como True, y si la condicion se cumpliera, es decir, si el valor de car no fuera igual a 'bmw', entonces la condicion se evaluaria como False, y se ejecutaria el bloque de codigo debajo del else, si es que hay un else en el if statement.

car = 'audi'
car == 'bmw'
#false

#para hacer tests 
car = 'Audi'
car == 'audi' 
#false

car = 'Audi'
car.lower() == 'audi'
#true
print(car) #imprime Audi, el lower no le afecta


#desigual
request_topping = 'mushrooms'

if request_topping != 'anchoives': #esto retorna true, por lo cual sigue con el codigo, siempre que sea true sigue 
    print("hold the anchoives")
    
#numerical comparisions

answer = 17

if answer != 42:
    print("that is not the correct answer. please try again")
    
#comparaciones matematicas
# <, >, <=, >=, 
age = 18
age < 21 
#true 


#multiple conditions, and y or 

age_0 = 22
age_1 = 18
age_0 >=21 and age_1 >= 21
#false
age_1 = 22 
age_0 >=21 and age_1 >= 21
#true

 
age_0 = 22
age_1 = 18
age_0 >=21 or age_1 >= 21
#true
age_0 = 18
age_0 >=21 or age_1 >= 21
#false


#checking values in a list
request_toppings = ['mushrooms', 'onions', 'pineapple']
'musrooms' in request_toppings 
#true
'pepperoni' in request_toppings
#false

#chequear valores que no estan dentro de una lista
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'
if user not in banned_users:
    print(f"{user.title()}, you cant post a response if you wish")


#if statements
    
#if conditional_test:        Aca yo puedo poner cualquier conditional test, si el conditional test da true, python sigue con el codigo
#   do something

age = 19 
if age >= 18:
    print("you are old enough the vote!")
    
#if-else
age = 17
if age >= 18:
    print("sos mayor de edad")
else:
    print("sos menor de edad")

#si no pasa el bloque del if, pasa al bloque del else y lo ejecuta, esto ocurre porque hay dos opciones

#if-elif-else

age = 12

if age < 4:
    print("your admision cost is $0")
elif age < 18:
    print("your admision cost is $25")
else:
    print("your admision cost is $40")
    
#casi siempre se usa el else-block para catchear errores y se deja solo con el elif
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


#tambien se pueden considerar varias opciones, poniendo varios if

request_toppings = ['mushrooms', 'extra cheese']
if 'mushrooms' in request_toppings:
    print("adding mushrooms")
if 'extra cheese' in request_toppings:
    print("adding extra cheese")
if 'pepperoni' in request_toppings:
    print('adding pepperoni')
    
#esto es distinto a poner 
request_toppings = ['mushrooms', 'extra cheese']
if 'mushrooms' in request_toppings:
    print("adding mushrooms")   
elif 'extra cheese' in request_toppings:
    print("adding extra cheese")
elif 'pepperoni' in request_toppings:
    print('adding pepperoni')
#en este caso, si el primer if se cumple, no se evalua el resto de los elif, por lo que solo se ejecuta el bloque de codigo del primer if que se cumple, y se ignoran los demas elif, aunque se cumplan,

#si solo quiero que corra un bloque hago un else-if-elif
#si quiero que corran varios bloques hago varios if separados

#using if statements with lists 
#sin if
requested_toppings = ['mushrooms', 'onions', 'pineapple']
for requested_topping in requested_toppings:
    print(f"adding {requested_topping}.")
print("\nFinished making your pizza!")
#con if
requested_toppings = ['mushrooms', 'onions', 'pineapple']
for requested_topping in requested_toppings:
    if requested_topping == 'green peppers':
        print("sorry, we are out of green peppers right now.")
    else:
        print(f"adding {requested_topping}.")
print("\nFinished making your pizza!")

#checking that a list is not empty
requested_toppings = []
if requested_toppings: #cuando yo paso una lista a un if statement, python evalua si la lista esta vacia o no, y si la lista esta vacia, python la evalua como False, y si la lista no esta vacia, python la evalua como True, por lo que si requested_toppings es una lista vacia, el if statement se evalua como False, y se ejecuta el bloque de codigo debajo del else, y si requested_toppings es una lista no vacia, el if statement se evalua como True, y se ejecuta el bloque de codigo debajo del if.
    for requested_topping in requested_toppings:
        print(f"adding {requested_topping}.")
    print("\nFinished making your pizza!")
else:
    print("Are you sure you want a plain pizza?")

#using multiple lists
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print(f"adding {requested_topping}.")
    else:
        print(f"sorry, we don't have {requested_topping}.")
        
print("\nFinished making your pizza!")