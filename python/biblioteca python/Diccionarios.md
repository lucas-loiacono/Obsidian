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

Si tenés este diccionario: `dic = { 101: [8, 9], 102: [4, 7] }`
`dic.items()` se ve internamente algo así: `[(101, [8, 9]), (102, [4, 7])]`

```python
# Así sería con índices (más complejo):
for p, notas in diccionario.items():
    for i in range(len(notas)):
        nota_actual = notas[i]
        print(f"El alumno {p} sacó un {nota_actual}")

# Así es como lo estamos haciendo (más simple):
for p, notas in diccionario.items():
    for n in notas:
        print(f"El alumno {p} sacó un {n}")
```

si yo tengo solo un par que no tenga listas

```python
 for part, vots in partidos_en_prov.items():
            if vots > ganador_votos:
                ganador_votos = vots
                ganador_nombre = part
```

.keys()
```python
for padron in alumnos.keys(): #esto devuelve una lista de las keys, una pegada de la otra, como ya es una lista, lo puedo ordenar
    print(padron)
```

.values()
```python
for padron in alumnos.values(): #esto devuelve una lista de los values de las keys
    print(padron)
```

si yo quiero pasar key-valor de un diccionario a una lista para despues ordenarlo
```python
ranking = []

    for clave, valor in diccionario.items():
        ranking.append((clave, valor))
    # Ordenamos de mayor a menor por cantidad (índice 1 de la tupla)
    ranking.sort(key=lambda par: par[1], reverse=True)
```
