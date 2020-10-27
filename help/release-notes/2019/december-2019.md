---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 11 de diciembre de 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 801da8a705360688f230eae5772a8bed9a1e856e
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 11 de diciembre de 2019**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite generar segmentos y audiencias a partir de sus [!DNL Real-time Customer Profile] datos. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform], lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto concreto de perfiles describiendo los criterios que distinguen a un grupo comercializable de personas dentro de la base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Ficha Audiencias combinadas de [!DNL Segment Builder] | Las fichas [!UICONTROL Segmentos] y [!UICONTROL Audiencias] de la [!DNL Segment Builder] se han combinado en una sola ficha [!UICONTROL Audiencias] . Esta ficha le permite explorar y buscar audiencias existentes, que puede arrastrar y soltar en el lienzo del generador de reglas para crear una nueva definición de segmento. Al hacer referencia a una audiencia se puede agregar uno de los siguientes conjuntos de lógica de regla a la nueva definición de segmento: Pertenencia a la audiencia como regla, conjunto completo de lógica de regla que definió la audiencia a la que se hace referencia. |
| Nueva ubicación para el selector de directivas de combinación | Se ha cambiado la ubicación del selector de directivas de combinación en el [!DNL Segment Builder] panel. Para seleccionar una directiva de combinación para una definición de segmento, haga clic en el icono de engranaje de la ficha **[!UICONTROL Campos]** y, a continuación, utilice el menú desplegable **[!UICONTROL Combinar directiva]** para seleccionar la directiva de combinación que desee utilizar. |

**Problemas conocidos**

* None

Para obtener más información, consulte la descripción general [del servicio](../../segmentation/home.md)de segmentación.

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] ofrece la capacidad de seleccionar programática e inteligentemente la &quot;Mejor experiencia siguiente&quot; de un conjunto de opciones disponibles para un individuo determinado, entregarlas a cualquier canal o aplicación y realizar sistemas de informes y análisis.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Funciones de clasificación | El orden de ofertas para perfiles ahora se deriva a través de una función de clasificación, en lugar de un conjunto fijo de ofertas en todos los perfiles. |

**Problemas conocidos**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamientos basados en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse en sus sistemas almacenamiento y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Conexión de flujo continuo | La ingestión por flujo continuo le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. La versión incluye una nueva interfaz de usuario de conexión de flujo continuo. |
| Compatibilidad con conectores para [!DNL Google Cloud Store] | Compatibilidad para recopilar datos de [!DNL Google Cloud Store]. |

**Problemas conocidos**

* None.

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Validación de esquema mejorada | Nuevas comprobaciones para asegurarse de que las referencias se resuelven en campos adicionales según lo esperado. Se añadieron comprobaciones adicionales a los campos definidos como una matriz de objetos para asegurarse de que los objetos están completamente definidos. Se han mejorado los mensajes de error para ayudar a identificar y corregir problemas. |

**Corrección de errores**

* Mantenimiento y mejoras relacionadas con controles de acceso y entornos limitados.
* Compatibilidad con `eTag` el `/descriptors` extremo en la [!DNL Schema Registry] API.

**Problemas conocidos**

* None

Para obtener más información sobre cómo trabajar con XDM mediante la [!DNL Schema Registry] API y la interfaz de usuario, lea la documentación [!DNL Schema Editor] del sistema [](../../xdm/home.md)XDM.