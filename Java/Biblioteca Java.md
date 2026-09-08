
## Hello World

```java
public class HelloWorld {

    public static void main(String[] args) {

        System.out.println("Hola, Java!");

    }

}
```


## Tipos de datos

```java
public class DataTypes {

    public static void main(String[] args) {

        // Tipos de datos primitivos

        int myInt = 37;
        System.out.println(myInt);

        double myDouble = 1.77;
        System.out.println(myDouble);

  

        // float, long, byte
        char myChar = 'a'
        System.out.println(myChar);
  

        boolean myBoolean = true;
        myBoolean = false;
        System.out.println(myBoolean);

        String myString = "Hola, Java";
        System.out.println(myString);

        // Tipo de dato en tiempo de compilación
        System.out.println(myString.getClass().getSimpleName());

    }

}
```

## Variables y constantes

```java

public class VariablesAndConstants {

    public static void main(String[] args) {

        // Variables

        String name = "Brais";
        System.out.println(name);

        name = "MoureDev";
        System.out.println(name);

        // name = 37; Error (no podemos cambiar el tipo de dato)

        int age = 37;
        System.out.println(age);

        var email = "mouredev@gmail.com";
        System.out.println(email);
  

        var year = 2025;
        System.out.println(year);
  

        // Constantes

        final String EMAIL = "mouredev@gmail.com";
        // EMAIL = "brais@gmail.com"; Es constante

        System.out.println(EMAIL);

    }

}
```

## Operadores

```java
public class Operators {

    public static void main(String[] args) {

        // Aritméticos

        var a = 5;
        var b = 3;


        System.out.println(a + b);
        System.out.println(a - b);
        System.out.println(a * b);
        System.out.println(a / b);
        System.out.println(a % b);

  
  
        // Asignación

        a = b;
        System.out.println(a);

        a = b * 2;
        System.out.println(a);

        a += 1; // a = a + 1
        System.out.println(a);

        a -= 1;
        System.out.println(a);
        
        a *= 2;
        System.out.println(a);

        a /= 2;
        System.out.println(a);

        a %= 2;

        System.out.println(a);


  
        // Comparación (Relacionales)

        System.out.println(a == b);
        System.out.println(a == 0);

        System.out.println(a != b);
        System.out.println(a > b);
        System.out.println(a >= b);
        System.out.println(a < b);
        System.out.println(a <= b);

  

        // Lógicos

        // Y (AND)

        System.out.println(true && true);

        System.out.println(true && false);

        System.out.println(false && true);

        System.out.println(false && false);


        System.out.println(3 > 2 && 5 == 2);

  

        // O (OR)

        System.out.println(true || true);

        System.out.println(true || false);

        System.out.println(false || true);

        System.out.println(false || false);

  

        System.out.println(3 > 2 || 5 == 2);

  

        // NO (NOT)

        System.out.println(!true);

        System.out.println(!false);

  
        System.out.println(!(3 > 2) || 5 == 2);

  
        // Unarios

        System.out.println(+b);

        System.out.println(-b);

        System.out.println(++b);

        System.out.println(b++);

        System.out.println(b);

        System.out.println(--b);

        System.out.println(b--);

        System.out.println(b);

    }

}
```

## Strings

```java
public class Strings {

    public static void main(String[] args) {

  

        // Declaración

        String name = "Brais";
        var surname = new String("Moure");
  

        // Operaciones básicas


        // Concatenación

        System.out.println(name + " " + surname);


        // Longitud

        System.out.println(name.length());


        // Obtener carácter

        System.out.println(name.charAt(name.length() - 1));

  

        // Subcadena

        System.out.println(name.substring(2));

        System.out.println(name.substring(1, 3));

    

        // Mayúsculas y minúsculas

        System.out.println(name.toUpperCase());

        System.out.println(name.toLowerCase());


        System.out.println(name);

  

        // Comprobar si contiene

        System.out.println("Hola, Java".contains("Brais"));

        System.out.println("Hola, Java".toUpperCase().contains("AVA"));

  

        // Comparación

        System.out.println(name.equals("Brais"));

        System.out.println(name.equals("brais"));

        System.out.println(name.equalsIgnoreCase("brais"));

  

        // == vs. equals

  

        var a = "Brais";

        var b = "Brais";

        var c = new String("Brais");

  

        System.out.println(a == b);

        System.out.println(a == c);

        System.out.println(a.equals(c));


        // Trim

        System.out.println(" Hola, me llamo Brais ".trim());

  
        // Replace

        System.out.println(" Hola, me llamo Brais ".replace("Brais", "Moure"));

  
        // Format

        var age = 37;

        System.out.println(String.format("Hola, %s. Tengo %d.", name, age));

    }

}


```

