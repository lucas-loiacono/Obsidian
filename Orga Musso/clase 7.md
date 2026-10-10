
![[Pasted image 20261001201035.png]]

![[Pasted image 20261001201100.png]]




# Registro de Desplazamiento (Shift Register)
#organizacion-del-computador #fiuba #electronica-digital #secuenciales #registros

---

## 1. ¿Qué es y cómo está construido?

Un **Registro de Desplazamiento** es un circuito secuencial diseñado para almacenar y mover múltiples bits de información de manera sincronizada.

Físicamente, se construye encadenando varios **Flip-Flops tipo D** ("copiadores") uno detrás del otro (en cascada). Para almacenar $N$ bits, se necesitan exactamente $N$ Flip-Flops (en nuestro caso, 4 biestables: `FF1`, `FF2`, `FF3` y `FF4` para guardar 4 bits).

### Conexiones internas del circuito
1. **Datos en cascada (`Q` $\rightarrow$ `D`):** 
   * La única entrada libre desde el exterior es el pin **`D` del primer biestable (`FF1`)**.
   * La salida **`Q` de `FF1`** (llamada nodo **`A`**) se conecta directamente a la entrada **`D` de `FF2`**.
   * La salida **`Q` de `FF2`** (nodo **`B`**) se conecta a la entrada **`D` de `FF3`**.
   * La salida **`Q` de `FF3`** (nodo **`C`**) se conecta a la entrada **`D` de `FF4`**.
   * La salida **`Q` de `FF4`** es el nodo final **`D`**.
2. **Reloj común (`CLK`):** Todos los Flip-Flops están unidos al **mismo cable de reloj (`CLK`)** y están sincronizados **por flanco** (identificado por el triangulito `>` en la entrada `CLK`). Esto garantiza que todos "disparen" exactamente al mismo instante.
3. **Reinicio común (`CLEAR` / `CLR`):** Todos comparten un cable asincrónico de `CLEAR` en la parte inferior. Al activarlo, todos los biestables se vacían y fuerzan sus salidas a `0` inmediatamente, sin importar el reloj.

### Esquema lógico en bloque
```text
                         (A)                 (B)                 (C)                 (D)
                          |                   |                   |                   |
Entrada ---> [D     Q] ---+----> [D     Q] ---+----> [D     Q] ---+----> [D     Q] ---+
 Serie       [  FF1  ]           [  FF2  ]           [  FF3  ]           [  FF4  ]
             [>CLK   ]           [>CLK   ]           [>CLK   ]           [>CLK   ]
                 ^                   ^                   ^                   ^
                 |___________________|___________________|___________________|
                                      Señal de CLK común
````

## 2. Analogía Mental: El "Pasamano" Simultáneo

Pensalo como una fila de 4 cajas (`A`, `B`, `C`, `D`) y una campana (`CLK`).

- No podés meter los 4 datos al mismo tiempo porque tenés **una sola puerta de entrada** a la izquierda de `FF1`.
    
- Tenés que poner los datos **en fila india** (uno por uno) en la puerta de entrada y hacer sonar la campana (`CLK`).
    
- Cada vez que suena el `CLK`, ocurre un **pasamano simultáneo hacia la derecha**: cada biestable agarra el número que tenía su vecino de la izquierda y lo guarda en su propia salida, mientras `FF1` agarra el número nuevo que pusiste en la puerta.
    

> [!IMPORTANT] Pregunta de examen: ¿Por qué el bit nuevo no viaja de un tirón desde `FF1` hasta `FF4` en un solo pulso de reloj?
> 
> Porque los biestables están sincronizados **por flanco** y existe un microscópico retardo físico de propagación en cada componente:
> 
> 1. El flanco ascendente del `CLK` dura apenas una fracción de nanosegundo (es como sacar una **foto con flash**).
>     
> 2. En ese instante exacto del flash, `FF2` mira qué valor tiene `A` **en ese momento** (el valor viejo) y le saca la foto.
>     
> 3. A `FF1` le toma unos nanosegundos internos procesar el bit nuevo de la entrada y actualizar la salida `A`.
>     
> 4. Para cuando `A` cambia al valor nuevo, **el flash del reloj ya terminó** y la compuerta de `FF2` ya se cerró. Por lo tanto, `FF2` recién va a ver ese valor nuevo en el próximo pulso de reloj.
>     

## 3. Simulación Paso a Paso

Supongamos que queremos cargar en el registro los 4 bits: **`1`, `0`, `1`, `1`** (en ese orden de entrada).

### Paso 0: Limpieza inicial (`CLEAR`)

Antes de empezar, mandamos un pulso por la línea `CLEAR`.

- **Qué pasa:** Se borra cualquier basura previa que hubiera en el circuito.
    
- **Estado actual de las salidas:** `A = 0` | `B = 0` | `C = 0` | `D = 0`
    

### Paso 1: Primer bit (Entra un `1`)

1. **Preparación:** Ponemos un **`1`** en el cable de entrada (a la izquierda de `FF1`). Todavía no cambió nada adentro porque no hubo flanco de reloj.
    
2. **Disparo (`1º Flanco de CLK`):** Todos los biestables copian lo que tienen a su izquierda:
    
    - `FF4` copia lo que había en `C` (`0`) $\rightarrow$ **`D` queda en `0`**.
        
    - `FF3` copia lo que había en `B` (`0`) $\rightarrow$ **`C` queda en `0`**.
        
    - `FF2` copia lo que había en `A` (`0`) $\rightarrow$ **`B` queda en `0`**.
        
    - `FF1` copia el bit de la entrada (`1`) $\rightarrow$ **`A` pasa a `1`**.
        

- **Estado actual de las salidas:** **`A = 1`** | `B = 0` | `C = 0` | `D = 0`
    

### Paso 2: Segundo bit (Entra un `0`)

1. **Preparación:** Cambiamos el cable de entrada y ponemos un **`0`**.
    
2. **Disparo (`2º Flanco de CLK`):** Se ejecuta el pasamano simultáneo:
    
    - `FF4` copia el valor viejo de `C` (`0`) $\rightarrow$ **`D` queda en `0`**.
        
    - `FF3` copia el valor viejo de `B` (`0`) $\rightarrow$ **`C` queda en `0`**.
        
    - `FF2` copia el valor viejo de `A` (`1`) $\rightarrow$ **`B` pasa a `1`** _(nuestro primer bit dio un paso a la derecha)_.
        
    - `FF1` copia el nuevo bit de la entrada (`0`) $\rightarrow$ **`A` pasa a `0`**.
        

- **Estado actual de las salidas:** **`A = 0`** | **`B = 1`** | `C = 0` | `D = 0`
    

### Paso 3: Tercer bit (Entra un `1`)

1. **Preparación:** Ponemos un **`1`** en el cable de entrada.
    
2. **Disparo (`3º Flanco de CLK`):**
    
    - `FF4` copia el valor viejo de `C` (`0`) $\rightarrow$ **`D` queda en `0`**.
        
    - `FF3` copia el valor viejo de `B` (`1`) $\rightarrow$ **`C` pasa a `1`**.
        
    - `FF2` copia el valor viejo de `A` (`0`) $\rightarrow$ **`B` pasa a `0`**.
        
    - `FF1` copia el nuevo bit de la entrada (`1`) $\rightarrow$ **`A` pasa a `1`**.
        

- **Estado actual de las salidas:** **`A = 1`** | **`B = 0`** | **`C = 1`** | `D = 0`
    

### Paso 4: Cuarto bit (Entra un `1`)

1. **Preparación:** Ponemos el último **`1`** en el cable de entrada.
    
2. **Disparo (`4º Flanco de CLK`):**
    
    - `FF4` copia el valor viejo de `C` (`1`) $\rightarrow$ **`D` pasa a `1`** _(el primer bit que metimos en el Paso 1 finalmente llegó al último casillero)_.
        
    - `FF3` copia el valor viejo de `B` (`0`) $\rightarrow$ **`C` pasa a `0`**.
        
    - `FF2` copia el valor viejo de `A` (`1`) $\rightarrow$ **`B` pasa a `1`**.
        
    - `FF1` copia el nuevo bit de la entrada (`1`) $\rightarrow$ **`A` pasa a `1`**.
        

- **Estado actual de las salidas:** **`A = 1`** | **`B = 1`** | **`C = 0`** | **`D = 1`**
    

> [!NOTE] ¿Qué pasa si damos un 5º pulso de reloj metiendo un `0` (como en la diapositiva)?
> 
> - El `1` que estaba en **`D`** es empujado hacia afuera del registro (se pierde si nadie lo lee, o sale como dato en serie).
>     
> - Todo se corre un lugar más: `A=0`, `B=1`, `C=1`, `D=0`.
>     

## 4. Tabla de Seguimiento Temporal (Resumen Visual)

En la tabla se ve claramente el efecto de "desplazamiento": cada bit que entra por la izquierda va **bajando en diagonal hacia la derecha** en cada golpe de reloj:

|**Instante**|**Bit en Entrada (D de FF1)**|**Salida A (FF1)**|**Salida B (FF2)**|**Salida C (FF3)**|**Salida D (FF4)**|**Qué sucedió**|
|---|---|---|---|---|---|---|
|**Inicio (`CLR`)**|-|`0`|`0`|`0`|`0`|Se vacía el registro.|
|**Pulso 1 `CLK`**|**1** _(1º bit)_|**1**|`0`|`0`|`0`|Entra el 1º bit a `A`.|
|**Pulso 2 `CLK`**|**0** _(2º bit)_|**0**|**1**|`0`|`0`|El 1º bit pasa a `B`; entra el 2º a `A`.|
|**Pulso 3 `CLK`**|**1** _(3º bit)_|**1**|**0**|**1**|`0`|Avanzan a `B` y `C`; entra el 3º a `A`.|
|**Pulso 4 `CLK`**|**1** _(4º bit)_|**1**|**1**|**0**|**1**|**Registro lleno:** Los 4 bits están cargados.|
|**Pulso 5 `CLK`**|**0** _(Nuevo)_|**0**|**1**|**1**|**0**|El 1º bit (`1`) sale por `D` y entra un `0` a `A`.|


osea lo que hago es que entran por donde esta el 0, el biestable ff1 lo copia y lo pasa a A
en la segunda vuelta el A sale, pasa por el flip flop y se guarda en b, mientras que pasa el nuevo dato pasa por FF1

![[Pasted image 20261001201356.png]]

![[Pasted image 20261001201434.png]]

![[Pasted image 20261001201524.png]]

![[Pasted image 20261001201544.png]]

![[Pasted image 20261001201602.png]]

![[Pasted image 20261001201630.png]]

![[Pasted image 20261001201934.png]]

![[Pasted image 20261001202833.png]]

![[Pasted image 20261001202930.png]]