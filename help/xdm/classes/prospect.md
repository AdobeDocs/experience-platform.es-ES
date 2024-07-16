---
title: Clase de perfil de cliente potencial individual XDM
description: Obtenga información acerca de la clase de perfil de cliente potencial individual XDM en Experience Data Model (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: f4ddcf14de7a5cec42b5ebc521203cfdd1498a9f
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# [!UICONTROL Perfil de cliente potencial individual XDM] clase

En Experience Data Model (XDM), la clase [!UICONTROL XDM Individual Prospect Profile] captura perfiles de clientes potenciales que generalmente provienen de socios de datos para casos de uso de adquisición de clientes principales.

>[!NOTE]
>
>Para establecer un campo en el perfil de cliente potencial individual de XDM como identidad, primero debe crear al menos un área de nombres de ID de socio. Obtenga más información acerca del ID de socio en la [sección tipos de identidad](../../identity-service/features/namespaces.md).

![Diagrama de esquema de la clase de cliente potencial XDM.](../images/classes/individual-prospect-profile.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_repo` | Objeto | Esta clase le permite incorporar perfiles de clientes potenciales procedentes de proveedores de datos para canalizar los casos de uso de adquisición de clientes. |
| `_repo.createDate` | [!UICONTROL DateTime] | La fecha y hora del servidor cuando se creó el recurso en el repositorio. La hora de creación podría ser la primera vez que se carga un archivo de recursos o cuando el servidor crea un directorio como elemento principal de un nuevo recurso. La propiedad datetime debe ajustarse a la normativa ISO 8601. Un ejemplo de este formato es &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | La fecha y hora del servidor cuando se modificó por última vez el recurso en el repositorio, como cuándo se cargó una nueva versión de un recurso o se agregó o eliminó un recurso secundario de un directorio. La propiedad datetime debe ajustarse a la normativa ISO 8601. Por ejemplo, &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `createdByBatchID` | [!UICONTROL Cadena] | El ID del lote ingerido que provocó la creación del registro. |
| `modifiedByBatchID` | [!UICONTROL Cadena] | El ID del último lote ingerido que provocó que se actualizara el registro. |
| `partnerID` | [!UICONTROL Cadena] | Normalmente, un identificador pseudonímico único que identifica a un cliente potencial individual. Consulte la documentación sobre [tipos de identidad](../../identity-service/features/namespaces.md#identity-type) para obtener más información sobre el ID de socio y los demás tipos de identidad disponibles en Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL Cadena] | El ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | [!UICONTROL Cadena] | El ID del usuario que modificó el registro por última vez. Cuando se crea el registro, el valor `modifiedByUser` se establece como el valor `createdByUser`. |

{style="table-layout:auto"}
