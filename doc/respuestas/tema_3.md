# TEMA 3.

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.
### Respuesta
``` Java
float raiz(float num) {
    if(num < 0) {
        return -1.0;
    }
    return Math.sqrt(num);
}
main() {
    var sc = new Scanner(System.in);
    float num = sc.nextLine();
    if(resultado == -1.0) {
        System.error.println("Error....");
    }else {
        printf("%d", resultado);
    }
}
//////////////////////////////////////////////
float raiz(float num, int error) {
    if(num < 0) {
        error = 1;
        return 0;
    }else {
        error = 0;
        return Math.sqrt(num);
    }
}
main() {
    int error = 0;
    var sc = new Scanner(System.in);
    float num = sc.nextLine();
    float resultado = raiz(num,error)

    if(error != 0) {
        System.error.println("Error....");
    }else {
        printf("%d", resultado);
    }
}
```
## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
### Respuesta
Surgue de situaciones atípicas. Cuando se implementan no permite indicar más claramente el error.
Cuando llamamos nos facilita separar la lógica normal de la reacción de manejo de la situacion erronea.


## 3. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
### Respuesta
``` Java
class Calculadora() {
    public static double raiz(double num) {
        if(num < 0.0) {
            throw new IlegalArgumentException("num negativo");
        } else {
            return Math.sqrt(num);
        }
    }
}
class App() {
    main() {
        var sc = new Scanner(System.in);
        double num = sc.nextDouble();
        try {
            double resultado = Calcualdora.raiz(num);
            System.out.println(resultado);
        }catch(IlegalArgumentException e) {
            System.out.println("texto error")
        }
    }
}
```
## 4. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
### Respuesta


## 6. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
### Respuesta

## 7. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
### Respuesta
- Un mensaje(getMessage())
- La traza de la pila(getStackTrace / printStackTrace)
- Ocasionalmente, la causa, es otra exceptcion que es la verdadera causa