# Tema 4.2. Herencia

## 1. En orientación a objetos, ¿qué es la **herencia** y su relación con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un método `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. Además, y de forma específica, el artillero tiene un número de cohetes y el zapador un número de minas, accesibles mediante "getters" específicos. Respecto a la compatibilidad de tipos, aprovechémosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). Recórrela y que todos te saluden.
### Respuesta
Tiene dos usos:
- Compatibilidad de tipos. Ej.: Vehiculo v = new Turismo();
- Herencia de estado (atributos) y comportamiento (métodos)
En orientación a objetos, la **herencia** es un mecanismo mediante el cual una clase (subclase) reutiliza y extiende el estado y el comportamiento definidos por otra clase (superclase). Conceptualmente, la herencia modela una relación **“A es-un B”**, lo que significa que un objeto de la subclase puede ser tratado como un objeto de la superclase. Por ejemplo, si `Artillero` hereda de `Soldado`, se puede afirmar que *un artillero es un soldado*.

La primera implicación importante es la **compatibilidad de tipos**. Esto permite que una referencia del tipo de la superclase (`Soldado`) apunte a objetos de cualquiera de sus subclases (`Artillero`, `Zapador`). Gracias a esto, se pueden escribir estructuras de código genéricas (arrays, métodos) que trabajen con el tipo base sin conocer los subtipos concretos, facilitando la reutilización y extensibilidad del programa.

La segunda implicación es la **herencia de estado y comportamiento**. Las subclases heredan los atributos y métodos accesibles (no privados de forma directa) de la superclase. En este caso, tanto `Artillero` como `Zapador` heredan el nombre del soldado y la capacidad de saludar, añadiendo además su propio estado y comportamiento específico.
***

# Compatibilididad de tipos
# Soldado s = new Artillero("pepe");
```Java
class Soldado {
    private String nombre;

    public Soldado(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

class Artillero extends Soldado {
    private int cohetes;

    public Artillero(String nombre, int cohetes) {
        super(nombre);
        this.cohetes = cohetes;
    }

    public int getCohetes() {
        return cohetes;
    }
}

class Zapador extends Soldado {
    private int minas;

    public Zapador(String nombre, int minas) {
        super(nombre);
        this.minas = minas;
    }

    public int getMinas() {
        return minas;
    }
}

Soldado[] ejercito = {
    new Artillero("Carlos", 10),
    new Zapador("Luis", 5),
    new Artillero("Ana", 7)
};

for (Soldado s : ejercito) {
    s.saludar();
}
```

## 2. Al crear los soldados concretos, ¿cuántos constructores se ejecutan y en qué orden? ¿Qué significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parámetros, ¿debo llamar a `super` siempre?
### Respuesta
Al crear un objeto de una clase concreta que hereda de otra (por ejemplo, Artillero o Zapador), siempre se ejecutan dos constructores: el de la clase base (Soldado) y el de la clase concreta. El orden de ejecución es fijo: primero se ejecuta el constructor de la superclase y, a continuación, el de la subclase. La palabra clave super dentro de un constructor se utiliza para invocar un constructor de la clase base. Si la clase base no tiene visible (public o protected) un constructor sin parámetros, entonces es obligatorio llamar explícitamente a super con los argumentos adecuados. De lo contrario, el código no compila, ya que Java no puede inventar una forma de construir correctamente la superclase.
***

## 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, ¿forman parte de una instancia de la subclase en memoria? En caso afirmativo ¿implica que se puedan usar desde el código de la subclase? Explícalo con el ejemplo de `Soldado` y alguna de sus subclases.
### Respuesta
En una jerarquía de herencia, los atributos privados de la superclase sí forman parte de la instancia en memoria de la subclase. Cuando se crea un objeto de una subclase como Artillero, la instancia resultante contiene internamente la parte correspondiente a Soldado (con todos sus atributos, incluidos los privados) y, además, la parte específica de Artillero. Sin embargo, que esos atributos existan físicamente en memoria no implica que puedan usarse directamente desde el código de la subclase. En Java, el modificador private restringe el acceso al código de la propia clase donde se declara el atributo, independientemente de la herencia. Por tanto, aunque un Artillero tenga internamente el atributo nombre heredado de Soldado, ese atributo no puede ser referenciado directamente desde la clase Artillero. Esto se observa claramente en el ejemplo de Soldado. El atributo nombre es privado, por lo que solo puede ser usado dentro de la clase Soldado. La subclase Artillero no puede escribir nombre ni leer su valor directamente. La forma correcta de interactuar con ese estado heredado es a través de métodos de la superclase, como saludar() o, si existiera, un método getNombre().
***

## 4. ¿Qué implica en términos de **extensibilidad** de código el hecho de que sean compatibles a nivel de tipos? Ilustra esto añadiendo un nuevo tipo de `Soldado` y demostrando que el código para pedir el saludo a todos los soldados no se modifica.
### Respuesta
``` java
class Soldado {
    private String nombre;

    public Soldado(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

class Medico extends Soldado {
    public Medico(String nombre) {
        super(nombre);
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
class Soldado {
    private String nombre;

    public Soldado(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
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
En el contexto de la ocultación de información y la herencia, el acceso protegido permite un equilibrio entre encapsulación y reutilización. Un atributo o método protegido no es accesible desde cualquier clase, pero sí puede ser utilizado por las subclases, además de por las clases del mismo paquete. Esto resulta útil cuando se desea que ciertos detalles internos no sean completamente públicos, pero sí estén disponibles para las clases que especializan el comportamiento de una superclase. En Java, el acceso protegido se implementa mediante la palabra clave protected. A diferencia de private, que restringe el acceso exclusivamente a la propia clase, protected permite que las subclases accedan directamente al atributo o método heredado. De este modo, se mantiene un cierto control sobre el estado interno, sin impedir que las subclases lo utilicen para implementar comportamientos más específicos. En el ejemplo de Soldado, hacer que el atributo nombre sea protegido permite que una subclase como Zapador lo use para personalizar su comportamiento, por ejemplo al mostrar un mensaje al colocar una bomba. El atributo sigue sin ser accesible desde código externo no relacionado, pero deja de estar completamente oculto para las clases hijas, lo que facilita la extensión controlada del comportamiento.
***

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
En orientación a objetos, no se recomienda usar herencia únicamente como mecanismo de reutilización de código porque la herencia introduce una relación semántica fuerte entre clases, no solo técnica. Cuando se utiliza herencia, se afirma explícitamente que “A es-un B”, es decir, que la subclase representa una especialización válida de la superclase en todos los contextos. Si esa relación no es cierta desde el punto de vista del modelo del problema, la herencia genera jerarquías artificiales y frágiles, aunque inicialmente permita ahorrar código. Además, la herencia crea un alto acoplamiento entre la subclase y la superclase. La subclase depende directamente de la implementación de la clase base, no solo de su interfaz pública. Cambios en la superclase (nuevos métodos, modificaciones de comportamiento, cambios en atributos protegidos) pueden afectar de forma inesperada a todas las subclases, incluso a aquellas que solo heredaban para “reutilizar código”. Esto dificulta el mantenimiento y la evolución del sistema a medio y largo plazo. La composición, en cambio, permite reutilizar código sin establecer una relación de tipo jerárquico. Cuando una clase tiene-un objeto de otra clase (en lugar de ser-un tipo de ella), se mantiene la encapsulación y se reduce el acoplamiento. La clase compuesta depende del comportamiento expuesto por la otra clase, no de su estructura interna, lo que hace el diseño más flexible y menos sensible a cambios. Por este motivo se suele decir: “favorecer la composición frente a la herencia”.
***

## 11. Herencia vs. Composición. Se dice que se debe *"favorecer la composición frente a la herencia"*, ¿por qué?
### Respuesta
Se recomienda favorecer la composición frente a la herencia porque la composición genera diseños más flexibles, desacoplados y fáciles de mantener. Mientras que la herencia establece una relación rígida y permanente (A es‑un B), la composición establece una relación más débil y modular (A tiene‑un B). Esto permite construir comportamientos combinando objetos, sin imponer una jerarquía fija que condicione todo el diseño del sistema. La herencia introduce un acoplamiento fuerte entre la clase base y las subclases. Una subclase no solo hereda una interfaz, sino también una implementación concreta, lo que hace que cambios en la clase base puedan afectar de forma indirecta y difícil de prever a todas las subclases. Esto provoca diseños frágiles, especialmente cuando la herencia se utiliza solo para reutilizar código y no porque exista una verdadera relación de especialización conceptual. La composición, en cambio, permite variar el comportamiento en tiempo de ejecución y sustituir componentes sin modificar la jerarquía de clases. Una clase delega parte de su comportamiento a otros objetos, usando sus interfaces públicas, lo que refuerza la encapsulación y reduce dependencias internas. Este enfoque encaja mejor con sistemas extensibles, donde se espera que el software evolucione con nuevos requisitos.
***

## 12. Herencia vs. Composición. Se dice que la *"herencia rompe la encapsulación"*, ¿a qué se refiere esto?
### Respuesta
Cuando se afirma que la herencia rompe la encapsulación, se hace referencia a que las subclases quedan expuestas a detalles internos de la superclase, rompiendo la idea de que una clase debería ocultar su implementación y mostrar solo una interfaz bien definida.
***

## 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en común: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composición, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.
### Respuesta
```Java
// Modelo con herencia
class Persona {
    protected String dni;
    protected String nombre;

    public Persona(String dni, String nombre) {
        this.dni = dni;
        this.nombre = nombre;
    }
}

class Estudiante extends Persona {
    public Estudiante(String dni, String nombre) {
        super(dni, nombre);
    }
}

class Trabajador extends Persona {
    public Trabajador(String dni, String nombre) {
        super(dni, nombre);
    }
}



// Modelo con composición
class DatosPersonales {
    private String dni;
    private String nombre;

    public DatosPersonales(String dni, String nombre) {
        this.dni = dni;
        this.nombre = nombre;
    }

    public String getDni() {
        return dni;
    }

    public String getNombre() {
        return nombre;
    }
}

class Estudiante {
    private DatosPersonales datos;

    public Estudiante(DatosPersonales datos) {
        this.datos = datos;
    }
}

class Trabajador {
    private DatosPersonales datos;

    public Trabajador(DatosPersonales datos) {
        thisdatos = datos;
    }
}
```