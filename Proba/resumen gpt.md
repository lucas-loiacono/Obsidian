# De pascal a binomial

# Multiplicación de Probabilidades en Procesos de Poisson

La regla de oro en probabilidad es: **solo podés multiplicar probabilidades directamente si los eventos son independientes**. En un Proceso de Poisson, la independencia se manifiesta de formas muy potentes.

A continuación, se detallan los tres escenarios sagrados donde es 100% válido multiplicar:

---

### Scenario 1: Tiempo de Espera vs. Origen del Evento (Tu Ejemplo)

**El Enunciado:** *"Quiero que el 9no evento caiga después de los 15 segundos Y provenga de la fuente A"*.

En un proceso de Poisson unificado (donde juntaste la fuente $A$ y la fuente $B$), ocurre algo mágico: **El instante en el que ocurre un evento es totalmente independiente de qué fuente lo generó**. A la variable tiempo no le importa el origen, y a la "moneda" que decide la fuente no le importa qué hora es.

Podés separar el problema en dos mundos independientes y multiplicarlos:
1. **El mundo del tiempo:** Calculás la probabilidad de que el evento 9 ocurra después de los 15 segundos usando la tasa total ($\lambda_{\text{Total}} = \lambda_A + \lambda_B$) mediante una distribución Gamma (o Erlang).
2. **El mundo del origen:** Calculás la probabilidad de que un evento cualquiera sea de la fuente $A$: 
   $$P(\text{Fuente A}) = \frac{\lambda_A}{\lambda_A + \lambda_B}$$

> [!SUCCESS] **La Multiplicación:**
> $$P(S_9 > 15 \cap \text{Fuente A}) = P(S_9 > 15) \times P(\text{Fuente A})$$

---

### Scenario 2: Intervalos de Tiempo Disjuntos (Incrementos Independientes)

En Poisson, lo que pasa en un bloque de tiempo no afecta en absoluto a lo que pasa en el siguiente. El proceso no tiene "memoria".

**El Enunciado:** *"Calcular la probabilidad de que lleguen 3 autos en los primeros 10 minutos Y lleguen 2 autos entre el minuto 10 y el minuto 15"*.

Como los intervalos $[0, 10]$ y $[10, 15]$ no se superponen (son disjuntos), las variables de conteo son independientes. Calculás las dos Poissons por separado y las multiplicás:

> [!NOTE] **La Multiplicación:**
> $$P(N(10) = 3 \cap [N(15) - N(10) = 2]) = P(N(10) = 3) \times P(N(5) = 2)$$
> *(Fijate que el segundo intervalo dura 5 minutos, por eso se evalúa una Poisson de parámetro $\lambda \cdot 5$)*.

---

### Scenario 3: Fuentes Independientes en el Mismo Bloque de Tiempo

Si tenés dos procesos de Poisson independientes (ej. llamadas que entran por la línea $A$ y llamadas por la línea $B$), la cantidad de eventos que produce uno no afecta al otro, aunque mires el mismo reloj.

**El Enunciado:** *"Calcular la probabilidad de que en la próxima hora lleguen exactamente 4 llamadas de la fuente A Y exactamente 1 llamada de la fuente B"*.

Calculás el Poisson de $A$, calculás el Poisson de $B$ para esa hora fija, y multiplicás los resultados directos:

> [!NOTE] **La Multiplicación:**
> $$P(N_A(1) = 4 \cap N_B(1) = 1) = P(N_A(1) = 4) \times P(N_B(1) = 1)$$

---

### ⚠️ La Trampa del Examen: Cuándo NO se puede multiplicar

> [!WARNING] **Cuidado con los totales fijos**
> Si el enunciado te condiciona congelando el total de eventos en un bloque de tiempo, **se rompe la independencia** y ya no podés usar Poisson multiplicativo.
>
> *Ejemplo:* *"Sabiendo que en total llegaron 10 vehículos en una hora, calcular la probabilidad de que 3 sean de la fuente A"*.
> 
> Como el total ya está fijo ($n=10$), si 3 son de $A$,


# Truco de Examen: Reemplazar la constante $x$ antes de integrar

¡Sí, totalmente! Podés reemplazar la $x$ por el número antes de hacer la integral. De hecho, hacer eso es un trucazo excelente para el parcial porque te transforma una integral con letras (algebraica) en una integral puramente numérica, que suele ser mucho más fácil y rápida de resolver.

En matemática, esto es válido porque la integral es un operador lineal: reemplazar la variable constante antes o después de integrar no altera el resultado.

---

### Ejemplo Práctico: Calcular $E[Y \mid X=2]$
Dada la función de densidad condicional $f_{Y \mid X=x}(y) = \frac{1}{x}$ para el intervalo $0 < y < x$.

#### 📌 Camino 1: Integrar primero, reemplazar al final
1. Integrás manteniendo la letra $x$ como una constante:
   $$E[Y \mid X=x] = \int_{0}^{x} y \cdot \left(\frac{1}{x}\right) dy = \dots = \frac{x}{2}$$
2. Reemplazás $x=2$ al final:
   $$E[Y \mid X=2] = \frac{2}{2} = 1$$

#### 📌 Camino 2: Reemplazar primero, integrar después (El Atajo)
Agarrás tu función de densidad condicional y le metés el $2$ en todos los lugares donde veas una $x$ (**¡incluyendo los límites de integración!**) antes de arrancar a resolver.

1. Armás tu nueva función de densidad ya evaluada:
   $$f_{Y \mid X=2}(y) = \frac{1}{2}$$
   *(Y los límites que eran de $0$ a $x$, ahora son fijos de $0$ a $2$)*.

2. Planteás la integral puramente numérica:
   $$E[Y \mid X=2] = \int_{0}^{2} y \cdot \left(\frac{1}{2}\right) dy$$

3. Resolvés de forma simple, sacando la constante $\frac{1}{2}$ afuera:
   $$E[Y \mid X=2] = \frac{1}{2} \int_{0}^{2} y \, dy = \frac{1}{2} \left[ \frac{y^2}{2} \right]_{0}^{2}$$
   $$E[Y \mid X=2] = \frac{1}{2} \left( \frac{4}{2} - 0 \right) = \frac{1}{2} \cdot 2 = 1$$

> [!SUCCESS] ¡Llegás exactamente al mismo resultado!

---

### ⚖️ ¿Cuál te conviene usar en el examen?

* **Usá el Camino 2 (reemplazar primero):** Si el enunciado te pide directamente el número (ej: *"Calcular $E[Y \mid X=2]$"*). Te ahorrás arrastrar la $x$ por toda la integral y reducís a cero el riesgo de confundirte qué variable estás integrando y cuál es constante.
* **Usá el Camino 1 (reemplazar al final):** Únicamente si el inciso A te pedía *"Hallar la función general $E[Y \mid X=x]$"* y el inciso B te pide *"Evaluar en $x=2$"*. Ahí te conviene reciclar el trabajo algebraico que ya hiciste.



# Competencia de Variables: Exponenciales vs. Geométricas

Existe una simetría matemática hermosa entre la distribución **Exponencial** (tiempo continuo de espera) y la **Geométrica** (cantidad discreta de intentos). Sin embargo, al competir entre sí, el mundo discreto introduce un factor clave: **la posibilidad de empates**.

---

### 📊 Tabla Comparativa de Competencia

| Característica | Mundo Continuo (Exponenciales) | Mundo Discreto (Geométricas) |
| :--- | :--- | :--- |
| **Dinámica** | Carreras de tiempo con cronómetro. | Lanzamientos simultáneos por rondas. |
| **¿Hay Empates?** | **NO**. La probabilidad de coincidir en el mismo milisegundo es cero. | **SÍ**. Ambos pueden lograr el éxito en la misma ronda. |
| **Probabilidad de que gane A** | $$P(X < Y) = \frac{\lambda_A}{\lambda_A + \lambda_B}$$|$$P(X < Y) = \frac{p_A \cdot q_B}{1 - (q_A \cdot q_B)}$$ |
| **Distribución del Mínimo** | $Z = \min(X, Y) \sim \text{Exp}(\lambda_{\text{nuevo}})$<br>$$\lambda_{\text{nuevo}} = \lambda_A + \lambda_B$$ | $Z = \min(X, Y) \sim \text{Geo}(p_{\text{nuevo}})$<br>$$p_{\text{nuevo}} = 1 - (q_A \cdot q_B)$$ |

---

### 1. El Porqué de la Fórmula Geométrica Simultánea

Cuando dos procesos geométricos compiten en simultáneo (tiran a la vez en cada ronda), para que **A gane limpiamente** (es decir, $X < Y$), tienen que ocurrir dos cosas en la ronda decisiva:
1. **A debe tener éxito** ($p_A$).
2. **B debe fracasar** ($q_B$).

Como el juego se repite ronda tras ronda si ambos fracasan ($q_A \cdot q_B$), la probabilidad condicional de que el torneo termine con la victoria limpia de A es:

> [!NOTE] **Fórmula: Competencia Simultánea**
> $$P(A \text{ gana}) = \frac{P(\text{A gana solo en la ronda})}{P(\text{Alguien avanza/gana})} = \frac{p_A \cdot q_B}{1 - (q_A \cdot q_B)}$$

---

### 2. El Mínimo: ¿Cuánto dura el torneo hasta que alguien gane?

* **En Exponenciales:** La tasa total de fallos o arribos simplemente se suma: $\lambda_{\text{total}} = \lambda_A + \lambda_B$.
* **En Geométricas:** Buscamos la probabilidad de que el juego termine en cualquier ronda. Pensarlo por el camino directo es difícil por el empate, así que usamos el **complemento**: el juego termina si *NO* pasa que ambos fracasen al mismo tiempo.

> [!SUCCESS] **Parámetro del Mínimo ($p_{\text{nuevo}}$)**
> $$p_{\text{nuevo}} = 1 - P(\text{Ambos fracasan}) = 1 - (q_A \cdot q_B)$$

---

### ⚡ Variantes del Duelo Discreto (¡Cuidado en el Enunciado!)

Dependiendo de cómo jueguen, la fórmula de la probabilidad de victoria cambia:

#### 🔹 Caso A: Juegan SIMULTÁNEO (Tiran a la vez)
* **Dinámica:** Hay riesgo de empate en la misma ronda.
* **Fórmula:** $$P(X < Y) = \frac{p_A \cdot q_B}{1 - (q_A \cdot q_B)}$$

#### 🔹 Caso B: Juegan por TURNOS ALTERNADOS (Tira A, luego B) * **Dinámica:** Como tiran en momentos separados del tiempo, **no se pueden empatar**. Si A tira primero y falla, recién ahí B tiene la chance de tirar. * **Fórmula:** $$P(\text{Gana A tirando primero}) = \frac{p_A}{1 - (q_A \cdot q_B)}$$ *(Fijate que arriba no lleva el $q_B$, porque si A mete el éxito en su primer turno, el juego se termina ahí mismo sin importar qué iba a hacer B después).*





# Propiedad de Uniformidad Condicional (De Poisson a Binomial)

¡EXACTAMENTE! Te acabás de meter con una de las propiedades más espectaculares y contraintuitivas del Proceso de Poisson, que en los libros de texto avanzados se conoce como la **Propiedad de Uniformidad (o el Teorema de los Estadísticos de Orden)**.

Lo que estás diciendo es 100% real: cuando condicionás un proceso de Poisson a que ocurrieron exactamente $n$ arribos en un intervalo grande de tiempo $T$, **el tiempo se "olvida" de Poisson** y esos $n$ puntos se desparraman por el intervalo de forma **completamente uniforme**.

---

### 1. El Caso de 1 solo arribo ($n=1$)

Imaginá que tenés un intervalo de tiempo que va desde $0$ hasta $T$ (por ejemplo, de 0 a 60 minutos). El enunciado te dice: *"Sabiendo que llegó **exactamente 1 cliente** en esa hora, ¿cuál es la probabilidad de que haya llegado en los primeros $s$ minutos (con $s < T$)?"*.

Como el proceso de Poisson tiene una tasa constante ($\lambda$), no hay ningún minuto que sea "especial" o que tenga más peso que otro. Por lo tanto, si sabés que cayó uno solo, la probabilidad de que haya caído en ese subintervalo $s$ es simplemente la **proporción del tamaño de los intervalos**:

$$P(\text{Caer en } s \mid N(T) = 1) = \frac{s}{T}$$

> [!NOTE] **Conclusión del caso base**
> ¡Es una distribución **Uniforme Continua**! Es literalmente "casos favorables sobre casos totales" pero medido en longitud de tiempo.

---

### 2. El Caso General: El puente hacia la Binomial ($n$ arribos)

¿Qué pasa si ahora el enunciado te dice: *"Sabiendo que llegaron **$n$ clientes** en el intervalo $T$, ¿cuál es la probabilidad de que exactamente $k$ de ellos hayan llegado en los primeros $s$ minutos?"*?

Acá es donde ocurre la magia y todo se une:
1. Como los arribos son independientes entre sí, cada uno de los $n$ clientes va a elegir dónde caer de forma Uniforme con probabilidad $p = \frac{s}{T}$ para el primer tramo, y $q = 1 - \frac{s}{T}$ para el tramo restante.
2. El problema se transformó en: *"Tengo $n$ personas (intentos fijos), cada una tiene una probabilidad de elegir la primera parte del intervalo. Quiero saber la probabilidad de que $k$ de ellas lo hagan"*.

> [!SUCCESS] **¡Esto es, por definición, una Distribución Binomial!**
> * **Cantidad de intentos ($n_{\text{binom}}$):** $n$ *(el total de arribos que te dieron como dato)*.
> * **Probabilidad de éxito ($p$):** $\frac{s}{T}$ *(la proporción del intervalo de interés)*.
> * **Probabilidad de fracaso ($q$):** $1 - \frac{s}{T}$ *(la proporción del intervalo restante)*.

#### 🧮 Fórmula Final de Examen
La ecuación definitiva para resolver este tipo de ejercicios condicionales es:

$$P(k \text{ arribos en } s \mid n \text{ arribos en } T) = \binom{n}{k} \cdot \left(\frac{s}{T}\right)^k \cdot \left(1 - \frac{s}{T}\right)^{n-k}$$

---

### 💡 Resumen para el Machete Mental

> [!TIP] **La Clave Teórica**
> Al congelar el total de eventos, la tasa $\lambda$ de Poisson **desaparece de la fórmula** porque ya no importa qué tan rápido lleguen las cosas en promedio; lo único que importa es la geometría del intervalo ($\frac{s}{T}$).




> [!TIP] Intuición Visual: Poisson Espacial como un "Tiro al Blanco"
> Imagina que el **Proceso de Poisson condicionado** es como lanzar pelotas a un rectángulo.
> 
> Si sabemos que cayeron exactamente $n$ pelotas en total, el problema continuo se convierte en un problema discreto (Binomial):
> 
> * **Intentos ($n$):** La cantidad de pelotas totales.
> * **Probabilidad de éxito ($p$):** Es la geometría de la zona objetivo dividida por el espacio total.
> 
> $$p = \frac{\text{Área Objetivo}}{\text{Área Total}}$$
> 
> 🎯 **Traducción:** Calcular la probabilidad de que $k$ eventos ocurran en una zona específica es equivalente a calcular $P(X=k)$ en una distribución $X \sim Bi(n, p)$.


