
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

Esta diapositiva es oro puro porque el profesor agarró las **3 cajas teóricas (`G`, `M`, `H`)** de las que veníamos hablando y las **pintó con colores arriba de un circuito real** (este es el estilo de ejercicio que te piden analizar en el punto **3.26** de la guía).

En un circuito real los cables están todos mezclados, pero gracias a los tres colores se ve clarísimo qué es cada cosa:

---

### 1. Color Turquesa / Celeste: El Bloque `"M"` (La Memoria)

Son los **3 Flip-Flops tipo JK**.

* Sus salidas actuales son **$Q_2$, $Q_1$ y $Q_0$** (esos 3 bits juntos forman tu bloque de estado actual **$E_t$**).


* Fijate que los tres tienen conectado el mismo cable **`clk`** abajo, por lo que es un sistema **sincrónico** (los tres actualizan su estado al mismo tiempo cuando pega el reloj).



---

### 2. Color Verde: El Bloque `"G"` (Prepara la actualización de la memoria)

Fijate dónde están parados los tres recuadros verdes: **justo a la izquierda (adelante) de las patitas `J` y `K` de cada Flip-Flop**.

Su trabajo es mezclar la entrada externa **`X`** con los cables que vuelven de las salidas **`Q` / `Q'**` para decidir qué reciben `J` y `K` antes del próximo pulso de reloj. Si seguís los cables de cada caja verde, salen las ecuaciones del recuadro verde de abajo:

* **Caja verde del Flip-Flop 0 (Derecha):** Las patitas $J_0$ y $K_0$ están unidas y conectadas a una flecha que apunta hacia arriba (eso en electrónica significa conectado directo a voltaje positivo, o sea un **`1` fijo**).


* Ecuación: **$J_0 = 1$** y **$K_0 = 1$** (en cada pulso de reloj, este Flip-Flop invierte su valor).




* **Caja verde del Flip-Flop 1 (Centro):** Tiene dos compuertas AND sumadas en una OR que alimentan tanto a $J_1$ como a $K_1$.


* A la AND de arriba le entran el cable **`X`** y el cable **$Q_0$** $\rightarrow Q_0 \cdot X$.


* A la AND de abajo le entran el cable **`X` negado** ($X'$) y el cable **$Q_0'$** $\rightarrow Q_0' \cdot X'$.


* La OR las suma: **$J_1 = K_1 = Q_0 X + Q_0' X'$**.




* **Caja verde del Flip-Flop 2 (Izquierda):** Hace lo mismo pero con compuertas AND de 3 patitas:


* La AND de arriba junta **$Q_0$, $Q_1$ y $X$**.


* La AND de abajo junta **$Q_0'$, $Q_1'$ y $X'$**.


* La OR las suma: **$J_2 = K_2 = Q_0 Q_1 X + Q_0' Q_1' X'$**.





---

### 3. Color Amarillo: El Bloque `"H"` (Muestra el resultado final $Y$)

Son las tres cajitas amarillas donde nacen las salidas finales del circuito (**$Y_2$, $Y_1$, $Y_0$**).

Mirá el recuadro amarillo de abajo a la izquierda para ver cómo se calcula cada salida:

* **$Y_2 = Q_2 \oplus Q_1$:** Es la compuerta **XOR** amarilla de arriba, que conecta las salidas $Q_2$ y $Q_1$.


* **$Y_1 = Q_1'$:** Es un cable directo conectado a la patita negada $Q'$ del Flip-Flop del medio (sin ninguna compuerta extra).


* **$Y_0 = Q_0$:** Es un cable directo conectado a la salida $Q_0$ del último Flip-Flop.



---

### La pregunta del millón: ¿Por qué sabemos al instante que esto es Modelo de MOORE?

Mirá las 3 ecuaciones amarillas del bloque `"H"`:


$$Y_2 = Q_2 \oplus Q_1$$

$$Y_1 = Q_1'$$

$$Y_0 = Q_0$$

¿Aparece la letra **`X`** (la entrada externa) en alguna de las fórmulas amarillas? ¡No! Ninguna caja amarilla tiene enchufado el cable `X`.

Como las salidas $Y_2, Y_1, Y_0$ se calculan mirando **únicamente el estado actual guardado en los Flip-Flops ($Q_2, Q_1, Q_0$)**, se cumple a rajatabla que **$Y_t = H(E_t)$**, o sea, es 100% **Modelo de Moore**.

(Si esa compuerta XOR amarilla de arriba tuviera una patita conectada al cable `X`, ahí aparecería la `X` en la fórmula amarilla y pasaría a ser Modelo de Mealy).

¿Viste qué claro queda cuando separás lo que entra a `J/K` (verde = `G`) de lo que sale hacia `Y` (amarillo = `H`)? ¿Tenés la diapositiva que sigue donde arman la tabla de este circuito?


![[Pasted image 20261010184330.png]]

![[Pasted image 20261010184636.png]]

# Análisis Práctico de un Sistema Secuencial: Ejemplo Modelo de Moore
#organizacion-del-computador #fiuba #electronica-digital #secuenciales #moore #analisis

---

## 1. Identificación de los 3 Bloques en el Circuito (`M`, `G` y `H`)

Al analizar un circuito secuencial ya dibujado (como pide el **Ejercicio 3.26** de la guía), el primer paso es separar visualmente las tres partes de la arquitectura[cite: 6]:

### A) Bloque `"M"` (Memoria — Color Celeste)
* **Qué es:** Son los **3 Flip-Flops tipo JK** conectados al mismo cable de reloj (`clk`)[cite: 6].
* **Qué guarda:** Sus salidas actuales ($Q_2, Q_1, Q_0$) forman el paquete o bloque de 3 bits llamado **Estado Actual ($E_t$)**[cite: 4, 6, 10]. Como hay $N = 3$ Flip-Flops, existen $2^3 = 8$ estados posibles (del `000` al `111`, bautizados desde `E0` hasta `E7`)[cite: 2, 10, 11].

### B) Bloque `"G"` (Lógica de Entrada / Transición — Color Verde)
* **Qué es:** Son las compuertas lógicas (`AND`, `OR`, `NOT`) conectadas **adelante** de las patitas `J` y `K` de cada Flip-Flop[cite: 6].
* **Ecuaciones de excitación (extraídas siguiendo los cables del dibujo):**
  * **Flip-Flop 0:** $J_0 = 1 \quad \vert{} \quad K_0 = 1$ *(Conectados fijo a positivo)*[cite: 6, 10]
  * **Flip-Flop 1:** $J_1 = Q_0 X + Q_0' X' \quad \vert{} \quad K_1 = Q_0 X + Q_0' X'$[cite: 6, 10]
  * **Flip-Flop 2:** $J_2 = Q_0 Q_1 X + Q_0' Q_1' X' \quad \vert{} \quad K_2 = Q_0 Q_1 X + Q_0' Q_1' X'$[cite: 6, 10]

### C) Bloque `"H"` (Lógica de Salida — Color Amarillo)
* **Qué es:** Son las conexiones y compuertas que están **al final** de los Flip-Flops para generar las 3 salidas del circuito ($Y_2, Y_1, Y_0$)[cite: 6, 11].
* **Ecuaciones de salida:**
  * $Y_2 = Q_2 \oplus Q_1$[cite: 6, 11]
  * $Y_1 = Q_1'$[cite: 6, 11]
  * $Y_0 = Q_0$[cite: 6, 11]
* **¿Por qué confirma que es Modelo de Moore?:** Porque en ninguna de las tres fórmulas amarillas aparece la entrada externa **`X`**[cite: 6, 11]. La salida depende exclusivamente del estado actual guardado en los Flip-Flops ($Y_t = H(E_t)$)[cite: 4, 6].

---

## 2. El Rol de la Entrada `X`: ¿Por qué evaluamos `X = 0` y `X = 1`?

Una duda muy común al ver la **Tabla de Estados** es: *¿Por qué hay 16 filas si solo existen 8 estados (`000` al `111`)?*[cite: 10, 11]

### La Entrada `X` como "Palanca de Cambios"
* **`X` NO es el dato que se guarda directamente en la memoria** (fijate que `X` es un solo cable de 1 bit, mientras que la memoria guarda un bloque de 3 bits)[cite: 6, 10].
* **`X` es una orden o condición externa** (como un volante o un `if / else`) que le dice a la función `G` **hacia qué lado debe actualizar el estado actual** cuando suene el próximo pulso de reloj[cite: 4, 10].
* Como las fórmulas verdes de $J_1, K_1, J_2, K_2$ tienen la letra **`X`** adentro de la cuenta[cite: 6, 10], el circuito va a tomar **dos caminos diferentes** desde un mismo estado según cuánto valga `X`[cite: 10, 11]:
  * **Tu Estado Actual ($Q_2, Q_1, Q_0$):** Te dice **en qué escalón estás parado hoy**[cite: 10].
  * **Tu Entrada (`X`):** Decide si en el próximo golpe de reloj vas a **subir un escalón (`X = 1`)** o **bajar un escalón (`X = 0`)**[cite: 10, 11].
  * **Tu Estado Futuro ($Q_2^+, Q_1^+, Q_0^+$):** Es el **nuevo escalón que se va a guardar en la memoria** cuando suene el `clk` ($E_{t+1} = G(X_t, E_t)$)[cite: 4, 10].

Por eso, en la Tabla de Estados cada uno de los 8 estados aparece **repetido dos veces**: una fila para calcular qué pasa si el usuario pone **`X = 0`**, y otra fila abajo para calcular qué pasa si pone **`X = 1`** ($8 \text{ estados} \times 2 \text{ opciones de } X = 16 \text{ filas}$)[cite: 10].

---

## 3. Cómo se arma la Tabla de Estados (El cálculo de $Q_2^+, Q_1^+, Q_0^+$)

Para completar las últimas tres columnas (**Estado Futuro**)[cite: 10], no alcanza con mirar cuánto dieron $J$ y $K$. Tenés que aplicar la orden que dan $J$ y $K$ sobre el bit que ya tenías en el **Estado Actual ($Q$)**, usando la regla del Flip-Flop JK:

> [!TIP] Machete de actualización del Flip-Flop JK
> * Si **$J = 0, K = 0$ $\rightarrow$ NO CAMBIA (Memoria):** El bit futuro ($Q^+$) copia exactamente el mismo valor que tenía en el Estado Actual ($Q$).
> * Si **$J = 1, K = 1$ $\rightarrow$ INVIERTE (Complementa):** El bit futuro ($Q^+$) pasa a valer lo contrario de lo que tenía en el Estado Actual ($Q$) (si era `0` pasa a `1`; si era `1` pasa a `0`).
> * *(Si $J=1, K=0$ pone un `1` fijo; si $J=0, K=1$ pone un `0` fijo).*

### Ejemplo paso a paso con las primeras filas de la tabla:

| Estado Actual ($Q_2 Q_1 Q_0$) | Entrada ($X$) | Entradas FF2 ($J_2 K_2$) | Entradas FF1 ($J_1 K_1$) | Entradas FF0 ($J_0 K_0$) | Estado Futuro ($Q_2^+ Q_1^+ Q_0^+$) | Explicación de la actualización ($E_t \rightarrow E_{t+1}$) |
| :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **`0 0 0`** (`E0`) | **`0`** | `1 1` | `1 1` | `1 1` | **`1 1 1`** (`E7`) | Como los tres FF reciben `1 1` (invertir)[cite: 10], los tres ceros del estado actual `000` se dan vuelta y pasan a **`111`**[cite: 10, 11]. *(Con $X=0$ retrocede del 0 al 7)*. |
| **`0 0 0`** (`E0`) | **`1`** | `0 0` | `0 0` | `1 1` | **`0 0 1`** (`E1`) | $Q_2$ y $Q_1$ reciben `0 0` (no cambian, siguen en `0`)[cite: 10]. Solo $Q_0$ recibe `1 1` (invierte su `0` a `1`)[cite: 10]. Resultado: **`001`**[cite: 10, 11]. *(Con $X=1$ avanza del 0 al 1)*. |
| **`0 0 1`** (`E1`) | **`0`** | `0 0` | `0 0` | `1 1` | **`0 0 0`** (`E0`) | $Q_2$ y $Q_1$ reciben `0 0` (siguen en `0`)[cite: 10]. $Q_0$ estaba en `1` y recibe `1 1` (invierte su `1` a `0`)[cite: 10]. Resultado: **`000`**[cite: 10, 11]. *(Con $X=0$ retrocede del 1 al 0)*. |
| **`0 0 1`** (`E1`) | **`1`** | `0 0` | `1 1` | `1 1` | **`0 1 0`** (`E2`) | $Q_2$ recibe `0 0` (sigue en `0`)[cite: 10]. $Q_1$ estaba en `0` y recibe `1 1` (pasa a `1`)[cite: 10]. $Q_0$ estaba en `1` y recibe `1 1` (pasa a `0`)[cite: 10]. Resultado: **`010`**[cite: 10, 11]. *(Con $X=1$ avanza del 1 al 2)*. |

---

## 4. Tabla de Salidas y Diagrama de Estados (El Gráfico de Globos)

En la Diapositiva 10 se resume todo el comportamiento del circuito en una tabla chiquita y en el gráfico de globos (**Diagrama de Estados**)[cite: 11]:

### A) ¿Cómo se lee cada Globo (Círculo)?
Cada círculo es uno de los 8 estados posibles de la memoria (`E0` = `000`, `E1` = `001`, ..., `E7` = `111`)[cite: 11]. Adentro del globo se escribe una "fracción" propia del **Modelo de Moore**:

$$\frac{\text{Nombre del Estado Actual } (E_t)}{\text{Salida fija en ese estado } (Y_2 Y_1 Y_0)}$$

* **Ejemplo en el globo `E0` (`000`):** Arriba dice **`E0`** y abajo dice **`010`**[cite: 11].
* ¿De dónde sale ese `010` de abajo? De reemplazar $Q_2=0, Q_1=0, Q_0=0$ en las ecuaciones amarillas del bloque `H`[cite: 11]:
  * $Y_2 = 0 \oplus 0 = \mathbf{0}$[cite: 11]
  * $Y_1 = 0' = \mathbf{1}$[cite: 11]
  * $Y_0 = \mathbf{0}$[cite: 11]
* Como es **Moore**, mientras el circuito esté parado en `E0`, la salida muestra siempre `010` sin importar si afuera tocás `X`[cite: 4, 11].

### B) ¿Cómo se leen las Flechas Azules (`1`) y Rojas (`0`)?
Las flechas representan las filas de la **Tabla de Estados** y te muestran cómo salta el circuito de un globo a otro cuando suena el `clk`, dependiendo de cuánto valga la entrada **`X`**[cite: 10, 11]:

* **Flechas Azules (tienen un `1` al lado):** Indican el camino que sigue el circuito cuando mantenés la entrada **`X = 1`**[cite: 11].
  * Si seguís las flechas azules en el dibujo, giran en sentido horario sumando de a uno: `E0` $\rightarrow$ `E1` $\rightarrow$ `E2` $\rightarrow$ `E3` $\rightarrow$ `E4` $\rightarrow$ `E5` $\rightarrow$ `E6` $\rightarrow$ `E7` $\rightarrow$ `E0` *(Contador Ascendente)*[cite: 11].
* **Flechas Rojas (tienen un `0` al lado):** Indican el camino que sigue el circuito cuando mantenés la entrada **`X = 0`**[cite: 11].
  * Si seguís las flechas rojas, giran en sentido antihorario restando de a uno: `E0` $\rightarrow$ `E7` $\rightarrow$ `E6` $\rightarrow$ `E5` $\rightarrow$ `E4` $\rightarrow$ `E3` $\rightarrow$ `E2` $\rightarrow$ `E1` $\rightarrow$ `E0` *(Contador Descendente)*[cite: 11].



**¡Exactamente eso!** La clave para no marearse es dividir el dibujo en **dos tandas de flechas**, separando las filas donde la entrada **`X = 0`** de las filas donde la entrada **`X = 1`**.

  

Si lo hacés con este método mecánico en un examen, sale rápido y sin errores:

  

### Paso 1: Dibujás los 8 globos vacíos de flechas

Primero ponés en la hoja los 8 círculos (`E0` hasta `E7`) con su salida escrita adentro (que sacaste de la Tabla de Salidas).

  

### Paso 2: Tanda de flechas para `X = 0` (Las filas pares / Flechas rojas)

Agarrás tu Tabla de Estados y **mirás solamente las filas donde la columna `X` vale `0`**. Por cada una de esas 8 filas, dibujás una flecha con un **`0`** encima que une el **Estado Actual** con su **Estado Futuro**:

  

- **En `E0` (`000`) con `X = 0`** $\rightarrow$ el Estado Futuro dio `111` (`E7`). _(Dibujás flecha con `0` de `E0` a `E7`)_.
    
      
    
- **En `E1` (`001`) con `X = 0`** $\rightarrow$ el Estado Futuro dio `000` (`E0`). _(Dibujás flecha con `0` de `E1` a `E0`)_.
    
      
    
- **En `E2` (`010`) con `X = 0`** $\rightarrow$ el Estado Futuro dio `001` (`E1`). _(Dibujás flecha con `0` de `E2` a `E1`)_.
    
      
    
- ...y así completás las 8 flechas del caso `X = 0`.
    
      
    

### Paso 3: Tanda de flechas para `X = 1` (Las filas impares / Flechas azules)

Ahora hacés lo mismo, pero **mirando solamente las filas de la tabla donde la columna `X` vale `1`**. Por cada una, dibujás una flecha con un **`1`** encima:

  

- **En `E0` (`000`) con `X = 1`** $\rightarrow$ el Estado Futuro dio `001` (`E1`). _(Dibujás flecha con `1` de `E0` a `E1`)_.
    
      
    
- **En `E1` (`001`) con `X = 1`** $\rightarrow$ el Estado Futuro dio `010` (`E2`). _(Dibujás flecha con `1` de `E1` a `E2`)_.
    
      
    
- **En `E2` (`010`) con `X = 1`** $\rightarrow$ el Estado Futuro dio `011` (`E3`). _(Dibujás flecha con `1` de `E2` a `E3`)_.
    
      
    
- ...y así completás las 8 flechas del caso `X = 1`.
    
      
    

### El control de calidad antes de entregar:

Cuando terminás de dibujar las dos tandas, te fijás en cada globo individual: **¿de cada globo salen exactamente una flecha con un `0` y una flecha con un `1`?** Si la respuesta es sí, pasaste toda la tabla al gráfico sin olvidarte de ninguna fila.

  

¿Querés que veamos las diapositivas que siguen donde seguro hacen el ejemplo de **Mealy**, o ya nos tiramos a hacer un ejercicio de la guía?

![[Pasted image 20261010185631.png]]

![[Pasted image 20261010185751.png]]

![[Pasted image 20261010185923.png]]


# Análisis Práctico de un Sistema Secuencial: Ejemplo Modelo de Mealy
#organizacion-del-computador #fiuba #electronica-digital #secuenciales #mealy #analisis

---

## 1. Identificación de los 3 Bloques en el Circuito (`M`, `G` y `H`)

Al analizar el circuito de la Diapositiva 11, separamos las tres etapas fundamentales de la arquitectura[cite: 8]:

### A) Bloque `"M"` (Memoria — Color Celeste)
* **Cantidad de bits:** Tiene **2 Flip-Flops** conectados al mismo reloj (`clk`)[cite: 8]. Sus salidas ($Q_1, Q_0$) forman un paquete de 2 bits para el **Estado Actual ($E_t$)**, lo que nos da $2^2 = \mathbf{4\text{ estados posibles}}$ (`00`, `01`, `10`, `11`)[cite: 9, 10].
* **Particularidad (Mezcla de tipos de Flip-Flop):**
  * El Flip-Flop 1 (izquierda, bit más significativo $Q_1$) es de **tipo JK**[cite: 8].
  * El Flip-Flop 0 (derecha, bit menos significativo $Q_0$) es de **tipo D**[cite: 8].

### B) Bloque `"G"` (Lógica de Transición / Entrada — Color Verde)
* **Qué hace:** Son las compuertas ubicadas adelante de las entradas de los Flip-Flops ($J_1, K_1$ y $D_0$)[cite: 8]. Preparan la orden de actualización esperando al próximo pulso de `clk`[cite: 1, 8].
* **Ecuaciones de excitación:**
  * $J_1 = Q_0 X'$[cite: 8, 9, 10]
  * $K_1 = Q_0 + X$[cite: 8, 9, 10]
  * $D_0 = X' Q_0'$[cite: 8, 9, 10]

### C) Bloque `"H"` (Lógica de Salida — Color Amarillo)
* **Qué hace:** Son las 3 compuertas `AND` sumadas en una `OR` en la parte superior que generan la única salida **`Y`**[cite: 8].
* **Ecuación de salida:**
  $$Y = Q_1 X + Q_0 X + Q_1 Q_0$$
[cite: 8, 9, 10]
* **¿Por qué confirma que es Modelo de Mealy?:** Porque el cable de entrada externa **`X`** sube directamente (sin pasar por los Flip-Flops) y se mete adentro de la caja amarilla[cite: 8]. En la ecuación de `Y` están combinados el Estado Actual ($Q_1, Q_0$) y la Entrada Externa ($X$), cumpliendo $Y_t = H(X_t, E_t)$[cite: 1, 8].

---

## 2. Regla de Oro: ¿La Salida `Y` depende del Estado Actual o del Estado Futuro?

> [!IMPORTANT] La salida SIEMPRE depende del Estado Actual ($E_t$)
> Tanto en Moore como en Mealy, la salida **`Y` se calcula SIEMPRE usando el Estado Actual ($Q_1, Q_0$)** y **NUNCA el Estado Futuro ($Q_1^+, Q_0^+$)**[cite: 1, 9, 10].
> 
> * **Razón física:** La caja amarilla (`H`) está enchufada a las salidas actuales `Q` de la memoria[cite: 8]. El Estado Futuro todavía está frenado en la puerta de entrada de los Flip-Flops esperando a que suene el `clk`[cite: 1, 8].
> * **Cómo no confundirse en la tabla:** Aunque la columna `Salida (Y)` esté dibujada al final de todo (a la derecha de `Estado futuro`)[cite: 9, 10], para calcular `Y` tenés que tapar las columnas del medio y reemplazar en la ecuación amarilla usando **únicamente las primeras tres columnas de la fila ($Q_1, Q_0$ y $X$)**[cite: 9, 10].

---

## 3. Cómo se arma la Tabla Unificada en Mealy (Diapositiva 12)

Como tenemos 2 bits de Estado Actual ($Q_1, Q_0$) y 1 bit de Entrada ($X$), la tabla tiene $2^3 = \mathbf{8\text{ filas}}$ (los 4 estados evaluados tanto con $X = 0$ como con $X = 1$)[cite: 9, 10].

### A) ¿Por qué la columna `Salida (Y)` está adentro de esta tabla y no en una tabla aparte?
* En **Moore**, cada estado tenía una única salida fija, por lo que alcanzaba con una tablita aparte de 1 fila por estado[cite: 4, 7].
* En **Mealy**, como `Y` depende también de `X`[cite: 1, 8], **un mismo estado puede mostrar una salida distinta según si `X = 0` o `X = 1`**[cite: 9, 10].
  * *Ejemplo en el estado `01` (Filas 3 y 4):* Estando parado en `01`, si ponés `X = 0` la salida da **`Y = 0`**; pero si cambiás a `X = 1` (sin que suene el reloj), la salida cambia en vivo a **`Y = 1`**[cite: 9, 10].

### B) Cálculo del Estado Futuro mezclando Flip-Flop JK y Flip-Flop D
* **Para $Q_1^+$ (Flip-Flop JK):** Mirás cómo estaba $Q_1$ al principio de la fila y aplicás la orden de $J_1, K_1$[cite: 8, 9]:
  * `0 0` $\rightarrow$ No cambia (copia a $Q_1$).
  * `0 1` $\rightarrow$ Reset (pone un `0` fijo).
  * `1 0` $\rightarrow$ Set (pone un `1` fijo).
  * `1 1` $\rightarrow$ Invierte (da vuelta el valor de $Q_1$).
* **Para $Q_0^+$ (Flip-Flop D):** ¡Es directo! El Flip-Flop D simplemente guarda lo que tiene en su entrada $D$ cuando suena el reloj. Por lo tanto, **la columna $Q_0^+$ es una copia exacta de la columna $D_0$** ($Q_0^+ = D_0$)[cite: 8, 9].

### Tabla completa explicada fila por fila:

| Estado Actual ($Q_1 Q_0$) | Entrada ($X$) | FF1 ($J_1 K_1$) | FF0 ($D_0$) | Estado Futuro ($Q_1^+ Q_0^+$) | Salida ($Y$) | Explicación del cálculo |
| :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **`0 0`** | **`0`** | `0 0` | `1` | **`0 1`** | **`0`** | $Q_1$ no cambia (`00` $\rightarrow$ sigue `0`). $Q_0^+$ copia a $D_0=1$[cite: 9]. Salida con $Q_1=0, Q_0=0, X=0 \rightarrow Y=0$[cite: 9]. |
| **`0 0`** | **`1`** | `0 1` | `0` | **`0 0`** | **`0`** | $Q_1$ se pone en `0` (`01`). $Q_0^+$ copia a $D_0=0$[cite: 9]. Salida con $Q_1=0, Q_0=0, X=1 \rightarrow Y=0$[cite: 9]. |
| **`0 1`** | **`0`** | `1 1` | `0` | **`1 0`** | **`0`** | $Q_1$ estaba en `0` y recibe `11` (invierte a `1`). $Q_0^+$ copia a $D_0=0$[cite: 9]. Salida da $Y=0$[cite: 9]. |
| **`0 1`** | **`1`** | `0 1` | `0` | **`0 0`** | **`1`** | $Q_1$ recibe `01` (va a `0`). $Q_0^+$ copia $D_0=0$[cite: 9]. **Salida:** como $Q_0=1$ y $X=1$, el término $Q_0 X$ vale `1` $\rightarrow \mathbf{Y=1}$[cite: 9]. |
| **`1 0`** | **`0`** | `0 0` | `1` | **`1 1`** | **`0`** | $Q_1$ estaba en `1` y recibe `00` (no cambia, sigue `1`). $Q_0^+$ copia $D_0=1$[cite: 9]. Salida da $Y=0$[cite: 9]. |
| **`1 0`** | **`1`** | `0 1` | `0` | **`0 0`** | **`1`** | $Q_1$ recibe `01` (pasa a `0`). $Q_0^+$ copia $D_0=0$[cite: 9]. **Salida:** como $Q_1=1$ y $X=1$, el término $Q_1 X$ vale `1` $\rightarrow \mathbf{Y=1}$[cite: 9]. |
| **`1 1`** | **`0`** | `1 1` | `0` | **`0 0`** | **`1`** | $Q_1$ estaba en `1` y recibe `11` (invierte a `0`). $Q_0^+$ copia $D_0=0$[cite: 9]. **Salida:** como $Q_1=1, Q_0=1$, el término $Q_1 Q_0$ vale `1` $\rightarrow \mathbf{Y=1}$[cite: 9]. |
| **`1 1`** | **`1`** | `0 1` | `0` | **`0 0`** | **`1`** | $Q_1$ recibe `01` (pasa a `0`). $Q_0^+$ copia $D_0=0$[cite: 9]. Todos los términos de la ecuación amarilla dan `1` $\rightarrow \mathbf{Y=1}$[cite: 9]. |

---

## 4. Diagrama de Estados (El Gráfico de Globos en Mealy — Diapositiva 13)

Al pasar de Moore a Mealy, cambia la forma de anotar las salidas en el dibujo de globos[cite: 4, 7, 10]:

### A) ¿Qué va adentro de cada Globo?
* Se escribe **solamente el Estado Actual** (`00`, `01`, `10`, `11`), **sin línea de fracción ni salida adentro**[cite: 10].
* No se puede poner la salida adentro del círculo porque en un mismo globo (como `01` o `10`) la salida cambia según cuánto valga `X`[cite: 9, 10].

### B) ¿Qué significa el cartelito `X / Y` arriba de cada Flecha?
En Mealy, la salida se muda **arriba de las flechas de transición** con el formato[cite: 10]:
$$\text{Entrada } (X) \;/\; \text{Salida Actual } (Y)$$

* **Cómo se lee una flecha (Ej. Flecha de `01` $\rightarrow$ `00` con cartel `1/1`)[cite: 10]:**
  * **Dónde nace la flecha (`01`):** Estoy parado hoy en el Estado Actual `01`[cite: 9, 10].
  * **Primer número del cartel (`1/`):** Pongo la entrada externa en **`X = 1`**[cite: 9, 10].
  * **Segundo número del cartel (`/1`):** Mientras estoy en `01` con `X = 1`, el circuito me muestra en vivo la salida **`Y = 1`**[cite: 9, 10].
  * **A dónde apunta la flecha (`00`):** Cuando suene el próximo pulso de `clk`, la memoria va a saltar al Estado Futuro **`00`**[cite: 9, 10].
* **¿Qué es un rulo / bucle que vuelve al mismo globo? (Ej. en `00` con cartel `1/0`)[cite: 10]:**
  * Representa la Fila 2: si estás en `00` y ponés `X = 1`, la salida muestra `0` y el Estado Futuro vuelve a ser **`00`** (se queda en el mismo globo cuando suena el `clk`)[cite: 9, 10].

> [!WARNING] Fe de erratas del gráfico de la Diapositiva 13
> En el dibujo de la cátedra, abajo a la izquierda, la flecha con el cartel **`0/1`** fue dibujada por error con la punta apuntando desde `00` hacia `11`[cite: 10]. Mirando la Fila 7 de la tabla (`Estado actual = 11`, `X = 0` $\rightarrow$ `Estado futuro = 00`, `Salida = 1`), esa flecha **`0/1` nace en `11` y apunta hacia `00`** (igual que su compañera `1/1`)[cite: 9, 10].






# Dudas

Las diferencias exactas al momento de armar las **tablas** y los **gráficos (diagramas de estados)** entre el Modelo de Moore y el Modelo de Mealy se resumen en cómo y dónde se anota la **Salida ($Y$)**:

  

### 1. Diferencias al armar las TABLAS

La parte donde calculás las entradas de los Flip-Flops ($J, K, D$) y el **Estado Futuro ($Q^+$)** se hace **exactamente igual en los dos modelos**. Lo único que cambia es dónde ponés la columna de **Salida ($Y$)**:

  

- **En el Modelo de MOORE (Se hacen 2 tablas separadas):**
    
      
    1. **Tabla de Estados (Grande):** Tiene los Estados Actuales, la Entrada $X$, las entradas de los Flip-Flops y el Estado Futuro. _(Por ejemplo, para 3 Flip-Flops y 1 entrada $X$, tiene **16 filas**)_. **Acá NO se pone la salida $Y$**.
        
          
        
    2. **Tabla de Salidas (Chiquita aparte):** Como la salida solo depende del Estado Actual ($Q$) y no le importa cuánto vale $X$, hacés una tablita aparte donde ponés cada estado una sola vez (sin repetir) y su salida al lado _(para 3 Flip-Flops, tiene solo **8 filas**, de `E0` a `E7`)_.
        
          
        
- **En el Modelo de MEALY (Se hace 1 sola tabla todo-en-uno):**
    
      
    - **Tabla Unificada:** Como la salida $Y$ depende del Estado Actual **y también de la Entrada $X$**, para un mismo estado la salida puede cambiar si $X=0$ o si $X=1$. Por eso, **agregás la columna `Salida (Y)` al final de todo (a la derecha de `Estado futuro`)** dentro de la misma tabla grande, y la calculás fila por fila.
        
          
        

### 2. Diferencias al armar los GRÁFICOS (Diagramas de Estados)

En ambos modelos hay algo que **NO cambia nunca**:

  

- **La cantidad de círculos (globos)** es siempre igual a la cantidad de estados posibles ($2^{\text{cantidad de Flip-Flops}}$).
    
      
    
- **Las flechas SIEMPRE nacen en el `Estado Actual` y apuntan al `Estado Futuro`** de esa fila.
    
      
    

Lo que cambia en el dibujo es **dónde escribís la Salida ($Y$)**:

  

|**Elemento del Gráfico**|**En Modelo de MOORE JPG**|**En Modelo de MEALY JPG**|
|---|---|---|
|**¿Qué se escribe ADENTRO del círculo?**|Se divide al medio como una fracción: **Arriba el Estado y abajo la Salida fija**.<br><br>  <br>  <br><br>$$\frac{\text{Estado}}{\text{Salida } (Y)}$$<br><br>  <br><br>_(Ej: $\frac{E0}{010}$)_|**Solo el nombre o número del Estado** (sin raya de fracción y sin salida adentro).<br><br>  <br>  <br>  <br><br>_(Ej: `00`, `01`, `10`, `11`)_|
|**¿Qué se escribe ARRIBA de la flecha?**|**Solamente el valor de la Entrada ($X$)** que provoca ese salto.<br><br>  <br>  <br>  <br><br>_(Ej: ponés solo `0` o `1`)_|**La Entrada ($X$) y la Salida ($Y$) separadas por una barra**:<br><br>  <br>  <br><br>$$\text{Entrada } (X) \;/\; \text{Salida } (Y)$$<br><br>  <br><br>_(Ej: ponés `0/0`, `1/0`, `1/1`)_|

### Miralo lado a lado con un ejemplo de una sola fila:

Supongamos que tu tabla dice que en el **Estado Actual `01`**, cuando metés la **Entrada `X = 1`**, pasás al **Estado Futuro `00`** y la **Salida da `Y = 1`**:

  

- **Si estás dibujando MOORE:**
    
    Adentro del globo `01` ya tenés escrita la salida abajo (`01 / 1`). Y en la flecha que va hacia `00` escribís **solamente el `1`** (de $X=1$):
    
      
    
    Plaintext
    
    ```
     ( 01 / 1 ) ────── 1 ──────► ( 00 / 0 )
    ```
    
- **Si estás dibujando MEALY:** Adentro de los globos solo dice `01` y `00`. Y arriba de la flecha que va de `01` a `00` escribís **`1/1`** (el primer `1` es por $X=1$, y el segundo `1` es por $Y=1$):
    
      
    
    Plaintext
    
    ```
       ( 01 ) ────── 1 / 1 ────► ( 00 )
    ```
    

¿Te gustaría que hagamos juntos el **Ejercicio 3.26** de la guía (que te da un circuito dibujado y te pide armar la tabla y los globos) para poner esto a prueba?






**Es exactamente lo segundo que dijiste:** `X` no es el dato que se guarda en la memoria, sino **la señal que modela cómo trabaja el circuito para decidir cuál va a ser el próximo bloque de datos a guardar**.

  

Mirá por qué tenés esa duda (que es súper lógica) y cómo funciona realmente adentro del circuito:

  

### 1. ¿Se guarda 1 solo bit (`X`) o se guarda un bloque entero?

**En la memoria (`M`) SIEMPRE se guarda un bloque entero de bits al mismo tiempo** (tantos bits como Flip-Flops tengas en el circuito):

  

- En el ejemplo de Moore tenías **3 Flip-Flops** ($Q_2, Q_1, Q_0$), así que en cada golpe de reloj se guarda un **bloque de 3 bits** completo (`Estado Futuro`: $Q_2^+ Q_1^+ Q_0^+$).
    
      
    
- En el ejemplo de Mealy tenías **2 Flip-Flops** ($Q_1, Q_0$), así que en cada golpe de reloj se guarda un **bloque de 2 bits** completo (`Estado Futuro`: $Q_1^+ Q_0^+$).
    
      
    

El bit **`X` NO entra para guardarse directamente en los Flip-Flops**. Fijate en los dibujos de los circuitos (Diapositivas 8 y 11) que el cable `X` nunca se enchufa solito directo a un Flip-Flop, sino que se mete adentro de las **cajas verdes (`G`)** para mezclarse en las compuertas `AND` y `OR` con los cables $Q$ que ya estaban en la memoria.

  

### 2. Entonces, ¿qué es `X` y por qué hay que ponerla en la tabla y en las flechas?

Pensá tu circuito como si fuera una **función en C o en Java** que actualiza el estado de un objeto cada vez que suena el reloj:

  

Java

```
// Et es el bloque guardado en memoria (ej: 3 bits, un número del 0 al 7)
// X es el parámetro externo (ej: 1 bit, un booleano 0 o 1)

int calcularEstadoFuturo_G(int Et, int X) {
    if (X == 1) {
        return Et + 1; // Si X vale 1, el bloque de 3 bits suma 1
    } else {
        return Et - 1; // Si X vale 0, el bloque de 3 bits resta 1
    }
}
```

Fijate qué pasa en ese código:

  

1. **¿Qué es lo que se guarda en la memoria?** Se guarda el nuevo valor de `Et` (el bloque entero de 3 bits: `001`, `010`, `111`, etc.).
    
      
    
2. **¿Por qué tenés que poner a `X` en la tabla y en las flechas?** Porque sin saber cuánto vale el parámetro **`X`**, no sabés si el circuito va a entrar por el `if (X == 1)` o por el `else (X == 0)`.
    
      
    - En las **cajas verdes (`G`)** de tus diapositivas, las compuertas `AND` y `OR` son literalmente ese `if / else` hecho con cables.
        
          
        
    - Como las ecuaciones verdes ($J, K, D$) tienen la letra **`X`** metida en la fórmula (por ejemplo, $J_1 = Q_0 X + Q_0' X'$), el bloque de bits que calculan las compuertas verdes para guardar en la memoria cambia radicalmente según si por el cable `X` viene electricidad (`1`) o no viene (`0`).
        
          
        

### 3. ¿`X` va a ser siempre de 1 solo bit?

**En el 95% de los ejercicios de la guía y de los parciales de FIUBA, sí: `X` es de 1 solo bit** (porque si te pusieran una entrada de 2 o 3 bits, la tabla de estados tendría 32 o 64 filas y no terminarías más de escribir en el examen).

  

Pero conceptualmente, `X` tiene la cantidad de bits según cuántas "órdenes distintas" acepte tu máquina desde afuera:

  

- **0 bits (Sin entrada `X` — Ej. 3.33 de la guía):** Es una máquina que hace siempre lo mismo en piloto automático (por ejemplo, un reloj digital que siempre suma 1 segundo tras otro). No tiene ningún botón externo, así que de cada globo sale **1 sola flecha fija** hacia el próximo estado.
    
      
    
- **1 bit (`X` vale `0` o `1` — Tus diapositivas y Ej. 3.34 / 3.35):** La máquina sabe hacer **2 cosas distintas** (ej: contar hacia adelante con `1` o hacia atrás con `0`). Por eso de cada globo salen **2 flechas** (`0` y `1`).
    
      
    
- **2 bits (`X1 X0` valen `00`, `01`, `10` o `11`):** Sería una máquina con 2 botones que sabe hacer **4 cosas distintas** (ej: `00` = quedarse quieta, `01` = sumar 1, `10` = restar 1, `11` = volver a cero). Ahí de cada globo saldrían **4 flechas**.
    
      
    

En resumen: **lo que se guarda en la memoria es siempre el paquete `Estado Futuro` ($Q_2^+ Q_1^+ Q_0^+$)**, y vos ponés a **`X`** en la tabla y en las flechas porque es **la condición que elige qué cuenta hace el circuito** para fabricar ese próximo estado. ¿Con esa comparación del `if / else` que modifica al bloque entero te cierra mejor el rol de `X`?

![[Pasted image 20261010202534.png]]

![[Pasted image 20261010202713.png]]

![[Pasted image 20261010202826.png]]

![[Pasted image 20261010203222.png]]

![[Pasted image 20261010203157.png]]

![[Pasted image 20261010203309.png]]

![[Pasted image 20261010203357.png]]

![[Pasted image 20261010203420.png]]