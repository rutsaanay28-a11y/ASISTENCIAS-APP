# Estructura del Proyecto — ControlAsistencias_API

API ASP.NET Core con arquitectura limpia (Clean Architecture) + CQRS.

## Stack y Tecnologías

| Categoría | Tecnología | Versión |
|-----------|-----------|---------|
| Runtime / Framework | .NET | 8.0 (net8.0) |
| Tipo de proyecto | ASP.NET Core Web API | SDK `Microsoft.NET.Sdk.Web` |
| Lenguaje | C# (Nullable + ImplicitUsings habilitados) | C# 12 |
| Base de datos | PostgreSQL | — |
| ORM | Entity Framework Core | 9.0.5 |
| Provider DB | Npgsql.EntityFrameworkCore.PostgreSQL | 9.0.4 |
| Patrón CQRS / Mediator | MediatR | 12.5.0 (+ DI 11.1.0) |
| Mapeo objetos | AutoMapper (DI Extensions) | 12.0.1 |
| Validación | FluentValidation | 12.0.0 (+ AspNetCore 11.3.0) |
| Tiempo real | ASP.NET Core SignalR (WebSocket) | 1.2.0 |
| Documentación API | Swashbuckle.AspNetCore (Swagger/OpenAPI) | 6.6.2 |
| EF Tools | EntityFrameworkCore.Design / .Tools | 9.0.5 |
| Contenedores | Docker + Docker Compose (puerto 5003) | — |
| Seguridad | PasswordHasher (hashing custom) | — |

### Patrones / Arquitectura
- **Clean Architecture** — capas Domain → Application → Infrastructure → Presentation.
- **CQRS** — separación Commands (escritura) / Queries (lectura) vía MediatR.
- **Repository implícito** vía EF Core `DbContext`.
- **Fluent API** — configuración de entidades por archivo.


```
ControlAsistencias_API/
│
├── ControlAsistencias_API.sln          # Solución
├── ControlAsistencias_API.csproj       # Proyecto
├── ControlAsistencias_API.http         # Requests de prueba
├── Program.cs                          # Punto de entrada / configuración DI
├── README.md
├── Dockerfile                          # Imagen backend (puerto 5003)
├── docker-compose.yml                  # Orquestación con WebSocket/SignalR
├── .dockerignore
├── .gitignore
├── appsettings.json                    # Config base
├── appsettings.Development.json        # Config desarrollo
│
├── Domain/                             # CAPA DOMINIO — entidades de negocio
│   └── Entities/
│       ├── Asistencia.cs
│       ├── Empleado.cs
│       └── Qr.cs
│
├── Application/                        # CAPA APLICACIÓN — lógica CQRS
│   ├── Commands/                       # Escritura (mutaciones)
│   │   ├── Asistencias/
│   │   │   └── CreateAsistencia/       # Command + Handler
│   │   ├── Empleados/
│   │   │   ├── CreateEmpleado/
│   │   │   ├── DeleteEmpleado/
│   │   │   ├── LoginEmpleado/
│   │   │   └── UpdateEmpleado/
│   │   └── Qrs/
│   │       └── CreateQr/
│   ├── Queries/                        # Lectura (consultas)
│   │   ├── Asistencias/
│   │   │   ├── GetAsistenciaById/
│   │   │   ├── GetAsistencias/
│   │   │   └── SearchAsistencias/
│   │   ├── Empleados/
│   │   │   └── GetEmpleados/
│   │   └── Qrs/
│   │       └── GetLastQr/
│   ├── DTOs/                           # Objetos de transferencia
│   │   ├── AsistenciaDto.cs
│   │   ├── EmpleadoDto.cs
│   │   └── QrDto.cs
│   └── Mappings/
│       └── MappingProfile.cs           # AutoMapper
│
├── Infrastructure/                     # CAPA INFRAESTRUCTURA — acceso a datos
│   ├── Data/
│   │   ├── AplicationDbContext.cs      # EF Core DbContext
│   │   ├── Converters/
│   │   │   └── DateTimeConverters.cs
│   │   └── EntityConfigurations/       # Fluent API por entidad
│   │       ├── AsistenciaConfiguration.cs
│   │       ├── EmpleadoConfiguration.cs
│   │       └── QrConfiguration.cs
│   ├── Json/
│   │   └── DateOnlyJsonConverter.cs
│   └── Security/
│       └── PasswordHasher.cs
│
├── Controllers/                        # CAPA PRESENTACIÓN — endpoints REST
│   ├── AsistenciasController.cs
│   ├── EmpleadosController.cs
│   └── QrsController.cs
│
├── Hubs/                               # SignalR (tiempo real)
│   └── AsistenciasHub.cs
│
├── Services/
│   └── SignalRService.cs               # Notificaciones WebSocket
│
├── Migrations/                         # EF Core migraciones
│   ├── 20250517170218_InitialCreate
│   ├── 20250518003354_dateonly
│   ├── 20250521011931_ConvertTimeSpanToTimeOnly
│   └── ApplicationDbContextModelSnapshot.cs
│
└── Properties/
    ├── launchSettings.json
    └── PublishProfiles/
        └── FolderProfile.pubxml
```

## Flujo de capas

```
Controllers → Application (Commands/Queries) → Domain
                     ↓
              Infrastructure (EF Core / DB)
```

- **Domain**: entidades puras, sin dependencias.
- **Application**: CQRS (MediatR), DTOs, mapeos.
- **Infrastructure**: persistencia, seguridad, conversores.
- **Controllers + Hubs**: entrada HTTP + tiempo real SignalR.
```
