
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

