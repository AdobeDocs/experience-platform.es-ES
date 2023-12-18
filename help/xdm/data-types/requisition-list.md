---
title: Tipo de datos de lista de solicitud
description: Obtenga información sobre el tipo de datos de la lista de solicitudes Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 5%

---

# [!UICONTROL Lista de solicitudes] tipo de datos

[!UICONTROL Lista de solicitudes] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe una recopilación depurada de elementos para su adquisición o compra. Utilice el [!UICONTROL Lista de solicitudes] tipo de datos para identificar y describir listas de solicitudes.

![Un diagrama de la [!UICONTROL Lista de solicitudes] tipo de datos.](../images/data-types/requisition-list.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL Identificador de lista de solicitud] | `ID` | string | Identificador único de la lista de solicitudes. |
| [!UICONTROL Nombre de lista de solicitudes] | `name` | string | Nombre de la lista de solicitudes especificada por el cliente. |
| [!UICONTROL Descripción de lista de solicitudes] | `description` | string | Descripción de la lista de solicitudes especificada por el cliente. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
