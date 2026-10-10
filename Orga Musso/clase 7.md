
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

![[Pasted image 20261001202930.png]]