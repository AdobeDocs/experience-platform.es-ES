---
keywords: Experience Platform;inicio;temas populares;control de datos;guía del usuario de políticas de uso de datos
solution: Experience Platform
title: Administrar políticas de uso de datos en la interfaz de usuario
topic-legacy: policies
description: Administración de datos de Adobe Experience Platform proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona información general sobre las acciones que puede realizar en el espacio de trabajo Directivas de la interfaz de usuario del Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# Administrar políticas de uso de datos en la interfaz de usuario

Adobe Experience Platform [!DNL Data Governance] proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona información general sobre las acciones que puede realizar en el espacio de trabajo **Directivas** de la interfaz de usuario [!DNL Experience Platform].

>[!IMPORTANT]
>
>De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una directiva individual se considere para su aplicación, debe habilitarla manualmente. Consulte la sección sobre [habilitación de políticas](#enable) para ver los pasos sobre cómo hacerlo en la interfaz de usuario.

## Requisitos previos

Esta guía requiere una comprensión práctica de los siguientes conceptos [!DNL Experience Platform]:

- [[!DNL Data Governance]](../home.md)
- [Políticas de uso de datos](./overview.md)

## Ver directivas existentes {#view-policies}

En la interfaz de usuario [!DNL Experience Platform], seleccione **[!UICONTROL Policies]** para abrir el espacio de trabajo **[!UICONTROL Policies]**. En la pestaña **[!UICONTROL Browse]**, puede ver una lista de las políticas disponibles, incluidas sus etiquetas asociadas, las acciones de marketing y el estado.

![](../images/policies/browse-policies.png)

Seleccione una directiva de la lista para ver su descripción y tipo. Si se selecciona una directiva personalizada, se muestran controles adicionales para editar, eliminar o [habilitar/deshabilitar la directiva](#enable).

![](../images/policies/policy-details.png)

## Crear una directiva personalizada {#create-policy}

Para crear una nueva directiva de uso de datos personalizada, seleccione **[!UICONTROL Create policy]** en la esquina superior derecha de la pestaña **[!UICONTROL Browse]** en el espacio de trabajo **[!UICONTROL Policies]**.

![](../images/policies/create-policy-button.png)

Aparece el flujo de trabajo **[!UICONTROL Create policy]** . Comience por proporcionar un nombre y una descripción para la nueva directiva.

![](../images/policies/create-policy-description.png)

A continuación, seleccione las etiquetas de uso de datos en las que se basará la directiva. Al seleccionar varias etiquetas, se le da la opción de elegir si los datos deben contener todas las etiquetas o solo una de ellas para que se aplique la política. Seleccione **[!UICONTROL Next]** cuando haya terminado.

![](../images/policies/add-labels.png)

Aparece el paso **[!UICONTROL Select marketing actions]**. Elija las acciones de marketing adecuadas en la lista proporcionada y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

>[!NOTE]
>
>Al seleccionar varias acciones de marketing, la política las interpreta como una regla &quot;O&quot;. En otras palabras, la política se aplica si se realizan **cualquiera** de las acciones de marketing seleccionadas.

![](../images/policies/add-marketing-actions.png)

Aparece el paso **[!UICONTROL Review]**, que le permite revisar los detalles de la nueva directiva antes de crearla. Una vez que esté satisfecho, seleccione **[!UICONTROL Finish]** para crear la directiva.

![](../images/policies/policy-review.png)

La pestaña **[!UICONTROL Browse]** vuelve a aparecer, que ahora enumera la política recién creada en estado &quot;Borrador&quot;. Para habilitar la directiva, consulte la siguiente sección.

![](../images/policies/created-policy.png)

## Habilitar o deshabilitar una directiva {#enable}

De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Puede habilitar o deshabilitar las directivas desde la pestaña **[!UICONTROL Browse]** en el espacio de trabajo **[!UICONTROL Policies]**. Seleccione una directiva personalizada de la lista para mostrar sus detalles a la derecha. En **[!UICONTROL Status]**, seleccione el botón de alternancia para habilitar o deshabilitar la directiva.

![](../images/policies/enable-policy.png)

## Ver acciones de marketing {#view-marketing-actions}

En el espacio de trabajo **[!UICONTROL Policies]** , seleccione la pestaña **[!UICONTROL Marketing actions]** para ver una lista de las acciones de marketing disponibles definidas por Adobe y su propia organización.

![](../images/policies/marketing-actions.png)

## Crear una acción de marketing {#create-marketing-action}

Para crear una nueva acción de marketing personalizada, seleccione **[!UICONTROL Create marketing action]** en la esquina superior derecha de la pestaña **[!UICONTROL Marketing actions]** en el espacio de trabajo **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

Aparece el cuadro de diálogo **[!UICONTROL Create marketing action]**. Introduzca un nombre y una descripción para la acción de marketing y, a continuación, seleccione **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

La acción recién creada aparece en la pestaña **[!UICONTROL Marketing actions]**. Ahora puede utilizar la acción de marketing al [crear nuevas políticas de uso de datos](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar o eliminar una acción de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Solo se pueden editar las acciones de marketing personalizadas definidas por su organización. Las acciones de marketing definidas por Adobe no se pueden cambiar ni eliminar.

En el espacio de trabajo **[!UICONTROL Policies]** , seleccione la pestaña **[!UICONTROL Marketing actions]** para ver una lista de las acciones de marketing disponibles definidas por Adobe y su propia organización. Seleccione una acción de marketing personalizada de la lista y, a continuación, utilice los campos proporcionados en la sección derecha para editar los detalles de la acción de marketing.

![](../images/policies/edit-marketing-action.png)

Si la acción de marketing no está siendo utilizada por ninguna directiva de uso existente, puede eliminarla seleccionando **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Si se intenta eliminar una acción de marketing que esté utilizando una directiva existente, aparecerá un mensaje de error indicando que el intento de eliminación ha fallado.

![](../images/policies/delete-marketing-action.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo administrar las políticas de uso de datos en la interfaz de usuario [!DNL Experience Platform]. Para ver los pasos sobre cómo administrar políticas usando [!DNL Policy Service API], consulte la [guía para desarrolladores](../api/getting-started.md). Para obtener información sobre cómo aplicar políticas de uso de datos, consulte la [información general sobre cumplimiento de políticas](../enforcement/overview.md).

El siguiente vídeo muestra cómo trabajar con políticas de uso en la interfaz de usuario de [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
