```python
from tkinter import *
from tkinter import messagebox

raiz = Tk()
raiz.title("ingreso de datos")
raiz.geometry("1920x1080)
raiz.resizable(False, False)
raiz.iconbitmap("ruta.ico")
raiz.config(bg="blue")
raiz.config(padx=30, pady=30)

raiz.mainloop
```

# frames

**Creación (El Contenido):**

- `miframe = Frame(raiz)`: Lo anclás a la ventana principal.
- **`bg`** o **`background`**: Color de fondo. Súper útil para diferenciar zonas (ej: un frame gris para el menú y un frame blanco para el formulario).
- **`width`** y **`height`**: El tamaño del frame _en píxeles_.
- **`bd`** o **`borderwidth`**: Grosor del borde en píxeles.
- **`relief`**: El tipo de borde si querés que parezca una caja 3D. Puede ser `"sunken"`, `"raised"`, `"groove"`, `"ridge"` o `"solid"`.
- _Tip:_ Para que el `relief` se vea, sí o sí tenés que ponerle un `bd` mayor a 0 (ej: `bd=5`).


**Posicionamiento (El Espacio):** Igual que todo lo demás, el Frame necesita ser empaquetado o grillado para existir.

- **`miframe.pack()`**: Ideal si vas a poner un solo frame centrado.
    
- **`miframe.grid(row=0, column=0)`**: Ideal si vas a usar varios frames (ej: uno a la izquierda para botones y uno a la derecha para mostrar datos).

### 💡 El "Pro-Tip" salvavidas de los Frames:

Hay algo que vuelve locos a todos cuando empiezan con Tkinter: si vos creás un Frame de 500x500 píxeles, pero adentro le metés un botoncito chiquito... **el Frame se va a achicar automáticamente al tamaño del botón**.

Tkinter hace esto por defecto (se llama "propagación"). Si alguna vez querés que tu Frame mantenga su tamaño fijo de 500x500 sin importar qué le metas adentro, tenés que apagarle esa propagación con esta línea mágica:

- `miframe.pack_propagate(False)` (si usaste pack)
- `miframe.grid_propagate(False)` (si usaste grid)




### 1. El método `.pack()`

Ideal para apilar elementos uno al lado del otro o uno abajo del otro.

- **`side`**: Define hacia qué pared se empuja el elemento. Valores: `"top"` (por defecto), `"bottom"`, `"left"`, `"right"`.
    
- **`fill`**: Hace que el elemento se estire para llenar el espacio libre. Valores: `"x"` (se estira horizontalmente), `"y"` (verticalmente), `"both"` (en ambas direcciones), `"none"` (por defecto).
    
- **`expand`**: Le dice al elemento si debe pedirle a la ventana que le asigne todo el espacio extra sobrante disponible. Valores: `True` o `False`.
    
- **`anchor`**: Si el espacio asignado es más grande que el elemento, define dónde se ancla. Valores con puntos cardinales: `"n"` (norte), `"s"`, `"e"`, `"w"`, `"nw"`, `"ne"`, `"sw"`, `"se"`, `"center"`.
    
- **`padx` / `pady`**: Márgenes **exteriores** (espacio en píxeles que separa al elemento de los demás o de la pared). `padx` es horizontal, `pady` es vertical.
    
- **`ipadx` / `ipady`**: Márgenes **interiores** (espacio en píxeles que ensancha o estira al elemento por dentro, alejando sus bordes de su propio texto).
    
- **`before` / `after`**: Permite alterar el orden de apilamiento indicando que se ubique justo antes o justo después de otro _widget_ específico.
    

---

### 2. El método `.grid()`

Ideal para crear formularios, tablas o diseños estructurados en filas y columnas.

- **`row`**: El número de fila donde querés ubicar el elemento. (Empieza en `0`).
    
- **`column`**: El número de columna donde querés ubicar el elemento. (Empieza en `0`).
    
- **`rowspan`**: Hace que el elemento se expanda hacia abajo y ocupe varias filas a la vez (ej: `rowspan=2`).
    
- **`columnspan`**: Hace que el elemento se expanda hacia los costados y ocupe varias columnas a la vez (ej: `columnspan=3`).
    
- **`sticky`**: Como un `fill` y un `anchor` combinados. Pega el elemento a los bordes de su celda si la celda es más grande que él. Valores cardinales: `"n"`, `"s"`, `"e"`, `"w"`, o combinaciones como `"ew"` (estirar horizontalmente), `"ns"` (estirar verticalmente), o `"nsew"` (llenar toda la celda).
    
- **`padx` / `pady`**: Márgenes **exteriores** (separa la caja del elemento de las paredes de la celda de la grilla).
    
- **`ipadx` / `ipady`**: Márgenes **interiores** (engorda al elemento por dentro).
    

---

### 3. El método `.place()`

Ideal para el control milimétrico y posicionamiento exacto mediante coordenadas.

- **`x` / `y`**: Posicionamiento absoluto. Especificás el píxel exacto de ubicación. `x=0, y=0` es la esquina superior izquierda.
    
- **`relx` / `rely`**: Posicionamiento relativo. Se usan números del `0.0` al `1.0` (porcentajes) basándose en el tamaño del contenedor padre. Ej: `relx=0.5, rely=0.5` centra el elemento, sin importar de qué tamaño sea la ventana.
    
- **`width` / `height`**: Fuerza al elemento a tener un tamaño absoluto específico en píxeles.
    
- **`relwidth` / `relheight`**: Fuerza al elemento a tener un tamaño relativo al padre, usando del `0.0` al `1.0`. Ej: `relwidth=1.0` hace que ocupe todo el ancho de su contenedor.
    
- **`anchor`**: Define qué punto exacto del propio elemento es el que se ubicará en la coordenada `x` o `relx` que le pasaste. Valores cardinales: `"n"`, `"s"`, `"e"`, `"w"`, `"nw"` (por defecto), `"ne"`, `"sw"`, `"se"`, `"center"`.
    
- **`bordermode`**: Decide si los cálculos relativos deben tener en cuenta el ancho del borde del contenedor padre o no. Valores: `"inside"` (por defecto) u `"outside"`.