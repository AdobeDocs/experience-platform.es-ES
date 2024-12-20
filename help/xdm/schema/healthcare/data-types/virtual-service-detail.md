---
title: Tipo de datos de detalles del servicio virtual
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia detallada del servicio virtual (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bde7363c-43b7-402d-96b2-7aa0160cd2ea
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# [!UICONTROL Tipo de datos de detalle del servicio virtual]

[!UICONTROL Detalle del servicio virtual] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de contacto del servicio virtual. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de detalle del servicio virtual](../../../images/healthcare/data-types/virtual-service-detail.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Punto de contacto de dirección] | `addressContactPoint` | [[!UICONTROL Punto de contacto]](../data-types/contact-point.md) | Los detalles de un punto de contacto mediado por tecnología, como un teléfono, un fax o un correo electrónico. |
| [!UICONTROL Detalle de contacto extendido de la dirección] | `addressExtendedContactDetail` | [[!UICONTROL Detalles de contacto extendidos]](../data-types/extended-contact-detail.md) | Información de contacto extendida. |
| [!UICONTROL Tipo de canal] | `channelType` | [[!UICONTROL Codificación]](../data-types/coding.md) | Tipo de servicio virtual al que se va a conectar, como Teams, Zoom o WhatsApp. |
| [!UICONTROL Información adicional] | `additionalInfo` | Matriz de cadenas | La dirección para ver detalles de conexión alternativos, representados como un URI. |
| [!UICONTROL Cadena de dirección] | `addressString` | Cadena | Dirección que se va a utilizar para conectarse al servicio virtual. |
| [!UICONTROL Dirección Url] | `addressUrl` | Cadena | Dirección URL que se va a utilizar para conectarse al servicio virtual, representada como URI. |
| [!UICONTROL Máximo de participantes] | `maxParticipants` | Entero | Número máximo de participantes admitidos, con un valor mínimo de `0`. |
| [!UICONTROL Clave de sesión] | `sessionKey` | Cadena | Clave de sesión requerida por el servicio virtual. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
