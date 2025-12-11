---
title: Información general sobre la extensión de Adobe Audience Manager
description: Obtenga información acerca de la extensión de etiquetas Adobe Audience Manager en Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 100%

---

# Información general sobre la extensión de Adobe Audience Manager

Con la extensión de etiquetas Audience Manager, puede integrar el código DIL utilizado por Audience Manager con sus propiedades en Adobe Experience Platform.

Utilice esta referencia para obtener información sobre las opciones disponibles al utilizar esta extensión para generar una regla.

>[!NOTE]
>
>Esta extensión no está pensada para utilizarse para el reenvío de eventos de datos de Adobe Analytics. Para reenvíos de eventos, utilice la [extensión de Adobe Analytics](../analytics/overview.md).

## Configurar la extensión de Adobe Audience Manager

Si la extensión de Adobe Audience Manager aún no está instalada, abra la propiedad, seleccione **[!UICONTROL Extensions > Catalog]**, coloque el puntero por encima de la extensión de Adobe Audience Manager y seleccione **[!UICONTROL Install]**.

Para configurar la extensión, abra la pestaña [!UICONTROL Extensions], coloque el puntero por encima de la extensión y, a continuación, seleccione **[!UICONTROL Configure]**.

### Configuración de DIL

Ajuste la configuración de DIL. Las opciones de configuración disponibles son las siguientes:

![](../../../images/ext-aam-config.png)

#### Versión de DIL

Muestra la versión de la biblioteca de integración de datos (DIL).

No se pueden modificar estas opciones de configuración.

#### Excluir rutas específicas

Si la dirección URL coincide con cualquiera de las rutas excluidas, la extensión no se carga.

Seleccione **[!UICONTROL Add Path]** para especificar una URL excluida.

Habilite Regex si la dirección URL es una expresión regular.

#### Uso del módulo DIL SiteCatalyst

El [módulo SiteCatalyst](https://experiencecloud.adobe.com/resources/help/es_ES/aam/r_dil_sc_init.html) funciona con DIL para enviar los elementos de etiquetas de Analytics a Audience Manager.

Utilice el Editor de código para configurar el archivo siteCatalyst.init.

También puede crear una nota que contenga información sobre esta configuración.

#### Uso del módulo DIL Google Analytics

Habilite el módulo de [Google Analytics](https://experiencecloud.adobe.com/resources/help/es_ES/aam/dil-google-universal-analytics.html).

#### Propiedades de inicialización de DIL.create

Agregue las propiedades de inicialización utilizadas por [DIL.create](https://experiencecloud.adobe.com/resources/help/es_ES/aam/r_dil_create.html) y la subpropiedad namespace para el [objeto visitorService](https://experiencecloud.adobe.com/resources/help/es_ES/aam/r_dil_visitor_service.html). En los comentarios del código se incluyen dos casos de uso de muestra, en el Editor de código.

Seleccione **[!UICONTROL Choose an Item]** para añadir propiedades adicionales.

Pase el puntero por encima de los iconos “i” para conocer lo que hace cada propiedad. Puede encontrar más información para las propiedades en la documentación de [Audience Manager DIL](https://experiencecloud.adobe.com/resources/help/es_ES/aam/r_dil_create.html).

Seleccione **[!UICONTROL Save]** cuando haya terminado de configurar la extensión.

## Tipos de acciones de extensión de Adobe Audience Manager

Este tema describe los tipos de acción disponibles en la extensión de Audience Manager.

La extensión de Adobe Audience Manager proporciona las siguientes acciones en la porción Then de una regla:

### Ejecutar código personalizado

Ejecutar código personalizado configurado en el Editor de código.

Introduzca el código deseado en el Editor de código y, a continuación, proporcione un nombre para el código. Este código estará disponible en la porción Then del Generador de reglas.

![](../../../images/ext-aam-then.png)

También puede agregar una nota con información sobre la configuración.
