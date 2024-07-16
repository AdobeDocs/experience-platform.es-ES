---
title: Clase de lista de marketing empresarial de XDM
description: Obtenga información acerca de la clase de lista de marketing empresarial de XDM en el modelo de datos de experiencia (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# clase [!UICONTROL XDM Business Marketing List]

>[!IMPORTANT]
>
>Esta clase está pensada para que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL La lista de marketing empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una lista de marketing. Las listas de marketing le permiten priorizar los clientes potenciales que tienen más probabilidades de comprar su producto.

![La estructura de la clase Lista de marketing empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-marketing-list.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema Source externo]](../../data-types/external-source-system-audit-attributes.md) | Si la lista de marketing proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de la lista de marketing. |
| `_id` | Cadena | Un identificador único del registro. Este es un valor generado por el sistema que es independiente de `marketingListID`. |
| `isDeleted` | Booleano | Indica si esta entidad de la lista de marketing se ha eliminado en el Marketo Engage.<br><br>Al usar el [conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Al establecer `isDeleted` en `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `marketingListDescription` | Cadena | Una descripción de la lista de marketing. |
| `marketingListID` | Cadena | Un ID único para la entidad de la lista de marketing. |
| `marketingListName` | Cadena | Nombre de la lista de marketing. |

{style="table-layout:auto"}

Consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para obtener información sobre cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
