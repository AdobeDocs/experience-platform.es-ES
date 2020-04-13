---
title: Flujo de trabajo de destinos de redes sociales
seo-title: Flujo de trabajo de destinos de redes sociales
description: Instrucciones para conectarse a las cuentas de publicidad de la red social
seo-description: Instrucciones para conectarse a las cuentas de publicidad de la red social
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Flujo de trabajo de autenticación de destinos de red social {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>El flujo de trabajo para crear destinos de redes sociales en Adobe Real-time CDP está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Flujo de trabajo para crear destinos de almacenamiento en la nube

Este tutorial utiliza Facebook como ejemplo, pero el flujo de trabajo en la plataforma de datos del cliente en tiempo real de Adobe será el mismo para todos los destinos de la red social, una vez que se agreguen más al producto.

1. En **[!UICONTROL Connections > Destinations]**, desplácese hasta la **[!UICONTROL Social]** categoría. Seleccione el destino preferido de la red social y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar al destino de red social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. En el paso **Autenticación** , si previamente ha configurado una conexión con el destino de red social, seleccione **[!UICONTROL Existing Account]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** configurar una nueva conexión con su destino de red social. Seleccione **[!UICONTROL Connect to destination]** y esto le llevará al destino de red social seleccionado para iniciar sesión y conectar Adobe Experience Cloud a su cuenta de publicidad de red social.

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en el ID de cuenta de la red social. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de red social: paso de autenticación](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Una vez confirmadas las credenciales y Adobe Experience Cloud conectado a la red social, puede seleccionar **[!UICONTROL Next]** continuar con el **[!UICONTROL Setup]** paso.

   ![Credenciales confirmadas](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. En el **[!UICONTROL Setup]** paso, escriba un **[!UICONTROL Name]** y un **[!UICONTROL Description]** para el flujo de activación y rellene el contenido **[!UICONTROL Account ID]** de la cuenta de publicidad de red social. Seleccione **[!UICONTROL Create Destination]** una vez rellenados los campos anteriores.

   >[!IMPORTANT]
   >
   >Para destinos de Facebook. **[!UICONTROL Account ID]** es su ID de cuenta de publicidad de Facebook. Puede encontrar este ID en el Administrador de publicidades de Facebook. Póngale el prefijo ID con `act_` como se muestra a continuación:

   ![Conectar con destino de red social: paso de configuración](/help/rtcdp/destinations/assets/social-network-step.png)

5. Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos en redes](#activate-segments)sociales, para el resto del flujo de trabajo.

## Activar segmentos en redes sociales {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en redes sociales, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).