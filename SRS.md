# SRS – Sistema de Control de Asistencia mediante Código QR

## Persona: Administrador y Empleado (Asistente)

### Requerimientos Funcionales (Logos)

#### RF-01

El sistema debe permitir crear, editar y eliminar eventos corporativos.(A)

#### RF-02

El sistema debe permitir registrar y administrar empleados participantes.(A)

#### RF-03

El sistema debe generar un código QR único para cada asistencia registrada.(A)

####RF-04

El sistema debe validar y registrar asistencias mediante el escaneo de códigos QR.(A)

####RF-05

El sistema debe permitir registrar la asistencia mediante el escaneo del código QR.(U)

---

###Requerimientos de Experiencia de Usuario (Pathos)

####RX-01

El administrador debe poder crear un evento en menos de 2 minutos.(A)

####RX-02

La interfaz debe mostrar claramente el estado de cada asistencia registrada.(A)

####RX-03

Los reportes deben ser fáciles de localizar y descargar.(A)

####RX-04

El sistema debe mostrar mensajes claros cuando ocurra un error en la validación.(U)

####RX-05

El empleado debe poder registrar su asistencia en menos de 5 segundos para minimizar filas y tiempos de espera.(U)

---

###Requerimientos de Seguridad y Confianza (Ethos)

####RS-01

El sistema debe requerir autenticación mediante usuario y contraseña para acceder al panel administrativo.(A)

####RS-02

El sistema debe garantizar que cada código QR esté asociado a un único registro de asistencia.(A)

####RS-03

El sistema debe registrar un historial de acciones realizadas por los administradores.(A)

####RS-04

El sistema debe proteger la información almacenada mediante comunicación segura con la API.(A)

####RS-05

El sistema debe garantizar que los datos del usuario y sus registros de asistencia se almacenen de forma segura y sin alteraciones.(U)

