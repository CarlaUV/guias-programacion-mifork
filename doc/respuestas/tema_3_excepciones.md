# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.
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

## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?
### Respuesta
Una excepción es un evento que ocurre durante la ejecución de un programa y que interrumpe el flujo normal de las instrucciones.
Se considera un objeto que encapsula información sobre un error o una condición inesperada que el método actual no sabe o no puede resolver por sí mismo.
Surgue de situaciones atípicas. Cuando se implementan no permite indicar más claramente el error.
Cuando los llamamos nos facilita separar la lógica normal de la reacción de manejo de la situacion erronea.

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.
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

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.
### Respuesta

### Lanzar una excepción consiste en crear un objeto de error y entregarlo al sistema de ejecución mediante la palabra throw. Controlar o capturar es el acto de interceptar ese objeto mediante un bloque catch para realizar una acción correctiva. La propagación es el proceso por el cual, si una función no captura la excepción, esta viaja hacia atrás por la pila de llamadas buscando a alguien que la gestione.

### A medida que la excepción se propaga, las funciones en la pila de llamadas finalizan de forma abrupta. No se llega a ejecutar ninguna línea de código posterior al punto donde se produjo el error o la llamada fallida. Estas funciones no se reanudan; simplemente desaparecen de la memoria (pila) como si hubieran terminado por un return forzado.

## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?
### Respuesta

### La principal ventaja frente a C es la limpieza del código. En C, si una función a nivel 5 de profundidad falla, todas las funciones intermedias (nivel 4, 3, 2 y 1) deben incluir código para capturar ese error y devolverlo manualmente hacia arriba.
### Con la propagación de Java, las funciones intermedias pueden ignorar completamente el error si no saben cómo arreglarlo. La excepción "salta" automáticamente por encima de ellas hasta encontrar un manejador competente.

## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?
### Respuesta

### En Java, las excepciones son objetos(heredan de Throwable) que pertenecen a una jerarquía de clases. Al ser objetos, se benefician de la encapsulación, permitiendo agrupar no solo un mensaje de error, sino también datos contextuales del momento del fallo. Esto permite que el manejador reciba una entidad rica en información en lugar de un simple número entero.
### Es posible y recomendable crear excepciones personalizadas mediante la herencia. Al crear una clase que hereda de Exception o RuntimeException, se dota al sistema de nombres de error específicos para el dominio del problema (por ejemplo, SaldoInsuficienteException), lo que hace el código mucho más legible y profesional.

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?
### Respuesta
- Un mensaje(getMessage())
- La traza de la pila(getStackTrace / printStackTrace)
- Ocasionalmente, la causa, es otra exceptcion que es la verdadera causa

## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?
### Respuesta
Sí, se puede tener más de uno
- Sólo se ejecuta uno
- Se va comprobando por orden hasta el primero que encaje
- Se deben poner del más especifico al más general, porque si no, los catch para excepciones específicas no se ejecutarán

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.
### Respuesta
El finally se EJECUTA SIEMPRE que la CPU entre en el bloque try(haya excepciones o no). 
``` Java
try {
    ...
    return 7;
} catch(..) {
    ...
} catch(..) {
    ...
} finally {
    ...
}
```

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?
### Respuesta
Si, puede ir sin catch
- Se ejecuta, puesto que es finally
- Si hubo excepción, como no tenemos catch, se propaga.

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.
### Respuesta
                             | IlegalArgumentException--|
                             |                          |
      No contorladas         | NullPointerException-----|------ RunTimeException |
  No obliga a try/catch      |                          |                        |
                             | ArrayOutOfBoundsException|                        |
                                                                                 |
                             |                                                   |
       Controladas           | AccessDeniedException------------IOException------|------- Exception
  Obliga a hacer try/catch   | 
## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?
### Respuesta
### Cuando tenemos una excepción controlada tenemos dos opciones, manejar la excepción con un try catch o desentendernos del error con el throw mandándolo a quién llame la función (el llamador). Si manejamos la excepción y la función devuelve un valor (por ejemplo, un string en una función para leer un archivo) debemos usar el finally.
### throws en la firma declara que un método puede lanzar ciertas checked exceptions. 
### Sirve para delegar la gestión al llamador, que decidirá capturar o volver a declarar. Es una alternativa a capturar localmente y forma parte del contrato del método.

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.
### Respuesta
``` Java
public String leerFichero(Path p) throws IOException {
    try {
        BufferReader lector = new BafferReader(lector);
    } finally {
        try { lector.close(); } 
        catch (IOException e) { /* registrar y continuar */ }
    }
}
```

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?
### Respuesta
### Por poder podemos, pero el compilador NO nos va a obligar a utilizar el bloque try/catch, aunque no es habitual (a veces te lo pone por documentacion).
### El llamador no está obligado a capturarla; lo hará solo si quiere interceptar para registrar, transformar o continuar.

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?
### Respuesta
### Se recomienda usar excepciones controladas para errores que son ajenos al control del programador (entorno, red, usuario). Se deben evitar para errores que el programador puede prevenir con un simple if (como comprobar si un puntero es nulo).
### No todos los lenguajes tienen ambos tipos. En C++ o Python, todas las excepciones son "no controladas" (el compilador no te obliga a nada). En los lenguajes donde solo existe una opción, la más habitual es el modelo de excepciones no controladas, ya que hace el código menos verboso y más flexible.

## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.
### Respuesta
Si, tiene sentido, puedo relanzar la misma excepción(mediante la referencia al crear la excepcion)
``` Java
    try {

    } catch(NumberforThatException e) {
        throw e; // modifica el stacktrace
    }
```
Envuelve en otra excepción nueva(será causa; ver 17)
``` Java
    try {

    } catch(IOException e) {
        throw new RunTimeException("excepción de E/S", e);
    }
```
Lanza otra excepción totalmente nueva
``` Java
    try {

    } catch(IOException e) {
        throw new AplicationException("error");
    }
```
## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?
### Respuesta
``` Java
    try {

    } catch(IOException e) {
        throw new NetfluxException("error E/S", e);
    }
```
Causa de excepción:
    - Se ve cuando la excepción se muestra por pantalla
            "Excepción externa" (NotFluxException)
            ------------------
            ------------------
            Cause by "Excepción interna" (IOException)