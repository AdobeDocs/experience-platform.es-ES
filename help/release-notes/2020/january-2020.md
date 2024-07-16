---
title: Notas de la versión de Adobe Experience Platform, enero de 2020
description: Las notas de la versión de enero de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 13%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 15 de enero de 2020**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## Sistema [!DNL Experience Data Model] (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Restricciones de tipo de campo para campos de igual jerarquía | Una vez definido un campo XDM como un tipo determinado, cualquier otro campo del mismo nombre y jerarquía debe utilizar el mismo tipo de campo, independientemente de las clases o grupos de campos de esquema en los que se utilice. Por ejemplo, si un grupo de campos para la clase XDM [!DNL Profile] contiene un campo `profile.age` de tipo &quot;entero&quot;, un grupo de campos similar para XDM [!DNL ExperienceEvent] no puede tener un campo `profile.age` de tipo &quot;cadena&quot;. Para utilizar un tipo de campo diferente, el campo debe tener una jerarquía diferente al campo definido anteriormente (por ejemplo, `profile.person.age`). Esta función está diseñada para evitar conflictos cuando los esquemas se unen en una unión. Aunque la restricción no afecta de forma retroactiva a los esquemas existentes, se recomienda revisar los esquemas para detectar conflictos de tipo de campo y editarlos según sea necesario. |
| Validación de campos que distinguen entre mayúsculas y minúsculas | Los campos personalizados del mismo nivel deben tener nombres diferentes, independientemente de las mayúsculas. Por ejemplo, si agrega un campo personalizado denominado &quot;Correo electrónico&quot;, no puede agregar otro campo personalizado en el mismo nivel denominado &quot;Correo electrónico&quot;. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre cómo trabajar con XDM mediante la API [!DNL Schema Registry] y la interfaz de usuario [!DNL Schema Editor], lea la [documentación del sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| [!DNL Privacy Service] cambio de marca | El anteriormente denominado &quot;Servicio de RGPD&quot; se ha cambiado a [!DNL Privacy Service] a medida que el servicio ha crecido para admitir otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta de acceso base para la API [!DNL Privacy Service] se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nueva propiedad `regulation` requerida | Al crear nuevos trabajos en la API [!DNL Privacy Service], se debe proporcionar una propiedad `regulation` en la carga de la solicitud para indicar en qué regulación se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. |
| Compatibilidad con [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] ahora acepta solicitudes de acceso o eliminación del Adobe [!DNL Primetime Authentication], usando `primetimeAuthentication` como valor de producto. |
| Mejoras en la IU de Privacy Service | Páginas de seguimiento de trabajos independientes para las regulaciones del RGPD y CCPA. Nuevo menú desplegable **Tipo de regulación** para cambiar entre los datos de seguimiento para el RGPD y la CCPA. |

**Problemas conocidos**

* Ninguna

Para obtener más información acerca de [!DNL Privacy Service], comience por leer la [descripción general del Privacy Service](../../privacy-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con datos de atributos del cliente | Compatibilidad con la interfaz de usuario y la API para crear conectores de flujo continuo para introducir datos de atributos del cliente. |
| Compatibilidad adicional con formatos de archivo para almacenamiento en la nube | La ingesta de archivos desde almacenamientos en la nube ahora es compatible con los formatos de archivo Parquet y JSON compatibles con XDM. |
| Compatibilidad con permisos de control de acceso | El marco de control de acceso de Adobe Experience Platform proporciona los permisos necesarios para conceder acceso a orígenes en la ingesta de datos. Según su nivel de permiso, un usuario puede ver orígenes, administrarlos o que se le deniegue el acceso. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Ingesta de datos | Administrar fuentes | Acceso para leer, crear, editar y deshabilitar orígenes. |
| Ingesta de datos | Ver orígenes | Acceso de solo lectura a orígenes disponibles en la ficha **[!UICONTROL Catálogo]** y orígenes autenticados en la ficha **[!UICONTROL Examinar]**. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md)

## Destinos {#destinations}

En [Real-Time CDP](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera perfecta.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con permisos de control de acceso | La funcionalidad Destinos de Real-Time CDP funciona con permisos de control de acceso de Adobe Experience Platform. Según el nivel de permisos del usuario, puede ver, administrar y activar destinos. |

**Permisos de control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Destinos | Administrar destinos | Acceso para leer, crear, editar y deshabilitar destinos. |
| Destinos | Ver destinos | Acceso de solo lectura a destinos disponibles en la ficha **[!UICONTROL Catálogo]** y destinos autenticados en la ficha **Examinar**. |
| Destinos | Activar destinos | Capacidad para activar datos en destinos. Este permiso requiere que se añada &quot;Administrar destinos&quot; o &quot;Ver destinos&quot; al perfil del producto. |

**Problemas conocidos**

* Ninguna

Consulte la [Descripción general de destinos](../../destinations/home.md) para obtener más información.
