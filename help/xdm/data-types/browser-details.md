---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;explorador;detalles del explorador;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles del explorador
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Detalles del explorador .
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 6%

---

# [!UICONTROL Browser details] tipo de datos

[!UICONTROL Browser details] es un tipo de datos XDM estándar que describe detalles relacionados con un explorador o aplicación.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `acceptLanguage` | Cadena | Una etiqueta de idioma IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica si la configuración del usuario permite la escritura de cookies. |
| `javaEnabled` | Booleano | Indica si Java estaba habilitado en el dispositivo desde el que se realizó la observación. |
| `javaScriptEnabled` | Booleano | Indica si JavaScript estaba habilitado en el dispositivo desde el que se realizó la observación. |
| `javaScriptVersion` | Cadena | Versión de JavaScript admitida durante la observación. |
| `javaVersion` | Cadena | Versión de Java admitida durante la observación. |
| `name` | Cadena | El nombre de la aplicación o del explorador. |
| `quicktimeVersion` | Cadena | La versión de Apple Quicktime admitida durante la observación. |
| `thirdPartyCookiesEnabled` | Booleano | Indica si se habilitaron cookies de terceros en el dispositivo desde el que se realizó la observación. |
| `userAgent` | Cadena | La cadena HTTP user-agent de la solicitud del cliente. |
| `vendor` | Cadena | El proveedor de la aplicación o del explorador. |
| `version` | Cadena | La aplicación o la versión del explorador. |
| `viewportHeight` | Número entero | Tamaño vertical en píxeles de la ventana en la que se mostró el evento. Para un evento de vista web, esta es la altura de la ventanilla del explorador. |
| `viewportWidth` | Número entero | El tamaño horizontal en píxeles de la ventana en la que se mostró el evento. Para un evento de vista web, esta es la anchura de la ventanilla del explorador. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
