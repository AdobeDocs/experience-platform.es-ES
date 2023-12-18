---
title: Tipo de datos del ámbito comercial
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia (XDM) del ámbito del comercio.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---

# [!UICONTROL Ámbito comercial] tipo de datos

[!UICONTROL Ámbito comercial] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que define identificadores para los casos en los que se produjo un evento dentro de un ecosistema comercial. Distingue entornos, sitios web, tiendas y vistas de tiendas.

![Diagrama del tipo de datos del ámbito comercial.](../images/data-types/commerce-scope.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID de entorno] | `environmentID` | string | El ID del entorno. Un ID alfanumérico de 32 dígitos. |
| [!UICONTROL Código del sitio web] | `websiteCode` | string | El código único del sitio web dentro de un entorno. |
| [!UICONTROL Código de tienda] | `storeCode` | string | El código de almacén único dentro de un sitio web. |
| [!UICONTROL Código de vista de tienda] | `storeViewCode` | string | El código de vista de tienda único dentro de una tienda. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
