---
keywords: Experience Platform;home;popular topics;query service;Query service;troubleshooting guide;faq;troubleshooting;
solution: Experience Platform
title: Guía de solución de problemas del servicio de Consulta de Adobe Experience Platform
topic: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---


# Errores y solución de problemas

## Errores de API de REST

| Código de estado HTTP | Descripción | Causas posibles |
| ---------------- | ----------- | --------------- |
| 400 | Solicitud incorrecta | Consulta mal formada o ilegal |
| 401 | Error de autenticación | Distintivo de autenticación no válido |
| 500 | Error interno del servidor | Error interno del sistema |

## Errores de API PostgreSQL

| Código de error y estado de conexión | Descripción | Posible causa |
| ------------------------------- | ----------- | -------------- |
| **inicio 28P01** : autenticación | Contraseña no válida | Distintivo de autenticación no válido |
| **inicio 28000** : autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **inicio 42P12** : autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **42601** Consulta | Error de sintaxis | Error de comando o sintaxis no válido |
| **58000** Consulta | Error del sistema | Error interno del sistema |
| **consulta 42P01** | No se encontró la tabla | No se encontró la tabla especificada en la consulta |
| **consulta 42P07** | La tabla existe | La tabla ya existe con el mismo nombre (CREAR TABLA) |
| **53400** Consulta | LIMIT excede el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **53400** Consulta | Tiempo de espera de la instrucción | La declaración en vivo enviada tardó más de 10 minutos |
| **08P01** N/D | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
