# RF03_03 - Base de Datos para Personajes Guardados

**Responsable:** Juan Beleño  
**Requerimiento:** RF03.03 - Base de datos que contenga la información personajes guardados  
**Tecnología:** Android Studio + Kotlin + Room Database  

---

## 📋 ¿Qué tengo que hacer?

Crear una **base de datos súper simple** en Android para que la app pueda:
1. ✅ **Guardar personajes** que crea el usuario
2. ✅ **Recordar personajes** cuando se abre la app
3. ✅ **Mostrar lista** de personajes guardados

---

## 🗄️ Estructura de la Base de Datos

### Solo 1 Tabla Simple: `personajes`

```sql
CREATE TABLE personajes (
    id INTEGER PRIMARY KEY,
    nombre TEXT NOT NULL,
    clase TEXT NOT NULL,        -- "Guerrero", "Mago", "Arquero"
    vida INTEGER DEFAULT 100,
    ataque INTEGER,
    defensa INTEGER,
    velocidad INTEGER
);
```

**Ejemplo de datos:**
```
id | nombre    | clase    | vida | ataque | defensa | velocidad
1  | "Arturo"  | "Guerrero"| 100  | 15     | 12      | 8
2  | "Merlín"  | "Mago"    | 100  | 20     | 6       | 10
```

---

## 🔧 Código Kotlin (Para Copiar y Pegar)

### 1. Clase Personaje
```kotlin
@Entity(tableName = "personajes")
data class Personaje(
    @PrimaryKey(autoGenerate = true)
    val id: Int = 0,
    val nombre: String,
    val clase: String,  // "Guerrero", "Mago", "Arquero"
    val vida: Int = 100,
    val ataque: Int,
    val defensa: Int,
    val velocidad: Int
)
```

### 2. DAO - Para Guardar y Buscar
```kotlin
@Dao
interface PersonajeDao {
    
    // Guardar un personaje nuevo
    @Insert
    fun guardarPersonaje(personaje: Personaje)
    
    // Ver todos los personajes guardados
    @Query("SELECT * FROM personajes")
    fun obtenerTodosLosPersonajes(): List<Personaje>
    
    // Buscar un personaje por nombre
    @Query("SELECT * FROM personajes WHERE nombre = :nombre LIMIT 1")
    fun buscarPersonajePorNombre(nombre: String): Personaje?
    
    // Contar cuántos personajes hay
    @Query("SELECT COUNT(*) FROM personajes")
    fun contarPersonajes(): Int
}
```

### 3. Base de Datos Principal
```kotlin
@Database(
    entities = [Personaje::class],
    version = 1,
    exportSchema = false
)
abstract class GameDatabase : RoomDatabase() {
    
    abstract fun personajeDao(): PersonajeDao
    
    companion object {
        @Volatile
        private var INSTANCE: GameDatabase? = null
        
        fun getDatabase(context: Context): GameDatabase {
            return INSTANCE ?: synchronized(this) {
                val instance = Room.databaseBuilder(
                    context.applicationContext,
                    GameDatabase::class.java,
                    "game_database"
                ).allowMainThreadQueries()  // Solo para aprender, no en producción
                .build()
                INSTANCE = instance
                instance
            }
        }
    }
}
```

---

## 📦 Qué Agregar en build.gradle

En tu archivo `build.gradle (Module: app)`:

```gradle
dependencies {
    // Room - Para base de datos fácil
    implementation "androidx.room:room-runtime:2.4.3"
    kapt "androidx.room:room-compiler:2.4.3"
}
```

Y arriba del archivo, agregar:
```gradle
apply plugin: 'kotlin-kapt'
```

---

## 🚀 Cómo Usar en las Activities

### Ejemplo 1: Guardar Personaje (en CreateCharacterActivity)
```kotlin
class CreateCharacterActivity : AppCompatActivity() {
    
    private lateinit var database: GameDatabase
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_create_character)
        
        // Conectar con la base de datos
        database = GameDatabase.getDatabase(this)
        
        // Cuando el usuario presiona "Crear"
        buttonCrear.setOnClickListener {
            val nuevoPersonaje = Personaje(
                nombre = editTextNombre.text.toString(),
                clase = claseSeleccionada,  // "Guerrero", "Mago", etc.
                ataque = ataque,
                defensa = defensa,
                velocidad = velocidad
            )
            
            // Guardar en la base de datos
            database.personajeDao().guardarPersonaje(nuevoPersonaje)
            
            // Volver al menú principal
            finish()
        }
    }
}
```

### Ejemplo 2: Mostrar Personajes (en MainActivity)
```kotlin
class MainActivity : AppCompatActivity() {
    
    private lateinit var database: GameDatabase
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        database = GameDatabase.getDatabase(this)
        
        // Ver cuántos personajes hay guardados
        val cantidadPersonajes = database.personajeDao().contarPersonajes()
        
        if (cantidadPersonajes > 0) {
            // Mostrar botón de "Combate"
            buttonCombate.visibility = View.VISIBLE
            textPersonajes.text = "Tienes $cantidadPersonajes personajes"
        } else {
            // Solo mostrar "Crear Personaje"
            buttonCombate.visibility = View.GONE
            textPersonajes.text = "Crea tu primer personaje"
        }
    }
}
```

---

## ✅ Lo que debe funcionar al final

1. **Crear personaje** → Se guarda en la base de datos
2. **Cerrar la app** → Los datos no se pierden
3. **Abrir la app** → Los personajes siguen ahí
4. **Ver personajes** → Mostrar lista de personajes guardados

---

## 🎯 Plan de Trabajo Simple

### Paso 1: Configurar Room
- [ ] Agregar dependencias en build.gradle
- [ ] Crear la clase Personaje con @Entity
- [ ] Probar que compila

### Paso 2: Crear DAO y Database
- [ ] Hacer PersonajeDao con métodos básicos
- [ ] Crear GameDatabase class
- [ ] Probar que se crea la base de datos

### Paso 3: Conectar con Activities
- [ ] Usar database en CreateCharacterActivity
- [ ] Mostrar personajes en MainActivity
- [ ] Probar guardado y carga

### Paso 4: Probar Todo
- [ ] Crear varios personajes
- [ ] Cerrar y abrir la app
- [ ] Verificar que todo funciona

---

## 🤝 Cómo conectarme con mi equipo

### Para el equipo de UI (pantallas):
- Les doy métodos simples para guardar personajes
- Les ayudo a mostrar listas de personajes guardados

### Para el equipo de Lógica (combate):
- Les paso personajes guardados para usar en combate
- Ayudo a cargar personaje seleccionado

---

## ❓ Dudas que puedo tener

1. **¿Qué es Room?** → Una librería que hace SQLite más fácil
2. **¿Dónde se guardan los datos?** → En el celular, no se pierden
3. **¿Puedo ver la base de datos?** → Sí, con herramientas de Android Studio
4. **¿Qué pasa si algo sale mal?** → Room maneja errores automáticamente

---

## 📝 Notas importantes

- ✅ **Empezar simple:** Solo guardar y mostrar personajes
- ✅ **Probar cada paso:** Un método a la vez
- ✅ **allowMainThreadQueries():** Solo para aprender, simplifica las cosas
- ✅ **version = 1:** Si cambio la estructura después, cambiar la versión

**Mi objetivo:** Que funcione básico primero, mejorarlo después 🎯
