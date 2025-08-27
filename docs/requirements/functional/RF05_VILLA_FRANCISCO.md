# RF05: Sistema de Combate por Turnos

**Descripción:**  
El juego debe implementar un sistema de combate básico por turnos entre el personaje del jugador y un enemigo, con una duración máxima de 180 segundos (3 minutos). Este sistema será la mecánica principal de interacción del jugador en las batallas del juego.

**Inicio del Combate:**  
El combate debe iniciar al entrar en una zona designada o al interactuar con un enemigo en el mapa.

**Asignación de Turno:**  
La iniciativa del primer turno será asignada al personaje con mayor Velocidad. Si la velocidad es igual, el turno se asignará aleatoriamente.

**Acciones Disponibles en el Turno del Jugador:**
- **Atacar:**  
  El daño infligido se calculará usando la fórmula:  
  `Daño = (2*Nivel + Control)/5 + 3 * STAB * Tipo1 * Tipo2 * Random`
  - **Nivel:** Nivel actual del personaje.
  - **Control:** Atributo de control del personaje.
  - **STAB:** Bonificación de ataque del mismo tipo (por ejemplo, un ataque de fuego de un mago de fuego).
  - **Tipo1/Tipo2:** Bonificaciones o penalizaciones de tipo (por ejemplo, fuego contra agua).
  - **Random:** Un valor aleatorio para variar el daño.

- **Defender:**  
  El personaje del jugador entrará en una postura defensiva que le permitirá reducir en un 50% el daño del siguiente ataque recibido.

**Actualización de Puntos de Vida:**  
Los puntos de vida (PV) de ambos combatientes (jugador y enemigo) deben actualizarse inmediatamente en la interfaz tras cada acción.

**Finalización del Combate:**  
El combate finalizará cuando los puntos de vida de cualquiera de los dos participantes sea menor o igual a 0, o cuando se agote el tiempo de 180 segundos. En ese momento, se mostrará un mensaje de Victoria o Derrota, según corresponda.

**Animaciones:**  
- Las animaciones de ataque o defensa no deben superar los 2 segundos de duración.
- La animación de victoria o derrota no debe superar los 3 segundos.

**Responsable:** Supported / Francisco Villa  
**Prioridad:** Crítica