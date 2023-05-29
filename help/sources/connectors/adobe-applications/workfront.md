---
keywords: Experience Platform;inicio;temas populares;
title: (Beta) Origen de Adobe Workfront
description: Adobe Workfront es una aplicación de administración de trabajo de marketing que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. Workfront incluye herramientas de análisis y creación de informes que puede utilizar para comprender y optimizar mejor el flujo de trabajo en su organización.
exl-id: ea714278-d84d-4929-9a34-81fc5fb70871
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (Beta) Origen de Adobe Workfront

>[!NOTE]
>
>La fuente de Adobe Workfront está en versión beta. Consulte la [Resumen de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Adobe Workfront es una aplicación de administración de trabajo de marketing que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. Workfront incluye herramientas de análisis y creación de informes que puede utilizar para comprender y optimizar mejor el flujo de trabajo en su organización.

La integración de Workfront con el catálogo de fuentes de Adobe Experience Platform le permite llevar los datos de Workfront a Experience Platform y realizar casos de uso como los siguientes:

* Combinar registros de trabajo con datos de terceros.
* Aplicar análisis históricos y de series temporales en registros de trabajo.
* Acceda a registros de trabajo a través de herramientas de inteligencia empresarial de terceros como [!DNL PowerBI].
* Consulta de datos de trabajo mediante SQL estándar.

Los siguientes elementos de trabajo y sus atributos correspondientes pueden incluirse en Experience Platform a través del origen de Workfront:

* Portafolio
* Programa
* Proyecto 
* Tarea
* Tarea operativa (problemas)
* Usuario

La fuente de Workfront transmite todas las nuevas actualizaciones a estos atributos y rellena hasta un año de eventos de cambio históricos. Una vez que los datos de Workfront estén en un conjunto de datos de Platform, puede utilizar [Servicio de consultas](../../../query-service/home.md) y otras herramientas para analizar más a fondo o unir los datos relacionados con el trabajo con otros conjuntos de datos según sea necesario.

## Conexión de Workfront a Platform mediante la IU

Para obtener instrucciones detalladas sobre cómo llevar los datos de Workfront a Platform, lea la guía sobre [creación de una conexión de origen para llevar los datos de Workfront a Platform](../../tutorials/ui/create/adobe-applications/workfront.md).
