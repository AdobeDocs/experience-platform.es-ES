---
description: Utilice las configuraciones de autenticación admitidas en Adobe Experience Platform Destination SDK para autenticar a los usuarios y activar los datos en el punto final de destino.
title: Configuración de autenticación
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Configuración de autenticación {#credentials}

## Tipos de autenticación admitidos {#supported-authentication-types}

La configuración de autenticación que seleccione determina cómo se autentica Experience Platform en el destino, en la IU de Platform.

El Adobe Experience Platform Destination SDK admite varios tipos de autenticación:

* [Autenticación del portador](#bearer)
* [Autenticación básica](#basic)
* [[!DNL Amazon S3] authentication](#s3)
* [[!DNL Azure Blob] Almacenamiento](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP con clave SSH](#sftp-ssh)
* [SFTP con contraseña](#sftp-password)
* [OAuth 2 con código de autorización](#oauth2)
* [OAUth 2 con concesión de contraseña](#oauth2)
* [OAuth 2 con concesión de credenciales de cliente](#oauth2)

Puede configurar la información de autenticación del destino mediante el `customerAuthenticationConfigurations` parámetros del `/destinations` punto final.

Consulte las secciones siguientes para obtener detalles sobre la configuración de autenticación para cada tipo de destino:

* [Configuraciones de autenticación para destinos de flujo continuo](destination-configuration.md#customer-authentication-configurations)
* [Configuraciones de autenticación para destinos basados en archivos](file-based-destination-configuration.md#customer-authentication-configurations)

## Autenticación básica {#basic}

La autenticación básica es compatible con los destinos de flujo continuo en Experience Platform.

Al configurar el tipo de autenticación básico, los usuarios deben introducir un nombre de usuario y una contraseña para conectarse al destino.

Para configurar la autenticación básica para el destino, configure el `customerAuthenticationConfigurations` a través de la `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticación del portador {#bearer}

La autenticación del portador es compatible con los destinos de streaming en Experience Platform.

Para configurar la autenticación de tipo portador para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] authentication {#s3}

[!DNL Amazon S3] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Para configurar [!DNL Amazon S3] para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Para configurar [!DNL Azure Blob] para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Para configurar [!DNL Azure Data Lake Storage] (ADLS) para su destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] autenticación con [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] autenticación con [!DNL SSH] La clave de es compatible con destinos basados en archivos en Experience Platform.

Para configurar la autenticación SFTP con clave SSH para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] autenticación con contraseña {#sftp-password}

[!DNL SFTP] la autenticación con contraseña es compatible con destinos basados en archivos en Experience Platform.

Para configurar la autenticación SFTP con contraseña para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] authentication {#oauth2}

[!DNL OAuth 2] la autenticación es compatible con los destinos de flujo continuo en Experience Platform.

Para obtener información sobre cómo configurar las distintas API compatibles [!DNL OAuth 2] flujos, así como para los flujos personalizados [!DNL OAuth 2] para obtener asistencia técnica, lea la documentación del Destination SDK sobre [[!DNL OAuth 2] authentication](./oauth2-authentication.md).


## Cuándo usar el `/credentials` Extremo de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, *no* necesita usar el `/credentials` Extremo de API. En su lugar, puede configurar la información de autenticación para su destino mediante el `customerAuthenticationConfigurations` parámetros del `/destinations` punto final.

El `/credentials` El extremo de la API se proporciona a los desarrolladores de destino para los casos en los que hay un sistema de autenticación global entre el Adobe y el destino y [!DNL Platform] los clientes no necesitan proporcionar credenciales de autenticación para conectarse a su destino.

En este caso, debe crear un objeto de credenciales utilizando `/credentials` Extremo de API. También debe seleccionar `PLATFORM_AUTHENTICATION` en el [configuración de destino](./destination-configuration.md#destination-delivery). Leer [Operaciones de extremo de API de credenciales](./credentials-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en la `/credentials` punto final.
