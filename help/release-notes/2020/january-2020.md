---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 15 de enero de 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 15 de enero de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM)  {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Restricciones de tipo campo para campos de jerarquía igual | Una vez definido un campo XDM como un tipo determinado, cualquier otro campo con el mismo nombre y jerarquía debe utilizar el mismo tipo de campo, independientemente de las clases o los grupos de campos de esquema en los que se utilicen. Por ejemplo, si un grupo de campos de la clase XDM [!DNL Profile] contiene un campo `profile.age` de tipo &quot;integer&quot;, un grupo de campos similar para XDM [!DNL ExperienceEvent] no puede tener un campo `profile.age` de tipo &quot;string&quot;. Para utilizar un tipo de campo diferente, el campo debe tener una jerarquía diferente a la definida anteriormente (por ejemplo, `profile.person.age`). Esta función está diseñada para evitar conflictos cuando los esquemas se unen en una unión. Aunque la restricción no afecta retroactivamente a los esquemas existentes, se recomienda encarecidamente que revise los esquemas para los conflictos de tipo campo y que los edite según sea necesario. |
| Validación de campos con distinción de mayúsculas y minúsculas | Los campos personalizados del mismo nivel deben tener nombres diferentes, independientemente de las mayúsculas y minúsculas. Por ejemplo, si agrega un campo personalizado llamado &quot;Correo electrónico&quot;, no puede agregar otro campo personalizado del mismo nivel llamado &quot;correo electrónico&quot;. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre cómo trabajar con XDM mediante la API [!DNL Schema Registry] y la interfaz de usuario [!DNL Schema Editor], lea la [Documentación del sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API y una interfaz de usuario de RESTful para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos de clientes personales o privados de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| [!DNL Privacy Service] cambio de marca | El anteriormente llamado &quot;Servicio de RGPD&quot; se ha cambiado a [!DNL Privacy Service] ya que el servicio ha crecido para admitir otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta base para la API [!DNL Privacy Service] se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nueva propiedad `regulation` necesaria | Al crear nuevos trabajos en la API [!DNL Privacy Service], se debe proporcionar una propiedad `regulation` en la carga útil de la solicitud para indicar en qué regulación se debe realizar un seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. |
| Compatibilidad con [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ahora acepta solicitudes de acceso/eliminación de Adobe  [!DNL Primetime Authentication], utilizando  `primetimeAuthentication` como valor de producto. |
| Mejoras en la interfaz de usuario del Privacy Service | Separe las páginas de seguimiento de trabajos para las regulaciones del RGPD y la CCPA. Nuevo **menú desplegable Tipo de reglamento **para cambiar entre los datos de seguimiento del RGPD y la CCPA. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre [!DNL Privacy Service], comience leyendo el [resumen del Privacy Service](../../privacy-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

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
| Ingesta de datos | Ver fuentes | Acceso de solo lectura a los orígenes disponibles en la pestaña **[!UICONTROL Catalog]** y a los orígenes autenticados en la pestaña **[!UICONTROL Browse]**. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte la [información general de las fuentes](../../sources/home.md)

## Destinos {#destinations}

En [CDP en tiempo real](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a esos socios de una manera transparente.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con permisos de control de acceso | La funcionalidad Destinations de CDP en tiempo real funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede ver, administrar y activar destinos. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Destinos | Administrar destinos | Acceso para leer, crear, editar y deshabilitar destinos. |
| Destinos | Ver destinos | Acceso de solo lectura a destinos disponibles en la pestaña **[!UICONTROL Catalog]** y destinos autenticados en la pestaña **Browse**. |
| Destinos | Activar destinos | Capacidad para activar datos en destinos. Este permiso requiere que &quot;Administrar destinos&quot; o &quot;Ver destinos&quot; se agreguen al perfil del producto. |

**Problemas conocidos**

* Ninguna

Consulte la [Información general sobre destinos](../../destinations/home.md) para obtener más información.
