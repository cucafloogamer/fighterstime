# 🔥 Firebase Guide - FightersTime

**Proyecto:** Fighter's Time
**Responsable:** Juan Beleño  
**Objetivo:** Base de datos online/offline con sincronización en tiempo real  

---

## 🚀 Pasos para Configurar Firebase

### 1. Crear Proyecto en Firebase Console

1. Ir a [console.firebase.google.com](https://console.firebase.google.com)
2. Click "Crear un proyecto"
3. Nombre: `fighters-time-[tu-nombre]`
4. Deshabilitar Google Analytics (no es necesario para este proyecto)
5. Click "Crear proyecto"

### 2. Agregar App Android

1. En el dashboard, click el ícono de Android
2. **Nombre del paquete:** `com.fighterstime.app` 
3. **Alias de la app:** `FightersTime`
4. **Certificado SHA-1:** Dejar vacío por ahora
5. Click "Registrar app"

### 3. Descargar Archivo de Configuración

1. Descargar `google-services.json`
2. Copiar a la carpeta `app/` de tu proyecto Android Studio
3. **IMPORTANTE:** Este archivo debe estar en `app/google-services.json`

### 4. Configurar Realtime Database

1. En Firebase Console, ir a "Realtime Database"
2. Click "Crear base de datos"
3. Seleccionar "Empezar en modo de prueba"
4. Ubicación: `us-central1` (más cercana)
5. Click "Listo"

---

## 🔧 Configuración de Android Studio

### 1. build.gradle (Project: FightersTime)
```gradle
buildscript {
    ext.kotlin_version = "1.8.20"
    dependencies {
        classpath "com.android.tools.build:gradle:8.0.2"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        // Agregar esta línea para Firebase
        classpath 'com.google.gms:google-services:4.3.15'
    }
}
```

### 2. build.gradle (Module: app)
```gradle
plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
    // Agregar plugin de Firebase
    id 'com.google.gms.google-services'
}

android {
    compileSdk 34
    
    defaultConfig {
        applicationId "com.fighterstime.app"
        minSdk 24
        targetSdk 34
        versionCode 1
        versionName "1.0"
    }
}

dependencies {
    implementation 'androidx.core:core-ktx:1.10.1'
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.9.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
    
    // Firebase BOM - Maneja todas las versiones de Firebase
    implementation platform('com.google.firebase:firebase-bom:32.2.3')
    
    // Firebase Database - Para datos en tiempo real
    implementation 'com.google.firebase:firebase-database-ktx'
    
    // Firebase Auth - Para autenticación de usuarios
    implementation 'com.google.firebase:firebase-auth-ktx'
    
    // Testing
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
}
```

---

## 🧪 Prueba Rápida de Conexión

### MainActivity.kt (Para probar)
```kotlin
package com.fighterstime.app

import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import com.google.firebase.database.ktx.database
import com.google.firebase.ktx.Firebase

class MainActivity : AppCompatActivity() {
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        val buttonTest = findViewById<Button>(R.id.buttonTestFirebase)
        val textResult = findViewById<TextView>(R.id.textFirebaseResult)
        
        buttonTest.setOnClickListener {
            probarFirebase(textResult)
        }
    }
    
    private fun probarFirebase(textResult: TextView) {
        textResult.text = "Probando conexión con Firebase..."
        
        val database = Firebase.database
        val testRef = database.getReference("test")
        
        // Escribir dato de prueba
        val testData = mapOf(
            "mensaje" to "¡Firebase funciona!",
            "timestamp" to System.currentTimeMillis(),
            "autor" to "Juan Beleño"
        )
        
        testRef.setValue(testData)
            .addOnSuccessListener {
                // Si se escribió exitosamente, ahora leer
                testRef.get().addOnSuccessListener { snapshot ->
                    if (snapshot.exists()) {
                        val mensaje = snapshot.child("mensaje").getValue(String::class.java)
                        textResult.text = "✅ ÉXITO: $mensaje"
                        textResult.setTextColor(resources.getColor(android.R.color.holo_green_dark))
                        Toast.makeText(this, "Firebase conectado correctamente", Toast.LENGTH_SHORT).show()
                    }
                }.addOnFailureListener {
                    textResult.text = "❌ Error al leer: ${it.message}"
                    textResult.setTextColor(resources.getColor(android.R.color.holo_red_dark))
                }
            }
            .addOnFailureListener { exception ->
                textResult.text = "❌ Error de conexión: ${exception.message}"
                textResult.setTextColor(resources.getColor(android.R.color.holo_red_dark))
                Toast.makeText(this, "Error: ${exception.message}", Toast.LENGTH_LONG).show()
            }
    }
}
```

### activity_main.xml (Layout básico)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="FightersTime - Firebase Test"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="30dp" />

    <Button
        android:id="@+id/buttonTestFirebase"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Probar Conexión Firebase"
        android:textSize="18sp"
        android:layout_marginBottom="20dp" />

    <TextView
        android:id="@+id/textFirebaseResult"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Presiona el botón para probar Firebase"
        android:textSize="16sp"
        android:padding="15dp"
        android:background="#f5f5f5"
        android:gravity="center" />

</LinearLayout>
```

---

## 📊 Estructura de Datos Propuesta

### JSON Structure en Firebase:
```json
{
  "users": {
    "unique_user_id": {
      "username": "jugador123",
      "email": "jugador@example.com",
      "created_at": 1693123456789
    }
  },
  "personajes": {
    "personaje_unique_id": {
      "user_id": "unique_user_id",
      "nombre": "Arturo",
      "clase": "Guerrero",
      "nivel": 5,
      "vida_maxima": 120,
      "vida_actual": 95,
      "ataque": 25,
      "defensa": 18,
      "experiencia": 750,
      "experiencia_siguiente_nivel": 1000,
      "created_at": 1693123456789,
      "updated_at": 1693123456789
    }
  },
  "combates": {
    "combate_unique_id": {
      "personaje_id": "personaje_unique_id",
      "enemigo": {
        "nombre": "Goblin Salvaje",
        "nivel": 3,
        "vida": 60,
        "ataque": 15,
        "defensa": 8
      },
      "resultado": "Victoria",
      "experiencia_ganada": 50,
      "duracion_turnos": 8,
      "fecha_combate": 1693123456789
    }
  },
  "test": {
    "mensaje": "¡Firebase funciona!",
    "timestamp": 1693123456789,
    "autor": "Juan Beleño"
  }
}
```

---

## 🔐 Reglas de Seguridad Básicas

En Firebase Console > Realtime Database > Reglas:

```javascript
{
  "rules": {
    // Datos de prueba - acceso completo temporalmente
    "test": {
      ".read": true,
      ".write": true
    },
    
    // Usuarios solo pueden leer/escribir sus propios datos
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    },
    
    // Personajes - solo el dueño puede modificar
    "personajes": {
      ".read": true,
      ".write": "auth != null",
      "$personaje_id": {
        ".validate": "newData.hasChildren(['user_id', 'nombre', 'clase'])"
      }
    },
    
    // Combates - cualquiera puede leer, solo usuarios autenticados escribir
    "combates": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

---

## ✅ Checklist de Implementación

### Configuración Inicial:
- [ ] Crear proyecto Firebase
- [ ] Descargar google-services.json
- [ ] Configurar build.gradle files
- [ ] Habilitar Realtime Database

### Prueba Básica:
- [ ] Crear MainActivity con botón de prueba
- [ ] Probar escritura en Firebase
- [ ] Probar lectura desde Firebase
- [ ] Verificar datos en Firebase Console

### Funcionalidad del Juego:
- [ ] Crear clase Personaje
- [ ] Implementar guardado de personajes
- [ ] Implementar carga de personajes
- [ ] Probar modo offline
- [ ] Configurar sincronización automática

### Documentación:
- [ ] Documentar estructura de datos
- [ ] Crear guía de uso para el equipo
- [ ] Documentar resultados de pruebas
- [ ] Manual de configuración

---

## 🆘 Solución de Problemas Comunes

### Error: "google-services.json not found"
- **Solución:** Verificar que el archivo esté en `app/google-services.json`

### Error: "FirebaseDatabase not initialized"
- **Solución:** Agregar plugin `com.google.gms.google-services` en build.gradle

### Error: "Permission denied"
- **Solución:** Revisar reglas de seguridad en Firebase Console

### Error: "No network connection"
- **Solución:** Firebase funciona offline automáticamente, verificar persistencia

---

## 📞 Recursos de Apoyo

- **Firebase Documentation:** [firebase.google.com/docs](https://firebase.google.com/docs)
- **Android Firebase Guide:** [firebase.google.com/docs/android](https://firebase.google.com/docs/android)
- **Stack Overflow:** Para dudas específicas
- **YouTube:** "Firebase Android Tutorial" para videos explicativos


