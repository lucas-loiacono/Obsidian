
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


Este circuito es una evolución del anterior: es un **Registro de Desplazamiento con Carga en Paralelo y Rotación Circular (Anillo)**. Aunque a primera vista parece un lío de cables, en realidad combina tres ideas que ya vimos por separado:


### 1. ¿Por qué usa Flip-Flops J-K en vez de D?

En el diagrama anterior usábamos Flip-Flops tipo D ("copiadores"). Acá el profesor armó esos mismos "copiadores" usando **Flip-Flops J-K**:

  

- Fijate que de cada biestable salen **dos cables** hacia la derecha: la salida normal **`Q`** va conectada a la entrada **`J`** del vecino, y la salida negada **`$\overline{Q}$`** va conectada a la entrada **`K`** del vecino.
    
      
    
- Como **`Q`** y **`$\overline{Q}$`** siempre tienen valores opuestos, al vecino siempre le llega `(J=1, K=0)` o `(J=0, K=1)`. Es decir, ¡se comportan exactamente igual que un Flip-Flop D copiando el dato de la izquierda!
    
      
    

### 2. La novedad de arriba: Carga en Paralelo (Las llaves `A, B, C, D`)

En el registro anterior, para meter 4 bits tenías que empujarlos de a uno por la izquierda esperando 4 pulsos de reloj.

  

Acá agregaron 4 interruptores (llaves) arriba a la izquierda rotulados en azul como **`A`, `B`, `C`, `D`** que viajan directo a la patita **`PS` (Preset)** de cada biestable:

  

- Como vimos antes, **`CLEAR` (`CLR`)** y **`PRESET` (`PS`)** son entradas **asincrónicas** (los "jefes absolutos" que actúan al instante sin esperar al reloj).
    
      
    
- **Paso 1:** Primero tirás un pulso por **`CLEAR`** abajo para poner los 4 casilleros en `0`.
    
      
    
- **Paso 2:** Si querés cargar el número `0 0 1 1` de un solo golpe (como se ve en la imagen donde `C` y `D` están prendidos en celeste), simplemente cerrás las llaves **`C`** y **`D`** arriba a la izquierda. Esos cables activan el `PS` (Preset) del 3er y 4to biestable y los clavan en `1` instantáneamente, sin haber gastado ni un solo pulso de reloj (`CLK`).
    
      
    
- Una vez cargado el número inicial, abrís las llaves para que dejen de forzar a los biestables y el circuito pueda empezar a moverse con el reloj.
    
      
    

### 3. Los cables largos que dan la vuelta: Rotación en Anillo

Fijate qué pasa con el último biestable de la derecha (el de la salida `D`):

  

- En vez de que sus datos se caigan al vacío cuando avanzan, su salida **`Q`** da toda la vuelta por arriba y se enchufa en la entrada **`J`** del primer biestable.
    
      
    
- Y su salida negada **$\overline{Q}$** da toda la vuelta por abajo y se enchufa en la entrada **`K`** del primer biestable.
    
      
    

**¿Qué logra esto?** Una **calesita (registro en anillo)**. Como no hay una puerta de entrada externa para meter bits nuevos en serie, los 4 bits que cargaste al principio con las llaves giran en círculo:

  

Supongamos que cargaste con las llaves el estado de la foto (**`A=0, B=0, C=1, D=1`**):

  

1. **1º Pulso de `CLK`:** Todo se corre un lugar a la derecha, y el `1` que estaba al final en **`D`** da la vuelta por el cable largo y se mete en **`A`**. Ahora tenés: **`A=1, B=0, C=0, D=1`**.
    
      
    
2. **2º Pulso de `CLK`:** El nuevo `1` de **`D`** da la vuelta y entra a **`A`**, empujando al resto. Ahora tenés: **`A=1, B=1, C=0, D=0`**.
    
      
    
3. **3º Pulso de `CLK`:** El `0` de **`D`** da la vuelta a **`A`**. Queda: **`A=0, B=1, C=1, D=0`**.
    
      
    
4. **4º Pulso de `CLK`:** Vuelve exactamente a la foto original: **`A=0, B=0, C=1, D=1`**.
    
      
    

### ¿Para qué sirve este circuito?

Tiene dos usos principales:

  

1. **Conversor Paralelo a Serie (PISO):** Cargás los 4 bits todos juntos de golpe por arriba usando las llaves (`A, B, C, D`), y después, en cada pulso de `CLK`, los vas sacando en fila india de a uno mirando únicamente el cable final **`D`** (como indica el texto rojo de abajo). Es lo que hace tu computadora para mandar un dato interno hacia afuera por un cable USB.
    
      
    
2. **Secuenciador cíclico:** Al tener el cable realimentado dando la vuelta, los bits nunca se pierden; quedan girando infinitamente con cada golpe de reloj (ideal para hacer secuencias de luces, motores paso a paso o repartir turnos cíclicos).
    
      
    

¿Te quedó claro cómo las llaves de arriba meten el dato de prepo usando el Preset (`PS`) antes de empezar a girar?



  

En el primer circuito tenías una sola puertita a la izquierda y estabas obligado a meter los bits de a uno esperando al reloj (entrada en serie). En cambio, acá **no tenés entrada en serie** porque ese primer biestable tiene sus patas `J` y `K` ocupadas recibiendo los cables que dan la vuelta desde el final.

  

Así que la mecánica de este circuito es tal cual la dijiste:

  

1. **Limpieza:** Le das un toque al **`CLEAR`** de abajo para que los 4 casilleros arranquen en `0`.
    
      
    
2. **Carga directa ("de prepo"):** Tenés los 4 cables de arriba a la izquierda (`A, B, C, D`) conectados a los **`PS` (Preset)** de cada biestable. Cerrás las llaves de los bits que querés que valgan `1` (en el dibujo cerraron `C` y `D`) y ¡pum!, se clavan adentro de los casilleros instantáneamente sin esperar ningún pulso de reloj.
    
      
    
3. **Soltás las llaves y activás el `CLK`:** Una vez que ya "estampaste" tu número fijo adentro del circuito con el Preset, abrís esas llaves para que dejen de forzar a los biestables y empezás a darle pulsos al `CLK`.
    
      
    
4. **El desplazamiento:** Con cada golpe de reloj, esos 4 bits que ya estaban adentro empiezan a correrse hacia la derecha (y el último de la derecha da la vuelta por los cables largos para volver a entrar por el primero).
    
      
    

En resumen: en el anterior los datos entraban caminando en fila india con el reloj; en este caen todos juntos "en paracaídas" desde arriba gracias al Preset, y el reloj solo se encarga de moverlos una vez que ya están adentro.

abcd pongo los 1 que quiero  y clear pongo el 0, seria primero clear y despues las compuertas de abcd que quiero

  


![[Pasted image 20261001201524.png]]

![[Pasted image 20261001201544.png]]


# Registro de Desplazamiento con Carga Paralela Asincrónica (`Load`)
#organizacion-del-computador #fiuba #electronica-digital #secuenciales #registros

---

## 1. ¿Qué problema resuelve este circuito?

En un registro de desplazamiento básico con llaves manuales conectadas únicamente a `Preset`, las llaves solo tienen la capacidad de escribir unos (`1`)[cite: 10]. Eso obliga a realizar **dos pasos manuales** cada vez que se quiere cargar un número nuevo:
1. Activar una línea general de `CLEAR` para vaciar todo el registro a `0000`[cite: 10].
2. Cerrar las llaves correspondientes para forzar los `1` mediante `Preset`[cite: 10].

Este circuito automatiza el proceso mediante una línea de control llamada **`Load` (Cargar)** y un juego de compuertas lógicas en cada etapa. Permite **sobreescribir cualquier número de 4 bits (`Ent. A, B, C, D`) en un único paso instantáneo**, forzando simultáneamente un `Preset` en los casilleros que deben valer `1` y un `Clear` en los casilleros que deben valer `0`, sin caer jamás en el estado prohibido[cite: 8, 11, 12].

---

## 2. Anatomía del Circuito (Bloque por Bloque)

El registro está formado por 4 Flip-Flops tipo D (`FF1`, `FF2`, `FF3`, `FF4`) conectados en cascada para el desplazamiento serie, más una red de carga paralela individual para cada biestable:

### A) Pines Asincrónicos Activos en Bajo ($\overline{PR}$ y $\overline{CLR}$)
En el símbolo de cada Flip-Flop, tanto **`PR` (Preset)** arriba como **`CLR` (Clear)** abajo tienen una **barra de negación encima** ($\overline{PR}$ y $\overline{CLR}$) y un circulito en la entrada del bloque:
* **Si reciben un `1`:** Están **INACTIVOS** (apagados). No interfieren con el Flip-Flop.
* **Si reciben un `0`:** Se **ACTIVAN** inmediatamente sin esperar al reloj (`Clock`):
  * $\overline{PR} = 0 \rightarrow$ Fuerza la salida `Q` a **`1`** (Set asincrónico).
  * $\overline{CLR} = 0 \rightarrow$ Fuerza la salida `Q` a **`0`** (Reset asincrónico).
  * $\overline{PR} = 0$ y $\overline{CLR} = 0$ a la vez $\rightarrow$ **Estado Prohibido** (nunca debe ocurrir).

### B) Compuertas NAND de Control y el Inversor (NOT)
Como $\overline{PR}$ y $\overline{CLR}$ se activan con un **`0`**, se utilizan **compuertas NAND** para controlarlos. 
> Recordatorio de tabla de verdad NAND: **Solo devuelve un `0` cuando TODAS sus entradas valen `1`**. Si alguna entrada es `0`, la NAND devuelve un `1` (dejando el pin inactivo).

Cada entrada paralela (`Ent. A`, `Ent. B`, `Ent. C`, `Ent. D`) se bifurca en dos caminos dentro de su propio Flip-Flop:
1. **Camino Superior (hacia $\overline{PR}$):** Entra a una compuerta NAND junto con el cable `Load`.
2. **Camino Inferior (hacia $\overline{CLR}$):** Pasa primero por un **inversor (compuerta NOT)** y luego entra a la compuerta NAND inferior junto con el cable `Load`.

```text
                  Load ──┬──────────────────┐
                         │                  ├──[ NAND ]──> a /PR (Arriba)
    Ent. A (Bit) ────────┼──┬───────────────┘
                         │  │
                         │  └──[ >o NOT ]───┐
                         │                  ├──[ NAND ]──> a /CLR (Abajo)
                         └──────────────────┘
````

_¿Para qué sirve ese inversor (NOT) abajo?_ Garantiza que el camino de arriba y el de abajo **siempre reciban valores opuestos** de la entrada. Así es físicamente imposible que un mismo Flip-Flop active su `Preset` y su `Clear` al mismo tiempo.

## 3. Funcionamiento Paso a Paso: Los Dos Modos de Operación

El circuito entero obedece a la orden del cable **`Load`**:

### MODO 1: Carga en Paralelo (`Load = 1`)

Cuando querés estampar de golpe un número de 4 bits desde las entradas inferiores (`Ent. A, B, C, D`), ponés **`Load = 1`**. Esto "habilita" todas las compuertas NAND del circuito.

Supongamos que queremos cargar el número **`1 0 1 0`** (`Ent. A = 1`, `Ent. B = 0`, `Ent. C = 1`, `Ent. D = 0`):

#### ¿Qué pasa en los casilleros donde pusiste un `1` (`FF1` y `FF3`)?

1. **`Ent. A = 1`** y **`Load = 1`**.
    
2. **NAND Superior ($\overline{PR}$):** Recibe `1` (de `Load`) y `1` (de `Ent. A`). Como tiene `(1, 1)`, su salida cae a **`0`**.
    
    - Ese `0` entra a $\overline{PR}$ y **activa el Preset**.
        
3. **NAND Inferior ($\overline{CLR}$):** El `1` de `Ent. A` atraviesa el inversor (NOT) y se convierte en **`0`**. La NAND inferior recibe `1` (de `Load`) y `0` (del inversor). Al tener `(1, 0)`, su salida se mantiene en **`1`**.
    
    - Ese `1` entra a $\overline{CLR}$ y **mantiene el Clear apagado**.
        
4. **Resultado instantáneo:** `FF1` (y `FF3`) clavan su salida `Q` en **`1`** sin esperar al reloj.
    

#### ¿Qué pasa en los casilleros donde pusiste un `0` (`FF2` y `FF4`)?

1. **`Ent. B = 0`** y **`Load = 1`**.
    
2. **NAND Superior ($\overline{PR}$):** Recibe `1` (de `Load`) y `0` (de `Ent. B`). Al tener `(1, 0)`, su salida se mantiene en **`1`**.
    
    - Ese `1` entra a $\overline{PR}$ y **mantiene el Preset apagado**.
        
3. **NAND Inferior ($\overline{CLR}$):** El `0` de `Ent. B` atraviesa el inversor (NOT) y se convierte en **`1`**. La NAND inferior recibe `1` (de `Load`) y `1` (del inversor). Como tiene `(1, 1)`, su salida cae a **`0`**.
    
    - Ese `0` entra a $\overline{CLR}$ y **activa el Clear**.
        
4. **Resultado instantáneo:** `FF2` (y `FF4`) clavan su salida `Q` en **`0`** sin esperar al reloj.
    

> [!SUCCESS] Resultado de poner `Load = 1`
> 
> En el mismo instante, `FF1` y `FF3` hicieron **Preset** (`1`), mientras que `FF2` y `FF4` hicieron **Clear** (`0`). El número `1010` quedó guardado adentro del registro en un solo paso, pisando cualquier dato viejo que hubiera antes.

### MODO 2: Desplazamiento Sincrónico (`Load = 0`)

Una vez que el dato ya entró, para poder moverlo con el reloj primero debés apagar la carga poniendo **`Load = 0`**.

1. **Bloqueo de las NAND:** Al poner `Load = 0`, todas las compuertas NAND (tanto las de arriba como las de abajo de los 4 Flip-Flops) reciben un **`0`** en una de sus patas[cite: 11, 12].
    
2. **Desactivación Asincrónica:** Cualquier NAND que recibe un `0` devuelve obligatoriamente un **`1`** en su salida (sin importar qué haya en `Ent. A, B, C, D`)[cite: 11, 12].
    
3. Como todos los pines $\overline{PR}$ y $\overline{CLR}$ reciben un **`1`**, **todos quedan completamente desactivados**.
    
4. **Habilitación del Reloj (`Clock`) y Serie (`Serial IN`):**
    
    - Ahora los Flip-Flops quedan libres para escuchar la línea **`Clock`** (sincronizada por flanco ascendente)[cite: 11, 12].
        
    - Con cada pulso de `Clock`, se produce el "pasamano" clásico de izquierda a derecha: `FF1` lee lo que venga por **`Serial IN`**, `FF2` copia a `FF1`, `FF3` copia a `FF2`, `FF4` copia a `FF3`, y los bits van saliendo en fila india por **`Salida serial`**[cite: 11, 12].
        

## 4. Tabla de Verdad del Bloque de Carga (Resumen Rápido)

|**Señal Load**|**Entrada Paralela (Ent. X)**|**Salida NAND Arriba (PR)**|**Salida NAND Abajo (CLR)**|**Acción en el Flip-Flop**|
|---|---|---|---|---|
|**`0`**|`X` _(No importa)_|**`1`** _(Inactivo)_|**`1`** _(Inactivo)_|**Modo Normal:** Obedece al `Clock` y desplaza en serie[cite: 11, 12].|
|**`1`**|**`1`**|**`0` (ACTIVO)**|**`1`** _(Inactivo)_|**Preset Asincrónico:** Clava el Flip-Flop en **`1`**[cite: 11, 12].|
|**`1`**|**`0`**|**`1`** _(Inactivo)_|**`0` (ACTIVO)**|**Clear Asincrónico:** Clava el Flip-Flop en **`0`**[cite: 11, 12].|


### MODO 2: Carga Normal en Serie por `Serial IN` (`Load = 0`)

Se usa cuando no querés usar las entradas de abajo, sino que querés **cargar datos en fila india desde el cable `Serial IN`** (izquierda) y desplazarlos pulso a pulso con el **`Clock`**.

#### Paso A: Cómo se "apagan" las compuertas de arriba y abajo

1. Ponés el cable **`Load = 0`**.
    
2. Todas las compuertas NAND (las 4 de arriba y las 4 de abajo) reciben un **`0`** fijo en una de sus entradas.
    
3. Por ley de compuertas NAND, cualquier cosa multiplicada por `0` y negada da **`1`**. Por lo tanto, **las 8 compuertas NAND clavan sus salidas en `1`**, sin importar qué valores haya en `Ent. A, B, C, D`.
    
4. Como todos los pines $\overline{PR}$ y $\overline{CLR}$ reciben un `1`, **quedan todos 100% inactivos**. A partir de este momento, es como si toda la red de compuertas NAND e inversores desapareciera del dibujo.
    

#### Paso B: Carga paso a paso por `Serial IN` (Pasamano Sincrónico)

Con `Load = 0`, los Flip-Flops solo escuchan su entrada **`D`** y el flanco ascendente del **`Clock`**. Supongamos que el registro está en `0000` y queremos cargar la secuencia **`1`, `0`, `1`, `1`** metiéndola por **`Serial IN`**:

- **1º Pulso de `Clock` (Ponés un `1` en `Serial IN`):**
    
    - `FF1` lee su entrada `D` (`Serial IN`) y guarda ese **`1`** en su salida `Q1`.
        
    - Los demás copian los ceros viejos de sus vecinos.
        
    - **Estado interno (`FF1` a `FF4`):** **`1`** - `0` - `0` - `0`.
        
- **2º Pulso de `Clock` (Ponés un `0` en `Serial IN`):**
    
    - El `1` que estaba en `FF1` salta a `FF2`.
        
    - Al mismo tiempo, `FF1` lee el nuevo **`0`** de `Serial IN` y lo guarda.
        
    - **Estado interno (`FF1` a `FF4`):** **`0`** - **`1`** - `0` - `0`.
        
- **3º Pulso de `Clock` (Ponés un `1` en `Serial IN`):**
    
    - El dato de `FF2` (`1`) pasa a `FF3`; el de `FF1` (`0`) pasa a `FF2`.
        
    - `FF1` guarda el nuevo **`1`** que entró por `Serial IN`.
        
    - **Estado interno (`FF1` a `FF4`):** **`1`** - **`0`** - **`1`** - `0`.
        
- **4º Pulso de `Clock` (Ponés un `1` en `Serial IN`):**
    
    - Todo da un paso más a la derecha y entra el último **`1`** a `FF1`.
        
    - **Estado interno (`FF1` a `FF4`):** **`1`** - **`1`** - **`0`** - **`1`** _(¡Los 4 bits ya quedaron cargados en serie y el primer bit ya asoma por **`Salida serial`**!)_.
        
- **Pulsos siguientes (5º, 6º, 7º...):**
    
    - A medida que sigas metiendo bits nuevos por `Serial IN`, los bits viejos seguirán empujándose hacia la derecha y saliendo uno por uno por **`Salida serial`** en cada golpe de reloj.

![[Pasted image 20261001201602.png]]

Aunque el título de la diapositiva sigue diciendo "Registro de Desplazamiento" por estar dentro del mismo tema, fijate en un detalle clave: **¡los Flip-Flops NO están conectados entre sí!** La salida `Q` de uno no va al `D` del vecino, sino que sube directo hacia afuera.

Es literalmente un **Registro de Memoria común y corriente** (como los registros internos del procesador: `AX`, `BX`, etc.).

### ¿Cómo pensarlo mentalmente?

Es una **cámara fotográfica de 4 bits**:

1. **Preparás los datos abajo (`Entrada de datos`):** Ponés los 4 bits que querés guardar en las patitas de abajo (`PD`, `PC`, `PB`, `PA`). Cada cable viaja directo a la entrada **`D`** de su propio Flip-Flop.
    
2. **Antes del `Clock`:** Aunque cambies los números de abajo mil veces, arriba en la `Salida de datos` (`QD`, `QC`, `QB`, `QA`) no cambia absolutamente nada.
    
3. **Disparo del `Clock` (1 solo pulso):** Como los 4 biestables comparten el mismo cable de `Clock`, cuando llega el pulso de reloj, **los 4 Flip-Flops copian su entrada al mismo tiempo**:
    
    - `FFA` copia `PD` y lo muestra en `QD`.
        
    - `FFB` copia `PC` y lo muestra en `QC`.
        
    - `FFC` copia `PB` y lo muestra en `QB`.
        
    - `FFD` copia `PA` y lo muestra en `QA`.
        
4. **Retención (Memoria):** Una vez que pasó el pulso de `Clock`, los 4 bits quedan "congelados" y disponibles arriba en `QD, QC, QB, QA` para que el resto de la computadora los lea tranquila, sin importar qué pase después en los cables de entrada de abajo.

![[Pasted image 20261001201630.png]]

![[Pasted image 20261001201934.png]]

![[Pasted image 20261001202833.png]]

### 1. La fórmula del recuadro: $M \le 2^N$ ("Estados" vs "Biestables")

Esta fórmula te responde la primera pregunta que te tenés que hacer al leer un ejercicio de parcial: **"¿Cuántos Flip-Flops ($N$) necesito dibujar para que entren todos los estados ($M$) que me piden?"**.

- **$N$ (Cantidad de Biestables / Flip-Flops):** Es la cantidad de bits que va a tener tu circuito. Cada Flip-Flop guarda 1 bit (`0` o `1`).
    
- **$2^N$ (Capacidad máxima):** Es la cantidad total de combinaciones binarias distintas que podés armar con $N$ Flip-Flops. (Por ejemplo, con $N=3$ Flip-Flops podés armar $2^3 = 8$ combinaciones: desde `000` hasta `111`).
    
- **$M$ (Módulo o Cantidad de Estados útiles):** Es la cantidad de pasos o números por los que realmente querés que cuente tu circuito antes de reiniciar.


![[Pasted image 20261010173119.png]]


![[Pasted image 20261010173328.png]]


# Modelos de Sistemas Secuenciales Sincrónicos: Modelo de Moore
#organizacion-del-computador #fiuba #electronica-digital #secuenciales #moore #mealy

---

## 1. Concepto General: ¿Por qué un sistema secuencial tiene "Memoria"?

A diferencia de un circuito combinacional puro (donde la salida depende únicamente de lo que estás apretando en este instante), en un **Sistema Secuencial** la salida actual depende de las entradas actuales **y de toda la historia pasada** de entradas[cite: 9, 10]:

$$Y_t = f(X_t, X_{t-1}, \dots, X_0)$$
[cite: 9, 10]

Como es físicamente imposible guardar infinitas señales del pasado, el circuito resume toda esa historia previa en un valor binario llamado **Estado Actual ($E_t$)**, el cual se almacena adentro de un bloque de **Memoria (`M`)** formado por Flip-Flops[cite: 9, 10].

---

## 2. Diccionario de Variables y Subíndices

En las ecuaciones de estado, el subíndice indica el **momento del tiempo** respecto al pulso del reloj (`clk`):
* **Subíndice $t$ (Presente):** Lo que está ocurriendo en el ciclo de reloj actual[cite: 9, 10].
* **Subíndice $t+1$ (Futuro):** Lo que va a ocurrir inmediatamente después del próximo flanco de reloj (`clk`)[cite: 9, 10].

| Símbolo | Nombre Técnico | ¿Qué es físicamente en el circuito? |
| :---: | :--- | :--- |
| **$X_t$** | **Entrada Actual** | Los cables o botones externos que manipulás desde afuera en este momento (ej. interruptor para contar hacia arriba o hacia abajo)[cite: 9, 10]. |
| **$E_t$** | **Estado Actual** | El número binario guardado **hoy** adentro de los Flip-Flops (se lee en las patitas de salida **`Q`** de la memoria)[cite: 9, 10]. |
| **$E_{t+1}$** | **Estado Siguiente** | El nuevo número que la lógica preparó y dejó esperando en las entradas (`D`, `J/K` o `T`) de los Flip-Flops para guardarse cuando suene el próximo `clk`. |
| **$Y_t$** | **Salida Actual** | El resultado final que el circuito muestra hacia el exterior (ej. un LED indicador de paridad)[cite: 9, 10]. |

---

## 3. Arquitectura Física: Las 3 Cajas (`G`, `M` y `H`)

Todo sistema secuencial sincrónico se divide en tres bloques conectados en serie, donde **`S.L.C.`** significa *Sistema Lógico Combinacional* (compuertas `AND`, `OR`, `NOT`, `XOR` sin reloj):

```text
           CAJA "G"                        CAJA "M"                   CAJA "H"
    (S.L.C. de Entrada)                   (Memoria)              (S.L.C. de Salida)
  ┌──────────────────────┐               ┌──────────┐           ┌──────────────────┐
  │                      │     Et+1      │          │    Et     │                  │    Yt
──► Xt                   ├──────────────►│          ├──────┬───►│                  ├────►
  │   Et+1 = G(Xt, Et)   │               │    M     │      │    │    Yt = H(Et)    │
┌─► Et                   │               │   / \    │      │    │                  │
│ └──────────────────────┘               └───┴─┴────┘      │    └──────────────────┘
│                                             ▲            │
│                                             │ clk        │
└─────────────────────────────────────────────┼────────────┘
          Realimentación del Estado Actual (Et)
````

### 1) Caja `G` (Preparar qué guardar en la memoria)

- **Qué es:** El grupo de compuertas lógicas conectadas **adelante** de los Flip-Flops (en sus entradas de excitación `D`, `J/K` o `T`). En los ejercicios, estas compuertas salen de resolver los Mapas de Karnaugh.
    
- **Qué hace:** Recibe la entrada externa ($X_t$) y un cable de realimentación con el estado actual ($E_t$). Con ambos datos calcula cuál debe ser el próximo estado ($E_{t+1}$).
    

### 2) Caja `M` (Guardar el estado)

- **Qué es:** El conjunto de **Flip-Flops** sincronizados por flanco mediante la señal de reloj (`clk`).
    
- **Qué hace:** Mantiene congelado el estado actual ($E_t$) en su salida. Cuando llega el flanco del `clk`, captura el valor que estaba esperando en su puerta ($E_{t+1}$) y lo convierte en el nuevo estado actual ($E_t$).
    

### 3) Caja `H` (Calcular y mostrar el resultado final)

- **Qué es:** El grupo de compuertas lógicas conectadas **atrás** de los Flip-Flops (tomando las salidas `Q`).
    
- **Qué hace:** Toma el estado actual guardado en la memoria ($E_t$), lo procesa (por ejemplo, pasándolo por una compuerta `XOR` para evaluar paridad) y genera la salida final del circuito ($Y_t$).
    

## 4. Las Dos Ecuaciones del Modelo de Moore

En el **Modelo de Moore**, el comportamiento del circuito queda definido por dos funciones:

### A) Ecuación de Transición de Estados (Caja `G`)

$$E_{t+1} = G(X_t, E_t)$$

- _Lectura:_ "El próximo estado a guardar ($E_{t+1}$) depende tanto de la entrada externa actual ($X_t$) como del estado en el que estoy parado hoy ($E_t$)".
    

### B) Ecuación de Salida (Caja `H`) — ¡La clave de Moore!

$$Y_t = H(E_t)$$

- _Lectura:_ "La salida final ($Y_t$) depende **ÚNICAMENTE del Estado Actual ($E_t$)** guardado en los Flip-Flops".
    
- _Detalle visual en el plano:_ A la caja `H` **solo le entran cables que vienen de la memoria `M` ($E_t$)**. No existe ningún cable directo que puentee la entrada $X_t$ hacia la caja `H`.

# Preguntas

## Yo
osea yo siempre guardo por bloques, no uno a uno, por eso me fijo el estado actual completo

## Gemini 

¡Tal cual! Le diste en el clavo a la lógica del diseño sincrónico.

En el diagrama de Moore (o de Mealy), esa flecha única llamada **$E_t$** en realidad representa un **paquete de cables que viajan juntos** (un bus de datos), donde cada cable es la salida `Q` de uno de tus Flip-Flops.

Por eso se trabaja siempre **por bloques completos** y no mirando un Flip-Flop aislado:

1. **El Estado Actual ($E_t$) es el bloque entero hoy:** Si tenés 3 Flip-Flops, vos no decís _"el Flip-Flop 1 vale 0"_; mirás la foto completa de los tres juntos, por ejemplo **`011`** (el estado 3).
    
2. **Para decidir el futuro ($E_{t+1}$), `G` necesita ver la foto completa:** Imaginate que un Flip-Flop quiere saber si en el próximo pulso de reloj tiene que cambiar a `1` o a `0`. No puede decidirlo mirándose solo a sí mismo; necesita saber qué tienen guardado sus compañeros para saber en qué número de la cuenta está parado el circuito entero. Por eso el bloque completo $E_t$ vuelve hacia atrás y entra a la caja `G`.
    
3. **Se guarda todo el bloque de un solo golpe:** Cuando la caja `G` termina de calcular el bloque siguiente ($E_{t+1}$, por ejemplo **`100`**) y suena el `clk`, los 3 Flip-Flops actualizan sus bits al mismo tiempo (como en el registro PIPO de la cuarta foto que me mostraste).
    
4. **La salida ($Y_t$) también mira el bloque completo:** La caja `H` del final agarra los 3 cables de $E_t$ al mismo tiempo (por ejemplo, para meterlos en la compuerta XOR y ver si el bloque entero tiene paridad par o impar).
    

Pensarlo así como **"entra un bloque viejo $\rightarrow$ las compuertas calculan el bloque nuevo $\rightarrow$ el reloj guarda el bloque nuevo de un saque"** te va a hacer muchísimo más fácil armar las tablas de verdad de los ejercicios de la guía.

## Yo
ah osea seria como una actualizacion, ya que si necesito mirar a mi Et para ver que cambios hago, no es que le paso datos nuevos sin verlo
## Gemini

¡Exactamente! Le diste la definición perfecta: **es una actualización sobre lo que ya tenés, no un reemplazo a ciegas.**

Si lo pensás como cuando programás, la diferencia entre un registro común y un sistema secuencial con realimentación (como los contadores) es esta:

- **Reemplazo a ciegas (El registro PIPO de la Foto 4):** Es como hacer `estado = dato_nuevo;`. A los Flip-Flops no les importa qué tenían guardado antes; simplemente pisan el valor viejo con lo que venga de afuera.
    
- **Actualización mirando a $E_t$ (El diagrama de Moore/Mealy):** Es como hacer `estado = estado + 1;` (o `estado_futuro = G(estado_actual, entrada);`). Para poder hacer ese `+ 1`, el circuito **está obligado a leer primero cuánto vale `estado` hoy ($E_t$)**, meterlo en la licuadora de compuertas `G` junto con la orden externa ($X_t$), y recién ahí guardar el resultado actualizado ($E_{t+1}$) cuando suena el reloj.
    

Por eso en el diagrama ves ese **cable largo por abajo que sale de la derecha de `M` y vuelve a meterse por la izquierda de `G`**: ese cable es literalmente el circuito "mirándose al espejo" para saber en qué estado está hoy ($E_t$) y decidir cómo actualizarse en el próximo pulso.

## Yo

y cuando estoy en Yt muestro el estado viejo o el nuevo?

## Gemini
Mostrás el **estado actual ($E_t$)**, es decir, el que ya está guardado adentro de la memoria `M` en este momento (lo que vos llamás el "viejo"). **Todavía NO muestra el estado nuevo ($E_{t+1}$)**.

Mirá el dibujo del Modelo de Moore (la segunda imagen de las cajas):

- El **estado nuevo ($E_{t+1}$)** recién salió de la caja `G` y está **frenado en la puerta de entrada** de la memoria `M`, esperando a que suene el próximo golpe de reloj (`clk`).
    
- La caja **`H`** (que calcula la salida $Y_t$) está conectada **del lado derecho de la memoria `M`**, recibiendo únicamente el cable **$E_t$**.
    

### Pensalo como dos momentos separados por el golpe del reloj (`clk`):

1. **Mientras estás en el pulso actual (Tiempo $t$):**
    
    - Adentro de la memoria `M` está guardado el estado actual **$E_t$** (por ejemplo, el número `2`).
        
    - La salida **$Y_t$** mira ese `2` que está en la memoria y te muestra el resultado correspondiente al `2` ($Y_t = H(E_t)$).
        
    - Mientras tanto, atrás en la puerta de la memoria, la caja `G` ya dejó preparado el número nuevo **$E_{t+1}$** (el `3`), pero **todavía no pudo pasar** porque no sonó el reloj.
        
2. **Recién cuando suena el próximo flanco del `clk` (Pasás al Tiempo $t+1$):**
    
    - La memoria `M` abre la puerta un instante, deja entrar al `3` ($E_{t+1}$) y pisa al `2`.
        
    - Ahora el `3` pasa a ser el nuevo dueño de la memoria, sale hacia la derecha, y recién en ese momento la caja **`H`** lo ve y actualiza la salida **$Y$**.
        

La caja de salida `H` nunca puede "espiar" a $E_{t+1}$ antes de tiempo porque la memoria `M` hace de pared en el medio hasta que suene el `clk`

## Yo

osea solo cambia cuando activo el clk, y siempre se muestra y esta trabajando, ya que este no depende del clk

## Gemini

Es tal cual lo decís por dos razones:

1. **Las cajas `G` y `H` trabajan las 24 horas en vivo (no tienen `clk`):** Como son simples compuertas lógicas (`AND`, `OR`, `XOR`), no tienen reloj ni botón de pausa. Están encendidas todo el tiempo calculando y mostrando en vivo lo que tienen conectado a sus entradas.
    
2. **La única que tiene un "portón con llave" (`clk`) es la Memoria `M`:**
    
    - Como `H` está conectada a la salida de `M` ($E_t$), `H` está mostrando permanentemente ese resultado hacia afuera ($Y_t$).
        
    - Pero como el número guardado en `M` ($E_t$) está congelado y **solo puede cambiar en el instante en que activás el `clk`**, el resultado que muestra `H` ($Y_t$) también queda fijo y **solo cambia cuando activás el `clk`** y entra el estado nuevo.
        

(Y lo mismo pasa del lado izquierdo con `G`: `G` ya calculó el próximo estado $E_{t+1}$ al toque y lo tiene ahí empujando contra la puerta de `M`, pero hasta que vos no actives el `clk`, ese dato nuevo no puede entrar a la memoria).

### El único caso donde la salida cambia SIN esperar al `clk`: **Mealy**

Ya que entendiste tan bien que la caja `H` trabaja todo el tiempo en vivo sin depender del `clk`, mirá qué fácil se entiende ahora qué pasa en el **Modelo de Mealy** (que es como el de Moore, pero tirando un cable directo desde la entrada $X_t$ hacia la caja `H`):

- En **Moore** (el que analizamos recién), aunque muevas el interruptor de entrada $X_t$ mil veces, la salida $Y_t$ ni se entera hasta que no suene el `clk`, porque el cambio quedó frenado en la puerta de la memoria `M`.
    
- En **Mealy**, como la entrada $X_t$ tiene un cable "VIP" que esquiva la memoria `M` y se mete directo en la caja `H`, y `H` trabaja todo el tiempo sin esperar al `clk`, **si vos cambiás la entrada $X_t$, la salida $Y_t$ cambia en el acto (en vivo), aunque no hayas activado el `clk`**.

![[Pasted image 20261010182032.png]]

![[Pasted image 20261010182846.png]]



# Modelos de Sistemas Secuenciales Sincrónicos: Modelo de Mealy
#organizacion-del-computador #fiuba #electronica-digital #secuenciales #mealy #moore

---

## 1. ¿Qué es el Modelo de Mealy y en qué se diferencia de Moore?

Al igual que en el Modelo de Moore, un circuito secuencial de **Mealy** utiliza un bloque de **Memoria (`M`)** formado por Flip-Flops para recordar el estado actual ($E_t$)[cite: 6, 7] y calcular a qué estado debe actualizarse en el próximo golpe de reloj ($E_{t+1}$)[cite: 6, 7].

La gran diferencia radica en **cómo se calcula la salida final ($Y_t$)**:
* **En Moore:** La salida mira **solamente** lo que está guardado fijo en la memoria ($E_t$). Por lo tanto, la salida solo puede cambiar cuando suena el reloj (`clk`).
* **En Mealy:** La salida mira lo que está guardado en la memoria ($E_t$) **Y TAMBIÉN espía en vivo la entrada externa ($X_t$)** sin pasar por la memoria.

$$\text{Ecuación de Transición de Estados (Caja G): } E_{t+1} = G(X_t, E_t)$$

$$\text{Ecuación de Salida (Caja H — ¡Clave de Mealy!): } Y_t = H(X_t, E_t)$$


> [!WARNING] Fe de erratas de la Diapositiva 7 de la cátedra
> Adentro del rectángulo del diagrama de la cátedra quedó escrito por error de tipeo $Y_t = H(E_t)$. La ecuación real que corresponde a ese bloque y que figura en el título superior es **$Y_t = H(X_t, E_t)$**.

---

## 2. Arquitectura Física: ¿Por qué `G` y `H` aparecen juntas?

En la diapositiva de la cátedra, las funciones combinacionales **`G`** (preparar el próximo estado) y **`H`** (calcular la salida) aparecen metidas adentro de una misma caja grande (`S.L.C.`) a la izquierda de la memoria `M`:

```text
                CAJA "G" y "H" Unificadas
                    (S.L.C. General)
            ┌──────────────────────────────┐
            │        G            H        │      Camino directo (Sin bloqueo de clk)
            │                              ├──────────────────────────────────────────► Salida (Yt)
Entrada ───►│ Xt                           │
 (Xt)       │       Yt = H(Xt, Et)         │                CAJA "M" (Memoria)
            │     Et+1 = G(Xt, Et)         │     Et+1      ┌──────────────────┐   Et
        ┌──►│ Et                           ├──────────────►│        M         ├───────┐
        │   └──────────────────────────────┘               │       / \        │       │
        │                                                  └───────┴─┴────────┘       │
        │                                                           ▲                 │
        │                                                           │ clk             │
        └───────────────────────────────────────────────────────────┼─────────────────┘
                           Realimentación del Estado Actual (Et)
````

  

### ¿Cómo se entiende esta arquitectura separando los roles?

Aunque el profesor las dibuje en una sola caja porque **ambas funciones reciben exactamente los mismos dos cables de entrada ($X_t$ y $E_t$)**, internamente siguen siendo dos circuitos de compuertas con tareas distintas:

  

1. **El circuito de `G` (Preparar la actualización de la memoria):**
    
      
    - Recibe el bloque de estado actual ($E_t$) y la entrada externa ($X_t$).
        
          
        
    - Calcula el próximo bloque de estado ($E_{t+1}$) y lo deja esperando en la puerta de la memoria **`M`**. Este dato **no puede pasar** hasta que suene el flanco del `clk`.
        
          
        
2. **El circuito de `H` (Mostrar el resultado combinando Memoria + Entrada en vivo):**
    
      
    - También recibe el estado fijo de la memoria ($E_t$), pero además **tiene un cable directo desde la entrada $X_t$ que esquiva a la memoria `M`** (la flecha larga superior del dibujo)[cite: 7].
        
          
        
    - Como las compuertas de `H` no tienen `clk` y trabajan las 24 horas en vivo, **cualquier cambio que hagas en la entrada $X_t$ viaja por esa flecha superior y actualiza la salida $Y_t$ de forma instantánea**, sin esperar al pulso de reloj.
        
          
        

## 3. Analogía Práctica: El "Día Fijo en Memoria" vs. "Datos en Vivo por $X_t$"

Para entender por qué es útil guardar una base fija en `M` ($E_t$) y al mismo tiempo mandar cambios en vivo por $X_t$, pensá en el ejemplo que armamos: **querer mantener fijo el día de hoy en memoria, pero seguir mostrando variantes en vivo en la pantalla**.

  

Imaginate una pantalla de precios de un cine o estacionamiento:

  

1. **Lo que guardás en la Memoria `M` ($E_t$ — La constante temporal):**
    
      
    - Querés que el sistema sepa qué día de la semana es hoy (ej. `Martes`).
        
          
        
    - Ese dato se guarda en los Flip-Flops de **`M`**[cite: 7]. Queda congelado durante las 24 horas y **solo se actualiza cuando suena el `clk`** a la medianoche (ahí la función `G` mira que hoy era `Martes`, calcula $E_{t+1} = \text{Miércoles}$ y el `clk` actualiza la memoria).
        
          
        
2. **Lo que mandás por la Entrada Externa ($X_t$ — La señal en vivo):**
    
      
    - Mientras el día sigue clavado en `Martes` adentro de la memoria `M`, vos querés seguir interactuando con el circuito en tiempo real sin cambiar de día (por ejemplo, tocando un botón $X_t$ para indicar si el cliente que tenés enfrente tiene `1 = Descuento` o `0 = Tarifa Normal`).
        
          
        
3. **Lo que muestra la Salida ($Y_t = H(X_t, E_t)$):**
    
      
    - La función **`H`** toma la constante que está guardada hoy en la memoria (`Martes` en $E_t$) y la mezcla en vivo con lo que le estás mandando por **`Xt`**[cite: 7].
        
          
        
    - **Resultado:** Sin necesidad de activar el `clk` (el día guardado en `M` sigue siendo `Martes`), cada vez que vos cambias $X_t$ de `0` a `1`, la salida $Y_t$ reacciona en el acto mostrando _"Martes - Precio Normal"_ o _"Martes - Precio con Descuento"_.
        
          
        

## 4. El Tamaño de los Cables: ¿$X_t$ y $E_t$ son siempre bloques?

- **El Estado ($E_t$ y $E_{t+1}$) SIEMPRE se maneja como un bloque:** Si tu memoria `M` tiene $N$ Flip-Flops, $E_t$ y $E_{t+1}$ son obligatoriamente un paquete (bus) de **$N$ bits** que se leen y se actualizan todos juntos en cada pulso de `clk` (ej. un bloque de 3 bits `Q2 Q1 Q0`).
    
      
    
- **La Entrada ($X_t$) y la Salida ($Y_t$) son independientes del tamaño de la memoria:**
    
      
    - Pueden ser un **bloque de varios cables** ($X_0 \dots X_m$) si tenés varios botones externos.
        
          
        
    - O pueden ser **1 solo cable individual (1 bit)**, que es el caso más común en la Guía 3 (por ejemplo, en el **Ejercicio 3.35**, donde $E_t$ es un bloque de **3 bits**, pero la entrada $X_t$ es de **1 solo bit** que elige entre contar hacia arriba o hacia abajo, y la salida $Y_t$ es de **1 solo bit** que prende el LED de paridad).
        
          
        

## 5. Cuadro Comparativo Definitivo: Moore vs. Mealy (Para los ejercicios 3.33 a 3.35)

| **Característica**                                     | **Modelo de MOORE PNG**                                                                                    | **Modelo de MEALY[cite: 7]**                                                                                         |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Ecuación de Próximo Estado (`G`)**                   | $E_{t+1} = G(X_t, E_t)$                                                                                    | $E_{t+1} = G(X_t, E_t)$<br><br>  <br><br>[cite: 7]                                                                   |
| **Ecuación de Salida (`H`)**                           | **$Y_t = H(E_t)$** _(Solo mira la memoria)_<br><br>  <br><br>[cite: 6]                                     | **$Y_t = H(X_t, E_t)$** _(Mira memoria + entrada)_<br><br>  <br><br>[cite: 7]                                        |
| **¿Qué cables entran a la compuerta de salida final?** | Únicamente las salidas `Q` de los Flip-Flops ($E_t$).                                                      | Las salidas `Q` de los Flip-Flops ($E_t$) **y también** el cable de entrada externa ($X_t$).                         |
| **¿Cuándo cambia la salida $Y_t$?**                    | **Solo cuando suena el `clk`** (porque depende 100% de la memoria `M`).                                    | Cambia cuando suena el `clk`, **pero también cambia en vivo** si alguien modifica la entrada $X_t$.                  |
| **¿Cómo se dibuja el Diagrama de Estados (Globos)?**   | La salida se anota **adentro del círculo del estado** (`Estado / Salida`), porque es fija para ese estado. | La salida se anota **arriba de la flecha de transición** (`Entrada / Salida`), porque depende de qué entrada toques. |
| **Ejercicios de la Guía 3**                            | **Ej. 3.33 y 3.34:** La compuerta XOR de paridad solo conecta los 3 Flip-Flops (`Q2 ⊕ Q1 ⊕ Q0`).           | **Ej. 3.35:** A la compuerta XOR de paridad le sumás el cable de entrada $X_t$ (`Q2 ⊕ Q1 ⊕ Q0 ⊕ X`).                 |

![[Pasted image 20261010183750.png]]

![[Pasted image 20261010184330.png]]

![[Pasted image 20261010184636.png]]

![[Pasted image 20261010185631.png]]

![[Pasted image 20261010185751.png]]

![[Pasted image 20261010185923.png]]