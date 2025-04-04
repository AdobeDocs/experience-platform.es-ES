---
title: Notas de la versión de Adobe Experience Platform, diciembre de 2019
description: Notas de la versión de diciembre de 2019 de Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 15%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 11 de diciembre de 2019**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API RESTful que le permiten generar segmentos y audiencias a partir de los datos de [!DNL Real-Time Customer Profile]. Estos segmentos se configuran centralmente y se mantienen en [!DNL Experience Platform], lo que hace que cualquier aplicación de Adobe pueda acceder a ellos fácilmente.

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Pestaña Audiencias combinadas en [!DNL Segment Builder] | Las pestañas [!UICONTROL Segmentos] y [!UICONTROL Audiencias] de [!DNL Segment Builder] se han combinado en una sola pestaña [!UICONTROL Audiencias]. Esta pestaña le permite examinar y buscar audiencias existentes, que luego puede arrastrar y soltar en el lienzo del generador de reglas para crear una nueva definición de segmento. Hacer referencia a una audiencia puede agregar uno de los siguientes conjuntos de lógica de regla a la nueva definición de segmento: Pertenencia a la audiencia como regla, Conjunto completo de lógica de regla que definió la audiencia a la que se hace referencia. |
| Nueva ubicación para el selector de políticas de combinación | Se ha cambiado la ubicación del selector de políticas de combinación en [!DNL Segment Builder]. Para seleccionar una política de combinación para una definición de segmento, seleccione el icono de engranaje en la pestaña **[!UICONTROL Campos]** y, a continuación, utilice el menú desplegable **[!UICONTROL Política de combinación]** para seleccionar la política de combinación que desee utilizar. |

**Problemas conocidos**

* Ninguna

Para obtener más información, consulte la [descripción general del servicio de segmentación](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] permite seleccionar de forma programática e inteligente la &quot;siguiente mejor experiencia&quot; de un conjunto de opciones disponibles para un individuo determinado, enviarlas a cualquier canal o aplicación y realizar informes y análisis.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Funciones de clasificación | El orden de las ofertas para perfiles ahora se deriva de una función de clasificación, en lugar de un conjunto fijo de ofertas en todos los perfiles. |

**Problemas conocidos**

* Ninguna.

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse en sus sistemas de almacenamiento y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Conexión de streaming | La introducción por transmisión le permite enviar datos desde dispositivos del cliente y del lado del servidor a [!DNL Experience Platform] en tiempo real. La versión incluye una nueva interfaz de usuario de conexión de flujo continuo. |
| Compatibilidad con el conector para [!DNL Google Cloud Store] | Compatibilidad para recopilar datos de [!DNL Google Cloud Store]. |

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).

## Sistema [!DNL Experience Data Model] (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Validación de esquema mejorada | Nuevas comprobaciones para garantizar que las referencias se resuelven en campos adicionales según lo esperado. Se han añadido comprobaciones adicionales a los campos definidos como una matriz de objetos para asegurarse de que los objetos estén completamente definidos. Se han mejorado los mensajes de error para ayudar a identificar y corregir los problemas. |

**Corrección de errores**

* Mantenimiento y mejoras relacionadas con el control de acceso y las zonas protegidas.
* Compatibilidad con `eTag` para el extremo `/descriptors` en la API [!DNL Schema Registry].

**Problemas conocidos**

* Ninguna

Para obtener más información sobre cómo trabajar con XDM mediante la API [!DNL Schema Registry] y la interfaz de usuario [!DNL Schema Editor], lea la [documentación del sistema XDM](../../xdm/home.md).
