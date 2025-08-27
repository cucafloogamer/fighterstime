# RF03_01 - Guardado de datos

Descripción: Este sistema  permitirá al jugador crear y guardar personajes en una lista cuando este se encuentre en partida. El maximo de personajes que este podra guardar sera de 3 personajes en la memoria.


cabe mencionar que cada personaje tendra los siguientes atributos: 

- Nombre del personaje <br>
- Clase<br>
- Nivel<br>
- Vida<br>
- Ataque <br>
- Defensa<br>

El sistema permitira que el jugador pueda realizar diferentes acciones con los personajes que este a creado y guardado.
- Guardar personaje: Registra un nuevo personaje
- Lista de personajes: Crea un listado de los personajes que se han creado en base a los atributos.
- Buscar personaje: Busca el personaje a traves de su nombre 
- Eliminar personaje: Elimina un personaje creado/guardado de la lista de personajes.

Este sistema debe asegurar que los personajes creados serán guardados en la memoria de manera correcta mientras que el programa se encuentre en ejecución, es importante que el tiempo de respuesta a esto no sea superior a los 500ms.
En cuanto a la persistencia, este sistema trabaja con un enfoque de almacenamiento en memoria durante la ejecución del programa.

<<<<<<< HEAD:docs/requirements/functional/RF03_01_FLORES_PEDRO.md
En cuanto a la persistencia, este sistema trabaja con un enfoque de almacenamiento en memoria durante la ejecución del programa.

Esto quiere decir que todos los personajes creados y guardados se almacenan en una estructura interna (como una lista de registro).

Ejemplo de codigo sistema de guardado de personajes 


Ejemplo de código sistema de guardado de personajes:

```java
    //Guardar personaje
    fun guardarPersonaje(personaje: Personaje) {
        personajes.add(personaje)
    }
    fun main () {
    val sistema = SistemaGuardado()

    val guerrero = Personaje 1 ("Nombre personaje", "Clase", 1, 10, 20, 30)
    }
```
