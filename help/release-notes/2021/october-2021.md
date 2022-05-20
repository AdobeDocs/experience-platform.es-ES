---
title: Notas de la versión de Adobe Experience Platform, octubre de 2021
description: Notas de la versión de octubre de 2021 para Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de octubre de 2021**

## Actualizaciones para el Experience Platform

Actualizaciones para el Experience Platform.

### Interfaz de usuario {#ui}

La interfaz de usuario se ha actualizado con los siguientes cambios:

| Función | Descripción |
| --- | --- |
| Tema oscuro | Utilice el conmutador de temas oscuros para alternar entre temas claros y oscuros en la interfaz de Platform. El conmutador se encuentra en el perfil de usuario debajo del nombre de usuario y el correo electrónico. |
| Alternar navegación izquierda | Utilice el botón de navegación mejorado en la parte superior del encabezado de la aplicación para mostrar u ocultar el menú que muestra las capacidades del Experience Platform. El sistema recuerda la última selección y muestra únicamente las funcionalidades a las que tiene acceso. |
| Visibilidad del acceso | La barra de navegación izquierda muestra únicamente las funciones a las que puede acceder. En versiones anteriores de Adobe Experience Platform, los elementos no disponibles eran visibles, incluso si no se podía acceder a ellos. |

Consulte la [Guía de la interfaz de usuario de Platform](../../landing/ui-guide.md) para obtener más información.

## Actualizaciones de funciones existentes

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Fuentes](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Función  de `contains_key` | La variable `contains_key` se ha introducido, lo que permite comprobar si el objeto existe en el origen. Esta función reemplaza a la función `is_set` , que ahora está en desuso. |
| Mensajes de error | Mensajes de error devueltos por el `/mappingSets/preview` en la API de preparación de datos ahora son coherentes con los mensajes de error generados durante el tiempo de ejecución. |

Consulte la [[!DNL Data Prep] información general](../../data-prep/home.md) para obtener más información sobre este servicio.

### Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| [!DNL Amazon S3] mejoras de la fuente | Ahora puede usar la variable `s3SessionToken` para conectar su [!DNL Amazon S3] cuenta a Platform con credenciales de seguridad temporales. Este token le permite proporcionar acceso temporal y a corto plazo a su [!DNL Amazon S3] recursos para usuarios en entornos de confianza. Consulte la [[!DNL Amazon S3] Documentación de la ](../../sources/connectors/cloud-storage/s3.md#prerequisites) para obtener más información. |
| [!DNL Generic REST API] (Beta) | Ahora puede crear un [!DNL Generic REST API] conexión de origen utilizando la variable [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) para traer datos de una aplicación REST genérica a Platform. Consulte la [[!DNL Generic REST API] información general](../../sources/connectors/protocols/generic-rest.md) para obtener más información. |
| [!DNL Zoho CRM] (Beta) | Ahora puede crear un [!DNL Zoho CRM] conexión de origen utilizando la variable [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) o [interfaz de usuario](../../sources/tutorials/ui/create/crm/zoho.md) para obtener datos de su [!DNL Zoho CRM] a Platform. Consulte la [[!DNL Zoho CRM] información general](../../sources/connectors/crm/zoho.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
