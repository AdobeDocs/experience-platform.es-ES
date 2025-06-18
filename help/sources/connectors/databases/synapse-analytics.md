---
title: Información general sobre el conector Source de Azure Synapse Analytics
description: Obtenga información sobre cómo conectar Azure Synapse Analytics a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 4%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>El origen [!DNL Azure Synapse Analytics] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

[!DNL Azure Synapse Analytics] es un servicio de análisis basado en la nube que unifica big data y data warehouse. Puede ingerir, explorar, preparar y analizar datos con SQL, [!DNL Spark] o herramientas en tiempo real, todo sin mover los datos.

Puede usar el origen [!DNL Azure Synapse Analytics] para conectar su cuenta y llevar los datos a Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar su cuenta de [!DNL Azure Synapse Analytics] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

### Configure los permisos

Para conectar la cuenta de origen a Experience Platform, la cuenta debe tener habilitados los dos permisos siguientes:

* **Ver orígenes**
* **Administrar orígenes**

Si no tiene estos permisos, póngase en contacto con el administrador del producto para solicitar acceso. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/ui/overview.md).

### Autenticar en Experience Platform

Puede usar la autenticación de clave de cuenta o la autenticación de clave principal de servicio para conectar su [!DNL Azure Synapse Analytics] a Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos [!DNL Azure Synapse Analytics] a Experience Platform mediante la autenticación de clave de cuenta.

| Credencial | Descripción |
| --- | --- |
| Cadena de conexión | Esta es la **cadena de conexión** usada para la autenticación con [!DNL Azure Synapse Analytics]. El formato estándar es: `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. Debe reemplazar los marcadores de posición con los detalles de conexión reales. |
| ID de especificación de conexión | La **especificación de conexión** proporciona las propiedades de conector de un origen de datos. Esto incluye detalles como especificaciones de autenticación y requisitos para crear conexiones **base** y **origen**. Para [!DNL Azure Synapse Analytics], el id. de especificación de conexión es: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Nota:** Esta credencial solo es necesaria cuando se conecta a través de API. |

>[!TAB Autenticación de clave principal de servicio]

Para recuperar sus credenciales para la autenticación de clave principal de servicio, vaya a [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home) y recupere los valores de lo siguiente:

* ID de la aplicación
* Nombre para mostrar
* Secreto
* ID de inquilino

A continuación, vaya a la [[!DNL Azure Synapse Analytics] instancia](https://azure.microsoft.com/en-ca/products/synapse-analytics) y seleccione la opción para crear un usuario a partir de un proveedor externo. Desde aquí, proporcione los permisos adecuados para la entidad de seguridad de servicio en el esquema. **NOTA:**: debe incluir &quot;SELECT&quot;, ya que es necesario para la vista previa del esquema, similar a &quot;COPY&quot;. Por ejemplo, un comando de ejemplo puede ser:

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos [!DNL Azure Synapse Analytics] a Experience Platform mediante la autenticación de clave principal de servicio.

| Credencial | Descripción |
| --- | --- |
| Servidor | El nombre de dominio completo de su extremo SQL [!DNL Azure Synapse Analytics]. |
| Base de datos | Nombre de la base de datos específica en el espacio de trabajo [!DNL Azure Synapse Analytics]. |
| Inquilino | El identificador de inquilino [!DNL Azure Active Directory] asociado con su suscripción a [!DNL Azure]. |
| ID principal de servicio | Id. de cliente de una aplicación [!DNL Azure Active Directory]. |
| Clave principal de servicio | El secreto de cliente o la contraseña asociados con la entidad de seguridad de servicio. |
| ID de especificación de conexión | La **especificación de conexión** proporciona las propiedades de conector de un origen de datos. Esto incluye detalles como especificaciones de autenticación y requisitos para crear conexiones **base** y **origen**. Para [!DNL Azure Synapse Analytics], el id. de especificación de conexión es: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Nota:** Esta credencial solo es necesaria cuando se conecta a través de API. |

Para obtener más información, lea la [[!DNL Azure] documentación sobre la administración de identidades para [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Conectar [!DNL Azure Synapse Analytics] a Experience Platform mediante API

* [Conectar  [!DNL Azure Synapse Analytics] a Experience Platform mediante la API de Flow Service](../../tutorials/api/create/databases/synapse-analytics.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Azure Synapse Analytics] a Experience Platform mediante la interfaz de usuario

* [Conectar  [!DNL Azure Synapse Analytics] a Experience Platform en la interfaz de usuario](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)

