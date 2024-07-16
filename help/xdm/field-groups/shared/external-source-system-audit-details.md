---
title: Detalles de auditoría del sistema de origen externo
description: Obtenga información sobre el grupo de campos Detalles de auditoría del sistema de Source externo Modelo de datos de experiencia (XDM).
source-git-commit: 656070cf69e3713c7889f53d51937e0e70085d96
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# [!UICONTROL Detalles de auditoría del sistema de Source externo] grupo de campos

[!UICONTROL Detalles de auditoría del sistema de Source externo] es un grupo de campos de modelo de datos de experiencia (XDM) estándar que amplía el tipo de datos principal &#39;Atributos de auditoría del sistema de Source externo&#39; al hacer referencia a sus propiedades y agregar metadatos contextuales. Esto permite un seguimiento detallado de la auditoría y una integración de datos flexible desde fuentes externas.

![Un diagrama de esquema del grupo de campos Detalles de auditoría del sistema de Source externo.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL Detalles de auditoría del sistema Source externo] | `external-source-system-audit-details` | [[!UICONTROL Atributos de auditoría del sistema Source externo]](../../data-types/external-source-system-audit-attributes.md) | El grupo de campos &#39;[!UICONTROL Detalles de auditoría del sistema de Source externo]&#39; amplía el tipo de datos &#39;Atributos de auditoría del sistema de Source externo&#39; haciendo referencia a sus propiedades y agregando metadatos contextuales. Esto facilita el seguimiento detallado de la auditoría y la integración de datos flexible para fuentes externas, lo que permite la naturaleza asíncrona de la ingesta de perfiles. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)