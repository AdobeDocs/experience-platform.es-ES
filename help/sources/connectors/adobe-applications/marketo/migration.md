---
title: Migrar la asignación de ECID de persona a actividad mediante el origen del Marketo Engage
description: Obtenga información sobre cómo migrar la asignación de ECID del conjunto de datos de persona al conjunto de datos de actividad mediante el origen del Marketo Engage.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Migrar asignación ECID desde [!DNL Person] conjunto de datos a [!DNL Activity] conjunto de datos

Puede migrar la asignación ECID desde su [!DNL Marketo Engage Person] conjunto de datos a su [!DNL Activity] conjunto de datos para proporcionar un comportamiento más estable de la ingesta de datos y la administración de identidades. Además, esta migración aborda los siguientes aspectos:

| Problema | Solución |
| --- | --- |
| Cuando su [!DNL Marketo Person] tiene vínculos a varios ECID, la ingesta de datos falla cuando el [el número total de identidades en un registro de modelo de datos de experiencia (XDM) supera las 20](../../../../identity-service/guardrails.md). | Migrando la asignación de campo ECID a [!DNL Activity], puede asegurarse de que el número de identidades del [!DNL Marketo Person] el flujo de datos se mantiene dentro del límite y, por lo tanto, permite que la ingesta de datos tenga éxito. |
| Cada vez que [!DNL Marketo Person] conjunto de datos se incorpora con ECID, la marca de tiempo en todos los ECID del [!DNL Marketo Person] Los conjuntos de datos de se actualizan con la última marca de tiempo actualizada del registro Persona. Esto podría provocar el [eliminación incorrecta de identidades más recientes del gráfico de identidades](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Migrando las asignaciones de campo de ECID a [!DNL Activity], el servicio de identidad puede reflejar correctamente la marca de tiempo de los ECID y el mecanismo de &quot;primero en entrar, primero en salir&quot; del servicio de identidad proporcionará un comportamiento más estable. |
| Cuando los ECID se ingieren mediante [!DNL Marketo Person] flujo de datos, los ECID recién añadidos no se incorporan en Experience Platform a menos que haya actualizaciones de [!DNL Person] grabar en [!DNL Marketo]. | Cuando se vincula un nuevo ECID al [!DNL Person] grabar en [!DNL Marketo], puede introducir esos datos de ECID mediante un [!DNL Marketo Activity] flujo de datos e solicitar inmediatamente una actualización del gráfico de identidades en el Experience Platform. |

Básicamente, debe:

* Actualice su [!DNL Marketo Activity] flujo de datos.
* Actualice su [!DNL Marketo Person] flujo de datos.

## Actualizar [!DNL Marketo Activity] flujo de datos {#update-activity-dataflow}

Siga los pasos a continuación para actualizar su [!DNL Marketo Activity] flujo de datos:

* En la interfaz de usuario del Experience Platform de, vaya a *Fuentes* y busque el flujo de datos existente para [!DNL Marketo Activity] datos.
* Dado que el flujo de datos está habilitado, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y seleccione **[!UICONTROL Actualizar flujo de datos]**.
* A continuación, seleccione **[!UICONTROL Siguiente]** hasta que llegue al *Asignación* interfaz.
* En el *Asignación* interfaz, seleccione **[!UICONTROL Nuevo campo]** y luego seleccione **[!UICONTROL Añadir campo calculado]**. A partir de aquí, debe agregar lo siguiente:

| Conjunto de datos de origen | Campo de destino XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Si la actualización a un existente [!DNL Marketo] El flujo de datos consiste únicamente en agregar o eliminar el campo de asignación ECID, y luego el flujo de datos omite automáticamente el trabajo de relleno histórico. La nueva ingesta de datos solo se producirá cuando se produzcan tipos de actividades como &quot;visitar página web&quot; y &quot;hacer clic en página web&quot;.

## Actualizar [!DNL Marketo Person] flujo de datos {#update-person-dataflow}

Siga los pasos a continuación para actualizar su [!DNL Marketo Person] flujo de datos:

* En la interfaz de usuario del Experience Platform de, vaya a *Fuentes* y busque el flujo de datos existente para [!DNL Marketo Person] datos.
* Dado que el flujo de datos está habilitado, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y seleccione **[!UICONTROL Actualizar flujo de datos]**.
* A continuación, seleccione **[!UICONTROL Siguiente]** hasta que llegue al *Asignación* interfaz.
* En el *Asignación* interfaz, elimine el campo calculado que se asigna a `identityMap` y luego seleccione **[!UICONTROL Siguiente]** y **[!UICONTROL Guardar e introducir]**.

>[!NOTE]
>
>Si la actualización a un existente [!DNL Marketo] El flujo de datos consiste únicamente en agregar o eliminar el campo de asignación ECID, y luego el flujo de datos omite automáticamente el trabajo de relleno histórico. La marca de tiempo de los ECID que se han introducido anteriormente seguirá siendo la misma. Solo se actualizarán cuando se ingieran nuevos datos que correspondan a los ECID existentes.

## Pasos siguientes

Al leer este documento, ahora sabe cómo migrar la asignación ECID desde su [!DNL Marketo Person] conjunto de datos a [!DNL Marketo Activity] conjunto de datos. Para obtener más información, lea lo siguiente [!DNL Marketo] documentos:

* [Crear un flujo de datos para la ingesta [!DNL Marketo] datos para el Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guía de asignación de campos](../mapping/marketo.md).