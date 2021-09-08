---
description: Esta configuración determina cómo se autentican los usuarios de Adobe Experience Platform en el punto final de destino para activar los datos.
title: Opciones de configuración para credenciales en el SDK de destino
source-git-commit: 11f6421665acc2041aa9483b1e0efb6fe48b6dfb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Configuración de autenticación {#credentials}

## Tipos de autenticación compatibles {#supported-authentication-types}

Adobe Experience Platform admite varios tipos de autenticación:

* Autenticación del portador
* OAuth 2 con código de autorización
* OUAth 2 con concesión de contraseña
* OAuth 2 con concesión de credenciales de cliente

Para los distintos flujos OAuth 2 compatibles, así como para la compatibilidad con OAuth 2 personalizada, lea la documentación del SDK de destino sobre [Autenticación OAuth 2](./oauth2-authentication.md).

Puede configurar la información de autenticación para el destino mediante los parámetros `customerAuthenticationConfigurations` del extremo `/destinations` . Consulte la sección [configuraciones de autenticación de cliente](./destination-configuration.md#customer-authentication-configurations) en el artículo de configuración de destino.

## Cuándo utilizar el extremo de la API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, *no* necesita utilizar el extremo de la API `/credentials`. En su lugar, puede configurar la información de autenticación para el destino mediante los parámetros `customerAuthenticationConfigurations` del extremo `/destinations` .

Utilice el extremo `activation/authoring/credentials` de la API y seleccione `PLATFORM_AUTHENTICATION` en la [configuración de destino](./destination-configuration.md#destination-delivery) si hay un sistema de autenticación global entre el Adobe y el destino y el cliente [!DNL Platform] no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando el extremo API `/credentials` . Lea [Credentials API endpoint operations](./credentials-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en el extremo `/credentials`.