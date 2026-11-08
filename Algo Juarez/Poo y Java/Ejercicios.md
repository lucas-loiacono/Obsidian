
![[Pasted image 20261107212427.png]]c

# Ejercicio 5.1: Herencia en Java

### Enunciado
¿Cuál de las siguientes afirmaciones sobre herencia es verdadera en Java?[cite: 13]
- (a) Una clase puede heredar de múltiples clases.
- (b) Los métodos y atributos protegidos se heredan como privados.
- (c) Una clase abstracta no puede tener métodos concretos.
- (d) Una clase puede heredar de una clase e implementar una interfaz al mismo tiempo.

### Análisis y Solución
Evaluamos cada afirmación según los conceptos de Programación Orientada a Objetos (POO) en Java:

*   **(a) Falso:** Java **no soporta herencia múltiple de clases** para evitar la ambigüedad conocida como el "Problema del Diamante". Una clase solo puede extender (`extends`) a una única superclase directa.
*   **(b) Falso:** Los miembros definidos como `protected` en la clase padre se heredan y mantienen su visibilidad para las clases hijas y para otras clases dentro del mismo paquete. No se convierten restrictivamente en `private`.
*   **(c) Falso:** A diferencia de las interfaces tradicionales, una clase `abstract` en Java fue diseñada específicamente para permitir una mezcla: puede tener métodos abstractos (sin cuerpo, que obligan a las hijas a implementarlos) y **métodos concretos** (con cuerpo y comportamiento por defecto ya programado).
*   **(d) Verdadero:** Esta es la forma estándar de trabajar en Java. Una clase puede extender de una única superclase base (herencia de código) y simultáneamente implementar una o múltiples interfaces (cumplimiento de contratos). Ejemplo de sintaxis válida: `public class MiClase extends ClasePadre implements MiInterfaz`.

**Opción correcta: (d)**[cite: 13]