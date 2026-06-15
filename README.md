# Resumen del Proyecto

## Nombre del Proyecto

**Sistema de Control de Asistencias mediante Código QR**

## Descripción General

El presente proyecto consiste en el desarrollo de una aplicación móvil para el registro y control de asistencias y salidas utilizando códigos QR. La solución está diseñada para optimizar el proceso de validación de entradas y registro de participantes en eventos, capacitaciones, reuniones o cualquier actividad que requiera control de acceso.

La aplicación móvil ha sido desarrollada utilizando **React Native**, permitiendo su funcionamiento en diferentes plataformas móviles. Por su parte, el backend fue implementado en **C#** utilizando **Entity Framework (EF)** como herramienta de acceso a datos y **PostgreSQL** como sistema gestor de base de datos.

## Objetivo

Desarrollar una plataforma que permita registrar asistencias de manera rápida, segura y eficiente mediante la lectura de códigos QR únicos, reduciendo errores manuales y facilitando la administración de usuarios y registros de acceso.

## Problema de Negocio

Las instituciones educativas, empresas y organizaciones que realizan eventos, capacitaciones o reuniones suelen registrar la asistencia de manera manual, provocando retrasos en el acceso de los participantes, errores en los registros y dificultades para generar reportes confiables.

En eventos con aproximadamente 100 asistentes, el proceso de registro puede requerir hasta 300 minutos acumulados de atención, afectando la eficiencia operativa y la experiencia de los participantes.

## Impacto del Problema

- Retrasos durante el ingreso de asistentes.
- Errores humanos en la captura de información.
- Dificultad para consultar asistencias históricas.
- Mayor carga administrativa para generar reportes.
- Riesgo de registros duplicados o incorrectos.

## Solución Propuesta

Desarrollar una aplicación móvil que permita registrar asistencias mediante códigos QR únicos asociados a cada participante o entrada.

El sistema automatiza la validación de accesos y almacena la información en tiempo real, permitiendo una gestión eficiente de usuarios, eventos y reportes.

## Arquitectura Tecnológica

### Frontend
- React Native
- Interfaz móvil multiplataforma
- Escaneo de códigos QR
- Gestión de usuarios y asistencias

### Backend
- C#
- ASP.NET Web API
- Entity Framework (EF)
- Arquitectura basada en servicios REST

### Base de Datos
- PostgreSQL
- Almacenamiento de usuarios, eventos, asistencias y registros de acceso

## Funcionamiento del Sistema

El sistema genera una asistencia única para cada participante o entrada registrada. Cada asistencia posee un identificador único universal (**UID**), el cual se almacena dentro de un código QR.

Cuando el usuario presenta su código QR, la aplicación realiza el escaneo y extrae el UUID contenido en él. Posteriormente, el backend valida la existencia y estado de dicho identificador en la base de datos para confirmar la asistencia correspondiente.

Este mecanismo garantiza que cada registro sea único y evita duplicidades o validaciones incorrectas.

## Características Principales

### Registro de Asistencias
- Escaneo de códigos QR.
- Validación automática de registros.
- Confirmación inmediata de asistencia.
- Prevención de registros duplicados.

### Administración de Usuarios
- Alta de usuarios.
- Modificación de información.
- Consulta de usuarios registrados.
- Gestión de permisos y accesos.

### Gestión de Entradas
- Creación de entradas o registros de asistencia.
- Generación de códigos QR únicos.
- Asociación de UUID a cada entrada.
- Control y seguimiento de accesos.

### Seguridad
- Uso de UUID como identificador único.
- Validación de datos desde el servidor.
- Integridad de la información almacenada.
- Comunicación entre cliente y servidor mediante API REST.

## Beneficios

- Automatización del proceso de registro de asistencias.
- Reducción de errores humanos.
- Mayor velocidad en el control de acceso.
- Trazabilidad completa de los registros.
- Escalabilidad para eventos de distintos tamaños.
- Administración centralizada de usuarios y entradas.

## Resultado Esperado

La implementación de este sistema permitirá contar con una plataforma moderna para el control de asistencias basada en tecnología móvil y códigos QR, proporcionando una gestión eficiente de usuarios, entradas y registros de acceso mediante una arquitectura robusta compuesta por React Native, C#, Entity Framework y PostgreSQL.
