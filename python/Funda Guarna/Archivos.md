
![[Pasted image 20260428180500.png]]

![[Pasted image 20260428180532.png]]

![[Pasted image 20260428180606.png]]

![[Pasted image 20260428180426.png]]

![[Pasted image 20260428180704.png]]

![[Pasted image 20260428180731.png]]

![[Pasted image 20260428180818.png]]

# Corte de control

![[Pasted image 20260428180908.png]]

# Merge

![[Pasted image 20260428181044.png]]


![[Pasted image 20260428181203.png]]

![[Pasted image 20260428181502.png]]

# Apareo o actualizaciones
![[Pasted image 20260428181623.png]]

```python
def main():

    deudas = obtener_archivo("ArchivosEjercicios/deudas.txt")
    actualizaciones = obtener_archivo("ArchivosEjercicios/actualizaciones.txt")
    nuevas_deudas = open("nuevasDeudas.txt", "w")

  

    deudor_actual, deuda_actual = leer_linea(deudas)
    deudor_a_actualizar, deuda_actualizacion = leer_linea(actualizaciones)
    deuda_acumulada = deuda_actual

    while not deudor_actual == FIN_ARCHIVO and not deudor_a_actualizar == FIN_ARCHIVO:

     #En el if (Acumular): El archivo "maestro" (deudas) se queda frenado en un registro mientras el de actualizaciones avanza para ver cuántos movimientos tiene esa misma persona.      

    #En el elif (Escritura): El archivo de actualizaciones se queda frenado (esperando que el maestro lo alcance) mientras el "maestro" avanza al siguiente deudor una vez que ya terminaste de escribir el anterior.

  

        ## CASO ACUMULAR si existe en la lista deudor a actualzar, lo actualizo
        if deudor_actual == deudor_a_actualizar:
            deuda_acumulada = actualizar_deuda(deuda_acumulada, deuda_actualizacion)
            deudor_a_actualizar, deuda_actualizacion = leer_linea(actualizaciones)

        ## CASO ESCRITURA no tengo nada que actualizar, paso a la siguiente linea
        elif deudor_actual < deudor_a_actualizar:
            if deuda_acumulada != SIN_DEUDA:
                nuevas_deudas.write(deudor_actual + " " + deuda_acumulada + "\n")
            deudor_actual, deuda_actual = leer_linea(deudas)
            deuda_acumulada = deuda_actual

        ## CASO NUEVO DEUDOR si tengo uno menor que yo, significa que es nuevo
        else:
            deudor_a_actualizar, deuda_actualizacion = agregar_nuevo_deudor(deudor_a_actualizar, deuda_actualizacion, actualizaciones, nuevas_deudas)
            
    ## DUMP deudas.txt
    while not deudor_actual == FIN_ARCHIVO:
        nuevas_deudas.write(deudor_actual + " " + deuda_acumulada + "\n")
        deudor_actual, deuda_acumulada = leer_linea(deudas)

  
    ## DUMP actualizaciones.txt
    while not deudor_a_actualizar == FIN_ARCHIVO:
        deudor_a_actualizar, deuda_actualizacion = agregar_nuevo_deudor(deudor_a_actualizar, deuda_actualizacion, actualizaciones, nuevas_deudas)

  
    deudas.close()
    actualizaciones.close()
    nuevas_deudas.close()
    remove("ArchivosEjercicios/deudas.txt")
    remove("ArchivosEjercicios/actualizaciones.txt")
    rename("nuevasDeudas.txt", "ArchivosEjercicios/deudas.txt")

main()
```