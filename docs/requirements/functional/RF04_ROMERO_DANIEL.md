# Requerimiento de Personajes #

## Propósito Principal ##

El primer requerimiento del proyecto **FightersTime** se enfoca en el desarrollo del sistema de personajes. El objetivo es crear un sistema **modular** y **flexible** que permita la existencia de tres tipos de personajes jugables: **Guerrero**, **Mago** y **Arquero**. Cada uno debe tener un conjunto de estadísticas y un rol de combate predefinido para ofrecer al jugador opciones estratégicas y un estilo de juego distinto.

## Clases de Personajes y sus Roles ##

Cada clase de personaje está diseñada con un rol específico en mente, reflejado en la distribución de sus atributos.

### Guerrero ###

Representa al "*tanque*" del juego. Su rol es **resistir el daño** y **sobrevivir** en el combate. Se caracteriza por tener **alta vida** y **defensa**, con ataque y velocidad moderados.

### Mago ###

Es el "*hechicero*", un especialista en **infligir una gran cantidad de daño**. Es poderoso, pero vulnerable al daño físico. Se caracteriza por su **alto ataque**, pero **baja vida** y **defensa**. Su velocidad es media.

### Arquero ###

El "*tirador*", un personaje **ágil** y **equilibrado**. Su rol es **atacar a distancia** de forma consistente y **evadir ataques**. Se caracteriza por su **buena velocidad**, con una distribución equilibrada de vida, ataque y defensa.

## Componentes Técnicos Clave ##

Para implementar este concepto, se utiliza una clase central en **Kotlin**: la clase `Personaje`.

### Atributos Fundamentales ###

La clase `Personaje` contiene las propiedades clave que definen a un héroe:

*   `vida`
*   `ataque`
*   `defensa`
*   `velocidad`

### Funciones de Comportamiento ###

La clase también incluye lógica para manejar las interacciones en el juego, como:

*   `recibirDanio()`: Una función que calcula el daño real que un personaje sufre, restando su defensa del ataque del enemigo.
*   `estaVivo()`: Una función que verifica si la vida del personaje es mayor que cero.

### Fábrica de Personajes ###

La creación de los personajes se simplifica mediante un `companion object`. Este objeto funciona como una "*fábrica*" que genera una instancia de la clase `Personaje` con las estadísticas exactas para la clase que el jugador elija (**Guerrero**, **Mago** o **Arquero**).