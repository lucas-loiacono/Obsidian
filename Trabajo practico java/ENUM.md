

Vamos a rastrear paso a paso qué pasa cuando se ejecuta esa línea, porque involucra varias piezas que ya vimos por separado.

## La línea en cuestión

```java
this.vidaActual = base.obtenerValor(Estadistica.VIDA);
```

`base` es un parámetro que **te dieron desde afuera** cuando alguien creó este `Campeon`. Es de tipo `Estadisticas` (la clase que armamos hace rato, con vida, daño, rango, cadencia, etc.).

## Un ejemplo concreto de cómo se llega hasta acá

Imaginemos que en algún lugar del código (por ejemplo, en tu programa principal, o en un test) alguien hace:

```java
Estadisticas statsRekSai = new Estadisticas(500, 60, 1, 10, 100, 20);
//                                            ↑    ↑   ↑  ↑   ↑    ↑
//                                          vida danio rango cadencia manaMax manaPorAtaque

Campeon rekSai = new Campeon("Rek'Sai", Rareza.RARA, statsRekSai);
```

Cuando eso pasa, adentro de tu constructor, el parámetro `base` **es** ese objeto `statsRekSai` — con `vida = 500`, `danio = 60`, etc. ya guardados adentro (porque así lo armamos en el constructor de `Estadisticas`).

## Qué hace `base.obtenerValor(Estadistica.VIDA)`

Recordemos cómo armamos `Estadisticas.obtenerValor()`:

```java
public int obtenerValor(Estadistica estadistica) {
    if (estadistica == null) {
        throw new IllegalArgumentException("La estadística no puede ser nula.");
    }
    switch (estadistica) {
        case VIDA:
            return this.vida;
        case DANIO:
            return this.danio;
        // ...
    }
}
```

Entonces, `base.obtenerValor(Estadistica.VIDA)` significa: _"Andá al objeto `base` (que en nuestro ejemplo es `statsRekSai`), y ejecutá su método `obtenerValor`, pasándole como argumento `Estadistica.VIDA`."_

Adentro de ese método (que se ejecuta usando los datos de `statsRekSai`):

1. `estadistica` (el parámetro del método) vale `Estadistica.VIDA`.
2. Entra al `switch`, y como `estadistica` es `VIDA`, cae en `case VIDA:`.
3. Devuelve `this.vida` — pero **acá el `this` es `statsRekSai`**, porque es el objeto que está ejecutando `obtenerValor()` en este momento. Entonces devuelve el `vida` de `statsRekSai`, que en nuestro ejemplo es `500`.

## Entonces, la línea completa

```java
this.vidaActual = base.obtenerValor(Estadistica.VIDA);
```

Se traduce, con nuestro ejemplo concreto, a:

```java
this.vidaActual = 500;
```

Donde `this` acá (en `Campeon`) es el `rekSai` que se está creando. O sea: **le estás preguntando a las estadísticas base que te pasaron cuál es el valor de vida, y guardás ese número como la vida actual del campeón recién creado.**

## Por qué se hace así (y no, por ejemplo, `base.vida` directo)

Fijate que `vida` es un atributo **privado** de `Estadisticas` — desde `Campeon` no podés acceder a `base.vida` directamente, Java no te deja (rompe el encapsulamiento). Por eso `Estadisticas` expone el método público `obtenerValor(Estadistica)`, que es la **única puerta de entrada** permitida para leer esos datos privados desde afuera.

Y usar un solo método genérico con un parámetro `Estadistica` (en vez de 6 métodos separados `obtenerVida()`, `obtenerDanio()`, etc.) es justamente la ventaja del enum que veníamos charlando: un único método sirve para consultar cualquiera de las 6 estadísticas, según cuál le pases como argumento.

