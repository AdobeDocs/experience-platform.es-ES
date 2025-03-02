---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquema;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del dispositivo
description: Obtenga información sobre el tipo de datos XDM del dispositivo.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 17%

---

# Tipo de datos [!UICONTROL Dispositivo]

[!UICONTROL Dispositivo] es un tipo de datos XDM estándar que describe un dispositivo identificado. Un dispositivo es una aplicación o instancia de explorador que se puede rastrear a través de sesiones (por lo general, mediante cookies).

![](../images/data-types/device.png){width=450}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `colorDepth` | Entero | La cantidad de colores que la pantalla puede renderizar. |
| `manufacturer` | Cadena | El nombre de la organización que posee el diseño y la creación del dispositivo. |
| `model` | Cadena | Nombre del modelo del dispositivo. Es el nombre común, en lenguaje natural o de marketing del dispositivo. Por ejemplo, el &quot;iPhone 6S&quot; es un modelo particular de teléfono móvil. |
| `modelNumber` | Cadena | La designación del número de modelo único asignada por el fabricante a este dispositivo. Los números de modelo no son versiones, sino identificadores únicos que identifican una configuración de modelo determinada. |
| `screenHeight` | Entero | El número de píxeles verticales de la pantalla activa del dispositivo en la orientación predeterminada. |
| `screenOrientation` | Cadena | La orientación de pantalla actual. Los valores aceptados incluyen `portrait` y `landscape`. |
| `screenWidth` | Cadena | El número de píxeles horizontales de la pantalla activa del dispositivo en la orientación predeterminada. |
| `type` | Cadena | El tipo de dispositivo que se rastrea. Los valores aceptados incluyen: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Cadena | Un identificador del dispositivo. Puede ser un identificador de DeviceAtlas u otro servicio que identifique el hardware que se está utilizando. |
| `typeIDService` | Cadena | El área de nombres del servicio que se utiliza para identificar el tipo de dispositivo. Consulte el [apéndice](#typeIDService) para obtener detalles sobre los valores aceptados. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre el tipo de datos [!UICONTROL Dispositivo].

## Valores aceptados para typeIDService {#typeIDService}

En la tabla siguiente se describen los valores aceptados para `typeIDService` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | El dispositivo se ha identificado mediante DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | El dispositivo se ha identificado mediante Adobe Campaign. |
