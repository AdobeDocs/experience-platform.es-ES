---
keywords: Experience Platform;inicio;temas populares;administración de datos;guía del usuario de la directiva de uso de datos
solution: Experience Platform
title: Administrar políticas de uso de datos en la interfaz de usuario
topic: policies
description: El Gobierno de datos de Adobe Experience Platform proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona información general sobre las acciones que puede realizar en el espacio de trabajo Directivas de la interfaz de usuario de Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# Administrar directivas de uso de datos en la interfaz de usuario

Adobe Experience Platform [!DNL Data Governance] proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona una visión general de las acciones que puede realizar en el área de trabajo **Directivas** de la interfaz de usuario [!DNL Experience Platform].

>[!IMPORTANT]
>
>Todas las directivas de uso de datos (incluidas las directivas principales proporcionadas por Adobe) están deshabilitadas de forma predeterminada. Para que una política individual se considere para su aplicación, debe habilitarla manualmente. Consulte la sección sobre [habilitación de políticas](#enable) para ver los pasos sobre cómo hacerlo en la interfaz de usuario.

## Requisitos previos

Esta guía requiere una comprensión práctica de los siguientes [!DNL Experience Platform] conceptos:

- [[!DNL Data Governance]](../home.md)
- [Directivas de uso de datos](./overview.md)

## Políticas existentes de vista {#view-policies}

En la interfaz de usuario [!DNL Experience Platform], seleccione **[!UICONTROL Directivas]** para abrir el espacio de trabajo **[!UICONTROL Directivas]**. En la ficha **[!UICONTROL Examinar]** puede ver una lista de las directivas disponibles, incluidas las etiquetas asociadas, las acciones de mercadotecnia y el estado.

![](../images/policies/browse-policies.png)

Seleccione una directiva de la lista para vista de su descripción y tipo. Si se selecciona una directiva personalizada, se muestran controles adicionales para editar, eliminar o [habilitar/deshabilitar la directiva](#enable).

![](../images/policies/policy-details.png)

## Crear una directiva personalizada {#create-policy}

Para crear una nueva directiva de uso de datos personalizada, seleccione **[!UICONTROL Crear directiva]** en la esquina superior derecha de la ficha **[!UICONTROL Examinar]** en el área de trabajo **[!UICONTROL Directivas]**.

![](../images/policies/create-policy-button.png)

Aparece el flujo de trabajo **[!UICONTROL Crear directiva]**. Inicio proporcionando un nombre y una descripción para la nueva directiva.

![](../images/policies/create-policy-description.png)

A continuación, seleccione las etiquetas de uso de datos en las que se basará la directiva. Al seleccionar varias etiquetas, se le da la opción de elegir si los datos deben contener todas las etiquetas o sólo una de ellas para que la política se aplique. Seleccione **[!UICONTROL Siguiente]** cuando termine.

![](../images/policies/add-labels.png)

Aparece el paso **[!UICONTROL Seleccionar acciones de mercadotecnia]**. Elija las acciones de mercadotecnia correspondientes en la lista proporcionada y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

>[!NOTE]
>
>Al seleccionar varias acciones de marketing, la política las interpreta como una regla &quot;O&quot;. En otras palabras, la política se aplica si **se realiza alguna** de las acciones de mercadotecnia seleccionadas.

![](../images/policies/add-marketing-actions.png)

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar los detalles de la nueva directiva antes de crearla. Una vez que esté satisfecho, seleccione **[!UICONTROL Finalizar]** para crear la directiva.

![](../images/policies/policy-review.png)

La ficha **[!UICONTROL Examinar]** vuelve a aparecer, que ahora lista la directiva recién creada con el estado &quot;Borrador&quot;. Para habilitar la directiva, consulte la siguiente sección.

![](../images/policies/created-policy.png)

## Habilitar o deshabilitar una directiva {#enable}

Todas las directivas de uso de datos (incluidas las directivas principales proporcionadas por Adobe) están deshabilitadas de forma predeterminada. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Puede habilitar o deshabilitar las directivas desde la ficha **[!UICONTROL Examinar]** en el área de trabajo **[!UICONTROL Directivas]**. Seleccione una directiva personalizada de la lista para mostrar sus detalles a la derecha. En **[!UICONTROL Estado]**, seleccione el botón de alternar para habilitar o deshabilitar la directiva.

![](../images/policies/enable-policy.png)

## Acciones de mercadotecnia de vista {#view-marketing-actions}

En el espacio de trabajo **[!UICONTROL Directivas]**, seleccione la ficha **[!UICONTROL Acciones de mercadotecnia]** para vista de una lista de acciones de mercadotecnia disponibles definidas por Adobe y su propia organización.

![](../images/policies/marketing-actions.png)

## Crear una acción de mercadotecnia {#create-marketing-action}

Para crear una nueva acción de mercadotecnia personalizada, seleccione **[!UICONTROL Crear acción de mercadotecnia]** en la esquina superior derecha de la ficha **[!UICONTROL Acciones de mercadotecnia]** en el área de trabajo **[!UICONTROL Directivas]**.

![](../images/policies/create-marketing-action.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear acción de mercadotecnia]**. Escriba un nombre y una descripción para la acción de mercadotecnia y, a continuación, seleccione **[!UICONTROL Crear]**.

![](../images/policies/create-marketing-action-details.png)

La acción recién creada aparece en la ficha **[!UICONTROL Acciones de mercadotecnia]**. Ahora puede usar la acción de mercadotecnia al [crear nuevas políticas de uso de datos](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar o eliminar una acción de mercadotecnia {#edit-delete-marketing-action}

>[!NOTE]
>
>Solo se pueden editar las acciones de mercadotecnia personalizadas definidas por su organización. Las acciones de marketing definidas por Adobe no se pueden cambiar ni eliminar.

En el espacio de trabajo **[!UICONTROL Directivas]**, seleccione la ficha **[!UICONTROL Acciones de mercadotecnia]** para vista de una lista de acciones de mercadotecnia disponibles definidas por Adobe y su propia organización. Seleccione una acción de marketing personalizada de la lista y, a continuación, utilice los campos proporcionados en la sección derecha para editar los detalles de la acción de marketing.

![](../images/policies/edit-marketing-action.png)

Si la acción de mercadotecnia no está siendo utilizada por ninguna directiva de uso existente, puede eliminarla seleccionando **[!UICONTROL Eliminar acción de mercadotecnia]**.

>[!NOTE]
>
>Si se intenta eliminar una acción de marketing que está utilizando una directiva existente, aparecerá un mensaje de error que indicará que el intento de eliminación ha fallado.

![](../images/policies/delete-marketing-action.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo administrar las políticas de uso de datos en la [!DNL Experience Platform] interfaz de usuario. Para ver los pasos sobre cómo administrar políticas mediante [!DNL Policy Service API], consulte la [guía para desarrolladores](../api/getting-started.md). Para obtener información sobre cómo aplicar políticas de uso de datos, consulte la [información general de cumplimiento de políticas](../enforcement/overview.md).

El siguiente vídeo muestra cómo trabajar con las políticas de uso en la interfaz de usuario [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)