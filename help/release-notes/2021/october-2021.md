---
title: Notas de la versión de Adobe Experience Platform de octubre de 2021
description: Las notas de la versión de octubre de 2021 de Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de octubre de 2021**

## Actualizaciones para el Experience Platform

Actualizaciones en el Experience Platform.

### Interfaz de usuario {#ui}

La interfaz de usuario de se ha actualizado con los siguientes cambios:

| Función | Descripción |
| --- | --- |
| Tema oscuro | Utilice el conmutador Tema oscuro para alternar entre los temas claro y oscuro en la interfaz de Platform. El conmutador se encuentra en el perfil de usuario, debajo del nombre de usuario y el correo electrónico. |
| Alternar navegación izquierda | Utilice la opción de navegación mejorada en la parte superior del encabezado de la aplicación para mostrar u ocultar el menú que muestra las funciones del Experience Platform. El sistema recuerda la última selección y muestra únicamente las funciones a las que tiene acceso. |
| Visibilidad de acceso | La barra de navegación izquierda muestra únicamente las funciones a las que puede acceder. En versiones anteriores de Adobe Experience Platform, los elementos no disponibles eran visibles, incluso si no podía acceder a ellos. |

Consulte la [Guía de IU de Platform](../../landing/ui-guide.md) para obtener más información.

## Actualizaciones de funciones existentes

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Fuentes](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Función  de `contains_key` | El `contains_key` se ha introducido la función, que permite comprobar si el objeto existe dentro del origen. Esta función sustituye a `is_set` función, que ahora está obsoleta. |
| Mensajes de error | Mensajes de error devueltos por el `/mappingSets/preview` Los puntos finales de la API de preparación de datos ahora son coherentes con los mensajes de error generados durante el tiempo de ejecución. |

Consulte la [[!DNL Data Prep] descripción general](../../data-prep/home.md) para obtener más información sobre este servicio.

### Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| [!DNL Amazon S3] mejoras de origen | Ahora puede utilizar la variable `s3SessionToken` para conectar su [!DNL Amazon S3] a Platform mediante credenciales de seguridad temporales. Este token le permite proporcionar acceso temporal a su organización a corto plazo. [!DNL Amazon S3] recursos para usuarios en entornos que no son de confianza. Consulte la [[!DNL Amazon S3] Documentación](../../sources/connectors/cloud-storage/s3.md#prerequisites) para obtener más información. |
| [!DNL Generic REST API] (Beta) | Ahora puede crear un [!DNL Generic REST API] conexión de origen mediante [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) para llevar datos de una aplicación REST genérica a Platform. Consulte la [[!DNL Generic REST API] descripción general](../../sources/connectors/protocols/generic-rest.md) para obtener más información. |
| [!DNL Zoho CRM] (Beta) | Ahora puede crear un [!DNL Zoho CRM] conexión de origen mediante [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) o el [interfaz de usuario](../../sources/tutorials/ui/create/crm/zoho.md) para obtener datos de su [!DNL Zoho CRM] a Platform. Consulte la [[!DNL Zoho CRM] descripción general](../../sources/connectors/crm/zoho.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
