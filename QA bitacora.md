# QA - Bitácora de Integración

| ID | Integración | Módulo Origen | Módulo Destino | Resultado Esperado | Estado |
|----|-------------|---------------|----------------|-------------------|--------|
| QA-001 | Login | Pantalla de Inicio | Menú Principal | El usuario inicia sesión correctamente | PASA |
| QA-002 | Escaneo QR | Escáner QR | Registro de Asistencia | Se registra la asistencia correctamente | PASA |
| QA-003 | Validación de UUID | Escáner QR | Backend | Solo acepta UUID válidos | PASA |
| QA-004 | Registro de Asistencia | Backend | Base de Datos | La asistencia queda almacenada | PASA |
| QA-005 | Consulta de Asistencias | Menú Principal | Historial | Se muestran todas las asistencias | PASA |
| QA-006 | Alta de Empleado | Administración | Base de Datos | El empleado queda registrado | PASA |
| QA-007 | Edición de Empleado | Administración | Base de Datos | Se actualiza la información | PASA |
| QA-008 | Eliminación de Empleado | Administración | Base de Datos | El empleado se elimina correctamente | PASA |
| QA-009 | Generación de QR | Administración | Generador QR | Se crea un QR único | PASA |
