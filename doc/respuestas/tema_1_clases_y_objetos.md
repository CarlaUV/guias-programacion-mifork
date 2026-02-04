# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta
- Abstracción:
Es un mecanismo que permite tratar temas complejos para facilitar el cambio.
El proceso de abstracción permite seleccionar las características relevantes dentro de un conjunto e identificar comportamientos comunes para definir nuevos tipos de entidades en el mundo real.
- Encapsulamiento:
Permite unir estado y comportamiento en una misma unidad y poder ocultar las partes de la misma.
Significa reunir todos los elementos que pueden considerarse pertenecientes a una misma entidad, al mismo nivel de abstracción.
- Polimorfismo: Comportamientos diferentes, asociados a objetos distintos, pueden compartir el mismo nombre; al llamarlos por ese nombre se utilizará el comportamiento correspondiente al objeto que se esté usando.
- Herencia:
Permite establecer jerarquías.
Las clases no se encuentran aisladas, sino que se relacionan entre sí, formando una jerarquía de clasificación. Los objetos heredan las propiedades y el comportamiento de todas las clases a las que pertenecen.

- Composición: 

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta
JavaScript, Python --> Dinámicos
C#, Java (con GC y con máquina virtual) / R, C++ (sin GC) --> Compilados

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta
Antes de la programación estructurada estaba la programación en ensamblador (secuencia, salto arbitrario (GOTO)).
La programación estructurada es un paradigma de programación orientado a mejorar la claridad, calidad y tiempo de desarrollo de un programa de computadora recurriendo únicamente a subrutinas y a tres estructuras de control básicas: secuencia, selección (if y switch) e iteración (bucles for y while). 
La programación modular es un paradigma de programación que consiste en dividir un programa en módulos o subprogramas con el fin de hacerlo más legible y manejable.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta
Los tres elementos que definen a un objeto son: la identidad (dirección de memoria), el comportamiento (métodos, las funciones que todos los objetos de esa clase pueden hacer) y el estado (atributo, en structs eran campos).

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta
Clase --> Molde para crear instancias durante la ejecución. Define la estructura del estado.
Una clase es una especie de "plantilla" en la que se definen los atributos y métodos predeterminados de un tipo de objeto. Esta plantilla se crea para poder crear objetos fácilmente. No es lo mismo que un objeto.
Objeto --> Variables de tipo 'alguna clase' con un estado concreto de sus atributos.
Una instancia es un bloque de memoria, que contiene la referencia a un objeto. En otras palabras, la instancia mantendrá la dirección del bloque de memoria de inicio donde se almacena el objeto.
Si, todos los lenguajes orientados a objetos manejan el concepto de clase.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta
Los objetos de guardan en la memria de montículo(heap). La memoria de montículo es una parte de la memoría de java.
No, dependiendo del lenguaje de programción es diferente. Por ejemplo en c++ los objetos se pueden guardar o en el montículo(heap) o en stack.
La recolección de basura es un proceso que permite liberar memoria ocupada por objetos que ya no son necesarios en un programa. Esto ayuda a prevenir fugas de memoria y mejora el rendimiento del sistema.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta
un método es una subrutina cuyo código es definido en una clase y puede pertenecer tanto a una clase, como es el caso de los métodos de clase o estáticos, como a un objeto, como es el caso de los métodos de instancia.
La sobrecarga es un concepto que permite a los desarrolladores definir múltiples métodos con el mismo nombre en una clase, pero con diferentes parámetros. Esto significa que los métodos pueden realizar tareas similares, pero con diferentes tipos de datos o cantidades de parámetros.

## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta
```c
struct Punto {
    int x;
    int y;
}

double calcularDistanciaAOrigen(Punto p) {
    return sqrt((p.x*p.x) + (p.y*p.y));
}
```
```java
class Punto {
    double x = 2.5;
    double y = 5.7;
    public static void main() {
        var distancia = calculaDistanciaAOrigen();
    }
    public double calculaDistanciaAOrigen() {
        return Math.sqrt((x*x) + (y*y));
    }
}
```
## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta
En Java, el punto de entrada de un programa es la ubicación específica donde la Máquina Virtual Java (Java Virtual Machine, JVM) comienza a ejecutar el programa.
La palabra reservada `static` es un modificador de acceso usado por métodos y atributos. Se puede acceder a los métodos y/o atributos estaticos pueden acceder a ellos sin tener que crean un objeto de una clase. No es exclusivo del método main.
Se utiliza con `final` ya que los metodos, clases y/o métodos que utilizan `final` no se pueden sobreescribir una vez declarados.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta
Para compilar el programa se utiliza el comando `javac` (javac miprograma.java) y para ejeculartlo se utiliza `java` (java miprograma.java).
Si es un lenguaje compilado a bytecode (clase Java), que puede ejecutarse en cualquier máquina virtual Java (JVM) sin importar la arquitectura de la computadora subyacente. 
La maquina virtual se ejecuta como un proceso normal dentro de un sistema operativo sirviendo de enlace entre un lenguaje de programación y el sistema operativo, realizando una interpretación u otra técnica de enlace entre fuente y código máquina.
El bytecode Java se encuentra dentro del archivo de extensión .class y es el tipo de instrucciones que la máquina virtual Java (JVM) espera recibir para posteriormente ser compiladas a lenguaje de máquina mediante un compilador JIT a la hora de su ejecución.
El archivo .class es una archivo que contiene el bytecode de java, que como se dijo previamente, se ejecuta con la máquina virtual de java. 

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta
`New` es una palabra reservada que se utiliza para crear nuevos objetos.
Un constructor es una subrutina cuya misión es inicializar un objeto de una clase. En el constructor se asignan los valores iniciales del nuevo objeto.
var empleado = new Empleado("*nombre*", "*apellidos*", "*DNI*");

## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta
`this` es una palabra reservada que hace referencia al objeto actual de un método o contructor dentro de una clase.
No se llama igual en todos los lenguajes.

```java
class Punto {
    double x = 2.5;
    double y = 5.7;
    public static void main() {
        var distancia = calculaDistanciaAOrigen();
    }
    public double calculaDistanciaAOrigen() {
        return Math.sqrt((this.x*this.x) + (this.y*this.y));
    }
}
```

## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta
```java
class Punto {
    double x;
    double y;
    public static void main() {
        var distancia = calculaDistanciaAOrigen();
        Punto punto1 = new Punto(4.3,8.9);
        Punto punto2 = new Punto(2.4,6.1);
        punto1.distanciaA(punto2);
    }
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    public double calculaDistanciaAOrigen() {
        return Math.sqrt((this.x*this.x) + (this.y*this.y));
    }
    public double distanciaA(Punto punto) {
        return Math.sqrt((Math.abs(this.x-punto.x)*Math.abs(this.x-punto.x))+(Math.abs(this.y-punto.y)*Math.abs(this.y-punto.y)));
    }
}
```

## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta
Es un método de la clase Object(el cual todas las clases contienen) el cual se llama y obtiene su instancia y se obtiene su representación en String.
Si, por ejemplo en C#.

System.out.println(punto.toString());

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?

### Respuesta
No, ya que en C un stuct es una colección de datos "publicos" y no tiene ninguna otra característica de las clases como: métodos, constructores, abstracción, etc.
Le hace falta abstracción, polimorfismo encapsulamiento y herencia.

## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta
```c
#include <math.h>
#include <io.h>
typedef struct Punto {
    double x;
    double y;
} Punto;

void main() {
    Punto punto1 = {2.5, 5.7};
    Punto punto2 = {6.5, 3.7};
    double distancia = calculaDistanciaAOrigen(punto1);
    printf("%d\n", distanciaA(punto1, punto2));
}
double calculaDistanciaAOrigen(Punto punto) {
    return sqrtd((punto.x*punto.x) + (punto.y*punto.y));
}
double distanciaA(Punto punto1, Punto punto2) {
    return sqrtd((absd(punto1.x-punto2.x)*absd(punto1.x-punto2.x))+(absd(punto1.y-punto2.y)*absd(punto1.y-punto2.y)));
}
```