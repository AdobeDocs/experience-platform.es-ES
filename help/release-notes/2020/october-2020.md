---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform Octubre de 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 43ceda3d95511c3972fd0588f472c6c412dd95bf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 14 de octubre de 2020**

- [Preparación de datos](#data-prep)
- [Perfil del cliente en tiempo real](#profile)
- [Fuentes](#sources)

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Función  de `is_set` | La `is_set` función permite comprobar la presencia de un atributo en los datos de origen. `is_set` puede utilizarse en combinación con `is_empty` para comprobar la presencia del atributo y la presencia del valor dentro del atributo. |
| Función  de `get_values` | La `get_values` función le permite obtener los valores del mapa de entrada para cualquier clave determinada. |

Para obtener más información, lea la descripción general [de](../../data-prep/home.md)la preparación de datos.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos dispares de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Adiciones a la API de previsualización de perfil | La API de previsualización de Perfil (`/previewsamplestatus`) ahora incluye la capacidad de vista de un desglose de los fragmentos de perfil totales en la organización de IMS, así como de vista de la distribución de fragmentos de perfil entre Áreas de nombres de identidad. |
| Actualizaciones de vista de esquema de unión | En la interfaz de usuario del Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como campos de identidad y relación. Estas actualizaciones mejoran la capacidad para solucionar problemas y validar que los perfiles estén correctamente configurados, que las identidades estén correctamente vinculadas y que los datos se hayan ingerido correctamente. |

Para obtener más información sobre [!DNL Real-time Customer Profile]tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] datos, lea la descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Asignación jerárquica | Durante el proceso de ingestión de datos, puede realizar la previsualización de un archivo de origen jerárquico, como JSON o Parquet. |
| Compatibilidad con autenticación SSH para SFTP | Puede conectar su cuenta SFTP con [!DNL Platform] las claves RSA/DSA Open SSH. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| Mejoras en los recursos | Puede habilitar el conjunto de datos para [!DNL Profile] durante el proceso de ingesta de datos. Consulte el tutorial de flujo de trabajo [de flujo de datos de almacenamiento de](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) nube para obtener más información. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.