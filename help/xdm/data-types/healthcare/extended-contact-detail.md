---
title: Tipo de datos de detalles de contacto extendido
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia detallada de contacto extendido (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# [!UICONTROL Detalle de contacto extendido] tipo de datos

[!UICONTROL Detalle de contacto extendido] es un tipo de datos de modelo de datos de experiencia (XDM) estándar que describe la información de un contacto extendido. Este tipo de datos se crea de acuerdo con las especificaciones de la versión 5 de HL7 FHIR.

![Estructura de tipo de datos de detalles de contacto extendidos](../../images/data-types/healthcare/extended-contact-detail.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Dirección] | `address` | [[!UICONTROL Dirección]](../healthcare/address.md) | La dirección del contacto. |
| [!UICONTROL Nombre] | `name` | Matriz de [[!UICONTROL nombre humano]](../healthcare/human-name.md) | El nombre de la persona o personas con las que se va a contactar. |
| [!UICONTROL Organización] | `organization` | [[!UICONTROL Referencia]](../healthcare/reference.md) | La organización que administra/supervisa los detalles de contacto. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../healthcare/period.md) | Período durante el cual el contacto es o era válido para su uso. |
| [!UICONTROL Finalidad] | `purpose` | [[!UICONTROL Concepto codificable]](../healthcare/codeable-concept.md) | El tipo de contacto. |
| [!UICONTROL Telecomunicaciones] | `telecom` | Matriz de [[!UICONTROL punto de contacto]](../healthcare/contact-point.md) | Los datos de contacto. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
