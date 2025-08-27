# RF08 - Base de Datos Firebase Online/Offline

**Responsable:** Juan Beleño  
**Requerimiento:** RF08 - Sistema de almacenamiento Firebase con modos online/offline  
**Tecnología:** Android Studio + Kotlin + Firebase Realtime Database  

---

## 📋 Objetivo del Requerimiento

Implementar un **sistema de base de datos híbrido** que permita:
- ✅ **Funcionamiento offline completo** sin conexión a internet
- ✅ **Sincronización automática** cuando se recupere la conexión
- ✅ **Persistencia de datos** tanto local como en la nube
- ✅ **Transición transparente** entre modos offline/online
- ✅ **Prueba de conectividad** para validar funcionamiento

---

## 📱 Definición de Modos de Almacenamiento

### 🔌 Modo OFFLINE (Sin Internet)

**¿Cómo funciona sin conexión?**
- Todos los datos se guardan **automáticamente en el dispositivo**
- Firebase mantiene una **caché local SQLite** con datos recientes
- El usuario puede realizar **todas las operaciones** normalmente
- Los cambios se almacenan en **cola de sincronización** interna

**Funcionalidades Disponibles:**
- ✅ Crear nuevos personajes
- ✅ Modificar personajes existentes  
- ✅ Realizar combates y ganar experiencia
- ✅ Ver lista completa de personajes guardados
- ✅ Todas las operaciones del juego funcionan normal

**Limitaciones:**
- ❌ No se sincronizan cambios hasta reconectar
- ⚠️ Datos solo existen en ese dispositivo específico

### 🌐 Modo ONLINE (Con Internet)

**¿Cómo funciona con conexión?**
- **Sincronización automática** de todos los cambios pendientes
- Datos locales se **suben a Firebase** inmediatamente
- **Actualización en tiempo real** de la base de datos
- **Descarga automática** de datos nuevos disponibles

**Funcionalidades Adicionales:**
- ✅ **Respaldo automático** en la nube
- ✅ **Sincronización entre dispositivos** del mismo usuario
- ✅ **Persistencia garantizada** - datos nunca se pierden
- ✅ **Actualizaciones instantáneas** de cambios

### 🔄 Transición Automática Entre Modos

**Al PERDER conexión:**
1. **Detección automática** de pérdida de red
2. **Cambio transparente** a modo offline
3. **Notificación discreta:** "Modo offline activado"
4. **Continúa funcionando** con datos locales

**Al RECUPERAR conexión:**
1. **Detección automática** de conexión restaurada
2. **Sincronización automática** en segundo plano
3. **Resolución de conflictos** si es necesario
4. **Notificación:** "Datos sincronizados"

**Gestión de Conflictos:**
- **Estrategia:** "Último cambio gana" (por timestamp)
- **Prioridad:** Cambios locales del usuario
- **Resolución:** Firebase maneja automáticamente
- **Seguridad:** Respaldo del estado anterior

---

## 💾 Arquitectura de Almacenamiento

### Almacenamiento Local (Dispositivo):
```
📱 Cache SQLite de Firebase
├── Datos del usuario actual
├── Cambios pendientes de sincronizar  
├── Configuración offline
└── Historial de operaciones
```

### Almacenamiento en la Nube (Firebase):
```
☁️ Firebase Realtime Database
├── Base de datos completa
├── Histórico de todos los cambios
├── Respaldo de todos los usuarios
└── Reglas de seguridad activas
```

### Políticas de Sincronización:
- **Inmediata:** Con conexión, cambios se suben al instante
- **Por lotes:** Sin conexión, cambios se agrupan para sincronizar
- **Inteligente:** Solo sincroniza datos realmente modificados
- **Eficiente:** Minimiza el uso de datos móviles

---

## 🚀 Configuración Técnica

### 1. Setup Firebase Console

**Crear Proyecto:**
1. Ir a [console.firebase.google.com](https://console.firebase.google.com)
2. Click "Crear un proyecto"
3. Nombre: `fighters-time-juan-beleno`
4. Deshabilitar Google Analytics
5. Click "Crear proyecto"

**Configurar Realtime Database:**
1. En Firebase Console → "Realtime Database"
2. Click "Crear base de datos"
3. Seleccionar "Empezar en modo de prueba"
4. Ubicación: `us-central1`
5. Click "Listo"

**Agregar App Android:**
1. Click ícono de Android en dashboard
2. **Nombre del paquete:** `com.fighterstime.app`
3. **Alias:** `FightersTime`
4. Registrar app
5. **Descargar** `google-services.json`
6. **Copiar** a carpeta `app/` del proyecto

### 2. Configuración Android Studio

**build.gradle (Project):**
- Agregar servicios de Google a nivel de proyecto
- Configurar classpath para Firebase

**build.gradle (Module: app):**
- Agregar plugins de Firebase
- Incluir dependencias de Realtime Database
- Configurar persistencia offline

### 3. Configuración de Persistencia

**Habilitación Offline:**
- `setPersistenceEnabled(true)` → Activar caché local
- **Tamaño automático** según espacio disponible
- **Prioridad:** Datos del usuario actual
- **Limpieza automática** gestionada por Firebase

---

## 🧪 Plan de Pruebas

### Prueba de Conectividad Básica:

**Objetivo:** Verificar que Firebase está correctamente configurado

**Proceso:**
1. Crear MainActivity con layout básico
2. Botón para "Probar Conexión Firebase"
3. Enviar datos de prueba a Firebase
4. Leer datos desde Firebase
5. Mostrar resultado en pantalla
6. Verificar datos en Firebase Console

**Resultado Esperado:**
- ✅ Escritura exitosa en Firebase
- ✅ Lectura exitosa desde Firebase  
- ✅ Datos visibles en Firebase Console
- ✅ Mensaje: "Conexión Firebase exitosa"

### Prueba de Modo Offline:

**Objetivo:** Verificar funcionamiento sin internet

**Proceso:**
1. Desactivar WiFi y datos móviles
2. Intentar guardar datos localmente
3. Verificar que la app sigue funcionando
4. Reactivar conexión a internet
5. Verificar sincronización automática

**Resultado Esperado:**
- ✅ App funciona offline normalmente
- ✅ Datos se guardan localmente
- ✅ Al reconectar, datos se sincronizan
- ✅ No se pierden datos en el proceso

---

## ✅ Checklist de Implementación

### Fase 1: Configuración Base
- [ ] Crear proyecto Firebase
- [ ] Descargar y configurar google-services.json
- [ ] Configurar build.gradle files
- [ ] Habilitar Realtime Database

### Fase 2: Prueba de Conectividad
- [ ] Crear MainActivity básico con layout
- [ ] Implementar botón de prueba de conexión
- [ ] Probar escritura y lectura básica
- [ ] Verificar datos en Firebase Console
- [ ] Documentar resultados de prueba

### Fase 3: Funcionalidad Offline/Online
- [ ] Configurar persistencia offline
- [ ] Probar funcionamiento sin internet
- [ ] Verificar sincronización automática
- [ ] Probar transición entre modos

### Fase 4: Documentación y Entrega
- [ ] Documentar estructura de datos final
- [ ] Crear manual de uso para el equipo
- [ ] Documentar resultados de todas las pruebas
- [ ] Preparar demostración del funcionamiento

---

## 🆘 Solución de Problemas

### Error: "google-services.json not found"
**Solución:** Verificar ubicación exacta en `app/google-services.json`

### Error: "FirebaseDatabase not initialized"  
**Solución:** Revisar plugin `com.google.gms.google-services` en build.gradle

### Error: "Permission denied"
**Solución:** Verificar reglas de seguridad en Firebase Console

### Error: "No network connection"
**Solución:** Firebase funciona offline automáticamente, verificar persistencia

---

## 📚 Recursos de Referencias

- **Firebase Documentation:** [firebase.google.com/docs](https://firebase.google.com/docs)
- **Android Firebase Guide:** [firebase.google.com/docs/android](https://firebase.google.com/docs/android)  
- **Offline Capabilities:** [firebase.google.com/docs/database/android/offline-capabilities](https://firebase.google.com/docs/database/android/offline-capabilities)
- **Stack Overflow:** Para dudas técnicas específicas

---