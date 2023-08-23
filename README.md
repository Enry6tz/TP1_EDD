## Interfaces y Genericidad parametrica

En Java, una interfaz es una colección de métodos abstractos (métodos sin implementación) que se utilizan para definir un contrato o conjunto de comportamientos que una clase concreta debe implementar. Las interfaces permiten la implementación de múltiples herencias, lo que facilita la creación de clases que puedan cumplir múltiples roles o funcionalidades.

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