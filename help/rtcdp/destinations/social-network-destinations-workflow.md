---
keywords: Facebook;facebook;Social network;Social Network;social network authentication;Social network authentication
title: Flujo de trabajo de destinos de redes sociales
seo-title: Flujo de trabajo de destinos de redes sociales
description: Instrucciones para conectarse a las cuentas de publicidad de la red social
seo-description: Instrucciones para conectarse a las cuentas de publicidad de la red social
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Flujo de trabajo de autenticación de destinos de red social {#social-network-destinations-workflow}

## Flujo de trabajo para crear destinos de redes sociales

Este tutorial utiliza [!DNL Facebook] como ejemplo, pero el flujo de trabajo de la plataforma de datos del cliente en tiempo real de Adobe será el mismo para todos los destinos de redes sociales, una vez que se añadan más al producto.

1. En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, desplácese hasta la categoría de **[!UICONTROL Social]** . Seleccione el destino preferido de la red social y, a continuación, seleccione **[!UICONTROL Configurar]**.

   ![Conectar al destino de red social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

   >[!NOTE]
   >
   >Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

2. En el paso **Autenticación** , si previamente ha configurado una conexión con el destino de red social, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de red social. Seleccione **[!UICONTROL Conectar al destino]** y esto le llevará al destino de red social seleccionado para iniciar sesión y conectar Adobe Experience Cloud a su cuenta de publicidad de red social.

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en el ID de cuenta de la red social. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de red social: paso de autenticación](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Una vez confirmadas las credenciales y que Adobe Experience Cloud esté conectado a la red social, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso de **[!UICONTROL configuración]** .

   ![Credenciales confirmadas](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. En el paso **[!UICONTROL Configuración]** , escriba un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación y rellene el ID **[!UICONTROL de]** cuenta de su cuenta de publicidad de red social. <br> También en este paso, puede seleccionar cualquier caso **[!UICONTROL de uso de]** Marketing que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos. <br> Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   >[!IMPORTANT]
   >
   > * El caso de uso de marketing de Personalización ** única de identidad está seleccionado de forma predeterminada para los destinos de redes sociales y no se puede eliminar.
   > * Para [!DNL Facebook] destinos. **[!UICONTROL La ID]** de cuenta es su [!DNL Facebook Ad Account ID]. Puede encontrar este ID en la página [!DNL Facebook Ads Manager]. Póngale el prefijo ID con `act_` como se muestra a continuación:


   ![Conectar con destino de red social: paso de configuración](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos en redes](#activate-segments)sociales, para el resto del flujo de trabajo.

## Activar segmentos en redes sociales {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en redes sociales, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).