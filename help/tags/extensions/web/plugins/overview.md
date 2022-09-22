---
title: Información general de la extensión Common Analytics
description: Obtenga información sobre la extensión de etiqueta Common Analytics en Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 96%

---

# Información general sobre la extensión Common Analytics Plugins

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Utilice esta referencia para obtener información sobre cómo configurar la extensión de complementos de Analytics comunes y las opciones disponibles al utilizar esta extensión para aumentar la extensión de [!DNL Adobe Analytics].

## Configuración de la extensión de complementos de Analytics comunes

Esta sección sirve como referencia sobre las opciones disponibles a la hora de configurar la extensión de complementos de Analytics comunes.

>[!IMPORTANT]
>
>La extensión de complementos de Analytics comunes aumenta la extensión de [!DNL Adobe Analytics]. Debe tener la extensión de [!DNL Adobe Analytics] instalada en la propiedad para que funcione. Además, debe hacer que el rastreador sea accesible globalmente en la extensión de [!DNL Adobe Analytics].

No se requiere ninguna configuración adicional en el nivel de extensión.

## Añadir complementos a la extensión de [!DNL Adobe Analytics]

Para utilizar los complementos proporcionados en esta extensión, primero debe inicializar los complementos que desea utilizar en su propia regla.

1. Crear una regla nueva.
1. Añada el evento Core - Library Loaded (Page Top).
1. Utilice cualquiera de los siguientes métodos de inicialización.

## Tipos de acciones de extensión de complementos de Analytics comunes

En esta sección se describen los tipos de acción disponibles en la extensión de complementos de Analytics comunes.

La extensión de complementos de Analytics comunes proporciona las siguientes acciones:

* [Inicializar](#initialize)
* [Inicializar complemento](#initialize-plugin)

### Inicializar

>[!IMPORTANT]
>
>Aunque esta acción es más fácil de implementar, Adobe Consulting no recomienda que utilice esta acción ya que aumenta el peso del complemento.

En esta acción, puede seleccionar cada complemento que desee incluir en la implementación y guardar los cambios. Seleccione tantos complementos como desee utilizar durante la implementación. En la [descripción general de los complementos](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=es) de Analytics encontrará vínculos a documentación sobre cómo utilizar cada complemento y una breve descripción.

### Inicializar complemento

Estas acciones inicializan el complemento específico que se va a utilizar individualmente. Para inicializar todos los complementos que pretenda utilizar en la propiedad, simplemente agregue la acción correspondiente a la regla y guarde la regla. Aunque se requiere un poco más de esfuerzo para configurar la extensión de esta manera, hace que el código sea más eficiente. Adobe recomienda este método.

## Elementos de datos de la extensión Common Analytics Plugins

En esta sección se describen los tipos de elementos de datos disponibles en la extensión Common Analytics Plugins.

### getGeoCoordinates

Permite a los usuarios aprovechar la IU nativa de recopilación de datos en Adobe Experience Platform para configurar el complemento getGeoCoordinates.

### getNewRepeat

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getNewRepeat.

### getPageName

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getPageName.

### getResponsiveLayout

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getResponsiveLayout.

### getTimeParting

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getTimeParting.

### getTimeSinceLastVisit

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getTimeSinceLastVisit.

### getVisitDuration

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getVisitDuration.

### getVisitNum

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar el complemento getVisitNum.
