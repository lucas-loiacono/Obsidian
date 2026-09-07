
La diferencia fundamental es que los **primitivos** son valores crudos y básicos almacenados directamente en memoria por pura velocidad, mientras que las **clases** (conocidas como _Wrapper classes_ o clases envolventes) son objetos completos que "envuelven" a ese valor y le agregan funcionalidades.

|**Característica**|**Primitivo (int, double, boolean)**|**Clase Envolvente (Integer, Double, Boolean)**|
|---|---|---|
|**Naturaleza**|Valor crudo en memoria (Stack).|Objeto en la memoria dinámica (Heap).|
|**Métodos**|No tienen métodos.|Tienen métodos útiles (ej. `Integer.parseInt()`).|
|**Valor nulo**|No pueden ser `null` (el valor por defecto de un `int` es `0`).|Pueden ser `null` (útil si un dato falta o no se cargó).|
|**Uso en Colecciones**|No se pueden usar en listas (ej. `ArrayList<int>` da error).|Obligatorios en colecciones (ej. `ArrayList<Integer>`).|
|**Rendimiento**|Muy rápidos y ligeros.|Más lentos y ocupan un poco más de memoria.|

### El ejemplo práctico: `int` vs `Integer`

Un `int` es solo un espacio en la memoria guardando un número. No sabe hacer nada más que existir y participar en operaciones matemáticas.


```Java
int edad = 21;
// Si escribís "edad." no pasa nada, no hay herramientas asociadas.
```

Un `Integer` es un objeto que _contiene_ el número 21, pero viene equipado con un panel de herramientas:


```Java
Integer edadObjeto = 21;
String texto = edadObjeto.toString(); // Convierte el número a texto
int maximo = Integer.MAX_VALUE;       // Te devuelve el número máximo que soporta Java
```

### Autoboxing y Unboxing

Para no volverte loco convirtiendo manualmente un `int` a un `Integer` y viceversa, Java hace la conversión automáticamente en segundo plano. A esto se le llama _Autoboxing_ (empaquetar) y _Unboxing_ (desempaquetar).


```Java
// Autoboxing: Java agarra el primitivo 5 y crea el objeto Integer automáticamente
Integer numeroObjeto = 5; 

// Unboxing: Java saca el valor primitivo de adentro del objeto
int numeroPrimitivo = numeroObjeto; 
```

### ¿Cuándo usar cada uno?

- Usá **primitivos (`int`, `double`)** por defecto. Son la mejor opción para bucles `for`, contadores, cálculos matemáticos y almacenamiento de datos simples porque son muchísimo más eficientes.
    
      
    
- Usá **clases envolventes (`Integer`, `Double`)** cuando el valor pueda estar vacío y necesites representarlo con un `null` (por ejemplo, al leer datos de una base de datos), o cuando necesites agrupar esos números en estructuras de datos dinámicas como un `ArrayList` o un `HashMap`, ya que estas estructuras de Java solo aceptan objetos.











  
|**Tipo Primitivo**|**Clase Asociada**|**Uso principal del dato**|
|---|---|---|
|`byte`|**`Byte`**|Números enteros muy pequeños (8 bits)|
|`short`|**`Short`**|Números enteros pequeños (16 bits)|
|`int`|**`Integer`**|Números enteros estándar (32 bits)|
|`long`|**`Long`**|Números enteros grandes (64 bits)|
|`float`|**`Float`**|Números decimales (precisión simple)|
|`double`|**`Double`**|Números decimales (doble precisión)|
|`char`|**`Character`**|Un solo carácter (letra, símbolo, espacio)|
|`boolean`|**`Boolean`**|Valores lógicos (`true` o `false`)|

Como regla general, las clases se llaman exactamente igual que su primitivo pero con la primera letra en mayúscula. Las únicas dos excepciones a las que tenés que prestar atención son **`int`**, que se transforma en **`Integer`**, y **`char`**, que se transforma en **`Character`**.

  

Aunque no es una clase envolvente de un primitivo en particular, **`String`** funciona como la clase oficial en Java para manejar cadenas de texto (que internamente se componen de múltiples `char`).