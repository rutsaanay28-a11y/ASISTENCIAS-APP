# Estructura de Directorios — ControlAsistencias

App móvil de control de asistencias (React Native + Expo + expo-router).

> Solo lo importante. Omite `android/`, `ios/`, `node_modules/` (nativo y dependencias).

## Stack / Tecnologías / Frameworks

| Capa | Tecnología | Versión |
|------|-----------|---------|
| Framework | React Native | 0.79.2 |
| Plataforma | Expo (bare workflow, con `android/` e `ios/` nativos) | SDK 53 |
| Lenguaje | JavaScript (no TypeScript) | React 19 |
| Routing | expo-router (file-based, carpeta `app/`) | ~5.0 |
| Estado global | React Context (`app/Context/dataContext.js`) | — |
| Persistencia local | `@react-native-async-storage/async-storage` | sesión usuario |
| Realtime | `@microsoft/signalr` | 8.0.7 |
| Cámara / QR | `expo-camera`, `react-native-qrcode-svg`, `react-native-svg` | — |
| UI extra | `@react-native-picker/picker`, `@react-native-community/datetimepicker`, `react-native-safe-area-context`, `react-native-screens` | — |
| Red | `fetch` nativo (sin axios) | — |


```
ControlAsistencias/
├── app/                              # Rutas expo-router (file-based)
│   ├── _layout.js                    # Layout raíz → DataContextProvider + <Slot>
│   ├── index.js                      # Ruta inicial
│   ├── theme.js                      # Tema UI ("Azure Ethos")
│   │
│   ├── Context/
│   │   └── dataContext.js            # Estado global usuario (AsyncStorage @user_data)
│   │
│   ├── Home/
│   │   ├── index.js                  # Home (router admin vs user)
│   │   ├── AltaEmpleados/
│   │   │   └── index.js              # Alta de empleados
│   │   └── Asistencias/
│   │       └── index.js              # Vista de asistencias
│   │
│   ├── components/home/
│   │   ├── adminHome.js              # Vista admin
│   │   ├── userHome.js               # Vista usuario normal
│   │   └── DrawerMenu.js             # Menú lateral
│   │
│   ├── lib/                          # Capa de acceso a API (fetch, 1 fn por endpoint)
│   │   ├── config.js                 # URL base API centralizada
│   │   ├── Empleados/
│   │   │   ├── CreateEmpleado.js
│   │   │   ├── DeleteEmpleado.js
│   │   │   ├── GetEmpleados.js
│   │   │   ├── UpdateEmpleado.js
│   │   │   └── Login/login.js
│   │   ├── RegistroAsistencias/
│   │   │   ├── createAsistencia.js   # Registra asistencia (escaneo QR)
│   │   │   ├── SearchAsistencia.js
│   │   │   └── getAsistencias.js
│   │   └── Qr/
│   │       └── GetLastQr.js          # Último QR generado
│   │
│   └── assets/
│       └── QrImg.png
│
├── assets/                           # Íconos app
│   ├── icon.png
│   ├── adaptive-icon.png
│   ├── splash-icon.png
│   └── favicon.png
│
├── android/                          # Proyecto nativo Android (Gradle, keystore, firma)
├── ios/                              # Proyecto nativo iOS
│
├── index.js                          # Entry (real: expo-router/entry vía package.json main)
├── app.json                          # Config Expo (nombre, permisos, plugins)
├── eas.json                          # Config EAS (NO usado, build local)
├── package.json
├── package-lock.json
├── eslint.config.js
├── my-upload-key.keystore            # ⚠️ Backup obligatorio — firma APK release
├── .env.example
├── COMPILAR.md                       # Guía compilación Android
└── CLAUDE.md                         # Instrucciones proyecto
```

## Conceptos clave

- **Routing:** `app/` = rutas file-based (expo-router).
- **Datos:** `app/lib/...` 1 función `async` por endpoint, retorna `{ data, ... }`, lanza `Error` en fallo.
- **Estado:** `useDataContext()` (no prop-drilling). Sesión en AsyncStorage `@user_data`.
- **Roles:** `adminHome.js` vs `userHome.js` según `userData.isAdmin`.
- **Flujo asistencia:** admin muestra QR → empleado escanea → `lib/RegistroAsistencias/createAsistencia.js`.