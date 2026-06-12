# Resumen del Proyecto

## Nombre del Proyecto
**Sistema de Control de Asistencias mediante Código QR**

## Descripción General

El presente proyecto consiste en el desarrollo de una aplicación móvil para el registro y control de asistencias utilizando códigos QR. La solución está diseñada para optimizar el proceso de validación de entradas y registro de participantes en eventos, capacitaciones, reuniones o cualquier actividad que requiera control de acceso.

La aplicación móvil ha sido desarrollada utilizando **React Native**, permitiendo su funcionamiento en diferentes plataformas móviles. Por su parte, el backend fue implementado en **C#** utilizando **Entity Framework (EF)** como herramienta de acceso a datos y **PostgreSQL** como sistema gestor de base de datos.

## Objetivo

Desarrollar una plataforma que permita registrar asistencias de manera rápida, segura y eficiente mediante la lectura de códigos QR únicos, reduciendo errores manuales y facilitando la administración de usuarios y registros de acceso.

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

El sistema genera una asistencia única para cada participante o entrada registrada. Cada asistencia posee un identificador único universal (**UUID**), el cual se almacena dentro de un código QR.

Cuando el usuario presenta su código QR, la aplicación realiza el escaneo y extrae el UUID contenido en él. Posteriormente, el backend valida la existencia y estado de dicho identificador en la base de datos para confirmar la asistencia correspondiente.

Este mecanismo garantiza que cada registro sea único y evita duplicidades o validaciones incorrectas.
