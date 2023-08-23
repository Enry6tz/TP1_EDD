# Interfaces y Genericidad parametrica


## Interfaces

>En Java, una interfaz es una colección de métodos abstractos (métodos sin implementación) que se utilizan para definir un contrato o conjunto de comportamientos que una clase concreta debe implementar. Las interfaces permiten la implementación de múltiples herencias, lo que facilita la creación de clases que puedan cumplir múltiples roles o funcionalidades.

1. Definicion de una interfaz:
```java
    public interface MiInterfaz{
        void metodo1();
        int metodo2(String parametro);
    }
```
2. Implementacion de una interfaz en una clase:

```java
    public class MiClase implements MiInterfaz{
        public void metodo1(){}

        public int metodo2(String Parametro){
            return 0;
        }
    }
```

3. Uso de una interfaz en Main:

```java
    public class Principal{
        public static void main(String[] args){
            MiInterfaz instancia = new MiClase();
            instancia.metodo1();
            int resultado = instancia.metodo2("Hola");
        }
    }
```
* En eclipse estos archivos pueden quedar distribuidos sencillamente como:
    (tener en cuenta importar `package proyectointerfaz;`)

        └── src/
            └── proyectointerfaz/
                ├── MiInterfaz.java
                ├── MiClase.java
                └── Principal.java

## Genericidad Parametrica

> Genericidad: La genericidad es una técnica que permite definir clases, interfaces y métodos que pueden trabajar con varios tipos de datos de manera segura y flexible. Antes de la introducción de la genericidad en Java, si querías escribir una estructura de datos (como una lista o un conjunto) que almacenara elementos de diferentes tipos, tendrías que crear una versión de esa estructura para cada tipo de dato, lo que resultaba en código duplicado y menos mantenible.

la *Genericidad Parametrica*  es un enfoque en el que se utiliza un tipo generico o parametro de tipo para definir una clase, interfaz o metodo. Esto permite que el mismo codigo fincione con varios tipos de datos diferentes. En Java, se utilizan los corchetes angulares `<T>` para indicar un tipo generico

```java
public class MiClase<T>{
    //...
}
```
> aquí `T` es un parametro de tipo generico. 
 
Se puede usar `T` como un tipo de dato real dentro de la clase `MiClase` pero no esta definido hasta que se instancie la clase con un tipo especifico. 
* Al crear una instancia de `MiClase` con un tipo especifico podria ser:

```java
    MiClase<Integer> instancia = new MiClase<>();
    // Esto significa que la clase queda definida para trabajar con valores de tipo Integer.
```

>La genericidad paramétrica mejora la seguridad del tipo en el código (evita errores de tipo en tiempo de compilación) y promueve la reutilización del código al máximo. Permite que una sola implementación maneje múltiples tipos de datos, lo que lleva a un código más limpio, más eficiente y más fácil de mantener.


### *Ejemplo*: implementando genericidad parametrica en una clase `MiClase`


```java

public class MiClase<T> {
    private T contenido;

    public MiClase(T contenido) {
        this.contenido = contenido;
    }

    public T getContenido() {
        return contenido;
    }

    public void setContenido(T contenido) {
        this.contenido = contenido;
    }

    public void imprimirTipo() {
        System.out.println("El tipo de contenido es: " + contenido.getClass().getSimpleName());
    }
}

```

* Esta clase puede ahora ser usada con diferentes tipos de datos:
  
```java

public class Principal {
    public static void main(String[] args) {
        MiClase<Integer> instanciaEntero = new MiClase<>(42);
        instanciaEntero.imprimirTipo(); 
        // Imprimirá "El tipo de contenido es: Integer"

        MiClase<String> instanciaString = new MiClase<>("Hola");
        instanciaString.imprimirTipo(); 
        // Imprimirá "El tipo de contenido es: String"
    }
}

```
****

# Interfaz usando Genericidad Parametrica

* *Ejemplo*:  
1. implementamos una interfaz pero ahora es con genericidad parametrica

```java
public interface MiInterfaz<T> {
    void agregar(T elemento);
    T obtener(int indice);
}
```
>En este ejemplo, la interfaz `MiInterfaz` se declara con un parámetro de tipo genérico `T`. Los métodos agregar y obtener también utilizan este tipo genérico para indicar el tipo de datos con el que la interfaz debe trabajar. 

2. Implementamos la interfaz de la siguiente manera:

```java

public class MiClase<T> implements MiInterfaz<T> {
    private List<T> elementos = new ArrayList<>();

    @Override
    public void agregar(T elemento) {
        elementos.add(elemento);
    }

    @Override
    public T obtener(int indice) {
        return elementos.get(indice);
    }
}

```
* En este ejemplo, la clase `MiClase` implementa la interfaz `MiInterfaz` utilizando la genericidad paramétrica. Esto permite que `MiClase` trabaje con cualquier tipo de dato que desees.
  
3. Luego, utilizar la interfaz y la clase implementadora de esta manera:
```java
public class Principal {
    public static void main(String[] args) {
        MiInterfaz<String> instanciaString = new MiClase<>();
        instanciaString.agregar("Hola");
        String resultadoString = instanciaString.obtener(0);

        MiInterfaz<Integer> instanciaInteger = new MiClase<>();
        instanciaInteger.agregar(42);
        int resultadoInteger = instanciaInteger.obtener(0);
    }
}
```
* En este ejemplo, creamos instancias de `MiClase` a través de la interfaz `MiInterfaz` con tipos de datos diferentes (String e Integer). La genericidad paramétrica en la interfaz y la clase implementadora permite que puedas trabajar con **diferentes tipos de datos** utilizando el mismo código.
***
**Obs:** *@Override es una anotación en Java que se utiliza antes de un método para indicar que estás sobrescribiendo un método de una clase padre o una interfaz. En otras palabras, estás proporcionando una implementación específica para ese método en la clase actual.*




