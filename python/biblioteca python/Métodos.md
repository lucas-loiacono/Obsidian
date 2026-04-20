## 1. Métodos de Strings (Cadenas de texto)

Se usan haciendo `texto.metodo()`. Son claves para limpiar datos.

- **`.lower()` / `.upper()`**: Pasa todo a minúsculas o mayúsculas.
- **`.capitalize()`**: Pasa solo la primera letra a mayúscula.
- **`.strip()`**: Quita los espacios vacíos (y saltos de línea) al principio y al final.
- **`.split()`**: Corta el texto en partes (por defecto donde hay espacios) y te devuelve una **lista**.
- **`.isalpha()`**: Devuelve `True` si el texto tiene **solo** letras.
- **`.isdigit()`**: Devuelve `True` si el texto tiene **solo** números.
- **`.isalnum()`**: Mezcla de los dos anteriores (letras y números).
- **`.replace(viejo, nuevo)`**: Cambia una parte del texto por otra.


```python
palabra = "Hola,123"
limpia = ""

for letra in palabra:
    if letra.isalpha():
        # Solo entra aquí si es 'H', 'o', 'l', 'a'
        limpia += letra

print(limpia) # Resultado: "Hola"
```

## 2. Métodos de Listas (Arrays)

Se usan para modificar tus colecciones de datos.

- **`.append(dato)`**: Agrega un elemento al final.
- **`.extend(otra_lista)`**: Une una lista al final de otra.
- **`.pop(indice)`**: Elimina y te devuelve el elemento en esa posición (si no ponés índice, saca el último).
- **`.remove(valor)`**: Busca el valor y elimina la primera aparición que encuentre.
- **`.sort()`**: Ordena la lista (de menor a mayor por defecto).
- **`.reverse()`**: Invierte el orden de los elementos.


## 3. Funciones Integradas (Built-in)

Estas se usan pasando el objeto adentro de los paréntesis: `funcion(objeto)`.

- **`len()`**: Te dice cuántos elementos tiene una lista o letras un string.
- **`sum()`**: Suma todos los números de una lista.
- **`min()` / `max()`**: Encuentra el valor más chico o más grande.
- **`sorted()`**: Te devuelve una **copia** ordenada de una lista (sin modificar la original).
- **`type()`**: Te dice qué tipo de dato es (int, str, list, etc.).
- **`input()`**: Para pedir datos al usuario.
- **`print()`**: Para mostrar datos en consola.
- **`range()`**: Genera una secuencia de números para los ciclos `for`.
- **`enumerate()`**: Te da el índice y el valor al mismo tiempo en un `for`.
- **`zip()`**: Junta dos o más listas para recorrerlas en paralelo.

## 4. Métodos de Diccionarios

Fundamentales para tus últimos ejercicios de provincias y alumnos.

- **`.keys()`**: Te da todas las claves.
- **`.values()`**: Te da todos los valores asociados.
- **`.items()`**: Te da las parejas (clave, valor) para desempaquetar en un `for`.
- **`.get(clave, defecto)`**: Busca una clave, y si no existe, te devuelve el "defecto" que vos elijas (evita que el programa explote).