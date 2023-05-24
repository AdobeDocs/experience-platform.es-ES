---
description: Obtenga información sobre cómo configurar un mecanismo de autenticación para su destino y obtener información sobre lo que los usuarios verán en la interfaz de usuario según el método de autenticación que seleccione.
title: Configuración de autenticación del cliente
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# Configuración de autenticación del cliente

Experience Platform proporciona una buena flexibilidad en los protocolos de autenticación disponibles para socios y clientes. Puede configurar su destino para que admita cualquiera de los métodos de autenticación estándar del sector, como [!DNL OAuth2], autenticación de token de portador, autenticación de contraseña y mucho más.

Esta página explica cómo configurar su destino utilizando el método de autenticación preferido. En función de la configuración de autenticación que utilice al crear el destino, los clientes verán diferentes tipos de páginas de autenticación al conectarse al destino en la interfaz de usuario de Experience Platform.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Para que los clientes puedan exportar datos de Platform a su destino de, deben crear una nueva conexión entre Experience Platform y su destino siguiendo los pasos que se describen en la [conexión de destino](../../../ui/connect-destination.md) tutorial.

Cuándo [creación de un destino](../../authoring-api/destination-configuration/create-destination-configuration.md) mediante el Destination SDK, la variable `customerAuthenticationConfigurations` define lo que los clientes ven en [pantalla de autenticación](../../../ui/connect-destination.md#authenticate). Según el tipo de autenticación de destino, los clientes deben proporcionar varios detalles de autenticación, como:

* Para destinos que utilizan [autenticación básica](#basic), los usuarios deben proporcionar un nombre de usuario y una contraseña directamente en la página de autenticación de la IU de Experience Platform.
* Para destinos que utilizan [autenticación de portador](#bearer), los usuarios deben proporcionar un token de portador.
* Para destinos que utilizan [Autenticación OAuth2](#oauth2), los usuarios se redirigen a la página de inicio de sesión de destino, donde pueden iniciar sesión con sus credenciales.
* Para [Amazon S3](#s3) destinos, los usuarios deben proporcionar su [!DNL Amazon S3] clave de acceso y clave secreta.
* Para [Azure Blob](#blob) destinos, los usuarios deben proporcionar su [!DNL Azure Blob] cadena de conexión.

Puede configurar los detalles de autenticación del cliente mediante el `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

En este artículo se describen todas las configuraciones de autenticación de cliente admitidas que puede utilizar para el destino y se muestra lo que los clientes verán en la interfaz de usuario de Experience Platform en función del método de autenticación que configure para el destino.

>[!IMPORTANT]
>
>La configuración de autenticación del cliente no requiere que configure ningún parámetro. Puede copiar y pegar los fragmentos de código que se muestran en esta página en las llamadas de API cuando [creación](../../authoring-api/destination-configuration/create-destination-configuration.md) o [actualización](../../authoring-api/destination-configuration/update-destination-configuration.md) Seleccione una configuración de destino y los usuarios verán la pantalla de autenticación correspondiente en la interfaz de usuario de Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Configuración de regla de autenticación {#authentication-rule}

Cuando utilice cualquiera de las configuraciones de autenticación de clientes descritas en esta página, establezca siempre el `authenticationRule` parámetro en [envío de destino](destination-delivery.md) hasta `"CUSTOMER_AUTHENTICATION"`, como se muestra a continuación.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Autenticación básica {#basic}

La autenticación básica es compatible con integraciones en tiempo real (streaming) en Experience Platform.

Al configurar el tipo de autenticación básico, los usuarios deben introducir un nombre de usuario y una contraseña para conectarse al destino.

![Representación de la IU con autenticación básica](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Para configurar la autenticación básica para el destino, configure el `customerAuthenticationConfigurations` a través de la `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticación del portador {#bearer}

Al configurar el tipo de autenticación de portador, los usuarios deben introducir el token de portador que obtienen de su destino.

![Representación de la IU con autenticación de portador](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Para configurar la autenticación de tipo portador para el destino, configure el `customerAuthenticationConfigurations` a través de la `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## Autenticación OAuth 2 {#oauth2}

Los usuarios seleccionan **[!UICONTROL Conectar con destino]** para almacenar en déclencheur el flujo de autenticación de OAuth 2 en su destino, como se muestra en el ejemplo siguiente para el destino de Audiencias personalizadas de Twitter. Para obtener información detallada sobre la configuración de la autenticación OAuth 2 en el extremo de destino, lea la [Página de autenticación de Destination SDK OAuth 2](oauth2-authentication.md).

![Representación de la interfaz de usuario con autenticación OAuth 2](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Para configurar [!DNL OAuth2] para el destino, configure el `customerAuthenticationConfigurations` a través de la `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Autenticación de Amazon S3 {#s3}

[!DNL Amazon S3] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Al configurar el tipo de autenticación de Amazon S3, los usuarios deben introducir sus credenciales de S3.

![Representación de la IU con autenticación S3](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Para configurar [!DNL Amazon S3] para el destino, configure el `customerAuthenticationConfigurations` a través de la `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Autenticación de Azure Blob  {#blob}

[!DNL Azure Blob Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Al configurar el tipo de autenticación de Azure Blob, los usuarios deben introducir la cadena de conexión.

![Representación de la IU con autenticación Blob](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Para configurar [!DNL Azure Blob] para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] authentication {#adls}

[!DNL Azure Data Lake Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Al configurar la variable [!DNL Azure Data Lake Storage] Tipo de autenticación, los usuarios deben introducir las credenciales de la entidad principal del servicio de Azure y su información de inquilino.

![Procesamiento de IU con [!DNL Azure Data Lake Storage] authentication](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Para configurar [!DNL Azure Data Lake Storage] (ADLS) para su destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP con autenticación de contraseña

[!DNL SFTP] la autenticación con contraseña es compatible con destinos basados en archivos en Experience Platform.

Al configurar el SFTP con un tipo de autenticación por contraseña, los usuarios deben introducir el nombre de usuario y la contraseña del SFTP, así como el dominio y el puerto del SFTP (el puerto predeterminado es 22).

![Representación de la interfaz de usuario con SFTP con autenticación por contraseña](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Para configurar la autenticación SFTP con contraseña para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP con autenticación de clave SSH

[!DNL SFTP] autenticación con [!DNL SSH] La clave de es compatible con destinos basados en archivos en Experience Platform.

Al configurar el SFTP con el tipo de autenticación de clave SSH, los usuarios deben introducir el nombre de usuario y la clave SSH del SFTP, así como el dominio y el puerto del SFTP (el puerto predeterminado es 22).

![Representación de la interfaz de usuario con SFTP con autenticación de clave SSH](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Para configurar la autenticación SFTP con clave SSH para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] authentication {#gcs}

[!DNL Google Cloud Storage] la autenticación es compatible con destinos basados en archivos en Experience Platform.

Al configurar la variable [!DNL Google Cloud Storage] tipo de autenticación, los usuarios deben introducir su [!DNL Google Cloud Storage] [!UICONTROL ID de clave de acceso] y [!UICONTROL clave de acceso secreta].

![Representación de la IU con autenticación de Google Cloud Storage](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Para configurar [!DNL Google Cloud Storage] para el destino, configure el `customerAuthenticationConfigurations` en el campo `/destinations` como se muestra a continuación:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo puede configurar la autenticación de usuarios en la plataforma de destino.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)