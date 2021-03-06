---
title: Tipo de datos de atributos de auditoría del sistema de fuentes externas
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias (XDM) de atributos de auditoría del sistema de fuentes externas.
source-git-commit: 8bf0c63f33ae9cbfb01d4db9e5220c6762575c5b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# [!UICONTROL Tipo de datos de ] atributos de auditoría de sistemas de origen externo

>[!NOTE]
>
>Este tipo de datos solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

[!UICONTROL Atribución de auditoría de sistemas de fuentes externas ] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Fuente B2B]](./b2b-source.md) | Identificador compuesto de la fuente utilizada para la auditoría. |
| `createdBy` | Cadena | Nombre del usuario que ha creado este registro. |
| `createdDate` | DateTime | La fecha en la que se creó este registro. |
| `externalID` | Cadena | Identificador único externo del origen. Este valor se utiliza para ayudar a identificar y deduplicar si es necesario. |
| `lastActivityDate` | DateTime | La última fecha de actividad del sistema de origen. |
| `lastReferencedDate` | DateTime | La última fecha a la que se hace referencia para el sistema de origen. |
| `lastUpdatedBy` | Cadena | El nombre de la persona que actualizó este registro por última vez. |
| `lastUpdatedDate` | DateTime | Fecha de la última actualización del sistema de origen. |
| `lastViewedDate` | DateTime | La última fecha de visualización del sistema de origen. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
