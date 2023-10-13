---
title: Tipo de datos de atributos de auditoría del sistema de origen externo
description: Este documento proporciona información general sobre el tipo de datos XDM (Experience Data Model) de los atributos de auditoría del sistema de origen externo.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: a7e6ebfe09566e6e027b13efc95dda97ff8f0315
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---

# [!UICONTROL Atributos de auditoría del sistema de origen externo] tipo de datos

[!UICONTROL Atributos de auditoría del sistema de origen externo] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Origen B2B]](./b2b-source.md) | Identificador compuesto del origen utilizado para la auditoría. |
| `createdBy` | Cadena | El nombre del usuario que creó este registro. |
| `createdDate` | DateTime | La fecha en la que se creó este registro. |
| `externalID` | Cadena | Identificador único externo del origen. Este valor se utiliza para ayudar a identificar y deduplicar si es necesario. |
| `lastActivityDate` | DateTime | Fecha de la última actividad del sistema de origen. |
| `lastReferencedDate` | DateTime | La última fecha de referencia del sistema de origen. |
| `lastUpdatedBy` | Cadena | Nombre de la persona que actualizó este registro por última vez. |
| `lastUpdatedDate` | DateTime | Fecha de la última actualización del sistema de origen. |
| `lastViewedDate` | DateTime | La última fecha de visualización del sistema de origen. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
