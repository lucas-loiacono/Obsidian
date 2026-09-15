`System.arraycopy` es una herramienta nativa de Java (escrita a muy bajo nivel, probablemente en C o C++) diseñada para mover bloques de memoria de un lugar a otro de forma extremadamente rápida y eficiente.

En lugar de usar un ciclo `for` para copiar elemento por elemento (lo cual es lento), `arraycopy` toma un bloque entero de datos y lo "teletransporta" a su nuevo destino.

### Los 5 parámetros de arraycopy

Para que funcione, siempre debes pasarle exactamente 5 parámetros en este orden:

`System.arraycopy(origen, posicionOrigen, destino, posicionDestino, cantidad);`

- **`origen`:** El arreglo _desde_ el cual quieres copiar los datos.
    
- **`posicionOrigen`:** El índice numérico donde vas a empezar a "recortar" o copiar.
    
- **`destino`:** El arreglo _hacia_ el cual vas a pegar los datos. Puede ser un arreglo totalmente nuevo o **el mismo arreglo de origen**.
    
- **`posicionDestino`:** El índice numérico donde vas a empezar a "pegar".
    
- **`cantidad`:** Cuántos elementos en total vas a mover.


### ¿Cómo lo usamos en tu Vector Dinámico?

Lo genial de tu código es que usaste este método de tres formas completamente distintas. Aquí te muestro qué hizo en cada caso:


**1. Mudanza a una casa más grande (Redimensionar)**

```Java
System.arraycopy(datos, 0, nuevoArray, 0, capacidadActual);
```

Tomaste todos los elementos del arreglo viejo (`datos`), empezando desde la posición `0`, y los pegaste en el `nuevoArray` vacío, también desde la posición `0`.


**2. Desplazamiento hacia la derecha (Agregar con índice)**


```Java
System.arraycopy(datos, indice, datos, indice + 1, cantidadElementos - indice);
```

Aquí origen y destino son el mismo arreglo. Le dijiste a Java: "Toma los elementos a partir de `indice` y pégalos un pasito hacia la derecha (`indice + 1`)". Esto empuja los datos y crea un "hueco" perfecto para insertar tu nuevo elemento sin perder nada.

  

**3. Desplazamiento hacia la izquierda (Eliminar con índice)**

```Java
System.arraycopy(datos, indice + 1, datos, indice, cantidadElementos - 1 - indice);
```

Igual que el anterior, pero al revés. Le dijiste: "Toma los elementos que están justo a la derecha del que quiero borrar (`indice + 1`) y pégalos un pasito hacia la izquierda (`indice`)". Al pegarlos encima, el dato viejo se "pisa" y el hueco se cierra.

  