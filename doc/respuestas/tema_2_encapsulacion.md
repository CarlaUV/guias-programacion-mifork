# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.
### Respuesta
La abstracción oculta los detalles de implementación y muestra solo la funcionalidad al usuario.
La encapsulación, tiene que ver con protección; he juntado estado y comportamiento en un artefacto(la clase) y ahora puedo ocultar ciertas partes del exterior.
    - Evito estados no válidos de mis objetos
    - Evito dependencias desde fuera que no quiero
La ocultación de datos es el proceso que garantiza el acceso exclusivo a los datos a los miembros de la clase y brinda integridad a los objetos al evitar cambios intencionales o no intencionados.

## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
### Respuesta
La interfaz pública son los `miembros` que son públicos, es decir que se pueden acceder desde fuera del paquete(sin protected).

## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?
### Respuesta
Si se cambia la interfaz pública tiene más consecuencias que en la parte oculta.
Depende que cuantos usuarios tengas es mas o menos díficil.

## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?
### Respuesta
Las invariantes de clase son todas aquellas condiciones que los objetos deben cumplir para zer válidos durante todas la vida de la instacia.
El tipo que debieran de tener los datos es algo de lo que se ocupa el sistema de tipos.

## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?
### Respuesta
```Java
class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }
}
```

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?
### Respuesta
En Java 
    - Public: clases, atributos y métodos
    - Private: clases internas(no las estamos viendo), atributos y métodos

## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?
### Respuesta
En Java
    - Protected, solo se ve desde "subclases"(Herencia)
    - Package-private o sin modificador, solo se ve desde el paquete
En C++ existen las clases "friend" para poder ver los atributos private

## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.
### Respuesta
```Java
class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }

    public double calcularDistanciaAOtroPunto(Punto otro) {
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?
### Respuesta
Son métodos que permiten dar acceso controlado a los atributos privados del objeto, para obtener o cambiar su valor desde fuera.

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?
### Respuesta
No, esto no es ciberseguridad, es facilitar una programación con menos bugs.

## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?
### Respuesta
Miembro de clase -> No asociado a ninguna instancia; es compartido por todas las instacias. En métodos no hay `this`.
Miembro de instacia -> Está asociado a cada instancia; no son compartidos.

## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?
### Respuesta
Si, a veces, por ejemplo:
    - Un constructor auxiliar oculto
    - Cuando prefiero usar métodos factoria
    - Cuando quiero controlar el núnero de instancias

## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.
### Respuesta
Con la palabra resevada `static`
```Java
class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    /* public static Punto nuevoEn(double x, double y) {
        return new Punto(x,y)
    }

    public static Punto puntoRedondeado(double x, double y) {
        return new Punto(Math.round(x), Math.round(y));
    } */

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }

    public double calcularDistanciaAOtroPunto(Punto otro) {
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    public double getX() {
        return this.x;
    }

    public void setX(x) {
        this.x = x;
    }

    public double getY() {
        return this.y;
    }

    public void setY(y) {
        this.y = y;
    }
}
```

## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 
### Respuesta


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.
### Respuesta
```Java
class Punto {
    /* private double x;
    private double y; */
    private double[] coordenadas = new double[2];

    public Punto(double x, double y) {
        this.coordenadas[0] = x;
        this.coordenadas[1] = y;
    }
    
    public double getX() {
        return this.coordenadas[0];
    }

    public void setX(x) {
        this.coordenadas[0] = x;
    }

    public double getY() {
        return this.coordenadas[1];
    }

    public void setY(y) {
        this.coordenadas[1] = y;
    }

    /* public static Punto nuevoEn(double x, double y) {
        return new Punto(x,y)
    }

    public static Punto puntoRedondeado(double x, double y) {
        return new Punto(Math.round(x), Math.round(y));
    } */

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(this.getX() * this.getX() + this.getY() * this.getY());
    }

    public double calcularDistanciaAOtroPunto(Punto otro) {
        double dx = this.getX() - otro.getX();
        double dy = this.getY() - otro.getY();
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?
### Respuesta
Si los hago públicos
    - para poder garantiza la invariantes de clase
    - Para poder cmabiar la representación interna
    - Convención es:
        - Atributos siempre priovados y emplear métodos de acceso.

## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?
### Respuesta
Inmontable -> su estado no cambia
modificador -> cualquier método que cambia el estado interno, por ejemplo: un setter.
Dos clases inmutables tienen ventajas -> no hacer clases mutables por defecto

## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?
### Respuesta
No.

## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?
### Respuesta
La clase String es inmutable. 

## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java?
### Respuesta
Se pueden comparan con métodos de clase o con operadores de comparación. Depende del método se compara su contenido o identidad.
El método equals se utiliza para comparar si dos objetos son iguales. Por defecto hace comparación por identidad(==), excepto en clases concretas donde se implementa una comparación por contenido, p.ej en String.
Se debe comparar por equals ya que quieres comparar los contenidos por String, y este método asegura ese proceso.

## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 
### Respuesta
Wrapper:
    - Ocurren en lenguajes que tiene tipos primitivo, p.ej Java.
    - Otros lenguajes no tienen tipos primitivos, como Python.
    |_  
      |  int <=> Integer
      |  float <=> Float
      |  char <=> Character
    Ventajas:
        - Añadirle comportamiento
        - Poder usarlos en contextos donde se necesitan objetos. List<T>
    Autoboxing/Unboxing

## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?
### Respuesta
- Enumerado es un tipo con un número determinado de valores posibles.
- En Java en enumerado es una clase, cuyas instancias son finitas, conocidas de antemano y tiene un nombre cada una (valor del enum)

## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.
### Respuesta
``` Java
public enum TipoIVA {
    GENRAL,REDUCIDO;
    private double factor;
    public double aplicar(double cant) {
        return cant * this.factor;
    }
    private TipoIVA(double factor) {
        this.factor = factor;
    }
}
```

## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`
### Respuesta
