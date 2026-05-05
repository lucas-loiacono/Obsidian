### 1. Parámetros de Creación del `Label` (El Contenido)

Estos son los que definen cómo se ve y qué dice tu etiqueta de texto. 
`mi_etiqueta = Label(padre, parametro=valor)`

**Los esenciales para el Texto:**

- **`text`**: El texto estático que va a mostrar. (Ej: `text="Ingrese su nombre:"`).
- **`textvariable`**: Se usa si querés que el texto cambie dinámicamente durante el programa (por ejemplo, un cartel que diga "Guardado exitoso" o un contador de puntos). Lo enlazás a un `StringVar()`.

**Para controlar la Estética:**

- **`font`**: El tipo, tamaño y estilo de la letra en formato tupla. (Ej: `font=("Verdana", 10, "italic")`).
- **`bg`** (o `background`): Color de fondo de la etiqueta. Si querés que se fusione con la ventana, le tenés que poner el mismo color que al `Frame`.
- **`fg`** (o `foreground`): Color del texto. (Ej: `fg="red"` o `fg="white"`).

**Para controlar el Tamaño:**

- **`width`** y **`height`**: Igual que en el Entry, si la etiqueta solo tiene texto, esto se mide en _cantidad de caracteres_ (ancho) y _cantidad de líneas_ (alto), no en píxeles.

**Para textos largos o múltiples líneas (¡Súper útiles!):**

- **`justify`**: Si tu texto tiene varios renglones (usando `\n`), esto decide cómo se alinean esos renglones entre sí. Puede ser `"left"`, `"center"` o `"right"`.

- **`wraplength`**: ¡Este es un salvavidas! Si le pasás un número en píxeles (ej: `wraplength=150`), Tkinter automáticamente va a cortar tu texto y pasarlo al renglón de abajo cuando alcance ese ancho, para que no te deforme la ventana.

- **`anchor`**: Hacia qué lado de su propia "caja" se va a apoyar el texto. Usa puntos cardinales como el sticky (`"n"`, `"s"`, `"e"`, `"w"`, `"center"`).


_(Nota rápida: `justify` alinea los renglones de un párrafo; `anchor` mueve todo el bloque de texto dentro del Label)._

---

### 2. Parámetros de Posicionamiento (El Espacio con `grid`)

**¡Acá viene la mejor noticia para tu examen!** El método `.grid()` es un "Administrador de Geometría" que pertenece a la ventana, no al elemento. Por lo tanto, **los parámetros son EXACTAMENTE LOS MISMOS que para el `Entry`, para un `Button` o para un `Frame`**.

Todo lo que aprendimos y dedujiste arriba, aplica igual acá:

- **`row`** y **`column`**: Fila y columna donde nace.
- **`columnspan`** y **`rowspan`**: Cuántas celdas "fusiona" o abarca.
- **`padx`** y **`pady`**: El escudo o margen protector hacia afuera (ideal para separar las etiquetas de los bordes o de otras filas).
- **`ipadx`** y **`ipady`**: El aire interno de la etiqueta (engorda el color de fondo).
- **`sticky`**: Cómo se comporta si la celda es más grande que su texto. En tu caso usamos `sticky="e"` para que los textos se peguen a la derecha, justito al lado de sus `Entry` correspondientes.