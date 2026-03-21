## Abstracción 

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

class Personaje:

	#esto no hace falta ya que lo declaro con el constructor 
	
	#nombre = "Default"
	#fuerza = 0
	#inteligencia = 0
	#defensa = 0
	#vida = 0
	
	
	def __init__(self, nombre, fuerza, inteligencia, defensa, vida)
	#self hace referencia a si mismo, y permite que con el punto pueda acceder a 
	#los elementos de la clase
		
		self.nombre = nombre  #como el = es un asignador, al nombre actual le 
		#asigno la fuerza que le pase al parametro
		self.fuerza = fuerza
		self.inteligencia = inteligencia
		self.defensa = defensa 
		self.vida = vida
	


mi_personaje = Personaje("loocakoo", 10, 50, 20, 10) 
print(mi_personaje) 
print("el nombre del jugador es", mi_personaje.nombre) 
print("el nombre del jugador es", mi_personaje.fuerza)  
mi_personaje.nombre = "loocakoo" 
```


El __init__() hace esto, reemplaza los ya declarados y los modifica, pero si lo uso no hace falta volverlos a declarar
![[Pasted image 20260321151030.png]]
Para declarar métodos que muestren el valor de sus atributos hago:

```python

class Personaje:

	def __init__(self, nombre, fuerza, inteligencia, defensa, vida)
	
		
		self.nombre = nombre  
		self.fuerza = fuerza
		self.inteligencia = inteligencia
		self.defensa = defensa 
		self.vida = vida
	
	def atributos(self): #creo esto para mostrar los atributos
		print(self.nombre, ":", sep="")
		print("fuerza", self.fuerza)
		print("inteligencia", self.inteligencia)
		print("defensa", self.defensa)
		print("vida", seld.vida)
	


mi_personaje = Personaje("loocakoo", 10, 50, 20, 10) 
mi_personaje.atributos() #asi accedo a todos los atributos

```

Puedo hacer un método para modificar los atributos:

```python

class Personaje:
	def __init__(self, nombre, fuerza, inteligencia, defensa, vida):
		self.nombre = nombre  
		self.fuerza = fuerza
		self.inteligencia = inteligencia
		self.defensa = defensa 
		self.vida = vida
	
	def atributos(self): 
		print(self.nombre, ":", sep="")
		print("fuerza", self.fuerza)
		print("inteligencia", self.inteligencia)
		print("defensa", self.defensa)
		print("vida", seld.vida)
	
	def subir_nivel(self, fuerza, inteligencia, defensa):
		self.fuerza = self.fuerza + fuerza
		self.inteligencia = self.inteligencia + inteligencia
		self.defensa = self.defensa + defensa
	
	def esta_vivo(self): #este metodo devuelve true si el personaje esta vivo 
		return self.vida > 0
	
	def morir(self):  #este metodo modifica la vida a 0
		self.vida = 0
		print(self.nombre, "ha muerto")
		
	def danio(self, enemigo) #aca agrego otra class personaje, enemigo, de donde
		#voy a poder sacar datos
		return self.fuerza - enemigo.defensa
		
	def atacar(self, enemigo)
		danio = self.danio(enemigo)
		enemigo.vida = enemigo.vida - danio
		print(self.nombre, "ha realizado", danio, "puntos de danio a", enemigo.nombre)
		if enemigo.esta_vivo():
			print("la vida de", enemigo.nombre, "es", enemigo.vida)
		else:
			enemigo.morir()


mi_personaje = Personaje("loocakoo", 10, 50, 20, 10) 
mi_enemigo = Personaje("ruiu", 8, 5, 3, 100)
 
mi.personaje.subir_nivel(1, 2, 0)
mi_personaje.atributos()

print(mi_personaje.esta_vivo())
mi_personaje.morir()
print(mi_personaje.esta_vivo())

print(mi_personaje.danio(mi_enemigo))

mi_personaje.atacar(mi_enemigo)
mi_enemigo.atributos()

```

Encapsulaciones, le agrego __ métodos y atributos para que no se pueda acceder del exterior, pero si puedo acceder si llamo a otra función que la llama

![[Pasted image 20260321163602.png]]

![[Pasted image 20260321163533.png]]


Para mostrar y cambiar atributos con codigo de control  se utilizan las funciones set y get

![[Pasted image 20260321163735.png]]

Herencia

```python

class Personaje:
	def __init__(self, nombre, fuerza, inteligencia, defensa, vida):
		self.nombre = nombre  
		self.fuerza = fuerza
		self.inteligencia = inteligencia
		self.defensa = defensa 
		self.vida = vida
	
	def atributos(self): 
		print(self.nombre, ":", sep="")
		print("fuerza", self.fuerza)
		print("inteligencia", self.inteligencia)
		print("defensa", self.defensa)
		print("vida", seld.vida)
	
	def subir_nivel(self, fuerza, inteligencia, defensa):
		self.fuerza = self.fuerza + fuerza
		self.inteligencia = self.inteligencia + inteligencia
		self.defensa = self.defensa + defensa
	
	def esta_vivo(self):  
		return self.vida > 0
	
	def morir(self):  
		self.vida = 0
		print(self.nombre, "ha muerto")
		
	def danio(self, enemigo) 
		return self.fuerza - enemigo.defensa
		
	def atacar(self, enemigo)
		danio = self.danio(enemigo)
		enemigo.vida = enemigo.vida - danio
		print(self.nombre, "ha realizado", danio, "puntos de danio a", enemigo.nombre)
		if enemigo.esta_vivo():
			print("la vida de", enemigo.nombre, "es", enemigo.vida)
		else:
			enemigo.morir()
			
			

class Guerrero(Personaje): #creo una clase heredando sus caracteristicas
	pass

mi_personaje = Personaje("loocakoo", 10, 50, 20, 10) 
mi_enemigo = Personaje("ruiu", 8, 5, 3, 100)
 
guts = Guerrero() #esto da error, ya que le tengo que pasar personajes, y personajes inicializa con init()

#inicializo los atributos de personaje
 guts = Guerrero("Guts", 20, 10, 100) #hereda el constructor de personaje
 print(guts.nombre) #puedo acceder a los atributos
 print(guts.esta_vivo()) #puedo acceder a los metodos
 guts.atributos

#si yo quiero agregar un atributo mas
guts = Guerrero("Guts", 20, 10, 100, 5) 
#tengo que definir un nuevo init

class Guerrero(Personaje)
	def __init__(self, nombre, fuerza, inteligencia, defensa, vida, espada)
		#hay que inicializar los atributos heredados
		Personaje.__init__(self, nombre, fuerza, inteligencia, defensa, vida)
		#sino super llama a los atributos y metodos de la super clase
		super().__init__(nombre, fuerza, inteligencia, defensa, vida)
		#no hace falta anadir self
		#super ayuda a que si cambio el nombre de la supercalse no lo tengo que 
		#cambiar en el codigo actual
		self.espada = espada #agrego el nuevo atributo
		
	def cambiar_arma(self)
		opcion = int(input("elige un arma: (1) acero valyrio, danio 8, (2)..."))
		if opcion == 1:
			self.espada = 8
		elif opcion == 2: 
			self.espada = 10
		else:
			 print("Numero de arma incorrecto") 
			 
	def atributos(self):
		super().atributos() #traigo de la superclase el metodo atributos
		print("Espada: ", self.espada)
		
	def danio(self, enemigo):
		return self.fuerza*self.espada - enemigo.defensa
	
guts = Guerrero("guts", 20, 10, 10, 100, 5) 
get.atributos() #ahora esto anda
print(guts.espada)

guts.cambiar_arma()
gut.atributos()
```