---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dispositivo;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del dispositivo
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos Device XDM .
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 4%

---

# [!UICONTROL Device] tipo de datos

[!UICONTROL Device] es un tipo de datos XDM estándar que describe un dispositivo identificado. Un dispositivo es una aplicación o instancia de explorador que se puede rastrear entre sesiones, normalmente mediante cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `colorDepth` | Número entero | Número de colores que la pantalla puede representar. |
| `manufacturer` | Cadena | Nombre de la organización propietaria del diseño y la creación del dispositivo. |
| `model` | Cadena | Nombre del modelo para el dispositivo. Es el nombre común, legible en lenguaje natural o de marketing del dispositivo. Por ejemplo, el &quot;iPhone 6S&quot; es un modelo particular de teléfono móvil. |
| `modelNumber` | Cadena | La designación única del número de modelo asignada por el fabricante para este dispositivo. Los números de modelo no son versiones, sino identificadores únicos que identifican una configuración de modelo determinada. |
| `screenHeight` | Número entero | Número de píxeles verticales de la visualización activa del dispositivo en la orientación predeterminada. |
| `screenOrientation` | Cadena | La orientación de la pantalla actual. Los valores aceptados incluyen `portrait` y `landscape`. |
| `screenWidth` | Cadena | Número de píxeles horizontales de la visualización activa del dispositivo en la orientación predeterminada. |
| `type` | Cadena | Tipo de dispositivo que se rastrea. Los valores aceptados incluyen: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Cadena | Identificador del dispositivo. Puede ser un identificador de DeviceAtlas u otro servicio que identifique el hardware que se está utilizando. |
| `typeIDService` | Cadena | El espacio de nombres del servicio que se utiliza para identificar el tipo de dispositivo. Consulte el [apéndice](#typeIDService) para obtener más información sobre los valores aceptados. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre el tipo de datos [!UICONTROL Device].

## Valores aceptados para typeIDService {#typeIDService}

La siguiente tabla describe los valores aceptados para `typeIDService` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | El dispositivo se ha identificado mediante DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | El dispositivo se ha identificado mediante Adobe Campaign. |
