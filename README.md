# HashSet-en-Java

Este repositorio contendrá información aprendida en el taller de OpenWebinars sobre la colección HashSet en java.

Para empezar hay que tener claro que HashSet lo que hace es almacenar una serie de valores en una tabla hash, 
y lo hace de manera DESORDENADA. Esta clase realiza un ordenamiento interno mediente el hashcode del elemento. 

HashSet tiene múltiples ventajas:
  -Mejor rendimiento que cualquier colección
  -Permite insertar valores nulos
  -Realiza las operaciones básicas
  -Se mejora aun más el rendimiento si se establece una capacidad inicial
  
Pongamos un ejemplo: vamos a almacenar un grupo de atletas, todos con la misma edad.

Para ello definimos un objeto llamado Atletas
```java
public class Atletas {
    private int age;
    private String name;

    Atletas(String name, int age){
    	this.name = name;
    	this.age = age;   
    }
}
```

Creamos algunos atletas y los insertamos en un HashSet
```java
Atleta person1 = new Atleta("Juan",18);
Atleta person2 = new Atleta("Miguel",25);
Atleta person3 = new Atleta("Luis",18);
Atleta person4 = new Atleta("Luis",18);
        
HashSet people = new HashSet();
people.add(person1);
people.add(person2);
people.add(person3);
people.add(person4);
```

Si verificamos el tamaño de people, con el método .size() veremos que nos devuelve 4, ya que hemos insertado 4 elementos

Ahora vamos con lo importante. Como HashSet no sigue ningún orden para guardar los objetos (como ya hemos dicho antes)
podemos sobrecargar sus métodos a nuestro antojo. Por ejemplo, vamos a sobrecargar el método .equals() para que solo
podemos almacenar un atleta con el mismo nombre y edad, es decir, que no esté repetido.
```java
@Override
public boolean equals(Object o) {
  if (o instanceof Atletas) {
    Atletas p = (Atletas) o;
    return this.name.equals(p.name);
  } else {
    return false;
  }
}
```
De igual manera sobrescribimos el método .hashCode(). Para generar el hascode utilizamos la variable edad y la longitud del String, consiguiendo así un entero.
```java
@Override
public int hashCode() {
  return age * this.name.length();
}
```
Ahora, una vez sobrescritos los métodos .hashCode() y .equals(), si verificamos el tamaño del HashSet alumnos veremos que nos devuelve «3» ya que, si hay un elemento igual, el metodo .add() devolvera false.
Una cosa que hay que tener en cuenta es que si se sobreescribe solo uno de sus metodos ya sea .hashCode() o .equals() no tendremos el comportamiento deseado. Hay que sobrescribir los dos.
