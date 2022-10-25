---
keywords: Experience Platform;inicio;temas populares;
title: (Beta) Fuente de Adobe Workfront
description: Adobe Workfront es una aplicación de administración de trabajo de marketing que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. Workfront incluye herramientas de análisis e informes que puede utilizar para comprender y optimizar el flujo de trabajo de su organización.
source-git-commit: 1af0863766e29c599e02f2a553d237bc62f455d2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (Beta) Origen de Adobe Workfront

>[!NOTE]
>
>La fuente de Adobe Workfront está en versión beta. Consulte la [Resumen de fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Workfront es una aplicación de administración de trabajo de marketing que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. Workfront incluye herramientas de análisis e informes que puede utilizar para comprender y optimizar el flujo de trabajo de su organización.

La integración de Workfront con el catálogo de fuentes de Adobe Experience Platform le permite llevar los datos de Workfront al Experience Platform y realizar casos de uso como:

* Combine registros de trabajo con datos de terceros.
* Aplique análisis históricos y de series temporales en registros de trabajo.
* Acceda a los registros de trabajo a través de herramientas de inteligencia empresarial de terceros como [!DNL PowerBI].
* Consulte los datos de trabajo mediante SQL estándar.

Los siguientes elementos de trabajo y sus atributos correspondientes pueden incluirse en Experience Platform a través de la fuente de Workfront:

* Portafolio
* Programa
* Proyecto
* Tarea
* Tarea operativa (problemas)
* Usuario

El origen de Workfront transmite todas las actualizaciones nuevas de estos atributos y rellena hasta un año de eventos de cambio históricos. Una vez que los datos de Workfront están en un conjunto de datos de Platform, puede utilizar [Servicio de consultas](../../../query-service/home.md) y otras herramientas para analizar más en profundidad o unir sus datos relacionados con el trabajo con otros conjuntos de datos según sea necesario.

## Conectar Workfront a Platform mediante la interfaz de usuario

Para obtener instrucciones detalladas sobre cómo llevar los datos de Workfront a Platform, consulte la guía de [crear una conexión de origen para llevar los datos de Workfront a Platform](../../tutorials/ui/create/adobe-applications/workfront.md).