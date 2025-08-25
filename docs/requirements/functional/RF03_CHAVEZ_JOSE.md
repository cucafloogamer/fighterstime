### Requerimiento Funcional: Sistema de Combate Básico

Este documento detalla el requerimiento funcional del sistema de combate, basado en la lógica de la clase `Personaje`. El objetivo es simular una batalla por turnos entre dos personajes hasta que uno de ellos sea derrotado, estableciendo así a un ganador.

#### **Mecánicas del Combate**

1.  **Preparación del Combate**: El sistema iniciará el combate con dos objetos `Personaje` previamente configurados.

2.  **Determinación del Turno Inicial**:
    * El combate se desarrollará por turnos.
    * Para el primer turno, el sistema debe comparar la propiedad `velocidad` de ambos personajes.
    * El personaje con el valor de **`velocidad`** más alto atacará primero.
    * En caso de que la `velocidad` sea idéntica, el orden de ataque inicial puede ser predefinido o asignado de manera aleatoria.

3.  **Lógica de Ataque y Daño**:
    * En su turno, un personaje ejecutará una acción de ataque contra el oponente.
    * El daño base del ataque será igual a la propiedad **`ataque`** del personaje atacante.
    * El personaje defensor debe procesar el daño recibido. El sistema llamará al método `recibirDanio()` del personaje defensor, pasando como argumento el valor del `ataque` del oponente.
    * El método `recibirDanio()` calculará el daño real restando la **`defensa`** del defensor del ataque recibido. Es crucial que el daño real resultante no sea un valor negativo.

4.  **Condiciones de Victoria y Finalización**:
    * Después de cada ataque, el sistema debe verificar la propiedad **`vida`** del personaje que recibió el daño.
    * Si la `vida` de un personaje cae a cero o menos, su propiedad **`estaVivo`** debe ser actualizada a `false`.
    * El combate finalizará de inmediato en el momento en que un personaje ya no esté vivo.
    * El personaje que permanezca con **`estaVivo = true`** será declarado como el **vencedor**.
    * Si, en un caso particular, la vida de ambos personajes llega a cero en el mismo turno, el combate se considerará un **empate**.