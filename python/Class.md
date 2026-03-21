![[Pasted image 20260321144939.png]]

Para declarar clases

```python

#esto lo puedo hacer para inicializar y despues les voy cambiando los atributos
class Personaje:
	nombre = "Default"
	fuerza = 0
	inteligencia = 0
	defensa = 0
	vida = 0
	
	
	
	


mi_personaje = Personaje() #esto crea al objeto personaje
print(mi_personaje) #esto devuelve que lo creo
print("el nombre del jugador es", mi_personaje.nombre) #pero para acceder a los atributos accedo asi
print("el nombre del jugador es", mi_personaje.fuerza) #accedo con el punto 
mi_personaje.nombre = "loocakoo" #para modificar
```

Para darle los valores a los atributos hago:

```python

#esto lo puedo hacer para inicializar y despues les voy cambiando los atributos
class Personaje:
	nombre = "Default"
	fuerza = 0
	inteligencia = 0
	defensa = 0
	vida = 0
	
	
	def __init__(self, nombre, fuerza, inteligencia, defensa, vida)
	#self hace referencia a si mismo, y permite que con el punto pueda acceder a 
	#los elementos de la clase
		
		self.nombre = nombre  #como el = es un asignador, al nombre actual le 
		#asigno la fuerza que le pase al parametro
		self.fuerza = fuerza
		self.inteligencia = inteligencia
		self.defensa = defensa 
		self.vida = vida
	


mi_personaje = Personaje() #esto crea al objeto personaje
print(mi_personaje) #esto devuelve que lo creo
print("el nombre del jugador es", mi_personaje.nombre) #pero para acceder a los atributos accedo asi
print("el nombre del jugador es", mi_personaje.fuerza) #accedo con el punto 
mi_personaje.nombre = "loocakoo" #para modificar
```