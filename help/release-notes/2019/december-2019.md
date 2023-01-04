---
title: Notas de la versión de Adobe Experience Platform, diciembre de 2019
description: Notas de la versión de diciembre de 2019 para Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de diciembre de 2019**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de su [!DNL Real-Time Customer Profile] datos. Estos segmentos están configurados de forma centralizada y se mantienen en [!DNL Platform], lo que permite que cualquier aplicación de Adobe pueda acceder a ellas fácilmente.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Ficha Audiencias combinadas en [!DNL Segment Builder] | La variable [!UICONTROL Segmentos] y [!UICONTROL Audiencias] en el [!DNL Segment Builder] se han combinado en un único [!UICONTROL Audiencias] pestaña . Esta pestaña le permite examinar y buscar audiencias existentes, que puede arrastrar y soltar en el lienzo del generador de reglas para crear una nueva definición de segmento. Al hacer referencia a una audiencia puede agregar uno de los siguientes conjuntos de lógica de regla a la nueva definición de segmento: Pertenencia a la audiencia como regla, conjunto completo de lógica de regla que definió la audiencia a la que se hace referencia. |
| Nueva ubicación para el selector de directivas de combinación | La ubicación del selector de directivas de combinación en la variable [!DNL Segment Builder] ha cambiado. Para seleccionar una política de combinación para una definición de segmento, seleccione el icono de engranaje en el **[!UICONTROL Campos]** y, a continuación, utilice la pestaña **[!UICONTROL Política de combinación]** menú desplegable para seleccionar la política de combinación que desee utilizar. |

**Problemas conocidos**

* Ninguna

Para obtener más información, consulte la [Información general del servicio de segmentación](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] permite seleccionar de forma programada e inteligente la &quot;Mejor experiencia siguiente&quot; de un conjunto de opciones disponibles para un individuo determinado, enviarlas a cualquier canal o aplicación y realizar informes y análisis.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Funciones de clasificación | El orden de las ofertas para los perfiles ahora se deriva de una función de clasificación, en lugar de de un conjunto fijo de ofertas en todos los perfiles. |

**Problemas conocidos**

* Ninguna.

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse en sus sistemas de almacenamiento y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Conexión de flujo continuo | La introducción por transmisión le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. La versión incluye una nueva interfaz de usuario de conexión de flujo continuo. |
| Compatibilidad con conectores para [!DNL Google Cloud Store] | Compatibilidad con la recopilación de datos de [!DNL Google Cloud Store]. |

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Validación de esquema mejorada | Nuevas comprobaciones para asegurarse de que las referencias se resuelven en campos adicionales según lo esperado. Se han añadido comprobaciones adicionales a los campos definidos como una matriz de objetos para asegurarse de que los objetos están totalmente definidos. Se han mejorado los mensajes de error para ayudar a identificar y solucionar problemas. |

**Corrección de errores**

* Mantenimiento y mejoras relacionadas con el control de acceso y los entornos limitados.
* Compatibilidad con `eTag` para el `/descriptors` en la variable [!DNL Schema Registry] API.

**Problemas conocidos**

* Ninguna

Para obtener más información sobre cómo trabajar con XDM mediante la variable [!DNL Schema Registry] API y [!DNL Schema Editor] interfaz de usuario, lea la [Documentación del sistema XDM](../../xdm/home.md).
