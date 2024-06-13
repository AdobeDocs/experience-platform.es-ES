---
title: Configuraciones de ejemplo
description: Obtenga información sobre configuraciones de ejemplo con el uso de la herramienta de simulación de gráficos.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 22%

---

# Ejemplo de configuraciones de gráficos

>[!NOTE]
>
>&quot;ID de CRM&quot; es un área de nombres personalizada. Por lo tanto, los ejemplos siguientes requieren que cree un área de nombres personalizada con un nombre para mostrar y un símbolo de identidad de &quot;CRM ID&quot;.

Los siguientes ejemplos de sección de escenarios de gráficos pueden ser útiles para la simulación de gráficos.

## Solo ID de CRM

Eventos:

* ID de CRM: Tom, ECID: 111

Configuración de algoritmo:

| Prioridad | Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID de CRM | ID de CRM | CROSS_DEVICE | Sí |
| 2 | ECID | ECID | COOKIE | NO |

+++Seleccionar para ver un gráfico simulado

+++

## ID de CRM con correo electrónico con hash

En esta situación, se incorpora un ID de CRM que representa los datos en línea (evento de experiencia) y sin conexión (registro de perfil). Este escenario también implica la ingesta de un correo electrónico con hash, que representa otro área de nombres enviado en el conjunto de datos de registro de CRM junto con el ID de CRM.

Eventos:

* ID de CRM: Tom, Email_LC_SHA256: tom<span>@acme.com
* ID de CRM: Tom, ECID: 111
* CRM ID: Summer, Email_LC_SHA256: Summer<span>@acme.com
* ID de CRM: Summer, ECID: 222

Configuración de algoritmo:

| Prioridad | Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID de CRM | ID de CRM | CROSS_DEVICE | Sí |
| 2 | Correos electrónicos (SHA256, en minúsculas) | Email_LC_SHA256 | Correo electrónico | NO |
| 3 | ECID | ECID | COOKIE | NO |

+++Seleccionar para ver un gráfico simulado

+++

## ID de CRM con correo electrónico con hash, teléfono con hash, GAID e IDFA

Eventos:

* ID de CRM: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* ID de CRM: Tom, ECID: 111
* ID de CRM: Tom, ECID: 222, IDFA: A-A-A
* ID de CRM: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* ID de CRM: Summer, ECID: 333
* ID de CRM: Summer, ECID: 444, GAID: B-B-B

Configuración de algoritmo:

| Prioridad | Nombre para mostrar | Símbolo de identidad | Tipo de identidad | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID de CRM | ID de CRM | CROSS_DEVICE | Sí |
| 2 | Correos electrónicos (SHA256, en minúsculas) | Email_LC_SHA256 | Correo electrónico | NO |
| 3 | Teléfono (SHA256) | Phone_SHA256 | Teléfono | NO |
| 4 | ID de anuncio de Google (GAID) | GAID | DISPOSITIVO | NO |
| 5 | Apple IDFA (ID para Apple) | IDFA | DISPOSITIVO | NO |
| 6 | ECID | ECID | COOKIE | NO |

+++Seleccionar para ver un gráfico simulado

+++