---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del usuario de directivas de uso de datos
topic: policies
translation-type: tm+mt
source-git-commit: 235a43ad72dee45db1b3d35ae84ce9a1c4d729b8

---


# Guía del usuario de directivas de uso de datos

El Gobierno de datos de la plataforma de experiencia de Adobe proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona una descripción general de las acciones que puede realizar en el espacio de trabajo _Directivas_ de la interfaz de usuario de la plataforma de experiencia.

## Requisitos previos

Esta guía requiere una comprensión práctica de los siguientes conceptos de la plataforma de experiencia:

- [Gobierno de datos](../home.md)
- [Directivas de uso de datos](./overview.md)

## Directivas de uso de datos de Vista

En la interfaz de usuario de la plataforma de experiencia, haga clic en **[!UICONTROL Policies]** para abrir el *[!UICONTROL Policies]* espacio de trabajo. En la **[!UICONTROL Browse]** ficha, puede ver una lista de las directivas disponibles, incluidas las etiquetas asociadas, las acciones de marketing y el estado.

![](../images/policies/browse-policies.png)

Haga clic en una directiva de la lista para vista de su descripción y tipo. Si se selecciona una directiva personalizada, se muestran controles adicionales para editar, eliminar o [habilitar/deshabilitar la directiva](#enable).

![](../images/policies/policy-details.png)

## Crear una directiva de uso de datos personalizada

Para crear una nueva directiva de uso de datos personalizada, haga clic en **[!UICONTROL Create policy]** en la esquina superior derecha del espacio de trabajo *Directivas* .

![](../images/policies/create-policy-button.png)

Aparece el *[!UICONTROL Create policy]* flujo de trabajo. Inicio proporcionando un nombre y una descripción para la nueva directiva.

![](../images/policies/create-policy-description.png)

A continuación, seleccione las etiquetas de uso de datos en las que se basará la directiva. Al seleccionar varias etiquetas, se le da la opción de elegir si los datos deben contener todas las etiquetas o sólo una de ellas para que la política se aplique. Haga clic en **[!UICONTROL Next]** cuando termine.

![](../images/policies/add-labels.png)

Aparecerá el *[!UICONTROL Select marketing actions]* paso. Elija las acciones de mercadotecnia correspondientes en la lista proporcionada y haga clic en **[!UICONTROL Next]** para continuar.

>[!NOTE] Al seleccionar varias acciones de marketing, la política las interpreta como una regla &quot;O&quot;. En otras palabras, la política se aplica si se realiza _cualquiera_ de las acciones de marketing seleccionadas.

![](../images/policies/add-marketing-actions.png)

Aparece el *[!UICONTROL Review]* paso, que le permite revisar los detalles de la nueva directiva antes de crearla. Una vez que esté satisfecho, haga clic en **[!UICONTROL Finish]** para crear la directiva.

![](../images/policies/policy-review.png)

La ficha *[!UICONTROL Browse]* vuelve a aparecer, que ahora lista la directiva recién creada con el estado &quot;Borrador&quot;. Para habilitar la directiva, consulte la siguiente sección.

![](../images/policies/created-policy.png)

## Habilitar o deshabilitar una directiva de uso de datos {#enable}

Puede habilitar o deshabilitar las directivas de uso de datos personalizadas en la *[!UICONTROL Browse]* ficha del espacio de trabajo *[!UICONTROL Policies]* . Seleccione una directiva personalizada de la lista para mostrar sus detalles a la derecha. En *[!UICONTROL Status]*, seleccione el botón de alternancia para habilitar o deshabilitar la directiva.

![](../images/policies/enable-policy.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo administrar las políticas de uso de datos en la interfaz de usuario de la plataforma de experiencia. Para ver los pasos sobre cómo administrar políticas mediante la API de directiva DULE, consulte la guía [para](../api/getting-started.md)desarrolladores. Para obtener información sobre cómo aplicar políticas de uso de datos, consulte la descripción general [de la aplicación de](../enforcement/overview.md)políticas.