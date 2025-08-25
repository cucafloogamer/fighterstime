# RF03_02 - Carga de datos

La aplicación debe ser capaz de cargar personajes/partida previamente guardados y recuperar datos, tales como:

- Nombre del personaje
- Clase del personaje
- Nivel
- Vida máxima
- Vida al momento del guardado
- Ataque
- Defensa

> Esta lista está sujeta a cambios posteriores dependiendo de los requerimientos que se necesiten*

Para esto se utilizará la librería de Java `java.nio.file`, cuya utilidad es el manejo de archivos dentro del programa.

Un ejemplo<sup>1</sup>:
```java
fun checkSavedFiles() {
    val saveFilePath = "/saves" //folder path
    val directory = File(saveFilePath) // this creates an object that represents the path

//this checks if the directory exist AND if it's a directory and not just a file
    if (directory.exists() && directory.isDirectory) { 

// if it's valid, this returns an array of all the items inside
        val filesAndFolders = directory.listFiles() 

// this part lists all the files and shows whether they are a file or a directory
        if (filesAndFolders != null) { 
            println("Contents of ${saveFilePath}.")
            filesAndFolders.forEachIndexed {index, item ->
                val type = if(item.isFile) "File" else null
                println("${index + 1}.  $type - ${item.name}")
                val saveArray = intArrayOf(index)
            }

//This allows to select the item you want to load
            print("Enter the number of the item you want to access: ")
            val userInput = readLine()?.toIntOrNull()

            if (userInput != null && userInput > 0 && userInput <= filesAndFolders.size) {
                val selectedItem = filesAndFolders[userInput - 1] // Convert to 0-based index
                val type = if (selectedItem.isFile) "File" else "Directory"
                println("Loading: $type - ${selectedItem.name}")
                println("Loaded ${selectedItem.name} from ${selectedItem.absolutePath}")
            } else {
                println("Invalid selection!")
            }
        } else {
            println("Could not list $saveFilePath.")
        }
    } else {
        println("The directory $saveFilePath does not exist.")
    }
}
```
Este código entrega una forma de revisar los archivos de guardado y da la posibilidad de elegir que archivo querer guardar.

Preferentemente el archivo de guardado debe ser `.sav` y los datos deben guardarse en hexadecimal para un menor peso de archivos.

----
<footer>
<sup>1. El código está renderizado en Java, ya que MD no tiene soporte para kotlin</sup> 
</footer>