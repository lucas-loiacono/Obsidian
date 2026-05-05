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