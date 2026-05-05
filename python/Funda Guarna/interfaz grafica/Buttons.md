### 1. Parámetros de Creación del `Button` (El Contenido y la Acción)

Acá definís cómo se ve el botón y qué hace cuando lo clickean. 
`mi_boton = Button(padre, parametro=valor)`

**El esencial para la Lógica:**

- **`command`**: **¡El fotógrafo!** Acá le pasás el nombre de la función que querés que se ejecute al hacer clic.
    
    - _Atención a la trampa clásica:_ Se pasa el nombre de la función **SIN paréntesis**. (Ej: `command=enviar_datos`, no `command=enviar_datos()`). Si le ponés paréntesis, la función se va a ejecutar sola apenas abras la ventana, y no cuando hagas clic.
    

**Para controlar el Texto y Estado:**

- **`text`**: El texto que lleva adentro el botón. (Ej: `text="Enviar"`).
- **`state`**: Podés deshabilitar el botón si te falta algún dato. Usá `state="disabled"` para que quede grisado y no se pueda clickear, o `state="normal"` (el por defecto).


**Para controlar la Estética y el Tamaño:**

- **`font`**: Tipo, tamaño y estilo de la letra. (Ej: `font=("Arial", 12, "bold")`).
- **`bg`** (o `background`): Color de fondo del botón.
- **`fg`** (o `foreground`): Color del texto del botón.
- **`width`** y **`height`**: Igual que antes, se miden en caracteres (ancho) y renglones (alto), no en píxeles.
- **`cursor`**: Cambia la formita del mouse al pasar por encima. Ponerle `cursor="hand2"` es un toque re profesional porque pone la "manito" típica de los links de internet.
- **`relief`**: El estilo del borde. Por defecto es `"raised"` (elevado, para que parezca un botón 3D), pero podés usar `"flat"` si querés un diseño más moderno y chato, o `"sunken"` (hundido).
    

---

### 2. Parámetros de Posicionamiento (El Espacio con `grid`)

Como dijimos antes, la magia de Tkinter es que `.grid()` es universal. Aplican las mismas reglas que para el `Entry` y el `Label`:

- **`row`** y **`column`**: Dónde lo ubicás.
- **`columnspan`**: Excelente para centrar un botón abajo de todo tu formulario, haciendo que ocupe las dos columnas de tu tabla (ej: `columnspan=2`).
- **`sticky`**: Hacia dónde lo empujás (`"e"` para la derecha, `"w"` para la izquierda, `"ew"` si querés que sea un botón largo que ocupe todo el ancho disponible).
- **`padx`** y **`pady`**: Para separarlo del resto de los elementos (¡imprescindible darle un buen `pady` al botón de Enviar para que no quede pegado a los recuadros!).
    

**El truco de oro para los Botones:**

- **`ipadx`** e **`ipady`** (Padding interno): Son los mejores amigos del `Button`. En lugar de pelear con el parámetro `width`, le agregás un poquito de aire interno (`ipadx=10, ipady=5`) y tu botón instantáneamente se ve más grande, más gordo y mucho más fácil de clickear, sin cambiar el tamaño de la letra.