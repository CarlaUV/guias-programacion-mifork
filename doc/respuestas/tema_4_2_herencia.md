# Tema 4.2. Herencia

## 1. En orientación a objetos, ¿qué es la **herencia** y su relación con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un método `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. Además, y de forma específica, el artillero tiene un número de cohetes y el zapador un número de minas, accesibles mediante "getters" específicos. Respecto a la compatibilidad de tipos, aprovechémosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). Recórrela y que todos te saluden.
### Respuesta
# Compatibilididad de tipos
# Soldado s = new Artillero("pepe");

## 2. Al crear los soldados concretos, ¿cuántos constructores se ejecutan y en qué orden? ¿Qué significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parámetros, ¿debo llamar a `super` siempre?
### Respuesta
Herencia de estado(atributos) y comportamiento(métodos)

## 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, ¿forman parte de una instancia de la subclase en memoria? En caso afirmativo ¿implica que se puedan usar desde el código de la subclase? Explícalo con el ejemplo de `Soldado` y alguna de sus subclases.
### Respuesta

## 4. ¿Qué implica en términos de **extensibilidad** de código el hecho de que sean compatibles a nivel de tipos? Ilustra esto añadiendo un nuevo tipo de `Soldado` y demostrando que el código para pedir el saludo a todos los soldados no se modifica.
### Respuesta
``` java
public class Soldado {
    private Stirng especialidad;

    public Medico(String nombre, String especialidad) {
        
    }
}

public class PruebaHerencia() {
    private static void pasarRevista(Soldado[] soldados) {
        for(Soldado soldado : soldados) {
            soldado.saludar();
        }
    }
    
    public static void main(String[] args) {
        Soldado[] soldadosVarios = new Soldado[3];

        soldadosVarios[0] = new Artillero("Juan", 3);
        soldadosVarios[1] = new Zapador("Ana", 1);
        soldadosVarios[2] = new Medico("Pepe", "traumatólogo");

        pasarRevista(soldadosVarios);
    }
}
```

## 5. En Java, cuando trabajo con referencias y herencia. ¿Puedo tener una referencia del supertipo que apunte a objetos reales de un subtipo? ¿Puedo invocar con la referencia del supertipo a métodos públicos del subtipo? ¿En qué consiste el **"upcasting"** y el **"downcasting"**? ¿Qué es el `instanceof`? Pon un ejemplo de recorrido de un array de `Soldado`, comprobando que, si el objeto real es un `Artillero`, solicite el número de cohetes que tiene y los imprima.
### Respuesta
``` java
public class Soldado {
    protected Stirng especialidad;

    public Medico(String nombre, String especialidad) {
        
    }
}

public class Artillero extends Soldado {
    private int numCohetes;
}
public class Zapador extends Soldado {
    private int numMinas;

    public Zapador(String nombre, int numMinas) {
        super(nombre);
        this.numMinas = numMinas;
    }
    public int getNumMinas() {
        return this.numMinas;
    }
    public void saludar() {
        System.out.println("Zapador " + super.getNombre() + " poniendo");
    }
}

public class PruebaHerencia() {
    private static void pasarRevista(Soldado[] soldados) {
        for(Soldado soldado : soldados) {
            soldado.saludar();

            if(soldado instanceof Artillero artillero) {
                System.out.println("munición: "+ artillero.getNumCohetes());
            }
            else if(soldado instanceof Zapador zapador) {
                System.out.println("minas: " + zapador.getNumMinas());
            }
        }
    }

    public static void main(String[] args) {
        Soldado[] soldadosVarios = new Soldado[3];

        soldadosVarios[0] = new Artillero("Juan", 3);
        soldadosVarios[1] = new Zapador("Ana", 1);
        soldadosVarios[2] = new Medico("Pepe", "traumatólogo");

        pasarRevista(soldadosVarios);
        
        Soldado soldado = new Artillero("Luis", 10); // upcasting, es automático. (implicito)    
        /* Versión vieja */
        if(soldado instanceof Artillero) {
            Artillero comoArtiellero = (Artillero) soldado; // downcasting, explícito (lo que va entre paréntesis)

            int cohetes = soldado.getNumCohetes();
            System.out.println("Cohetes: " + cohetes);
        }
        /* Versión nueva, haciendo downcasting automático */
        if(soldado instanceof Artillero comoArtillero) {
            int cohetes = soldado.getNumCohetes();
            System.out.println("Cohetes: " + cohetes);
        }
    }
}
```

## 6. Respecto a la ocultación de información y herencia, ¿qué significa acceso **"protegido"** de métodos y/o atributos? ¿Cómo se implementa en Java? Pon un ejemplo de uso de en la clase `Soldado` para que su nombre sea protegido y pueda usarse en el método de poner bombas del `Zapador`.
### Respuesta


## 7. En los lenguajes orientados a objetos ¿hay una **clase base** para todos los objetos? ¿Ocurre en todos los lenguajes? ¿Qué ocurre en Java?
### Respuesta
C++ no tiene una clase más implícita, Java sí la tiene: Object

## 8. ¿Qué es la **"herencia múltiple"**? ¿Existe en Java herencia múltiple?
### Respuesta
Herencia múltiple -> heredar de más de una clase
En Java no está sopoertada poeque lo decidieron así, para evitar porblemas como herencia en diamante.

## 9. Las excepciones en los lenguajes orientados a objetos son objetos. Por tanto, se pueden crear excepciones personalizadas. Pon un ejemplo en Java de una excepción personalizada (`UsuarioNoEncontradoException`), que sea *no controlada* y que además este compuesto con un `Usuario`, para saber qué `Usuario` dio el problema. Permite además que se pueda incluir la causa, es decir, sobrecarga el constructor para tener una versión que permita añadir la causa subyacente. 
### Respuesta
``` Java
public class UsuarioNoEncontradoException extends RuntimeException {
    private Usuario usuarioNoEncontrado;

    public UsuarioNoEncontradoException(String mensaje, Throwable cuasa, Usuario usuarioNoEncontrado) {
        super(mensaje, causa);
        this.usuarioNoEncontrado = usuarioNoEncontrado;
    }
    public UsuarioNoEncontradoException(String mensaje, Usuario usuarioNoEncontrado) {
        super(mensaje);
        this.usuarioNoEncontrado = usuarioNoEncontrado;
    }

    public Usuario getUsuarioNoEncotrado() {
        return this.usuarioNoEncontrado;
    }

/*
    Usuario usuarioABuscar = ...

    //...
    throw new UsuarioNoEncontrado("El usuario no se encuentra en la BD.", usuarioABuscar);
*/
/*
    try {
    } catch() {
    }
*/
}
```

## 10. Herencia vs. Composición. Se dice que no se debe emplear herencia simplemente por reutilizar código, es decir, que si quiero reutilizar código simplemente, no debo pensar en herencia como primera opción ¿por qué?
### Respuesta


## 11. Herencia vs. Composición. Se dice que se debe *"favorecer la composición frente a la herencia"*, ¿por qué?
### Respuesta


## 12. Herencia vs. Composición. Se dice que la *"herencia rompe la encapsulación"*, ¿a qué se refiere esto?
### Respuesta


## 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en común: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composición, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.
### Respuesta
