# Fighter's Time - Proyecto Académico

**Visión Unificada para Análisis de Sistemas**

## Descripción del Proyecto
Fighter's Time es un juego de rol simple para dispositivos móviles donde los jugadores controlan personajes de diferentes épocas históricas en batallas por turnos. Este proyecto está diseñado como ejercicio académico para estudiantes de programación y análisis de sistemas.

---

## Características Principales (Versión Académica)

### 1. Sistema de Personajes Básico
* **3 Clases Principales:** Guerrero, Mago, Arquero
* **Atributos Simples:**
    * Vida (HP)
    * Ataque
    * Defensa
    * Velocidad
* **3 Épocas:** Antigua, Medieval, Moderna

### 2. Sistema de Combate Simplificado
* **Combate por Turnos:** Cada jugador elige una acción por turno.
* **Acciones Básicas:**
    * Atacar
    * Defender
    * Usar Ítem
    * Habilidad Especial
* **Cálculo de Daño:** Ataque del atacante - Defensa del defensor

### 3. Estructura del Juego
* **Menú Principal:** Nuevo Juego, Continuar, Configuración
* **Selección de Personaje:** Elegir clase y época
* **Modo Historia:** 5 niveles con enemigos progresivamente más difíciles
* **Sistema de Guardado:** Guardar progreso del jugador

### 4. Tecnologías Propuestas
* **Frontend:** Kotlin (multiplataforma)
* **Base de Datos Local:** Firebase
* **Estructura:** Patrón MVC (Modelo-Vista-Controlador)

---

## Módulos del Sistema

### Módulo 1: Gestión de Personajes
* Clase Personaje
* Atributos y métodos básicos
* Sistema de creación de personajes

### Módulo 2: Sistema de Combate
* Lógica de turnos
* Cálculo de daño
* Condiciones de victoria/derrota

### Módulo 3: Interfaz de Usuario
* Pantallas principales
* Menús de navegación
* Mostrar información del personaje

### Módulo 4: Persistencia de Datos
* Guardado de progreso
* Carga de partidas
* Configuraciones del juego

### Módulo 5: Lógica del Juego
* Flujo de niveles
* Progresión del jugador
* Sistema de recompensas básico

---

## Funcionalidades Mínimas Viables (MVP)

### Versión 1.0 - Básica
1.  Crear personaje con clase y época.
2.  Combate 1vs1 contra un enemigo.
3.  Sistema de turnos funcional.
4.  Pantalla de victoria/derrota.
5.  Guardado básico.

### Versión 2.0 - Mejorada
1.  5 niveles de historia.
2.  Diferentes enemigos por nivel.
3.  Sistema de experiencia básico.
4.  Mejores gráficos e interfaz.
5.  Sonidos básicos.
