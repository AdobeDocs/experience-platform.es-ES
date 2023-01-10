---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;entorno;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de entorno
description: Este documento proporciona información general sobre el tipo de datos XDM de entorno.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 5%

---

# [!UICONTROL Entorno] tipo de datos

[!UICONTROL Entorno] es un tipo de datos XDM estándar que describe el entorno de un evento observado, detallando específicamente información transitoria como versiones de red y software.

>[!IMPORTANT]
>
>Todos los valores deben alinearse con la variable [DeviceAtlas](https://deviceatlas.com) base de datos, con licencia de Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_dc` | Objeto | Un objeto que contiene un único campo, `language`, que indica el idioma del entorno que representa las preferencias lingüísticas, geográficas o culturales del usuario para la presentación de datos. Los idiomas se especifican en el código de idioma tal como se define en [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Detalles del explorador](./browser-details.md) | Describe los detalles del entorno específicos del explorador, como el nombre del explorador, la versión, la versión de JavaScript, la cadena del agente de usuario y el idioma de aceptación. |
| `ISP` | Cadena | Nombre del proveedor de servicios de Internet del usuario. |
| `carrier` | Cadena | El nombre del operador de red móvil o MNO (también conocido como proveedor de servicios inalámbricos, operador de telefonía inalámbrica, empresa celular o operador de red móvil) que vende y ofrece servicios de comunicación al usuario. |
| `colorDepth` | Número entero | El número de bits utilizado para cada componente de color de un solo píxel. |
| `connectionType` | Cadena | Tipo de conexión a Internet. Los valores aceptados incluyen: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Cadena | Dominio del ISP del usuario. |
| `ipV4` | Cadena | Etiqueta numérica asignada a un dispositivo que participa en una red de equipos que utiliza el Protocolo de Internet para la comunicación (32 bits). |
| `ipV6` | Cadena | Etiqueta numérica asignada a un dispositivo que participa en una red de equipos que utiliza el Protocolo de Internet para la comunicación (128 bits). |
| `operatingSystem` | Cadena | Nombre del sistema operativo utilizado cuando se realizó la observación. El atributo no debe contener información de versión como `10.5.3`, pero en su lugar contiene designaciones de &quot;edición&quot; como `Ultimate` o `Professional`. |
| `operatingSystemVendor` | Cadena | Nombre del proveedor del sistema operativo utilizado cuando se realizó la observación. |
| `operatingSystemVersion` | Cadena | Identificador de versión completa del sistema operativo utilizado cuando se realizó la observación. Las versiones suelen estar compuestas numéricamente, pero pueden tener un formato definido por el proveedor. |
| `type` | Cadena | Tipo del entorno de la aplicación. Consulte la [apéndice](#type) para valores aceptados. |
| `viewportHeight` | Número entero | Tamaño vertical en píxeles de la ventana en la que se mostraba la experiencia. Para un evento de vista web, esta es la altura de la ventanilla del explorador. |
| `viewPortWidth` | Número entero | El tamaño horizontal en píxeles de la ventana en la que se mostraba la experiencia. Para un evento de vista web, esta es la anchura de la ventanilla del explorador. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre la variable [!UICONTROL Dispositivo] tipo de datos.

## Valores aceptados para el tipo {#type}

La siguiente tabla describe los valores aceptados para `type` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `browser` | Explorador |
| `application` | Aplicación |
| `iot` | Internet de cosas |
| `external` | Sistema externo |
| `widget` | Extensión de la aplicación |
