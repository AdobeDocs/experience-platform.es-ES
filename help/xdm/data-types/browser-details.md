---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;explorador;detalles del explorador;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles del explorador
description: Obtenga información sobre el tipo de datos XDM Detalles del explorador.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 7%

---

# [!UICONTROL Detalles del explorador] tipo de datos

[!UICONTROL Detalles del explorador] es un tipo de datos XDM estándar que describe detalles relacionados con un explorador o una aplicación.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `acceptLanguage` | Cadena | Una etiqueta de idioma IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica si la configuración del usuario permite la escritura de cookies. |
| `javaEnabled` | Booleano | Indica si Java estaba habilitado en el dispositivo desde el que se realizó la observación. |
| `javaScriptEnabled` | Booleano | Indica si JavaScript estaba habilitado en el dispositivo desde el que se realizó la observación. |
| `javaScriptVersion` | Cadena | La versión de JavaScript admitida durante la observación. |
| `javaVersion` | Cadena | La versión de Java admitida durante la observación. |
| `name` | Cadena | El nombre del explorador o la aplicación. |
| `quicktimeVersion` | Cadena | La versión de Apple Quicktime admitida durante la observación. |
| `thirdPartyCookiesEnabled` | Booleano | Indica si las cookies de terceros se habilitaron en el dispositivo desde el que se realizó la observación. |
| `userAgent` | Cadena | La cadena del agente de usuario HTTP de la solicitud del cliente. |
| `vendor` | Cadena | El proveedor del explorador o la aplicación. |
| `version` | Cadena | La versión del explorador o la aplicación. |
| `viewportHeight` | Número entero | El tamaño vertical en píxeles de la ventana en la que se mostró el evento. En el caso de los eventos de visualización web, esta es la altura de la ventanilla del explorador. |
| `viewportWidth` | Número entero | El tamaño horizontal en píxeles de la ventana en la que se mostró el evento. En un evento de visualización web, esta es la anchura de la ventanilla del explorador. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
