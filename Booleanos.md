### 1. Iniciar en `False` (Búsqueda de un Tesoro)

Esta es la más común cuando buscas **una coincidencia** o quieres verificar si algo existe.

- **Estado inicial:** Apagado (`False`).
    
- **Lógica:** "Asumo que no existe, hasta que lo encuentre".
    
- **Cuándo usarla:**
    
    - Para saber si un número está en una lista.
        
    - Para saber si hay un error en un formulario (inicias `error = False`).
        
    - En tu ejercicio del club: "Asumo que no entro, hasta que compruebe que hay suficientes actividades".
        

> **Analogía:** Es como buscar una llave en una caja. Empiezas pensando que no la tienes, y solo cuando la tocas, "prendes la luz".

### 2. Iniciar en `True` (El Filtro de Seguridad)

Se usa cuando necesitas que se cumplan **todas** las condiciones o cuando quieres validar que algo sea perfecto.

- **Estado inicial:** Encendido (`True`).
    
- **Lógica:** "Asumo que todo está bien, hasta que algo falle".
    
- **Cuándo usarla:**
    
    - Para verificar una contraseña (empieza como válida, pero si un carácter está mal, se apaga).
        
    - En validaciones de "cumple con todos los requisitos".
        
    - En tu ejercicio del club: Podrías haber iniciado en `True` y apagarlo inmediatamente si el precio es mayor a `MAX_CUOTA`.
        

---

### Comparativa: ¿Cuál es más eficiente?

Depende de qué sea más probable que ocurra o de qué condición sea más fácil de "romper".

|**Inicio**|**Nombre Técnico**|**Cuándo "cambia la tecla"**|
|---|---|---|
|**`False`**|**Acumulador/Bandera de éxito**|En cuanto encuentras **un** caso positivo.|
|**`True`**|**Bandera de validación**|En cuanto encuentras **un** solo fallo o error.|

---

### Un consejo de "limpieza" (Clean Code)

Aunque usar la "tecla" (bandera) está bien, a medida que avances verás que **lo más eficiente es no usar la tecla si puedes devolver el resultado directamente**.

En tu código anterior hacías:

Python

```
band = True
if precio > MAX_CUOTA:
    band = False
return band
```

Pero los programadores experimentados prefieren el **"Retorno Temprano"**:

Python

```
if precio > MAX_CUOTA:
    return False # Apagamos y salimos de la habitación directamente
```

**Resumen:** Si estás contando cosas para llegar a una meta (como las 2 actividades), inicia en `False`. Si estás verificando que nada falle, inicia en `True`.