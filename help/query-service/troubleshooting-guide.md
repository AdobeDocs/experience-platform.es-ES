---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;guía de solución de problemas;preguntas frecuentes;solución de problemas;
solution: Experience Platform
title: Guía de solución de problemas del servicio de consultas
topic-legacy: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# [!DNL Query Service] Guía de resolución de problemas

## Errores de API de REST

| Código de estado HTTP | Descripción | Posibles causas |
| ---------------- | ----------- | --------------- |
| 400 | Solicitud incorrecta | Consulta no formada o no válida |
| 401 | Error de autenticación | Token de autenticación no válido |
| 500 | Error interno del servidor | Fallo interno del sistema |

## Errores de API PostgreSQL

| Código de error y estado de conexión | Descripción | Posible causa |
| ------------------------------- | ----------- | -------------- |
| **28P01** Inicio: autenticación | Contraseña no válida | Token de autenticación no válido |
| **28000** Inicio: autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **42P12** Inicio: autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **Consulta 42601**  | Error de sintaxis | Error de sintaxis o comando no válido |
| **Consulta 58000**  | Error del sistema | Fallo interno del sistema |
| **Consulta 42P01**  | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **Consulta 42P07**  | La tabla existe | La tabla ya existe con el mismo nombre (CREATE TABLE) |
| **Consulta 53400**  | El LÍMITE supera el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **Consulta 53400**  | Tiempo de espera de la instrucción | La declaración en directo presentada tardó más de 10 minutos |
| **08P01** N/D | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
