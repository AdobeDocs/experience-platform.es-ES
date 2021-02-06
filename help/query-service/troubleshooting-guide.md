---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;guía de resolución de problemas;faq;solución de problemas;
solution: Experience Platform
title: Guía de resolución de problemas del servicio de consulta
topic: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---


# [!DNL Query Service] Guía de resolución de problemas

## Errores de API de REST

| Código de estado HTTP | Descripción | Causas posibles |
| ---------------- | ----------- | --------------- |
| 400 | Solicitud incorrecta | Consulta mal formada o ilegal |
| 401 | Error de autenticación | Distintivo de autenticación no válido |
| 500 | Error interno del servidor | Error interno del sistema |

## Errores de API PostgreSQL

| Código de error y estado de conexión | Descripción | Posible causa |
| ------------------------------- | ----------- | -------------- |
| **28P01** Inicio: autenticación | Contraseña no válida | Distintivo de autenticación no válido |
| **28000** Inicio: autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **42P12** Inicio: autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **42601** Consulta | Error de sintaxis | Error de comando o sintaxis no válido |
| **58000** Consulta | Error del sistema | Error interno del sistema |
| **42P01** Consulta | No se encontró la tabla | No se encontró la tabla especificada en la consulta |
| **42P07** Consulta | La tabla existe | La tabla ya existe con el mismo nombre (CREAR TABLA) |
| **53400** Consulta | LIMIT excede el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **53400** Consulta | Tiempo de espera de la instrucción | La declaración en vivo enviada tardó más de 10 minutos |
| **08P01** N/D | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
