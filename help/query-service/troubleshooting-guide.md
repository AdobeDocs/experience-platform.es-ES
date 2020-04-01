---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de solución de problemas del servicio de Consulta de Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda

---


# Errores y solución de problemas

## Errores de API de REST

| Código de estado HTTP | Descripción | Causas posibles |
| ---------------- | ----------- | --------------- |
| 400 | Solicitud incorrecta | consulta mal formada o ilegal |
| 401 | Error de autenticación | Distintivo de autenticación no válido |
| 500 | Error interno del servidor | Error interno del sistema |

## Errores de API PostgreSQL

| Código de error y estado de conexión | Descripción | Posible causa |
| ------------------------------- | ----------- | -------------- |
| **Inicio 28P01** : autenticación | Contraseña no válida | Distintivo de autenticación no válido |
| **Inicio 28000** : autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **Inicio 42P12** : autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **42601** Consulta | Error de sintaxis | Error de comando o sintaxis no válido |
| **58000** Consulta | Error del sistema | Error interno del sistema |
| **Consulta 42P01** | No se encontró la tabla | No se encontró la tabla especificada en la consulta |
| **Consulta 42P07** | La tabla existe | La tabla ya existe con el mismo nombre (CREAR TABLA) |
| **53400** Consulta | LIMIT excede el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **53400** Consulta | Tiempo de espera de la instrucción | La declaración en vivo enviada tardó más de 10 minutos |
| **08P01** N/D | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
