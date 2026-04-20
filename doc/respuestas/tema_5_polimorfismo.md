# Tema 5. Polimorfismo

## 1. Brevemente, ¿qué es el **"polimorfismo"** y para qué sirve en programación orientada a objetos? ¿qué es la **"sobreescritura"** de métodos?
### Respuesta
El objetivo del polimorfismo es facilitar la extensión de los programas, facilita que esta extensión se haga creando código nuevo frente a editar código existente.

## 2. ¿En qué consiste la **"ligadura dinámica"** o **"enlace tardío"**? ¿qué relación tiene con el polimorfismo? ¿hay que indicarlos explícitamente al programar o depende esto del lenguaje? Compara C++ y Java. Indicalo después también para Python.
### Respuesta


## 3. Pon un ejemplo sencillo en Java, de un `Soldado`, con un método `saluda`, con dos subclases: `Zapador` y `Artillero`, donde `Zapador` sobreescribe el método `saludar`, sustituyendo por completo su comportamiento. Ilustra el funcionamiento del polimorfismo creando un array de `Soldados` de dos tipos y luego recorriéndolo empleando referencias de tipo `Soldado` y llamando a `saludar`.
### Respuesta
``` Java
public class Soldado {
    public void saluda() {
        Systme.out.println("A sus ordenes!");
    }
}

public class Artillero extends Soldado {
    public void saluda() {
        System.out.println("Artillero a sus ordenes!");
    }
}

public class pruebaPolimorfismo {
    public static void pasarRevista(Soldado[] soldados) {
        for(Soldado soldado : soldados) {
            soldado.saluda();
        }
    }
    public static void main(String[] args) {
        Soldado[] solados = new Soldado[2];

        soldados[0] = new Artillero();
        soldados[1] = new Solado();

        pasarRevista(soldados);
    }
}
```

## 4. Si sobreescribo un método, ¿puedo invocar el método base para trabajar a partir de su resultado? Haz que zapador cambie ligeramente la forma de saludar, que salude de forma normal, tal cual hace el soldado base, pero que además añada un "ZAPADOR A SUS ORDENES" ¿qué palabra clave del lenguaje has usado para invocar al método de la clase base?
### Respuesta
``` Java
public class Soldado {
    public void saluda() {
        Systme.out.println("A sus ordenes!");
    }
}

public class Artillero extends Soldado {
    public void saluda() {
        System.out.println("Artillero a sus ordenes!");
    }
}
public class Zapador extends Soldado {
    public void saluda() {
        super.saluda();
        System.out.println("Zapador a sus ordenes!");
    }
}

public class pruebaPolimorfismo {
    public static void pasarRevista(Soldado[] soldados) {
        for(Soldado soldado : soldados) {
            soldado.saluda();
        }
    }
    public static void main(String[] args) {
        Soldado[] solados = new Soldado[3];

        soldados[0] = new Artillero();
        soldados[1] = new Solado();
        soldados[2] = new Zapador();

        pasarRevista(soldados);
    }
}
```

## 5. Al sobreescribir un método en Java, ¿qué restricciones existen sobre los tipos de los parámetros y el tipo de retorno? ¿Qué diferencia hay entre sobreescritura (*overriding*) y sobrecarga (*overloading*)? ¿Para qué sirve la anotación `@Override` y por qué es recomendable usarla siempre?
### Respuesta
``` Java
public class Soldado {
    public void saluda() {
        Systme.out.println("A sus ordenes!");
    }
}

public class Artillero extends Soldado {
    public void saluda() {
        System.out.println("Artillero a sus ordenes!");
    }
}
public class Zapador extends Soldado {
    @Override
    public void saluda() {
        super.saluda();
        System.out.println("Zapador a sus ordenes!");
    }
}

public class pruebaPolimorfismo {
    public static void pasarRevista(Soldado[] soldados) {
        for(Soldado soldado : soldados) {
            soldado.saluda();
        }
    }
    public static void main(String[] args) {
        Soldado[] solados = new Soldado[3];

        soldados[0] = new Artillero();
        soldados[1] = new Solado();
        soldados[2] = new Zapador();

        pasarRevista(soldados);
    }
}
```

## 6. Entonces, cuando se estudia Java, ¿se emplea el polimorfismo desde el principio? Por ejemplo, sobreescribiendo `toString` o sobreescribiendo `equals`, ¿ya estoy usando polimorfismo?
### Respuesta
Sí, por eso se suele utilizar @Override en ellos.

## 7. ¿Qué es una **"clase abstracta"**? ¿Qué es un **"método abstracto"**? ¿Puedo crear instancias de una clase abstracta? Pongamos un ejemplo en Java: Redefinamos `Soldado`, hagamos que, además del método `saluda` que ya tenía, tenga un método `atacar`, que sea abstracto y que cada tipo de soldado haga su acción cuando se le pida atacar. ¿Donde debemos poner `abstract`?
### Respuesta
``` Java
public class Soldado {
    public void saluda() {
        Systme.out.println("A sus ordenes!");
    }

    public abstract void atacar();
}

public class Artillero extends Soldado {
    public void saluda() {
        System.out.println("Artillero a sus ordenes!");
    }

    @Override
    public void atacar() {
        System.out.println("Artillero atacando");
    }
}
public class Zapador extends Soldado {
    @Override
    public void saluda() {
        super.saluda();
        System.out.println("Zapador a sus ordenes!");
    }
    
    @Override
    public void atacar() {
        System.out.println("Zapador atacando");
    }
}

public class pruebaPolimorfismo {
    public static void pasarRevista(Soldado[] soldados) {
        for(Soldado soldado : soldados) {
            soldado.atacar();
        }
    }
    public static void main(String[] args) {
        Soldado[] solados = new Soldado[3];

        soldados[0] = new Artillero();
        soldados[1] = new Solado();
        soldados[2] = new Zapador();

        pasarRevista(soldados);
    }
}
```

## 8. ¿Qué efecto tiene la palabra clave `final` sobre métodos y clases en Java? ¿Cómo se relaciona con el polimorfismo? ¿Conoces algún ejemplo de clase `final` en la propia API estándar de Java?
### Respuesta
`final` en clases -> prohibe la herencia
`final` en métodos -> prohibe aobreescribir

## 9. En Java, qué son las **"interfaces"**? ¿Son como clases abstractas? ¿Una clase puede implementar más de una interfaz?
### Respuesta
# Macanismos en Java
#    - Sobreescritura
#    - Clases abstractas y métodos abstractos
#    - Interfaces
#       - Todos los métodos son abstractos, es decir, sin código (Apartir de cierta versión de Java, se deja meter una implementación "default")
#       - No tienen estado
#       - Un una clase puede implmentar más de una interfaz
```Java
public interface EntradaSalida {
    public String leerEntrada();
    public void escribirEnSalida(String salida);
}

public class TecladoPantalla implements EntradaSalida, MiOtraInterfaz {
    ...
}
```
## 10. Vamos a poner un ejemplo nuevo con polimorfismo. Queremos implementar una clase `Punto`, con un método `calcularDistanciaA`, que permite calcular la distancia a otro `Punto`. Sin embargo, como queremos trabajar con puntos 2D y 3D, haz que ese método sea abstracto y haya dos implementaciones de ese cálculo de distancia. Emplea `instanceof` y *downcasting* para verificar que se recibe un punto compatible y poder calcular correctamente la distancia siempre entre puntos del mismo subtipo. Aprovecha este diseño para crear ahora una clase `Linea`, que acepta `Punto`, sin saber de qué tipo es, y es capaz de dar su longitud independientemente de las dimensiones de sus puntos (las cuales desconoce).
### Respuesta
```Java
public class Punto2D extends Punto {
    private double x,y;
    public Punto2D(double x, double y) {
        this.x = x;
        this.y = y;
    }
    @Override
    public double calcularDistanciaA(Punto otro) {
        if(otro instanceof Punto2D otro2D) {
                return Math.sqrt(Math.pow(this.x - otro2D.x, 2 + Math.pow(this.y - otro2D.y, 2)));
        } else {
            throw new IlegalArgumentException("No puedo calcular la distancia a otro punto de distancia dimensionalidad");
        }
    }
}
public class Punto3D extends Punto {
    private double x,y,z;
    public Punto3D(double x, double y, double z) {
        this.x = x;
        this.y = y;
        this.z = z;
    }
    @Override
    public double calcularDistanciaA(Punto otro) {
        if(otro instanceof Punto3D otro3D) {
                return Math.sqrt(Math.pow(this.x - otro3D.x, 2 + Math.pow(this.y - otro3D.y, 2) + Math.pow(this.z - otro3D.z)));
        } else {
            throw new IlegalArgumentException("No puedo calcular la distancia a otro punto de distancia dimensionalidad");
        }
    }
}
public class Linea {
    private Punto puntoInicial;
    private Punto puntoFinal;

    public Linea(Punto puntoInicial, Punto puntoFinal) {
        this.puntoInicial = puntoInicial;
        this.puntoFinal = puntoFinal;
    }

    public double calcularLongitud() {
        return this.puntoInicial.calcularDistanciaA(this.puntoFinal);
    }

    public static void main(String[] args) {
        Linea l2d = new Linea(new Punto2D(4,5), new Punto2D(7,8));
        Linea l3d = new Linea(new Punto3D(4,5,8), new Punto3D(7,8,10));
    }
}
```
## 11. ¿Qué es la **"herencia de interfaces"** en Java? ¿Existe **"herencia múltiple de interfaces"**? Pon un ejemplo de una interfaz `Fichero` que tenga un método para leer su contenido en forma de `String` y luego dicha interfaz sea extendida por otra que sea `FicheroEscribible` que permita enviar contenido e incluso eliminar el fichero.
### Respuesta
