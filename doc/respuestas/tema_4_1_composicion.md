Estamos hablando de dependencia(ej: Punto depende de String y StringBuilder), NO de composición; ya que se 
# Tema 4.1. Composición


## 1. En C, podemos crear estructuras mayores **componiendo** unas con otras, que suelen describirse como "A tiene-un/tiene-varios B". Pon un ejemplo, empleando `struct`, de una línea de puntos, donde puntos tienen dos coordenadas (`x` e `y`), y la línea esta hecha de dos puntos. Incluye una función para calcular la distancia entre puntos y otra para hallar la longitud de una línea.
### Respuesta
```c
    struct Punto {
        double x;
        double y;
    };
    struct Linea {
        struct Punto p1;
        struct Punto p2;
    };
    double distancia(struct Punto p1, struct Punto p2) {
        ...
    }
    double longitud(struct Linea l) {
        return distancia(l.p1, l.p2);
    }
```

## 2. Ahora transforma ese ejemplo a orientación a objetos con Java, para tener un primer ejemplo de **composición** en orientación a objetos. Crea una clase `Punto`, y una clase `Linea`. La clase `Punto` debe tener un método para calcular distancia a otro `Punto` y `Linea` debe tener un método para calcular su longitud. Gracias a la ocultación de información, supera a C, garantizando que los puntos sean inmutables, al igual que la línea, que una vez creada, no queremos que se modifique de qué a qué puntos va dicha línea.  
### Respuesta
```java
    class Punto() {
        private double x;
        private double y;

        public Punto(double x, double y) {
            this.x = x;
            this.y = y;
        }
        // encapsulado dentro de de Punto metemos la función distancia
        public distancia(Punto p2) {
            return Math.sqrt(Math.abs(this.x-p2.x)*Math.abs(this.x-p2.x) + Math.abs(this.y-p2.y)*Math.abs(this.y-p2.y));
        }
    }
    class Linea {
        private Punto p1;
        private Punto p2;
        
        public Linea(Punto p1, Punto p2) {
            this.p1 = p1;
            this.p2 = p2;
        }
        void getP1() {
            return p1;
        }
        void getP2() {
            return p2;
        }
        Punto setP1(p1) {
            this.p1 = p1;
        }
        Punto setP2() {
            this.p2 = p2;
        }

        public longitud() {
            return this.p1.distancia(this.p2);
        }
    }
```

## 3. ¿Qué significa la **multiplicidad** en la composición? En el ejemplo anterior, ¿cuál es la multiplicidad entre `Linea` y `Punto`? Indícalo expresando la multiplicidad en ambas direcciones, de `Linea` a `Punto` y de `Punto` a `Linea`.
### Respuesta
La multiplicidad es la cualidad multiple entre clases.
En el ejemplo anterior una linea tiene como mínimo y como máximo 2 puntos.
Un punto puede tener como mínimo 0 lineas y como máximo n.


## 4. ¿Qué significa composición **fuerte** y composición **débil**? ¿Qué consecuencia implica en relación al ciclo de vida de los objetos? Indica a cuál solemos referirnos como **"asociación o agregación"** y a cuál como **"composición"** propiamente.
### Respuesta
Composición fuerte vs débil
Fuerte -> El contenedor (pj Linea) es el que contiene(pj Punto) y estos no viven más allá del contendor.
El ciclo de vida del contenido está vinculado al contendor.
Débil -> El contendor y contenido tienen ciclos de vida independientes (pj los objetos Punto pueden vivir sin estar en objetos línea)
En el ejemplo anterior sería compisición débil.
En UML hablamos de composición propiamente hace referencia a la fuerte y asociación o agregación hace referencia a la composición débil.

## 5. Cuando una clase usa a otra al recibirla o devolverla como parámetro en algún método, al hacer `new` dentro de un método, o al usarlas como variables locales, ¿hablamos de composición o de **"dependencia"**?
### Respuesta
necesita que otra clase exista para poder ejecutarse.
No toda la dependencia es composición pero toda la composición es dependencia.
ej:
```java
    class Punto() {
        ...
        public String toString() {
            StringBuilder sb = new StringBuilder();
        }
    }
    class OperadorFichero{
        public static String leerFichero(Path p) {
            ...
        }
    }
```
Estamos hablando de dependencia(ej: Punto depende de String y StringBuilder), NO de composición; ya que se 


## 6. En el ejemplo anterior de línea y punto, programa la relación entre `Linea` y `Punto` de dos formas. Una **como composición fuerte**, donde el ciclo de vida de los puntos está ligado al de Linea y otra **como composición débil**, donde no.
### Respuesta
COMPOSICIÓN FUERTE
```java
class Linea {
    private Punto p1;
    private Punto p2;

    public Linea(double x1, double y1, double x2, double y2) {
        this.p1 = new Punto(x1, y1);
        this.p2 = new Punto(x2, y2);
    }
}
```

## 7. En Java, en la composición fuerte, ¿cuando el contenedor destruye los objetos? No se observa que `Linea` destruya los `Punto` explícitamente, ¿Por qué?
### Respuesta
En Java, la vida de Punto termina cuando es inacesible, y en el ejemplo ocurre cuando Linea deja de serlo a su vez. Por tanto cuando linea "es basura" también lo serán sus Puntos y serán eliminados de memoria por el recolector de basura.

## 8. Pon un ejemplo de composicion débil entre un departamento que tiene varios profesores. Implementa dos composiciones a la vez: entre el departamento y todos sus profesores y entre el departamento y su director, que es un profesor del departamento. Siempre debe haber un director en el departamento desde el inicio. Lanza excepciones si se viola la invariante. Emplea arrays primitivos de Java, estilo `Profesor[]`, con máximo 50, pero no rompas la encapsulación, no desveles que estás empleando un array, permite añadir un `Profesor` al final de la lista, y eliminar un profesor dada su posición. Da acceso a los profesores con un método para saber cuántos hay y otro para obtener un profesor por posición. El director se puede cambiar por otro profesor del departamento. Sin embargo, ten en cuenta esta invariante de clase: el director debe formar siempre parte de la lista de profesores, es decir, ten cuidado al cambiar el director o al eliminar un profesor.
### Respuesta
```java
    class Profesor {
        private String nombre;

        public Profesor(String nombre) {
            this.nombre = nombre;
        }
    }
    class Departamento {
        // Composición débil 1:
        // 1 Departamento como mínimo 0 y como máximo n Profesor
        // 1 Profesor como mínimo 0 y como máximo n Departamentos
        private Profesor[] profesores = new Profesor[50];
        private int numProfesores = 0;

        // composición débil 2
        // 1 Departamento tiene como mínimo 1 y como máximo 1 Profesor Director
        // 1 Profesor puede ser director como mínimo de 0 y como máximo de n Departamentos
        private Profesor director;

        public Departamento(Profesor Director) {
            // 0. Si director es null lanzamos IAE
            // 1. añadirmos el director al conjunto de Profesores
            // 2. Establecemos ese profesor como director.
        }

        public int getNumProfesores() {
            return this.numProfesores;
        }
        public Profesor getProfesor(int pos) {
            // 0. Validamos pos, y si no valida lanzamos IAE
            return this.profesores[pos];
        }
        public void addProfesor(Profesor p) {
            // 0. Si ya no hay más sitio lanzar IIOBE (ArrayIndexOutOfBoundsException)
        }
        public void eliminarProfesor(int pos) {
            // 0. Si pos no está en el rango correcto (0 - numProfesores), lanzar IAE
            // 1. Si el profesor en pos ES EL DIRECTOR, lanzar IAE  
        }
        public void cambiarDirector(Profesor nuevoDirector) {
            // 0. Si nuevo Director es nnull, IAE
            // 1. Si nuevoDirectro no lo encuentro (bucle de busqueda), lanzo IAE, diciendo que hay que meterlo en el departamento de nuevo
        }
        public Profesor getDirector() {
            return this.director;
        }
        // No se debería de devolver un array de Profesores ya que da problemas de tratamiento y seguridad (INAVARIANTE DE CLASE)
    }
```
Hay dos composiciones débiles y no es expone el array al exterior.
En los métodos que gestiona el departamento se controla que no se viole la invariante de clase.

## 9. En Java, existen también `List`, cambia y muestra cómo sería el código anterior empleando `List` en vez de arrays primitivos. ¿Qué parte del código original te has ahorrado? Además, fíjate en el método `getProfesor(int pos)`: si en su lugar existiera un método que devolviera todos los profesores a la vez, ¿qué problema tendría devolver directamente la lista interna? ¿Cómo lo resolverías?
### Respuesta
```java
    class Profesor {
        private String nombre;

        public Profesor(String nombre) {
            this.nombre = nombre;
        }
    }
    class Departamento {
        // Composición débil 1:
        // 1 Departamento como mínimo 0 y como máximo n Profesor
        // 1 Profesor como mínimo 0 y como máximo n Departamentos
        private Profesor[] profesores = new Profesor[50];
        private int numProfesores = 0;

        // composiciñon debil 1 (version con list):
        private List<Profesor> profesores = new ArrayList<>();

        // composición débil 2
        // 1 Departamento tiene como mínimo 1 y como máximo 1 Profesor Director
        // 1 Profesor puede ser director como mínimo de 0 y como máximo de n Departamentos
        private Profesor director;

        public Departamento(Profesor Director) {
            // 0. Si director es null lanzamos IAE
            // 1. añadirmos el director al conjunto de Profesores
            // 2. Establecemos ese profesor como director.
        }

        public int getNumProfesores() {
            return this.numProfesores;
        }
        public Profesor getProfesor(int pos) {
            // 0. Validamos pos, y si no valida lanzamos IAE
            return this.profesores[pos];
        }
        public void addProfesor(Profesor p) {
            // 0. Si ya no hay más sitio lanzar IIOBE (ArrayIndexOutOfBoundsException)
        }
        public void eliminarProfesor(int pos) {
            // 0. Si pos no está en el rango correcto (0 - numProfesores), lanzar IAE
            // 1. Si el profesor en pos ES EL DIRECTOR, lanzar IAE
            // 2. Eliminar el elemento pos en array (duble de copia del siguiente y establecer a null la ultima posición usada)  
        }
        public void cambiarDirector(Profesor nuevoDirector) {
            // 0. Si nuevo Director es nnull, IAE
            // 1. Si nuevoDirectro no lo encuentro (bucle de busqueda), lanzo IAE, diciendo que hay que meterlo en el departamento de nuevo
        }
        public Profesor getDirector() {
            return this.director;
        }
        // No se debería de devolver un array de Profesores ya que da problemas de tratamiento y seguridad (INVARIANTE DE CLASE)
        // Si se devuelve la List<Profesor> -> la lista es mutable, perdemos el control sobre la variante de clase
        // si insisto en que me gusta est ainterfaz, pero quiero garantizar que solo se use para recorrerlo y no modificar, puedo;
        
        // 1- Devolver una copia de la lista
        // solución clásica, con copia (penlización pequela en rendimiento)
        // return new ArrayList<>(this.profesores);
        // solución alternativa, sin copia
        // return Collection.unmodificableList(this.profesores);
        // 2- Deolver un envoltorio no mutable
    }
```
Con `List<Profesor>`
    1- No cambia la interfaz pública
    2- Es más fácil implementar algunos métodos, delegando en métodos de List 
    3- Si se devuelve hay que devolver una copia para proteger la invariante de clase

## 10. Al igual que ocurre con las excepciones en Java, que pueden encerrar causas (que son excepciones), de forma recursiva, suponen un tipo especial de composiciones, denominadas composiciones recursivas. Pon un ejemplo en Java de una `Persona`, que sea inmutable, y que tiene una madre, que es otra `Persona`. Haz un main con un ejemplo de uso con una familia de personas, desde el nieto hasta la abuela. Enumera algún otro ejemplo clásico de composiciones recursivas.
### Respuesta

## 11. ¿Qué son las relaciones de composición "bidireccionales"? ¿Qué habría que hacer para implementar este tipo de relación en el ejemplo de `Profesor` y `Departamento`?
### Respuesta
