---
keywords: Facebook;facebook;red social;red social;autenticación social;autenticación de red social
title: Crear un destino social
type: Tutorial
description: Aprenda a conectarse a sus cuentas de anuncios sociales en Adobe Experience Platform.
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Crear un destino social {#social-network-destinations-workflow}

## Información general {#overview}

Este tutorial utiliza [!DNL Facebook] como ejemplo, pero el flujo de trabajo de Adobe Experience Platform es el mismo para todos los destinos sociales.

## Configuración del destino social: tutorial de vídeo {#video}

El siguiente vídeo muestra cómo configurar un destino social y activar segmentos en Adobe Experience Platform. Los pasos también se describen secuencialmente en las secciones siguientes.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Seleccionar destino social {#select-destination}

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, desplácese hasta la categoría **[!UICONTROL Social]**. Seleccione su destino social preferido y, a continuación, seleccione **[!UICONTROL Configure]**.

![Conectarse a destino social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

## Paso de cuenta {#account}

En el paso **Cuenta**, si anteriormente ha configurado una conexión con su destino social, seleccione **[!UICONTROL Existing Account]** y la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** para configurar una nueva conexión con su destino social. Seleccione **[!UICONTROL Connect to destination]** y esto le llevará al destino social seleccionado para iniciar sesión y conectar Adobe Experience Cloud a su cuenta de publicidad social.

>[!NOTE]
>
>Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en el ID de cuenta social. Esto garantiza que no complete el flujo de trabajo con credenciales incorrectas.

![Conectar con destino social: paso de autenticación](../../assets/catalog/social/workflow/pre-connect.png)

Una vez confirmadas las credenciales y que Adobe Experience Cloud esté conectado a la red social, puede seleccionar **[!UICONTROL Next]** para continuar con el paso **[!UICONTROL Authentication]**.

![Credenciales confirmadas](../../assets/catalog/social/workflow/post-connect.png)

## Paso de autenticación {#authentication}

En el paso **[!UICONTROL Authentication]**, introduzca un [!UICONTROL Name] y un [!UICONTROL Description] para el flujo de activación y rellene el [!UICONTROL Account ID] de su cuenta de publicidad de red social.

>[!IMPORTANT]
>
> * Para destinos [!DNL Facebook], **[!UICONTROL Account ID]** es su [!DNL Facebook Ad Account ID]. Puede encontrar este ID en [!DNL Facebook Ads Manager]. Agregue el prefijo `act_` como se muestra en la imagen siguiente.
> * Para destinos [!DNL LinkedIn], **[!UICONTROL Account ID]** es su [!DNL LinkedIn Campaign Manager Account ID]. Puede encontrar este ID en [!DNL LinkedIn Campaign Manager].


![Conectar con destino social: paso de autenticación](../../assets/catalog/social/workflow/authentication.png)

En este paso, también puede seleccionar cualquier **[!UICONTROL Marketing action]** que deba aplicarse a este destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** para continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos en redes sociales](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos en redes sociales {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en redes sociales, consulte [Activar datos en destinos](../../ui/activate-destinations.md).
