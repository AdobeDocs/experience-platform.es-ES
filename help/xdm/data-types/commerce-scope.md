---
title: Tipo de datos del ámbito de Commerce
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) del ámbito de Commerce.
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# [!UICONTROL Tipo de datos del ámbito de Commerce]

[!UICONTROL Ámbito de Commerce] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que define los identificadores para los casos en los que se produjo un evento dentro de un ecosistema comercial. Distingue entornos, sitios web, tiendas y vistas de tiendas.

![Un diagrama del tipo de datos de ámbito de Commerce.](../images/data-types/commerce-scope.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Id. de entorno] | `environmentID` | cadena | El ID del entorno. Un ID alfanumérico de 32 dígitos. |
| [!UICONTROL Código de sitio web] | `websiteCode` | cadena | El código único del sitio web dentro de un entorno. |
| [!UICONTROL Código de tienda] | `storeCode` | cadena | El código de almacén único dentro de un sitio web. |
| [!UICONTROL Código de vista de tienda] | `storeViewCode` | cadena | El código de vista de tienda único dentro de una tienda. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
