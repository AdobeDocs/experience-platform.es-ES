---
title: Notas de la versión de Adobe Experience Platform, enero de 2020
description: Notas de la versión de enero de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 15 de enero de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Restricciones de tipo campo para campos de jerarquía igual | Una vez definido un campo XDM como un tipo determinado, cualquier otro campo con el mismo nombre y jerarquía debe utilizar el mismo tipo de campo, independientemente de las clases o los grupos de campos de esquema en los que se utilicen. Por ejemplo, si un grupo de campos para el XDM [!DNL Profile] la clase contiene un `profile.age` campo de tipo &quot;integer&quot;, un grupo de campos similar para XDM [!DNL ExperienceEvent] no puede tener un `profile.age` campo de tipo &quot;cadena&quot;. Para utilizar un tipo de campo diferente, el campo debe tener una jerarquía diferente a la definida anteriormente (por ejemplo, `profile.person.age`). Esta función está diseñada para evitar conflictos cuando los esquemas se unen en una unión. Aunque la restricción no afecta retroactivamente a los esquemas existentes, se recomienda encarecidamente que revise los esquemas para los conflictos de tipo campo y que los edite según sea necesario. |
| Validación de campos con distinción de mayúsculas y minúsculas | Los campos personalizados del mismo nivel deben tener nombres diferentes, independientemente de las mayúsculas y minúsculas. Por ejemplo, si agrega un campo personalizado llamado &quot;Correo electrónico&quot;, no puede agregar otro campo personalizado del mismo nivel llamado &quot;correo electrónico&quot;. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre cómo trabajar con XDM mediante la variable [!DNL Schema Registry] API y [!DNL Schema Editor] interfaz de usuario, lea la [Documentación del sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos de clientes personales o privados de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| [!DNL Privacy Service] cambio de marca | El anteriormente denominado &quot;Servicio de RGPD&quot; se ha cambiado a [!DNL Privacy Service] ya que el servicio ha crecido para admitir otras regulaciones además del RGPD. |
| Nuevos extremos de API | Ruta base para la variable [!DNL Privacy Service] La API se ha actualizado desde `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nuevo obligatorio `regulation` property | Al crear nuevos trabajos en el [!DNL Privacy Service] API, un `regulation` debe proporcionarse en la carga útil de la solicitud para indicar en qué regulación debe rastrearse el trabajo. Los valores aceptados son `gdpr` y `ccpa`. |
| Compatibilidad con [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ahora acepta solicitudes de acceso/eliminación de Adobe [!DNL Primetime Authentication], usando `primetimeAuthentication` como su valor de producto. |
| Mejoras en la interfaz de usuario del Privacy Service | Separe las páginas de seguimiento de trabajos para las regulaciones del RGPD y la CCPA. Nuevo **menú desplegable Tipo de reglamento **para cambiar entre los datos de seguimiento del RGPD y la CCPA. |

**Problemas conocidos**

* Ninguna

Para obtener más información, consulte [!DNL Privacy Service], empiece leyendo el [Información general del Privacy Service](../../privacy-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con datos de atributos del cliente | Compatibilidad de la interfaz de usuario y la API para crear conectores de flujo continuo con el fin de introducir datos de atributos del cliente. |
| Compatibilidad con formatos de archivo adicionales para almacenamiento en la nube | La ingesta de archivos desde almacenamiento en la nube ahora es compatible con los formatos de archivo JSON y Parquet compatibles con XDM. |
| Compatibilidad con permisos de control de acceso | El marco de control de acceso de Adobe Experience Platform proporciona los permisos necesarios para conceder acceso a los orígenes en la ingesta de datos. En función de su nivel de permiso, un usuario puede ver las fuentes, administrar las fuentes o no tener acceso completo. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Ingesta de datos | Administrar fuentes | Acceso para leer, crear, editar y deshabilitar orígenes. |
| Ingesta de datos | Ver fuentes | Acceso de solo lectura a los orígenes disponibles en la **[!UICONTROL Catálogo]** y fuentes autenticadas en la **[!UICONTROL Examinar]** pestaña . |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md)

## Destinos {#destinations}

En [Real-Time CDP](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera sencilla.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con permisos de control de acceso | La funcionalidad Destinations de Real-Time CDP funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede ver, administrar y activar destinos. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Destinos | Administrar destinos | Acceso para leer, crear, editar y deshabilitar destinos. |
| Destinos | Ver destinos | Acceso de solo lectura a destinos disponibles en la variable **[!UICONTROL Catálogo]** y destinos autenticados en la **Examinar** pestaña . |
| Destinos | Activar destinos | Capacidad para activar datos en destinos. Este permiso requiere que &quot;Administrar destinos&quot; o &quot;Ver destinos&quot; se agreguen al perfil del producto. |

**Problemas conocidos**

* Ninguna

Consulte la [Información general sobre destinos](../../destinations/home.md) para obtener más información.
