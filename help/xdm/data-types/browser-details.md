---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de detalles del explorador
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Detalles del explorador.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---


# [!UICONTROL Tipo de datos de detalles] del explorador

[!UICONTROL Los detalles] del explorador son un tipo de datos XDM estándar que describe los detalles relacionados con un explorador o una aplicación.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `acceptLanguage` | Cadena | Una etiqueta de idioma IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica si la configuración del usuario permite la escritura de cookies. |
| `javaEnabled` | Booleano | Indica si Java se habilitó en el dispositivo desde el que se realizó la observación. |
| `javaScriptEnabled` | Booleano | Indica si JavaScript estaba habilitado en el dispositivo desde el que se realizó la observación. |
| `javaScriptVersion` | Cadena | Versión de JavaScript admitida durante la observación. |
| `javaVersion` | Cadena | Versión de Java admitida durante la observación. |
| `name` | Cadena | El nombre de la aplicación o del explorador. |
| `quicktimeVersion` | Cadena | Versión de Apple Quicktime admitida durante la observación. |
| `thirdPartyCookiesEnabled` | Booleano | Indica si las cookies de terceros estaban habilitadas en el dispositivo desde el que se realizó la observación. |
| `userAgent` | Cadena | La cadena HTTP user-agent de la solicitud de cliente. |
| `vendor` | Cadena | El proveedor de la aplicación o del explorador. |
| `version` | Cadena | La versión de la aplicación o del explorador. |
| `viewportHeight` | Número entero | Tamaño vertical en píxeles de la ventana en la que se mostraba el evento. Para un evento de vista web, esta es la altura de la ventanilla del navegador. |
| `viewportWidth` | Número entero | Tamaño horizontal en píxeles de la ventana en la que se mostraba el evento. Para un evento de vista web, es el ancho de la ventanilla del navegador. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)