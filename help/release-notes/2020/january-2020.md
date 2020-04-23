---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 15 de enero de 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 5199a344a66381ef9d7eea1ea8314e5de7152e3b

---


# Notas de la versión de Adobe Experience Platform

## Fecha de la versión: 15 de enero de 2020

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM)](#xdm)
* [Privacy Service](#privacy)
* [Fuentes](#sources)
* [Destinos](#destinations)

## Sistema de modelo de datos de experiencia (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan la plataforma de experiencia. El modelo de datos de experiencia (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de la plataforma Adobe Experience. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Restricciones de tipo de campo para campos de jerarquía igual | Después de definir un campo XDM como un tipo determinado, cualquier otro campo con el mismo nombre y jerarquía debe utilizar el mismo tipo de campo, independientemente de las clases o mezclas en las que se utilicen. Por ejemplo, si una mezcla para la clase de Perfil XDM contiene un `profile.age` campo de tipo &quot;integer&quot;, una combinación similar para XDM ExperienceEvent no puede tener un `profile.age` campo de tipo &quot;string&quot;. Para utilizar un tipo de campo diferente, el campo debe tener una jerarquía diferente a la definida anteriormente (por ejemplo, `profile.person.age`). Esta función está pensada para evitar conflictos cuando los esquemas se unen en una unión. Aunque la restricción no afecta retroactivamente a los esquemas existentes, se recomienda encarecidamente que revise los esquemas para los conflictos de tipo campo y que los edite según sea necesario. |
| Validación de campo con distinción entre mayúsculas y minúsculas | Los campos personalizados del mismo nivel deben tener nombres diferentes, independientemente del uso de mayúsculas y minúsculas. Por ejemplo, si agrega un campo personalizado llamado &quot;Correo electrónico&quot;, no podrá agregar otro campo personalizado en el mismo nivel llamado &quot;correo electrónico&quot;. |

**Problemas conocidos**

* None

Para obtener más información sobre cómo trabajar con XDM mediante la API del Registro de Esquema y la interfaz de usuario del Editor de Esquemas, lea la documentación [del sistema](../../xdm/home.md)XDM.

## Privacy Service {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan. Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con Privacy Service, puede enviar solicitudes para acceder a los datos personales o privados de los clientes y eliminarlos de las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas de privacidad legales y de la organización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Cambio de marca de Privacy Service | El llamado anteriormente &quot;Servicio de RGPD&quot; ha sido rebautizado como Servicio de Privacidad ya que el servicio ha crecido para apoyar otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta de acceso base para la API de Privacy Service se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs`. |
| Nueva propiedad requerida `regulation` | Al crear nuevos trabajos en la API de Privacy Service, se debe proporcionar una `regulation` propiedad en la carga útil de la solicitud para indicar en qué regla se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. |
| Compatibilidad con la autenticación Adobe Primetime | Privacy Service ahora acepta solicitudes de acceso/eliminación de la autenticación Adobe Primetime, utilizando `primetimeAuthentication` como valor de producto. |
| Mejoras en la interfaz de usuario de Privacy Service | Páginas de seguimiento de trabajos independientes para las regulaciones de RGPD y CCPA. Nuevo menú desplegable _de tipo_ de reglamento para cambiar entre los datos de seguimiento del RGPD y del CCPA. |

**Problemas conocidos**

* None

Para obtener más información acerca de Privacy Service, lea la información general [de](../../privacy-service/home.md)Privacy Service para obtener inicios.

## Fuentes {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con datos de atributos del cliente | Compatibilidad con la interfaz de usuario y la API para crear conectores de flujo continuo con el fin de ingestar datos de atributos del cliente. |
| Compatibilidad adicional con formatos de archivo para almacenamientos en la nube | La ingestión de archivos desde almacenamientos en la nube ahora es compatible con los formatos de archivo Parquet y JSON compatibles con XDM. |
| Compatibilidad con permisos de control de acceso | El marco de control de acceso de Adobe Experience Platform proporciona los permisos necesarios para conceder acceso a los orígenes en la ingesta de datos. Según el nivel de permiso, un usuario puede realizar vistas de fuentes, administrar fuentes o denegarle el acceso. |

**Permisos de Control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Ingesta de datos | Administrar fuentes | Acceso para leer, crear, editar y deshabilitar fuentes. |
| Ingesta de datos | Fuentes de Vista | Acceso de sólo lectura a los orígenes disponibles en la ficha *Catálogo* y a los orígenes autenticados en la ficha *Examinar* . |

**Problemas conocidos**

* None

Para obtener más información sobre las fuentes, consulte la descripción general de [las fuentes](../../sources/home.md)

## Destinos {#destinations}

En CDP [en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de una manera transparente.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con permisos de control de acceso | La funcionalidad Destinations de CDP en tiempo real funciona con los permisos de control de acceso de Adobe Experience Platform. Según el nivel de permiso del usuario, puede realizar vistas, administrar y activar destinos. |

**Permisos de Control de acceso**

| Categoría | Permiso | Descripción |
|--- | --- | ---|
| Destinos | Administrar destinos | Acceso para leer, crear, editar y deshabilitar destinos. |
| Destinos | Destinos de Vista | Acceso de sólo lectura a los destinos disponibles en la ficha _Catálogo_ y a los destinos autenticados en la ficha _Examinar_ . |
| Destinos | Activar destinos | Capacidad para activar datos en destinos. Este permiso requiere que se agregue &quot;Administrar destinos&quot; o &quot;Destinos de Vista&quot; al perfil del producto. |

**Problemas conocidos**

* None

Consulte la información general [](../../rtcdp/destinations/destinations-overview.md) Destinos para obtener más información.