---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 15 de enero de 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 15 de enero de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM) [!DNL]](#xdm)
* [[!Privacy Service DNL]](#privacy)
* [[!Fuentes DNL]](#sources)
* [[!Destinos DNL]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Restricciones de tipo de campo para campos de jerarquía igual | Después de definir un campo XDM como un tipo determinado, cualquier otro campo con el mismo nombre y jerarquía debe utilizar el mismo tipo de campo, independientemente de las clases o mezclas en las que se utilicen. Por ejemplo, si una mezcla para la clase XDM [!DNL Profile] contiene un `profile.age` campo de tipo &quot;integer&quot;, una mezcla similar para XDM [!DNL ExperienceEvent] no puede tener un `profile.age` campo de tipo &quot;string&quot;. Para utilizar un tipo de campo diferente, el campo debe tener una jerarquía diferente a la definida anteriormente (por ejemplo, `profile.person.age`). Esta función está pensada para evitar conflictos cuando los esquemas se unen en una unión. Aunque la restricción no afecta retroactivamente a los esquemas existentes, se recomienda encarecidamente que revise los esquemas para los conflictos de tipo campo y que los edite según sea necesario. |
| Validación de campo con distinción entre mayúsculas y minúsculas | Los campos personalizados del mismo nivel deben tener nombres diferentes, independientemente del uso de mayúsculas y minúsculas. Por ejemplo, si agrega un campo personalizado llamado &quot;Correo electrónico&quot;, no podrá agregar otro campo personalizado en el mismo nivel llamado &quot;correo electrónico&quot;. |

**Problemas conocidos**

* None

Para obtener más información sobre cómo trabajar con XDM mediante la [!DNL Schema Registry] API y la interfaz de usuario, lea la documentación [!DNL Schema Editor] del sistema [](../../xdm/home.md)XDM.

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales o privados de clientes desde las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas legales y de privacidad de la organización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| [!DNL Privacy Service] renovación de marca | El llamado anteriormente &quot;Servicio de RGPD&quot; ha sido renombrado a [!DNL Privacy Service] medida que el servicio ha crecido para apoyar otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta de acceso base para la [!DNL Privacy Service] API se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nueva propiedad requerida `regulation` | Al crear nuevos trabajos en la [!DNL Privacy Service] API, se debe proporcionar una `regulation` propiedad en la carga útil de la solicitud para indicar en qué regulación se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. |
| Compatibilidad con [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ahora acepta solicitudes de acceso o eliminación de Adobe [!DNL Primetime Authentication], utilizando `primetimeAuthentication` como valor de producto. |
| Mejoras en la interfaz de usuario de Privacy Service | Páginas de seguimiento de trabajos independientes para las regulaciones de RGPD y CCPA. Nuevo **Tipo de Reglamento **menú desplegable para cambiar entre los datos de seguimiento del RGPD y del CCPA. |

**Problemas conocidos**

* None

Para obtener más información sobre [!DNL Privacy Service], lea la descripción general [del](../../privacy-service/home.md)Privacy Service y inicio.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con datos de atributos del cliente | Compatibilidad con la interfaz de usuario y la API para crear conectores de flujo continuo con el fin de ingestar datos de atributos del cliente. |
| Compatibilidad adicional con formatos de archivo para almacenamientos en la nube | La ingestión de archivos desde almacenamientos en la nube ahora es compatible con los formatos de archivo Parquet y JSON compatibles con XDM. |
| Compatibilidad con permisos de control de acceso | El marco de control de acceso de Adobe Experience Platform proporciona los permisos necesarios para otorgar acceso a fuentes en la ingesta de datos. Según el nivel de permiso, un usuario puede realizar vistas de fuentes, administrar fuentes o denegarle el acceso. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Ingesta de datos | Administrar fuentes | Acceso para leer, crear, editar y deshabilitar fuentes. |
| Ingesta de datos | Fuentes de vista | Acceso de sólo lectura a los orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y a los orígenes autenticados en la ficha **[!UICONTROL Examinar]** . |

**Problemas conocidos**

* None

Para obtener más información sobre las fuentes, consulte la descripción general de [las fuentes](../../sources/home.md)

## Destinos {#destinations}

En CDP [en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan datos a dichos socios de una manera transparente.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con permisos de control de acceso | La funcionalidad Destinations de CDP en tiempo real funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede realizar vistas, administrar y activar destinos. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Destinos | Administrar destinos | Acceso para leer, crear, editar y deshabilitar destinos. |
| Destinos | Destinos de vista | Acceso de sólo lectura a los destinos disponibles en la ficha **[!UICONTROL Catálogo]** y a los destinos autenticados en la ficha **Examinar** . |
| Destinos | Activar destinos | Capacidad para activar datos en destinos. Este permiso requiere que se agregue &quot;Administrar destinos&quot; o &quot;Destinos de Vista&quot; al perfil del producto. |

**Problemas conocidos**

* None

See the [Destinations overview](../../rtcdp/destinations/destinations-overview.md) for more information.