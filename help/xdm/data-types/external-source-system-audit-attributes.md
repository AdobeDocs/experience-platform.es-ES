---
title: Tipo de datos de atributos de auditoría del sistema de Source externo
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de atributos de auditoría del sistema de Source externo.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# [!UICONTROL Atributos de auditoría del sistema de Source externo] tipo de datos

[!UICONTROL Atributos de auditoría del sistema de Source externo] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Source B2B]](./b2b-source.md) | Identificador compuesto del origen utilizado para la auditoría. |
| `createdBy` | Cadena | El nombre del usuario que creó este registro. |
| `createdDate` | Fecha/Hora | La fecha en la que se creó este registro. |
| `externalID` | Cadena | Identificador único externo del origen. Este valor se utiliza para ayudar a identificar y deduplicar si es necesario. |
| `lastActivityDate` | Fecha/Hora | Fecha de la última actividad del sistema de origen. |
| `lastReferencedDate` | Fecha/Hora | La última fecha de referencia del sistema de origen. |
| `lastUpdatedBy` | Cadena | Nombre de la persona que actualizó este registro por última vez. |
| `lastUpdatedDate` | Fecha/Hora | Fecha de la última actualización del sistema de origen. Este valor lo usa la [política de combinación de atributos](../../profile/api/merge-policies.md#attribute-merge) para determinar la prioridad en caso de conflictos de combinación. |
| `lastViewedDate` | Fecha/Hora | La última fecha de visualización del sistema de origen. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
