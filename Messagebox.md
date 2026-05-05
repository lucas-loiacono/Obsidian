### Familia 1: Los Informativos (Solo avisan)

Estos solo muestran un mensaje y tienen un único botón de "Aceptar" (`OK`). Tu programa se pausa hasta que el usuario hace clic.

- **`messagebox.showinfo("Título", "Mensaje")`**: Muestra información general. Aparece con el ícono de una letra "i" azul.
- **`messagebox.showwarning("Título", "Mensaje")`**: Súper útil si el usuario dejó un Entry en blanco. Aparece con un triángulo amarillo de advertencia.
- **`messagebox.showerror("Título", "Mensaje")`**: Ideal para cuando falla una conexión a la base de datos o el dato ingresado es totalmente inválido. Aparece con un círculo rojo y una "X".


---

### Familia 2: Los Interrogativos (Piden una decisión)

Acá está la verdadera magia. Estos te **devuelven un valor** según el botón que toque el usuario, por lo que siempre tenés que guardarlos en una variable o usarlos en un `if`.

**Los que devuelven `True` o `False` (booleanos):**

- **`messagebox.askyesno("Título", "¿Mensaje?")`**: Tiene botones "Sí" y "No". Devuelve `True` si toca Sí, y `False` si toca No. **¡Es el que más vas a usar!**
- **`messagebox.askokcancel("Título", "¿Mensaje?")`**: Tiene botones "Aceptar" y "Cancelar". Devuelve `True` o `False`.
    
- **`messagebox.askretrycancel("Título", "¿Mensaje?")`**: Tiene botones "Reintentar" y "Cancelar". Devuelve `True` o `False`.
    

**Las excepciones tramposas (¡Ojo acá!):**

- **`messagebox.askquestion("Título", "¿Mensaje?")`**: Aunque parezca igual al `askyesno`, este NO devuelve booleanos. Devuelve un texto: el string **`"yes"`** o el string **`"no"`**.
    
- **`messagebox.askyesnocancel("Título", "¿Mensaje?")`**: Tiene TRES botones: "Sí", "No" y "Cancelar". Devuelve `True` (Sí), `False` (No) y **`None`** (Cancelar). Es ideal para cuando vas a cerrar un archivo sin guardar.
    

---

### Ejemplo de cómo se usa en la vida real (y en un parcial):

Nunca tires un `askyesno` suelto al aire. Siempre tenés que atajar su respuesta:

Python

``` python
def borrar_datos():
    # Guardamos la respuesta del usuario (True o False)
    respuesta = messagebox.askyesno("Confirmar", "¿Estás seguro que querés borrar todo?")
    
    if respuesta == True:
        # Acá hacés la lógica para borrar
        messagebox.showinfo("Éxito", "Los datos fueron borrados.")
    else:
        # Acá no hacés nada, o le avisás que se canceló
        messagebox.showinfo("Cancelado", "Uf, menos mal, no borramos nada.")
```