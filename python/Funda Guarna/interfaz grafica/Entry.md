### 1. Parámetros de Creación del `Entry` (El Contenido)

Estos son los parámetros que ponés adentro de los paréntesis cuando "bautizás" al recuadro: `mi_entry = Entry(padre, parametro=valor)`

**Para controlar el Tamaño y Aspecto:**

- **`width`**: El ancho del recuadro. **Ojo:** Se mide en cantidad de _caracteres_ (letras), no en píxeles. (Ej: `width=30`).
- **`font`**: El tipo, tamaño y estilo de la letra. Se pasa como tupla. (Ej: `font=("Arial", 12, "bold")`).
- **`bg`** (o `background`): Color de fondo del recuadro. (Ej: `bg="white"` o `bg="#F0F0F0"`).
- **`fg`** (o `foreground`): Color del texto que el usuario escribe. (Ej: `fg="black"`).
- **`bd`** (o `borderwidth`): El grosor del borde del recuadro en píxeles. (Ej: `bd=2`).
- **`relief`**: El estilo 3D del borde. Los más usados son `"sunken"` (hundido, el por defecto), `"solid"` (una línea plana), `"raised"` (elevado) o `"flat"` (sin borde).


**Para controlar la Lógica y los Datos:**

- **`textvariable`**: **¡El más importante!** Lo enlazás con una variable (como `StringVar()`) para poder sacarle "la foto" después con `.get()`.
- **`show`**: Súper útil para contraseñas. Reemplaza visualmente lo que el usuario escribe por el carácter que le digas. (Ej: `show="*"`).
- **`state`**: El estado del recuadro. Puede ser `"normal"` (por defecto), `"disabled"` (grisado, no se puede escribir ni hacer clic) o `"readonly"` (se puede copiar el texto pero no modificarlo).
- **`justify`**: Alineación del texto que el usuario va escribiendo. Puede ser `"left"`, `"center"` o `"right"`.

---

### 2. Parámetros de Posicionamiento (El Espacio con `grid`)

Una vez creado, cuando lo mandás a la ventana con `.grid()`, acá es donde le asignás su espacio en la grilla y cómo respira respecto a los demás.

**Ubicación principal:**

- **`row`**: El número de fila (empieza en 0).
- **`column`**: El número de columna (empieza en 0).

**Manejo de Celdas (Expansión):**

- **`columnspan`**: Cuántas columnas de ancho va a abarcar esta celda. (Ej: `columnspan=2`).
- **`rowspan`**: Cuántas filas de alto va a abarcar (menos usado en formularios simples, pero existe).


**Manejo del Espacio Exterior (Márgenes / Padding):**

- **`padx`**: Espacio vacío a los costados (izquierda y derecha). Puede ser un número o una tupla `(izq, der)`.
- **`pady`**: Espacio vacío arriba y abajo. Puede ser un número o una tupla `(arriba, abajo)`.


**Manejo del Espacio Interno (Padding interno):**

- **`ipadx`** (Internal Padding X): Engorda el `Entry` agregando espacio vacío _adentro_ del recuadro, a los costados del texto.
- **`ipady`** (Internal Padding Y): **¡Un truco buenísimo!** Engorda el `Entry` haciéndolo más alto _sin necesidad de cambiar el tamaño de la letra_. Le da un aspecto de formulario moderno, más ancho y cómodo de clickear.

**Comportamiento dentro de su Celda (Alineación / Estiramiento):**

- **`sticky`**: Hacia dónde se "pega" o se estira si la celda es más grande que el recuadro. Funciona con los puntos cardinales en inglés:
    
    - `"n"`, `"s"`, `"e"`, `"w"` (Norte, Sur, Este, Oeste).
        
    - Combinaciones para esquinas: `"ne"`, `"nw"`, `"se"`, `"sw"`.
        
    - **Para estirar:** `"ew"` (se estira horizontalmente llenando el ancho de la celda), `"ns"` (se estira verticalmente), `"nsew"` (se estira para todos lados, llenando la celda entera).