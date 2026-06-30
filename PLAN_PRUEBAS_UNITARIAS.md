# Plan de Pruebas Unitarias (Propuesta)

> **Nota:** Debido a que el equipo únicamente dispone del archivo APK y
> no del código fuente del proyecto, las pruebas unitarias presentadas
> corresponden a una **propuesta de implementación** basada en la
> arquitectura y tecnologías del sistema.

## 1. Información general

  -----------------------------------------------------------------------
  Elemento                       Descripción
  ------------------------------ ----------------------------------------
  Capa a probar                  Aplicación (Application)

  Patrón arquitectónico          CQRS + MediatR

  Framework de pruebas           xUnit

  Lenguaje                       C# 12

  Runtime                        .NET 8

  Base de datos para pruebas     Entity Framework Core InMemory
                                 (propuesta)

  Simulación de dependencias     Moq (propuesta)

  Validaciones                   FluentValidation
  -----------------------------------------------------------------------

## 2. Justificación

  -----------------------------------------------------------------------
  Aspecto                       Explicación
  ----------------------------- -----------------------------------------
  ¿Por qué esta capa?           La capa de Aplicación contiene la lógica
                                de negocio del sistema.

  ¿Por qué no el Controller?    El Controller solo recibe las peticiones
                                HTTP y delega la ejecución al Handler de
                                MediatR.

  ¿Qué se prueba?               Los Handlers y las reglas de validación
                                que registran y validan las asistencias.

  ¿Qué se simula?               La conexión con PostgreSQL mediante
                                Entity Framework Core InMemory o Moq para
                                aislar la lógica.
  -----------------------------------------------------------------------

# Función seleccionada

## Registrar asistencia mediante código QR

  -----------------------------------------------------------------------
  Elemento                       Descripción
  ------------------------------ ----------------------------------------
  Método (supuesto)              `RegistrarAsistenciaCommandHandler`

  Responsabilidad                Validar el UUID y registrar la
                                 asistencia del empleado.

  Capa                           Aplicación

  Tecnologías                    MediatR + Entity Framework Core +
                                 FluentValidation
  -----------------------------------------------------------------------

# Prueba 1 -- Camino Feliz

  -------------------------------------------------------------------------
  Patrón AAA                         Descripción
  ---------------------------------- --------------------------------------
  Arrange                            Se prepara un UUID válido asociado a
                                     un empleado y a un evento activo.

  Act                                Se ejecuta el método
                                     `RegistrarAsistenciaCommandHandler`.

  Assert                             La asistencia se registra
                                     correctamente y el resultado es
                                     exitoso.
  -------------------------------------------------------------------------

**Resultado esperado**

-   Registro exitoso.
-   Devuelve respuesta de éxito.
-   La asistencia queda almacenada.

# Prueba 2 -- Camino Triste

  -------------------------------------------------------------------------
  Patrón AAA                         Descripción
  ---------------------------------- --------------------------------------
  Arrange                            Se prepara un UUID inexistente o
                                     inválido.

  Act                                Se ejecuta el método
                                     `RegistrarAsistenciaCommandHandler`.

  Assert                             El sistema rechaza la solicitud y
                                     devuelve un mensaje indicando que el
                                     código QR no es válido.
  -------------------------------------------------------------------------

**Resultado esperado**

-   No registra la asistencia.
-   Devuelve mensaje de error.
-   No modifica la base de datos.

# Prueba 3 -- Caso Extremo

  -------------------------------------------------------------------------
  Patrón AAA                         Descripción
  ---------------------------------- --------------------------------------
  Arrange                            Se envía un UUID vacío (`Guid.Empty`)
                                     o nulo.

  Act                                Se ejecuta el método
                                     `RegistrarAsistenciaCommandHandler`.

  Assert                             El sistema valida la entrada y
                                     responde con un error controlado sin
                                     generar excepciones.
  -------------------------------------------------------------------------

**Resultado esperado**

-   No se produce un fallo del sistema.
-   Se informa que el UUID es obligatorio.
-   La base de datos permanece sin cambios.

# Herramientas propuestas

  -----------------------------------------------------------------------
  Herramienta                                         Uso
  --------------------------------------------------- -------------------
  xUnit                                               Framework para
                                                      pruebas unitarias.

  Moq                                                 Simulación de
                                                      dependencias
                                                      externas.

  Entity Framework Core InMemory                      Simulación de la
                                                      base de datos
                                                      durante las
                                                      pruebas.

  FluentValidation                                    Validación de los
                                                      datos de entrada.
  -----------------------------------------------------------------------

## Tecnologías del proyecto

  Categoría             Tecnología                              Versión
  --------------------- --------------------------------------- ---------------------------
  Runtime / Framework   .NET                                    8.0
  API                   ASP.NET Core Web API                    SDK Microsoft.NET.Sdk.Web
  Lenguaje              C#                                      12
  Base de datos         PostgreSQL                              ---
  ORM                   Entity Framework Core                   9.0.5
  Provider              Npgsql.EntityFrameworkCore.PostgreSQL   9.0.4
  CQRS                  MediatR                                 12.5.0
  Mapeo                 AutoMapper                              12.0.1
  Validación            FluentValidation                        12.0.0
  Tiempo real           SignalR                                 1.2.0
  Documentación API     Swagger                                 6.6.2
  Contenedores          Docker + Docker Compose                 ---
  Seguridad             PasswordHasher                          ---
