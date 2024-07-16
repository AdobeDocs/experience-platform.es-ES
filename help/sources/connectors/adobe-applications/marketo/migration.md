---
title: Migrar la asignación de ECID de persona a actividad mediante el origen del Marketo Engage
description: Obtenga información sobre cómo migrar la asignación de ECID del conjunto de datos de persona al conjunto de datos de actividad mediante el origen del Marketo Engage.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Migrar asignación ECID del conjunto de datos [!DNL Person] al conjunto de datos [!DNL Activity]

Puede migrar su asignación ECID del conjunto de datos [!DNL Marketo Engage Person] al conjunto de datos [!DNL Activity] para proporcionar un comportamiento más estable de la ingesta de datos y la administración de identidades. Además, esta migración aborda los siguientes aspectos:

| Problema | Solución |
| --- | --- |
| Cuando el conjunto de datos [!DNL Marketo Person] tiene vínculos a varios ECID, la ingesta de datos falla cuando el [número total de identidades en un registro de modelo de datos de experiencia (XDM) supera las 20](../../../../identity-service/guardrails.md). | Al migrar la asignación de campo de ECID a [!DNL Activity], puede asegurarse de que el número de identidades del flujo de datos [!DNL Marketo Person] se mantenga dentro del límite y, por lo tanto, permita que la ingesta de datos se realice correctamente. |
| Cada vez que el conjunto de datos [!DNL Marketo Person] se ingiere con ECID, la marca de tiempo de todos los ECID del conjunto de datos [!DNL Marketo Person] se actualiza con la última marca de tiempo actualizada del registro de persona. Esto podría resultar en la eliminación [incorrecta de identidades más recientes del gráfico de identidades](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Al migrar las asignaciones de campo de ECID a [!DNL Activity], el servicio de identidad puede reflejar correctamente la marca de tiempo de los ECID y el mecanismo de &quot;primero en entrar y primero en salir&quot; del servicio de identidad proporcionará un comportamiento más estable. |
| Cuando los ECID se incorporan a través del flujo de datos [!DNL Marketo Person], los ECID recién agregados no se incorporan en el Experience Platform a menos que haya actualizaciones en el registro [!DNL Person] en [!DNL Marketo]. | Cuando se vincula un nuevo ECID al registro [!DNL Person] en [!DNL Marketo], se pueden ingerir esos datos de ECID a través de un flujo de datos [!DNL Marketo Activity] y solicitar inmediatamente una actualización del gráfico de identidades en el Experience Platform. |

Básicamente, debe:

* Actualice su flujo de datos [!DNL Marketo Activity].
* Actualice su flujo de datos [!DNL Marketo Person].

## Actualizar flujo de datos [!DNL Marketo Activity] {#update-activity-dataflow}

Siga los pasos a continuación para actualizar su flujo de datos de [!DNL Marketo Activity]:

* En la interfaz de usuario del Experience Platform, vaya al área de trabajo *Sources* y busque el flujo de datos existente para [!DNL Marketo Activity] datos.
* Dado que el flujo de datos está habilitado, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione **[!UICONTROL Actualizar flujo de datos]**.
* A continuación, seleccione **[!UICONTROL Siguiente]** hasta que llegue a la interfaz *Mapping*.
* En la interfaz *Mapping*, selecciona **[!UICONTROL Nuevo campo]** y, a continuación, selecciona **[!UICONTROL Agregar campo calculado]**. A partir de aquí, debe agregar lo siguiente:

| Conjunto de datos Source | Campo de destino XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Si la actualización a un flujo de datos de [!DNL Marketo] existente consiste únicamente en agregar o eliminar el campo de asignación ECID, el flujo de datos omite automáticamente el trabajo de relleno histórico. La nueva ingesta de datos solo se producirá cuando se produzcan tipos de actividades como &quot;visitar página web&quot; y &quot;hacer clic en página web&quot;.

## Actualizar flujo de datos [!DNL Marketo Person] {#update-person-dataflow}

Siga los pasos a continuación para actualizar su flujo de datos de [!DNL Marketo Person]:

* En la interfaz de usuario del Experience Platform, vaya al área de trabajo *Sources* y busque el flujo de datos existente para [!DNL Marketo Person] datos.
* Dado que el flujo de datos está habilitado, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione **[!UICONTROL Actualizar flujo de datos]**.
* A continuación, seleccione **[!UICONTROL Siguiente]** hasta que llegue a la interfaz *Mapping*.
* En la interfaz *Mapping*, quita el campo calculado que se asigna a `identityMap` y, a continuación, selecciona **[!UICONTROL Next]** y **[!UICONTROL Save &amp; Ingest]**.

>[!NOTE]
>
>Si la actualización a un flujo de datos de [!DNL Marketo] existente consiste únicamente en agregar o eliminar el campo de asignación ECID, el flujo de datos omite automáticamente el trabajo de relleno histórico. La marca de tiempo de los ECID que se han introducido anteriormente seguirá siendo la misma. Solo se actualizarán cuando se ingieran nuevos datos que correspondan a los ECID existentes.

## Pasos siguientes

Al leer este documento, ahora sabe cómo migrar su asignación ECID del conjunto de datos [!DNL Marketo Person] al conjunto de datos [!DNL Marketo Activity]. Para obtener más información, lea los [!DNL Marketo] documentos siguientes:

* [Crear un flujo de datos para ingerir [!DNL Marketo] datos en el Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guía de asignación de campos](../mapping/marketo.md).
