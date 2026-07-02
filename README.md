# Control de Asistencias — API (binarios)

API REST para control de asistencias por QR. ASP.NET Core 8, PostgreSQL, SignalR.

Esta entrega contiene los **binarios compilados** (Release), no el código fuente.

## Requisitos
- .NET 8 runtime (o Docker)
- PostgreSQL

## Configuración
La cadena de conexión NO viene incluida. Edita `app/appsettings.json` (o usa
la variable de entorno `ConnectionStrings__DefaultConnection`). Plantilla en
`appsettings.example.json`:

```json
"DefaultConnection": "Host=TU_HOST;Port=5432;Database=TU_DB;Username=TU_USUARIO;Password=TU_PASSWORD"
```

## Ejecutar

### Con .NET
```bash
cd app
dotnet ControlAsistencias_API.dll
```

### Con Docker
```bash
docker compose up --build
```

La API escucha en `http://localhost:5003`. Swagger en `http://localhost:5003/swagger`.
Las migraciones se aplican automáticamente al arrancar (entorno Development).

## Endpoints principales
- `GET  /api/empleados`
- `POST /api/empleados`
- `POST /api/asistencias`
- `GET  /api/asistencias`
- `GET  /api/qrs/last`
- Hub SignalR: `/api/asistenciasHub`

## Pruebas
Binario de pruebas en `tests/`. Resultado en `TEST_RESULTS.txt`.
```bash
dotnet test tests/ControlAsistencias_API.Tests.dll
```
