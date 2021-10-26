---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 14%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de octubre de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Fuentes](#sources)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| [!DNL Amazon S3] mejoras de la fuente | Ahora puede usar la variable `s3SessionToken` para conectar su [!DNL Amazon S3] cuenta a Platform con credenciales de seguridad temporales. Este token le permite proporcionar acceso temporal y a corto plazo a su [!DNL Amazon S3] recursos para usuarios en entornos de confianza. Consulte la [[!DNL Amazon S3] documentación](../../sources/connectors/cloud-storage/s3.md#prerequisites) para obtener más información. |
| [!DNL Generic REST API] (Beta) | Ahora puede crear un [!DNL Generic REST API] conexión de origen utilizando la variable [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) o [interfaz de usuario](../../sources/tutorials/ui/create/protocols/generic-rest.md) para traer datos de una aplicación REST genérica a Platform. Consulte la [[!DNL Generic REST API] información general](../../sources/connectors/protocols/generic-rest.md) para obtener más información. |
| [!DNL Zoho CRM] (Beta) | Ahora puede crear un [!DNL Zoho CRM] conexión de origen utilizando la variable [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) o [interfaz de usuario](../../sources/tutorials/ui/create/crm/zoho.md) para obtener datos de su [!DNL Zoho CRM] a Platform. Consulte la [[!DNL Zoho CRM] información general](../../sources/connectors/crm/zoho.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
