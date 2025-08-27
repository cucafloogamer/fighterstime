## descripcion general requerimientos

## ¿Qué vamos a hacer?
Una **app Android súper simple** donde puedes:
1. ✅ Crear un personaje (Guerrero, Mago o Arquero)
2. ✅ Pelear contra un enemigo básico
3. ✅ Guardar tu personaje en el celular


### Pantalla 1: Menú Principal
- Botón "Crear Personaje"
- Botón "Combate" 
- Botón "Salir"

### Pantalla 2: Crear Personaje
- 3 botones: Guerrero, Mago, Arquero
- Mostrar números: Vida, Ataque, Defensa, Velocidad
- Botón "Crear"

### Pantalla 3: Combate
- Mostrar vida tuya y del enemigo
- Botón "Atacar"
- Botón "Defenderse"
- Mostrar "Ganaste" o "Perdiste"

### DESCRIPCIÓN SISTEMA DE COMBATE (PVP PVE)

### PVE
Sistema PVE el cual demostrará un combate contra un personaje npc, enemigo basico combate por turnos, donde el jugador puede tomar decisiones ya sea de atacar, defenderse o ocupar un objeto, el cual gastará un turno y no podrá hacer nada hasta que el enemigo ocupe su turno, el enemigo solo puede atacar o fortalecerse y tendra habilidades pasivas que lo ayudarán contra el jugador cada luchador tendra un numero base de defensa, el cual, absorberá X cantidad de daño, depenediendo de el ataque que reciba, una vez se rompa o se nullifique esa defensa, el personaje podrá recibir daño en su totalidad.

Jugador: El jugador tendra la opcion de atacar, la cual dañará la defensa base de quien recibe el ataque, una vez esta defensa se acabe, le restará vida a el enemigo, el jugador puede causar daño critico, o puede ocupar distintos items o habilidades para potenciar más su ataque o fortalecer su defensa. Dependiendo de la habilidad pasiva de el personaje, tendrá más defensa a distintos tipos de ataque por ejemplo:

Un vikingo naturalmente tendrá mas defensa fisica, por lo tanto, se le otorga un numero alto de defensa base, los ataques directos no serán muy eficases contra este.
Por otro lado, el mago no tendrá buena defensa fisica, pero será más dificil que le afecten daño especial ya sea por habilidades como paralizar o otras habilidades que nullifiquen sus movimientos, este también puede infligir daño especial a el vikingo, el cual sería eficaz contra este.

Habilidades pasivas: distintos enemigos serán más eficaces dependiendo de el tipo de personaje que ocupa el jugador, vea el ejemplo de el mago contra el vikingo para tener una idea basica de como será este sistema.
Las habilidades pasivas tambien serán distintas dependiendo de el personaje, por ejemplo, personajes con "Resistencia" pueden continuar peleando aunque su vida llegue a 0 por dos turnos o una vez su vida llegue a 0, se activa esta habilidad y se recupera un 20% de su vida total.

#### PVP

El combate PVP seguirá las mismas reglas que el PVE, pero esta vez se tienen en tomar en cuenta los items, equipamientos, habilidades especiales y pasivas que estos personajes tengan en contra el otro. por temas de balance y mayor satisfacción, no habrá "Hard counters" contra un personaje en especifico, cada jugador puede mejorar y equipar su personaje con un item para completar un kit que le ayude a enfrentar su oponente.
Las condiciones de pelea tambien serán por turnos, pero con un tiempo limite de 3 minutos por pelea, (180s) para evitar que las peleas duren para siempre, en caso de que se acabe el tiempo, el jugador que causó más daño será el ganador.
Para lograr la victoria el jugador tendrá que considerar las habilidades, fuerzas y debilidades de su personaje, y crear un kit basado en su personaje.

## ⏰ Cronograma Realista:
- **Semanas 1-2**: Crear personaje
- **Semanas 3-5**: Combate básico  
- **Semana 6**: Guardar datos
- **Semanas 7-8**: Pulir y probar

## �️ Tecnología:
- **Kotlin** (lenguaje)
- **Android Studio** (programa para programar)
- **3 pantallas** (Activities)
- **SharedPreferences** (para guardar datos)
