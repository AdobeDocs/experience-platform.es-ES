---
title: Detalles de auditoría del sistema de Source externo
description: Obtenga información sobre el grupo de campos Detalles de auditoría del sistema de Source externo Modelo de datos de experiencia (XDM).
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 4%

---

# [!UICONTROL External Source System Audit Details] grupo de campos

[!UICONTROL External Source System Audit Details] es un grupo de campos estándar del Modelo de datos de experiencia (XDM) que amplía el tipo de datos principal &quot;Atributos de auditoría del sistema de Source externo&quot; haciendo referencia a sus propiedades y agregando metadatos contextuales. Esto permite un seguimiento detallado de la auditoría y una integración de datos flexible desde fuentes externas.

![Un diagrama de esquema del grupo de campos Detalles de auditoría del sistema de Source externo.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL External Source System Audit Details] | `external-source-system-audit-details` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | El grupo de campos &#39;[!UICONTROL External Source System Audit Details]&#39; amplía el tipo de datos &#39;Atributos de auditoría del sistema de Source externo&#39; principal haciendo referencia a sus propiedades y agregando metadatos contextuales. Esto facilita el seguimiento detallado de la auditoría y la integración de datos flexible para fuentes externas, lo que permite la naturaleza asíncrona de la ingesta de perfiles. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)
