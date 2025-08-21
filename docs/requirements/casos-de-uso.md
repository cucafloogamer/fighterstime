# Casos de Uso - FightersTime
## Proyecto Académico - Análisis de Sistemas I

---

## CU-001: Crear Personaje Simple

### Descripción
**Para estudiantes**: Permite practicar la creación de objetos y validación de entrada básica.

### Actores
- Usuario (Jugador/Estudiante probando el código)

### Precondiciones
- El programa está ejecutándose
- El usuario está en el menú principal (texto en consola)

### Flujo Principal (Pasos Simples)
1. **Mostrar menú**: "1. Nuevo Personaje 2. Salir"
2. **Usuario selecciona**: Opción 1
3. **Mostrar clases**: "Elige clase: 1-Guerrero 2-Mago 3-Arquero"
4. **Usuario elige**: Un número del 1 al 3
5. **Mostrar épocas**: "Elige época: 1-Antigua 2-Medieval 3-Moderna"
6. **Usuario elige**: Un número del 1 al 3
7. **Sistema calcula**: Atributos usando tabla simple
8. **Mostrar resultado**: "Tu personaje: Guerrero Medieval - Vida:100, Ataque:20..."
9. **Preguntar**: "¿Guardar este personaje? (s/n)"
10. **Si dice 's'**: Crear objeto Personaje y continuar

### Flujos Alternativos (Casos de Error)
- **Si usuario ingresa número inválido**: Mostrar "Opción no válida, intenta de nuevo"
- **Si usuario presiona Ctrl+C**: Salir del programa
- **Si dice 'n' en paso 9**: Volver al menú principal

### Postcondiciones
- Objeto Personaje creado en memoria
- Listo para usar en combate

### 💡 **Conceptos que Practicas:**
- Validación de entrada con Scanner
- Uso de switch/when para opciones
- Creación de objetos con constructor
- Manejo básico de strings

---

## CU-002: Combate Básico por Turnos

### Descripción
**Para estudiantes**: Permite practicar bucles, condicionales y lógica de juegos simple.

### Actores
- Usuario (Jugador)
- Sistema (Enemigo automático)

### Precondiciones
- Personaje del jugador existe
- Sistema genera un enemigo simple (Orc con stats fijos)

### Flujo Principal (Lógica de Bucle)
1. **Inicializar**: `turnoJugador = true`, mostrar stats de ambos
2. **Bucle de combate**: `while (vidaJugador > 0 && vidaEnemigo > 0)`
3. **Si es turno del jugador**:
   - Mostrar: "Tu turno: 1-Atacar 2-Defender"
   - Leer opción del usuario
   - Si elige 1: calcular daño y restarlo al enemigo
   - Si elige 2: aumentar defensa temporalmente
4. **Si es turno del enemigo**:
   - Enemigo siempre ataca (IA simple)
   - Calcular daño y restarlo al jugador
5. **Cambiar turno**: `turnoJugador = !turnoJugador`
6. **Verificar condición de fin**: Si alguien llega a 0 HP, salir del bucle
7. **Mostrar resultado**: "¡Victoria!" o "¡Derrota!"

### Flujos Alternativos
- **Si usuario ingresa opción inválida**: Mostrar error, repetir turno
- **Si daño calculado es negativo**: Establecer daño mínimo = 1
- **Si usuario quiere huir**: Terminar combate (opcional)

### Postcondiciones
- Combate terminado
- Resultado mostrado al usuario

### 💡 **Conceptos que Practicas:**
- Bucles while con condición compuesta
- Variables booleanas para control de flujo
- Operaciones matemáticas básicas
- Lógica de estado (vida, daño, turnos)

---

## CU-003: Guardar Partida en Archivo

### Descripción
**Para estudiantes**: Permite practicar manejo de archivos, serialización simple y manejo de excepciones.

### Actores
- Usuario (Jugador)

### Precondiciones
- Personaje existe en memoria
- Usuario quiere guardar su progreso

### Flujo Principal (Manejo de Archivos)
1. **Usuario solicita**: Desde menú, elige "Guardar Partida"
2. **Validar datos**: Verificar que personaje no sea null
3. **Crear string**: Convertir datos a formato simple
   ```
   "Guerrero,Medieval,85,20,15,10,1"
   // clase,época,vida,ataque,defensa,velocidad,nivel
   ```
4. **Intentar escribir archivo**:
   ```kotlin
   try {
       File("partida.txt").writeText(datosPersonaje)
       println("Partida guardada exitosamente")
   } catch (e: Exception) {
       println("Error al guardar: ${e.message}")
   }
   ```
5. **Confirmar**: Mostrar mensaje de éxito

### Flujos Alternativos
- **Si archivo no se puede crear**: Mostrar error específico
- **Si personaje es null**: Mostrar "No hay datos para guardar"
- **Si disco lleno**: Manejar excepción y mostrar mensaje

### Postcondiciones
- Archivo "partida.txt" creado o actualizado
- Usuario informado del resultado

### 💡 **Conceptos que Practicas:**
- Try-catch para manejo de excepciones
- Escritura de archivos con File.writeText()
- Conversión de objetos a strings
- Validación de datos antes de procesar

---

## 📊 Ejemplo de Código Simple para Casos de Uso

### CU-001: Ejemplo de Creación de Personaje
```kotlin
// Ejemplo básico para estudiantes
class Personaje(
    val clase: String,
    val epoca: String,
    var vida: Int,
    val ataque: Int,
    val defensa: Int,
    val velocidad: Int
) {
    fun mostrarInfo() {
        println("=== INFORMACIÓN DEL PERSONAJE ===")
        println("Clase: $clase")
        println("Época: $epoca")
        println("Vida: $vida")
        println("Ataque: $ataque")
        println("Defensa: $defensa")
        println("Velocidad: $velocidad")
    }
}

fun crearPersonaje(): Personaje {
    println("Selecciona clase: 1-Guerrero 2-Mago 3-Arquero")
    val claseOpcion = readLine()?.toIntOrNull() ?: 1
    
    val clase = when(claseOpcion) {
        1 -> "Guerrero"
        2 -> "Mago" 
        3 -> "Arquero"
        else -> "Guerrero"
    }
    
    // Tabla simple de stats
    val stats = when(clase) {
        "Guerrero" -> arrayOf(100, 20, 15, 10)  // vida, ataque, defensa, velocidad
        "Mago" -> arrayOf(80, 25, 10, 15)
        "Arquero" -> arrayOf(90, 18, 12, 20)
        else -> arrayOf(100, 15, 15, 15)
    }
    
    return Personaje(clase, "Medieval", stats[0], stats[1], stats[2], stats[3])
}
```

### CU-002: Ejemplo de Combate Simple
```kotlin
fun combateSimple(jugador: Personaje, enemigo: Personaje) {
    var turnoJugador = true
    
    println("¡COMBATE INICIADO!")
    println("${jugador.clase} vs ${enemigo.clase}")
    
    while (jugador.vida > 0 && enemigo.vida > 0) {
        if (turnoJugador) {
            println("\n--- TU TURNO ---")
            println("Tu vida: ${jugador.vida} | Enemigo vida: ${enemigo.vida}")
            println("1. Atacar  2. Defender")
            
            val accion = readLine()?.toIntOrNull() ?: 1
            
            when(accion) {
                1 -> {
                    val daño = maxOf(1, jugador.ataque - enemigo.defensa)
                    enemigo.vida -= daño
                    println("¡Atacas por $daño de daño!")
                }
                2 -> {
                    println("Te defiendes. Próximo ataque reducido.")
                    // Lógica simple de defensa
                }
            }
        } else {
            // Turno del enemigo (IA simple)
            val daño = maxOf(1, enemigo.ataque - jugador.defensa)
            jugador.vida -= daño
            println("El enemigo te ataca por $daño de daño!")
        }
        
        turnoJugador = !turnoJugador  // Cambiar turno
        Thread.sleep(1000)  // Pausa dramática
    }
    
    if (jugador.vida > 0) {
        println("¡VICTORIA!")
    } else {
        println("¡DERROTA!")
    }
}
```

---

## 🎯 Ejercicios Prácticos para Estudiantes

### Ejercicio 1: Validación Básica
Modifica la función `crearPersonaje()` para que:
- No acepte números fuera del rango 1-3
- Pida al usuario que intente de nuevo si ingresa algo inválido

### Ejercicio 2: Mejora el Combate
Agrega a la función `combateSimple()`:
- Una opción "Huir" que termine el combate
- Mostrar el porcentaje de vida restante
- Que el enemigo a veces se defienda en lugar de atacar

### Ejercicio 3: Persistencia
Crea funciones para:
- `guardarPersonaje(personaje: Personaje)` - que escriba a un archivo
- `cargarPersonaje(): Personaje?` - que lea del archivo
- Manejar el caso cuando el archivo no existe

---

## 📝 Notas de Implementación

### Para el Profesor:
- Estos casos de uso están diseñados para enseñar gradualmente
- Cada caso de uso introduce 2-3 conceptos nuevos máximo
- Los ejemplos de código son funcionales y educativos
- Se puede implementar todo en consola antes de agregar interfaz gráfica

### Para los Estudiantes:
- No intenten hacer todo perfecto desde el inicio
- Empiecen con lo básico y vayan agregando funcionalidades
- Prueben cada función individualmente antes de integrar
- ¡Comentar el código es parte del aprendizaje!

---
*Casos de Uso Académicos - Primer Año*  
*Enfoque: Aprendizaje gradual y conceptos fundamentales*
