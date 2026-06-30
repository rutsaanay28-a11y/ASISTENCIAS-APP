# Plan de Pruebas Unitarias (Propuesta)

# 1. Información General

| Elemento | Descripción |
|----------|-------------|
| Capa a probar | Aplicación (Application) |
| Framework de pruebas | xUnit |
| Lenguaje | C# 12 |
| Runtime | .NET 8 |
| Patrón arquitectónico | CQRS + MediatR |
| ORM | Entity Framework Core |
| Validación | FluentValidation |
| Simulación de dependencias | Moq |
| Base de datos de prueba | Entity Framework Core InMemory |

---

# 2. Función Seleccionada

| Elemento | Descripción |
|----------|-------------|
| Función | Registrar asistencia mediante código QR |
| Método (propuesto) | `RegistrarAsistenciaCommandHandler` |
| Entrada | UUID del código QR |
| Salida | Confirmación o rechazo del registro |
| Tecnologías relacionadas | MediatR, Entity Framework Core y FluentValidation |

---

# 3. Prueba 1 – Camino Feliz

| Etapa (AAA) | Descripción |
|--------------|-------------|
| **Arrange** | Preparar un UUID válido asociado a un empleado y a un evento activo. |
| **Act** | Ejecutar el método `RegistrarAsistenciaCommandHandler`. |
| **Assert** | Verificar que la asistencia sea registrada correctamente. |

### Resultado esperado

 Validación 
|------------|
| Registro exitoso |  
| Devuelve respuesta de éxito | 
| Guarda la asistencia en la base de datos | 

---

# 4. Prueba 2 – Camino Triste

| Etapa (AAA) | Descripción |
|--------------|-------------|
| **Arrange** | Preparar un UUID inexistente o inválido. |
| **Act** | Ejecutar el método `RegistrarAsistenciaCommandHandler`. |
| **Assert** | Verificar que el sistema rechace el registro. |

### Resultado esperado

| Validación | Estado esperado |
|------------|-----------------|
| No registra la asistencia | ✅ |
| Devuelve mensaje de error | ✅ |
| No modifica la base de datos | ✅ |

---

# 5. Prueba 3 – Caso Extremo

| Etapa (AAA) | Descripción |
|--------------|-------------|
| **Arrange** | Enviar un UUID vacío (`Guid.Empty`) o nulo. |
| **Act** | Ejecutar el método `RegistrarAsistenciaCommandHandler`. |
| **Assert** | Verificar que el sistema responda con un error controlado sin producir una excepción. |

### Resultado esperado

| Validación | Estado esperado |
|------------|-----------------|
| No ocurre una excepción | ✅ |
| El sistema informa que el UUID es obligatorio | ✅ |
| La base de datos permanece sin cambios | ✅ |

---

# 6. Herramientas Propuestas

| Herramienta | Propósito |
|-------------|-----------|
| xUnit | Framework para pruebas unitarias |
| Moq | Simulación de dependencias |
| Entity Framework Core InMemory | Simulación de la base de datos |
| FluentValidation | Validación de datos de entrada |

---

# 7. Tecnologías del Proyecto

| Categoría | Tecnología | Versión |
|-----------|------------|---------|
| Runtime / Framework | .NET | 8.0 |
| Tipo de proyecto | ASP.NET Core Web API | Microsoft.NET.Sdk.Web |
| Lenguaje | C# | 12 |
| Base de datos | PostgreSQL | — |
| ORM | Entity Framework Core | 9.0.5 |
| Provider | Npgsql.EntityFrameworkCore.PostgreSQL | 9.0.4 |
| Patrón CQRS | MediatR | 12.5.0 |
| Mapeo de objetos | AutoMapper | 12.0.1 |
| Validación | FluentValidation | 12.0.0 |
| Tiempo real | ASP.NET Core SignalR | 1.2.0 |
| Documentación API | Swagger (Swashbuckle) | 6.6.2 |
| Contenedores | Docker + Docker Compose | — |
| Seguridad | PasswordHasher | — |
