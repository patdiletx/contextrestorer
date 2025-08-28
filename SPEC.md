# 🧠 ContextRestorer – Especificación Técnica Viva

> **App de Restauración de Contexto Cognitivo y Estimulación Productiva**  
> Versión: 0.1.0 (MVP)  
> Estado: En desarrollo  
> Última actualización: 2025-04-05

---

## 🎯 Visión

Una aplicación de escritorio que ayuda a desarrolladores, diseñadores y analistas a **recuperar rápidamente el contexto de trabajo** tras interrupciones, combinando:
- Monitoreo pasivo de aplicaciones, ventanas y navegación
- Captura manual de "snapshots" de contexto
- Restauración con un clic
- Todo 100% local, privado y eficiente

**Problema que resuelve**:  
La pérdida de contexto cognitivo tras interrupciones cuesta en promedio 15-25 minutos por distracción.

**Solución**:  
Automatizar la captura del estado técnico y mental del trabajo para permitir una reanudación instantánea.

---

## 🏗️ Arquitectura General

Aplicación **Electron + TypeScript**, con separación clara entre procesos:

- **Main Process**: Lógica del sistema, monitores, base de datos, IPC
- **Renderer Process**: Interfaz de usuario (React + Tailwind)
- **Shared**: Tipos, constantes y utilidades compartidas

**Patrones clave**:
- Observer (para eventos de contexto)
- Singleton (DatabaseManager)
- Repository (acceso a datos)
- Factory (monitores por plataforma)

---

## 📁 Estructura de Carpetas
contextrestorer/
├── main/ # Proceso principal (Node.js)
│ ├── app.ts # Entry point
│ ├── ipc/ # Handlers de IPC
│ ├── services/ # Lógica de negocio
│ ├── monitors/ # Detectores de actividad
│ └── utils/ # Logging, config
├── renderer/ # UI (React)
│ ├── pages/ # Dashboard, Snapshot, Settings
│ ├── components/ # UI reusables
│ ├── store/ # Zustand
│ └── hooks/ # Custom hooks
├── shared/
│ └── types/ # Interfaces compartidas
├── database/ # SQLite
│ ├── schema.sql
│ └── DatabaseManager.ts
├── extensions/ # Chrome/Edge extension
│ ├── manifest.json
│ ├── background.js
│ └── content-script.js
├── tests/
│ ├── unit/
│ └── integration/
├── SPEC.md # ← Este archivo (fuente de verdad)
├── package.json
├── tsconfig.json
└── electron-builder.json


---

## 💾 Modelo de Datos (SQLite)

```sql
-- Eventos de actividad del sistema
CREATE TABLE activity_events (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
  event_type TEXT NOT NULL,        -- 'window_focus', 'url_change'
  app_name TEXT,
  window_title TEXT,
  process_path TEXT,
  url TEXT,
  metadata JSON
);

-- Snapshots manuales del usuario
CREATE TABLE snapshots (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  name TEXT,
  description TEXT,
  data JSON NOT NULL,              -- { apps: [...], urls: [...] }
  tags TEXT                        -- "coding,debug,meeting"
);

-- Configuración del usuario
CREATE TABLE user_settings (
  id INTEGER PRIMARY KEY,
  monitor_windows BOOLEAN DEFAULT 1,
  monitor_browser BOOLEAN DEFAULT 1,
  idle_threshold_seconds INTEGER DEFAULT 300,
  data_retention_days INTEGER DEFAULT 30
);

CREATE INDEX idx_events_timestamp ON activity_events(timestamp);
CREATE INDEX idx_snapshots_created ON snapshots(created_at);

profile
Qwen3-235B-A22B-2507
12:30 pm
Aquí tienes el contenido completo y actualizado del archivo SPEC.md, listo para guardarse en tu repositorio. Este archivo es la especificación viva del proyecto, diseñado para ser leído y actualizado tanto por el Arquitecto como por Jules (jules.google), quien lo usará como guía para implementar el código automáticamente.

📄 SPEC.md – Especificación Técnica Viva de ContextRestorer
markdown


1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
⌄
⌄
⌄
⌄
⌄
⌄
# 🧠 ContextRestorer – Especificación Técnica Viva

> **App de Restauración de Contexto Cognitivo y Estimulación Productiva**  
> Versión: 0.1.0 (MVP)  
> Estado: En desarrollo  
> Última actualización: 2025-04-05

---

## 🎯 Visión

Una aplicación de escritorio que ayuda a desarrolladores, diseñadores y analistas a **recuperar rápidamente el contexto de trabajo** tras interrupciones, combinando:
- Monitoreo pasivo de aplicaciones, ventanas y navegación
- Captura manual de "snapshots" de contexto
- Restauración con un clic
- Todo 100% local, privado y eficiente

**Problema que resuelve**:  
La pérdida de contexto cognitivo tras interrupciones cuesta en promedio 15-25 minutos por distracción.

**Solución**:  
Automatizar la captura del estado técnico y mental del trabajo para permitir una reanudación instantánea.

---

## 🏗️ Arquitectura General

Aplicación **Electron + TypeScript**, con separación clara entre procesos:

- **Main Process**: Lógica del sistema, monitores, base de datos, IPC
- **Renderer Process**: Interfaz de usuario (React + Tailwind)
- **Shared**: Tipos, constantes y utilidades compartidas

**Patrones clave**:
- Observer (para eventos de contexto)
- Singleton (DatabaseManager)
- Repository (acceso a datos)
- Factory (monitores por plataforma)

---

## 📁 Estructura de Carpetas

contextrestorer/
├── main/ # Proceso principal (Node.js)
│ ├── app.ts # Entry point
│ ├── ipc/ # Handlers de IPC
│ ├── services/ # Lógica de negocio
│ ├── monitors/ # Detectores de actividad
│ └── utils/ # Logging, config
├── renderer/ # UI (React)
│ ├── pages/ # Dashboard, Snapshot, Settings
│ ├── components/ # UI reusables
│ ├── store/ # Zustand
│ └── hooks/ # Custom hooks
├── shared/
│ └── types/ # Interfaces compartidas
├── database/ # SQLite
│ ├── schema.sql
│ └── DatabaseManager.ts
├── extensions/ # Chrome/Edge extension
│ ├── manifest.json
│ ├── background.js
│ └── content-script.js
├── tests/
│ ├── unit/
│ └── integration/
├── SPEC.md # ← Este archivo (fuente de verdad)
├── package.json
├── tsconfig.json
└── electron-builder.json


---

## 💾 Modelo de Datos (SQLite)

sql
-- Eventos de actividad del sistema
CREATE TABLE activity_events (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
  event_type TEXT NOT NULL,        -- 'window_focus', 'url_change'
  app_name TEXT,
  window_title TEXT,
  process_path TEXT,
  url TEXT,
  metadata JSON
);

-- Snapshots manuales del usuario
CREATE TABLE snapshots (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  name TEXT,
  description TEXT,
  data JSON NOT NULL,              -- { apps: [...], urls: [...] }
  tags TEXT                        -- "coding,debug,meeting"
);

-- Configuración del usuario
CREATE TABLE user_settings (
  id INTEGER PRIMARY KEY,
  monitor_windows BOOLEAN DEFAULT 1,
  monitor_browser BOOLEAN DEFAULT 1,
  idle_threshold_seconds INTEGER DEFAULT 300,
  data_retention_days INTEGER DEFAULT 30
);
Índices:

sql



CREATE INDEX idx_events_timestamp ON activity_events(timestamp);
CREATE INDEX idx_snapshots_created ON snapshots(created_at);


🛠️ Backlog de Tareas Atómicas
Cada tarea es pequeña, ejecutable y verificable.
Jules debe implementarlas una por una, en orden.

T-001
Crear estructura de carpetas básica
🔴 Pendiente
Jules
2025-04-05
T-002
Inicializar proyecto Electron + TypeScript
🔴 Pendiente
Jules
2025-04-05
T-003
Configurar
better-sqlite3
y crear
DatabaseManager.ts
🔴 Pendiente
Jules
Pendiente PR
T-004
Implementar
WindowMonitor
para Windows usando
node-ffi-napi
🔴 Pendiente
Jules
Espera T-003
T-005
Crear
ContextService
que reciba eventos de monitores
🔴 Pendiente
Jules
—
T-006
Implementar IPC para enviar eventos al renderer
🔴 Pendiente
Jules
—
T-007
Crear extensión básica de Chrome para capturar URLs activas
🔴 Pendiente
Jules
—
T-008
Implementar
SnapshotService
(guardar/leer snapshots)
🔴 Pendiente
Jules
—
T-009
Crear UI: Dashboard con timeline de actividad
🔴 Pendiente
Jules
—
T-010
Implementar botón "Take Snapshot" en UI
🔴 Pendiente
Jules
—
T-011
Añadir notificación al tomar snapshot
🔴 Pendiente
Jules
—

🧩 Instrucciones para Jules (Agente Desarrollador)
Este archivo es tu fuente de verdad. Sigue estas reglas:

✅ Flujo de trabajo
Lee el estado actual del proyecto.
Toma la siguiente tarea en estado "Pendiente".
Implementa solo esa tarea.
Genera:
Código en las rutas correctas
Tests unitarios (si aplica)
Documentación inline (JSDoc)
Actualiza este archivo:
Cambia el estado de la tarea a ✅ Hecho
Añade fecha y breve nota
Haz commit: feat: implementa T-XXX - [descripción]
📌 Reglas clave
No implementes más de una tarea por commit.
Sigue la estructura de carpetas y tipos definidos.
Usa TypeScript estricto.
Maneja errores con try/catch en APIs del sistema.
No envíes datos a servidores externos. Todo es local.
🔐 Seguridad
nodeIntegration: false en renderer.
Usa preload solo para IPC seguro.
Valida todos los payloads de IPC.
No almacenes contenido de archivos o contraseñas.
🔄 Flujo de Trabajo del Equipo
Arquitecto actualiza SPEC.md con nueva tarea
Jules detecta cambio, lee tarea, la implementa
Jules actualiza SPEC.md y hace commit
Arquitecto revisa (opcionalmente)
Repetir