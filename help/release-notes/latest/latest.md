---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 28 de julio de 2021.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: dc01e03975fdda375b31f44edc8459fa32b5a61b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 10%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 28 de julio de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Data Science Workspace](#dsw)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Fuentes](#sources)

## Data Science Workspace {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Actualizaciones de biblioteca y sistema operativo | Data Science Workspace ha realizado actualizaciones importantes de la biblioteca y el sistema operativo para mejorar la funcionalidad y el uso. Esto incluye JupyterLab 1.2.20, Python 3.7, Pandas 1.2.4, Tensorflow 2.4.1 con soporte para CUDA 11 y CUDNN 8, y más. Para aprender a ver las bibliotecas disponibles en JupyterLab, visite la sección [bibliotecas compatibles](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) en la documentación de información general de los blocs de notas de JupyterLab. |

Para obtener información más general sobre Data Science Workspace, consulte [Información general sobre Data Science Workspace](../../data-science-workspace/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

Experience Data Model (XDM) es una especificación de código abierto diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para los datos en forma de esquemas, que permiten a cualquier aplicación comunicarse con los servicios de Platform.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Filtro del sector de las telecomunicaciones | Al agregar grupos de campos a un esquema en la interfaz de usuario, ahora puede filtrar por sector de telecomunicaciones. Consulte el [diagrama de relación de entidades del sector de las telecomunicaciones (ERD)](../../xdm/schema/industries/telecom.md) para ver un modelo de datos recomendado para casos de uso de telecomunicaciones. |

Para obtener información más general sobre XDM en Platform, consulte [Información general del sistema XDM](../../xdm/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (Beta) | Ahora puede conectar [!DNL Salesforce Marketing Cloud] al Experience Platform mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [[!DNL Salesforce Marketing Cloud] descripción general del conector](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
