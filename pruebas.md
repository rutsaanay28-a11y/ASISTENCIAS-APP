# Plan de Pruebas de Interfaz (Propuesta)


---

# 1. Información General

| Elemento | Descripción |
|----------|-------------|
| Tipo de prueba | Prueba de Interfaz (UI) |
| Plataforma | Aplicación móvil (React Native) |
| Objetivo | Verificar que la interfaz permita registrar correctamente la asistencia mediante código QR y muestre mensajes adecuados al usuario. |
| Usuario de prueba | Empleado |

---

# 2. Función Seleccionada

| Elemento | Descripción |
|----------|-------------|
| Función | Registro de asistencia mediante código QR |
| Pantalla | Escaneo de código QR |
| Entrada | Código QR válido o inválido |
| Salida | Confirmación o mensaje de error |

---

# 3. Prueba 1 – Camino Feliz

| Etapa | Descripción |
|--------|-------------|
| Preparación | El usuario inicia sesión y accede a la pantalla de escaneo. |
| Acción | Escanea un código QR válido correspondiente a un evento activo. |
| Resultado esperado | El sistema muestra un mensaje indicando que la asistencia fue registrada correctamente. |

### Validaciones

| Validación | Resultado esperado |
|-------------|-------------------|
| Mensaje de éxito | Se muestra correctamente al usuario. |
| Respuesta de la interfaz | La pantalla responde sin errores. |
| Registro de asistencia | La asistencia queda almacenada correctamente. |

---

# 4. Prueba 2 – Camino Triste

| Etapa | Descripción |
|--------|-------------|
| Preparación | El usuario accede al módulo de escaneo. |
| Acción | Escanea un código QR inexistente o inválido. |
| Resultado esperado | El sistema informa que el código QR no es válido y no registra la asistencia. |

### Validaciones

| Validación | Resultado esperado |
|-------------|-------------------|
| Mensaje de error | Se informa que el código QR no es válido. |
| Registro de asistencia | No se registra ninguna asistencia. |
| Respuesta de la interfaz | La aplicación continúa funcionando correctamente. |

---

# 5. Prueba 3 – Caso Extremo

| Etapa | Descripción |
|--------|-------------|
| Preparación | El usuario abre el módulo de escaneo. |
| Acción | Intenta registrar la asistencia sin escanear un código QR o con un código vacío. |
| Resultado esperado | El sistema solicita escanear un código válido y no permite continuar. |

### Validaciones

| Validación | Resultado esperado |
|-------------|-------------------|
| Mensaje de validación | El sistema indica que el código es obligatorio. |
| Estabilidad de la interfaz | No ocurre ningún bloqueo de la aplicación. |
| Registro de asistencia | No se registra ninguna asistencia. |

---

# Plan de Pruebas de Validación (Propuesta)

> **Nota:** Estas pruebas verifican que el sistema valide correctamente los datos antes de registrar una asistencia.

---

# 1. Información General

| Elemento | Descripción |
|----------|-------------|
| Tipo de prueba | Prueba de Validación |
| Objetivo | Verificar que el sistema valide correctamente los datos antes de registrar una asistencia. |
| Mecanismo | FluentValidation y reglas de negocio |

---

# 2. Función Seleccionada

| Elemento | Descripción |
|----------|-------------|
| Función | Validación del registro de asistencia mediante código QR |
| Entrada | UUID del código QR |
| Salida | Aceptación o rechazo de la solicitud |

---

# 3. Prueba 1 – Camino Feliz

| Etapa | Descripción |
|--------|-------------|
| Preparación | Existe un código QR válido asociado a un empleado y a un evento activo. |
| Acción | El usuario escanea el código QR. |
| Resultado esperado | Todas las validaciones son correctas y el sistema registra la asistencia. |

### Validaciones

| Validación | Resultado esperado |
|-------------|-------------------|
| UUID | Es válido. |
| Evento | Se encuentra activo. |
| Empleado | Está registrado en el sistema. |
| Registro | La asistencia se almacena correctamente. |

---

# 4. Prueba 2 – Camino Triste

| Etapa | Descripción |
|--------|-------------|
| Preparación | El usuario intenta registrar un código QR inexistente. |
| Acción | Envía el código al sistema. |
| Resultado esperado | El sistema rechaza la solicitud indicando que el código no existe. |

### Validaciones

| Validación | Resultado esperado |
|-------------|-------------------|
| Registro de asistencia | No se registra. |
| Mensaje | Se informa que el código QR no existe. |
| Base de datos | No se modifica la información. |

---

# 5. Prueba 3 – Caso Extremo

| Etapa | Descripción |
|--------|-------------|
| Preparación | El usuario intenta registrar un código QR vacío (`Guid.Empty`) o nulo. |
| Acción | Envía la solicitud al sistema. |
| Resultado esperado | El sistema detecta que el dato es inválido y evita procesar la solicitud. |

### Validaciones

| Validación | Resultado esperado |
|-------------|-------------------|
| UUID | Es obligatorio. |
| Mensaje | Se informa el error al usuario. |
| Registro | No se ejecuta el registro de asistencia. |
| Base de datos | Permanece sin cambios. |
