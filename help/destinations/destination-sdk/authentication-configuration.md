---
description: Utilice las configuraciones de autenticación admitidas en Adobe Experience Platform Destination SDK para autenticar usuarios y activar datos en el punto final de destino.
title: Configuración de autenticación
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Configuración de autenticación {#credentials}

## Tipos de autenticación compatibles {#supported-authentication-types}

La configuración de autenticación que seleccione determina cómo se autentica el Experience Platform en el destino, en la interfaz de usuario de Platform.

Adobe Experience Platform Destination SDK admite varios tipos de autenticación:

* [Autenticación del portador](#bearer)
* [Autenticación básica](#basic)
* [[!DNL Amazon S3] autenticación](#s3)
* [[!DNL Azure Blob] Almacenamiento](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP con clave SSH](#sftp-ssh)
* [SFTP con contraseña](#sftp-password)
* [OAuth 2 con código de autorización](#oauth2)
* [OUAth 2 con concesión de contraseña](#oauth2)
* [OAuth 2 con concesión de credenciales de cliente](#oauth2)

Puede configurar la información de autenticación de su destino mediante el `customerAuthenticationConfigurations` parámetros de la variable `/destinations` punto final.

Consulte las secciones siguientes para obtener detalles de configuración de autenticación para cada tipo de destino:

* [Configuraciones de autenticación para destinos de flujo continuo](destination-configuration.md#customer-authentication-configurations)
* [Configuraciones de autenticación para destinos basados en archivos](file-based-destination-configuration.md#customer-authentication-configurations)

## Autenticación básica {#basic}

La autenticación básica es compatible con los destinos de flujo continuo en Experience Platform.

Al configurar el tipo de autenticación básica, se requiere que los usuarios introduzcan un nombre de usuario y una contraseña para conectarse al destino.

Para configurar la autenticación básica para el destino, configure la variable `customerAuthenticationConfigurations` a través de la sección `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticación del portador {#bearer}

La autenticación del portador es compatible con los destinos de flujo continuo en el Experience Platform.

Para configurar la autenticación de tipo al portador para el destino, configure la variable `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] autenticación {#s3}

[!DNL Amazon S3] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Para configurar [!DNL Amazon S3] autenticación para el destino, configure la variable `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Para configurar [!DNL Azure Blob] autenticación para el destino, configure la variable `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Para configurar [!DNL Azure Data Lake Storage] (ADLS) autenticación para su destino, configure el `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

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

[!DNL SFTP] autenticación con [!DNL SSH] se admite para destinos basados en archivos en Experience Platform.

Para configurar la autenticación SFTP con la clave SSH para el destino, configure la variable `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] autenticación con contraseña {#sftp-password}

[!DNL SFTP] la autenticación con contraseña es compatible con destinos basados en archivos en Experience Platform.

Para configurar la autenticación SFTP con contraseña para el destino, configure la variable `customerAuthenticationConfigurations` en el `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] autenticación {#oauth2}

[!DNL OAuth 2] la autenticación es compatible con los destinos de flujo continuo en Experience Platform.

Para obtener información sobre cómo configurar los distintos [!DNL OAuth 2] flujos, así como para [!DNL OAuth 2] soporte técnico, lea la documentación del Destination SDK en [[!DNL OAuth 2] autenticación](./oauth2-authentication.md).


## Cuándo usar la variable `/credentials` Punto de conexión de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, usted *no* es necesario usar la variable `/credentials` extremo de API. En su lugar, puede configurar la información de autenticación de su destino mediante la variable `customerAuthenticationConfigurations` parámetros de la variable `/destinations` punto final.

La variable `/credentials` Se proporciona un punto final de API a los desarrolladores de destino en los casos en que haya un sistema de autenticación global entre el Adobe y el destino y [!DNL Platform] los clientes de no necesitan proporcionar credenciales de autenticación para conectarse al destino.

En este caso, debe crear un objeto credentials utilizando la variable `/credentials` extremo de API. También debe seleccionar `PLATFORM_AUTHENTICATION` en el [configuración de destino](./destination-configuration.md#destination-delivery). Lectura [Operaciones de extremo de la API de credenciales](./credentials-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en la `/credentials` punto final.
