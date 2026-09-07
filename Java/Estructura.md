En Java, la estructura de archivos está estrictamente atada a cómo organizas tu código. A diferencia de otros lenguajes donde puedes poner múltiples cosas en un solo archivo, Java te obliga a ser muy ordenado. Piensa en tu proyecto como un sistema de carpetas físico.

  

**1. Archivos = Clases (Regla 1 a 1)**

Cada clase pública en Java **debe** tener su propio archivo, y el archivo debe llamarse exactamente igual que la clase (respetando mayúsculas y minúsculas).

  

- Si escribes `public class Estudiante`, el archivo tiene que llamarse `Estudiante.java`.
    
      
    

**2. Packages = Carpetas**

Un `package` (paquete) no es más que **una carpeta** dentro de tu proyecto. Sirve para agrupar clases relacionadas y mantener el código ordenado.

  

- Si guardas `Estudiante.java` dentro de una carpeta llamada `modelos`, la primera línea de código de ese archivo tiene que decir obligatoriamente `package modelos;`.
    
      
    
- Esto le avisa a Java dónde está ubicado ese archivo.
    
      
    

**3. El archivo Main = El punto de arranque**

Java no ejecuta todos los archivos a la vez; necesita saber por dónde empezar. Para eso busca el método `public static void main(String[] args)`.

  

- Por convención y limpieza, se suele crear una clase separada llamada `Main.java`. Este archivo actúa como el "director de orquesta": no tiene mucha lógica propia, sino que se encarga de crear los objetos de tus otras clases y ponerlos a trabajar.




### Cómo se ve esto en la práctica

En entornos como IntelliJ IDEA, tu código fuente siempre va dentro de una carpeta base llamada `src` (source). Una estructura típica se ve así:


```
src/
├── Main.java               (Está suelto en la raíz, no tiene package)
└── universidad/            (Esto es un package/carpeta)
    ├── Estudiante.java
    └── Materia.java
```

### ¿Cómo se comunican los archivos entre sí?

Si tu `Main.java` quiere usar la clase `Estudiante`, necesita saber en qué carpeta (package) buscarla. Para eso usamos el **import**.

  

**Archivo 1: `universidad/Estudiante.java`**

```java
package universidad; // 1. Avisa en qué carpeta está

public class Estudiante {
    public String nombre;
    
    public Estudiante(String nombre) {
        this.nombre = nombre;
    }
}
```

**Archivo 2: `Main.java`**

```java
import universidad.Estudiante; // 2. Trae la clase desde su carpeta

public class Main {
    public static void main(String[] args) {
        // 3. El programa arranca acá
        Estudiante lucas = new Estudiante("Lucas");
        System.out.println("El estudiante es: " + lucas.nombre);
    }
}
```

Al separar el `main` de las clases, logras que tus clases (como `Estudiante`) sean puros moldes o representaciones abstractas de datos, mientras que el `main` es el único lugar que da las órdenes de ejecución.