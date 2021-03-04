---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de Experience Platform 11 de diciembre de 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de diciembre de 2019**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite crear segmentos y generar audiencias a partir de sus datos [!DNL Real-time Customer Profile]. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform], lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Pestaña Audiencias combinadas en [!DNL Segment Builder] | Las pestañas [!UICONTROL Segments] y [!UICONTROL Audiences] de [!DNL Segment Builder] se han combinado en una sola pestaña [!UICONTROL Audiences]. Esta pestaña le permite examinar y buscar audiencias existentes, que puede arrastrar y soltar en el lienzo del generador de reglas para crear una nueva definición de segmento. Al hacer referencia a una audiencia puede agregar uno de los siguientes conjuntos de lógica de regla a la nueva definición de segmento: Pertenencia a la audiencia como regla, conjunto completo de lógica de regla que definió la audiencia a la que se hace referencia. |
| Nueva ubicación para el selector de directivas de combinación | Se ha cambiado la ubicación del selector de directivas de combinación en [!DNL Segment Builder]. Para seleccionar una política de combinación para una definición de segmento, seleccione el icono de engranaje en la pestaña **[!UICONTROL Fields]** y, a continuación, utilice el menú desplegable **[!UICONTROL Merge Policy]** para seleccionar la política de combinación que desea utilizar. |

**Problemas conocidos**

* Ninguna

Para obtener más información, consulte la [información general del Servicio de segmentación](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] permite seleccionar de forma programada e inteligente la &quot;Mejor experiencia siguiente&quot; de un conjunto de opciones disponibles para un individuo determinado, enviarla a cualquier canal o aplicación y realizar informes y análisis.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Funciones de clasificación | El orden de las ofertas para los perfiles ahora se deriva de una función de clasificación, en lugar de de un conjunto fijo de ofertas en todos los perfiles. |

**Problemas conocidos**

* Ninguna.

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurar, etiquetar y mejorar esos datos mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse en sus sistemas de almacenamiento y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Conexión de flujo continuo | La introducción por transmisión le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. La versión incluye una nueva interfaz de usuario de conexión de flujo continuo. |
| Compatibilidad con conectores para [!DNL Google Cloud Store] | Compatibilidad para recopilar datos de [!DNL Google Cloud Store]. |

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre las fuentes, consulte la [información general de las fuentes](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM)  {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Validación de esquema mejorada | Nuevas comprobaciones para asegurarse de que las referencias se resuelven en campos adicionales según lo esperado. Se han añadido comprobaciones adicionales a los campos definidos como una matriz de objetos para asegurarse de que los objetos están totalmente definidos. Se han mejorado los mensajes de error para ayudar a identificar y solucionar problemas. |

**Corrección de errores**

* Mantenimiento y mejoras relacionadas con el control de acceso y los entornos limitados.
* Compatibilidad con `eTag` para el extremo `/descriptors` en la API [!DNL Schema Registry].

**Problemas conocidos**

* Ninguna

Para obtener más información sobre cómo trabajar con XDM mediante la API [!DNL Schema Registry] y la interfaz de usuario [!DNL Schema Editor], lea la [Documentación del sistema XDM](../../xdm/home.md).