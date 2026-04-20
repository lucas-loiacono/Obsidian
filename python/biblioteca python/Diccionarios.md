Insertar en un diccionario
```python
frecuencias = {}
  for palabra in palabras:

        if palabra in frecuencias:
            # Si ya existe, sumamos 1
            frecuencias[palabra] += 1
        else:
         # Si es nueva, la creamos con valor 1
            frecuencias[palabra] = 1
```

si yo quiero insertar los datos en forma de dos valores en una lista hago

```python
lista = []
    for clave in diccionario:  
        cantidad_alum_aprobados = diccionario[clave][2]
        cantidad_alum_rindieron = diccionario[clave][1]
        porcentaje = (cantidad_alum_aprobados/cantidad_alum_rindieron)*100
        lista.append((clave, porcentaje)) #aca los agrego como par
```

.items()