---
description: Utilice las configuraciones de autenticación admitidas en el SDK de destino de Adobe Experience Platform para autenticar usuarios y activar datos en el punto final de destino.
title: Configuración de autenticación
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Configuración de autenticación {#credentials}

## Tipos de autenticación compatibles {#supported-authentication-types}

El SDK de destino de Adobe Experience Platform admite varios tipos de autenticación:

* Autenticación del portador
* OAuth 2 con código de autorización
* OUAth 2 con concesión de contraseña
* OAuth 2 con concesión de credenciales de cliente

Puede configurar la información de autenticación de su destino mediante el `customerAuthenticationConfigurations` parámetros de la variable `/destinations` punto final. Consulte la [sección configuraciones de autenticación de cliente](./destination-configuration.md#customer-authentication-configurations) en el artículo de configuración de destino y en las secciones siguientes para obtener información específica sobre las configuraciones de cada tipo de autenticación.

## Autenticación del portador {#bearer}

Para configurar la autenticación de tipo al portador para sus destinos, solo necesita configurar la variable `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## Autenticación OAuth 2 {#oauth2}

Para obtener información sobre cómo configurar los distintos flujos de OAuth 2 admitidos, así como para la compatibilidad con OAuth 2 personalizado, consulte la documentación del SDK de destino en [Autenticación OAuth 2](./oauth2-authentication.md).


## Cuándo usar la variable `/credentials` Punto de conexión de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, usted *no* es necesario usar la variable `/credentials` extremo de API. En su lugar, puede configurar la información de autenticación de su destino mediante la variable `customerAuthenticationConfigurations` parámetros de la variable `/destinations` punto final.

La variable `/credentials` Se proporciona un punto final de API a los desarrolladores de destino en los casos en que haya un sistema de autenticación global entre el Adobe y el destino y [!DNL Platform] los clientes de no necesitan proporcionar credenciales de autenticación para conectarse al destino.

En este caso, debe crear un objeto credentials utilizando la variable `/credentials` extremo de API. También debe seleccionar `PLATFORM_AUTHENTICATION` en el [configuración de destino](./destination-configuration.md#destination-delivery). Lectura [Operaciones de extremo de la API de credenciales](./credentials-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en la `/credentials` punto final.
