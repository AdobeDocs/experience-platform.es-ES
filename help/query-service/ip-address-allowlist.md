---
keywords: Dirección IP, rango de IP, lista de permitidos, lista de permitidos, servicio de consultas, acceso a la red
title: LISTA DE PERMITIDOS de direcciones IP para el servicio de consultas
description: Esta página proporciona rangos de IP actualizados que puede agregar a su lista de permitidos para obtener acceso seguro al servicio de consultas.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * El Adobe recomienda marcar esta página y volver a visitarla cada tres meses para comprobar las direcciones IP más recientes. El Adobe no notifica nuevos intervalos de IP.
> * A partir del 15 de octubre de 2024, solo los nuevos intervalos de IP son válidos para el acceso al servicio de consulta. Las direcciones IP obsoletas ya no funcionan. Asegúrese de que la lista de permitidos incluya solo las nuevas IP para evitar interrupciones en el servicio.

## Información general {#overview}

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el acceso al Servicio de consultas.

Como parte de las mejoras en curso, Adobe ha actualizado los intervalos de IP para el acceso de red al servicio de consultas. Las direcciones IP anteriores quedan obsoletas y solo son válidas las nuevas. Es esencial actualizar la lista de permitidos para incluir los siguientes intervalos de IP nuevos para mantener el servicio ininterrumpido.

El Adobe recomienda añadir los siguientes intervalos de IP específicos de la región a una lista de permitidos en función de su región. Si no se agregan estos intervalos de IP específicos de la región, pueden producirse errores o interrupciones en el servicio.

## VA7: Clientes de EE. UU. y de Estados Unidos {#us-americas}

**Nueva IP:** 4.152.211.251

## NLD2: Clientes de EMEA {#emea}

**Nueva IP:** 108.141.12.47

## AUS5: Clientes de APAC {#apac}

**Nueva IP:** 40.82.220.111

## CAN2: Clientes canadienses {#can2}

**Nueva IP:** 4.172.28.20

## GBR9: clientes del Reino Unido {#gbr9}

**Nueva IP:** 20.254.80.141

## Configurar restricciones basadas en IP {#set-ip-restrictions}

Use las [guías de la API de autorización de Data Distiller](./auth-api/overview.md) para configurar restricciones basadas en IP. Estas restricciones basadas en IP garantizan que solo las redes y los equipos cliente aprobados puedan acceder a los datos a través de SQL en Adobe Experience Platform. Obtenga información sobre cómo configurar, aplicar y supervisar restricciones de IP para mantener altos estándares de seguridad, con funciones de seguimiento y alertas de acceso en tiempo real.

* [Guía de introducción](./auth-api/getting-started.md)
* [Guía de extremo de acceso IP](./auth-api/ip-access.md)
* [Guía de extremo de validación de IP](./auth-api/validate.md)
