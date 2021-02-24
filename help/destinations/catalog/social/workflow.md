---
keywords: Facebook;Facebook;red social;red social;red social;autenticación de redes sociales;autenticación de redes sociales
title: Crear un destino de red social
type: Tutorial
description: Obtenga información sobre cómo conectarse a sus cuentas de publicidad de red social en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---


# Crear un destino de red social {#social-network-destinations-workflow}

Este tutorial utiliza [!DNL Facebook] como ejemplo, pero el flujo de trabajo de Adobe Experience Platform es el mismo para todos los destinos de redes sociales.

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, desplácese a la categoría **[!UICONTROL Social]**. Seleccione el destino preferido de la red social y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Conectar al destino de red social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Autenticación**, si previamente había configurado una conexión con el destino de red social, seleccione **[!UICONTROL Cuenta existente]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de red social. Seleccione **[!UICONTROL Conectar al destino]** y esto le llevará al destino de red social seleccionado para iniciar sesión y conectar Adobe Experience Cloud a su cuenta de publicidad de red social.

>[!NOTE]
>
>La plataforma admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en el ID de cuenta de la red social. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

![Conectar con destino de red social: paso de autenticación](../../assets/catalog/social/workflow/pre-connect.png)

Una vez confirmadas las credenciales y Adobe Experience Cloud conectado a la red social, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso **[!UICONTROL Configuración]**.

![Credenciales confirmadas](../../assets/catalog/social/workflow/post-connect.png)

En el paso **[!UICONTROL Configuración]**, escriba un [!UICONTROL Nombre] y una [!UICONTROL Descripción] para el flujo de activación y rellene el [!UICONTROL ID de cuenta] de la cuenta de publicidad de red social.

>[!IMPORTANT]
>
> Para destinos [!DNL Facebook], **[!UICONTROL ID de cuenta]** es su [!DNL Facebook Ad Account ID]. Puede encontrar este ID en [!DNL Facebook Ads Manager]. Agregue el prefijo `act_` como se muestra a continuación:

![Conectar con destino de red social: paso de configuración](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> Para destinos [!DNL LinkedIn], **[!UICONTROL ID de cuenta]** es su [!DNL LinkedIn Campaign Manager Account ID]. Puede encontrar este ID en [!DNL LinkedIn Campaign Manager].

También en este paso, puede seleccionar cualquier **[!UICONTROL acción de mercadotecnia]** que deba aplicarse a este destino. Las acciones de marketing indican la intención de los datos que se exportarán al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o puede crear su propia acción de marketing. Para obtener más información acerca de las acciones de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos en redes sociales](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos en redes sociales {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en redes sociales, consulte [Activar datos en destinos](../../ui/activate-destinations.md).