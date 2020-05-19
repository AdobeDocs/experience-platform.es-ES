---
title: Flujo de trabajo de destinos de redes sociales
seo-title: Flujo de trabajo de destinos de redes sociales
description: Instrucciones para conectarse a las cuentas de publicidad de la red social
seo-description: Instrucciones para conectarse a las cuentas de publicidad de la red social
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Flujo de trabajo de autenticación de destinos de red social {#social-network-destinations-workflow}

## Flujo de trabajo para crear destinos de redes sociales

Este tutorial utiliza Facebook como ejemplo, pero el flujo de trabajo de la plataforma de datos del cliente en tiempo real de Adobe será el mismo para todos los destinos de redes sociales, una vez que se añadan más al producto.

1. En **[!UICONTROL Destinos > Catálogo]**, desplácese hasta la categoría de **[!UICONTROL Social]** . Seleccione el destino preferido de la red social y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

   ![Conectar al destino de red social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. En el paso **Autenticación** , si previamente ha configurado una conexión con el destino de red social, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de red social. Seleccione **[!UICONTROL Conectar a destino]** y esto le llevará al destino de red social seleccionado para iniciar sesión y conectar Adobe Experience Cloud a su cuenta de publicidad de red social.

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en el ID de cuenta de la red social. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de red social: paso de autenticación](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Una vez confirmadas las credenciales y Adobe Experience Cloud conectado a la red social, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso **[!UICONTROL Configuración]** .

   ![Credenciales confirmadas](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. En el paso **[!UICONTROL Configuración]** , escriba un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación y rellene el ID **[!UICONTROL de]** cuenta de su cuenta de publicidad de red social. Seleccione cualquier caso de uso de mercadotecnia que deba aplicarse a este destino. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   >[!IMPORTANT]
   >
   > Para destinos de Facebook. **[!UICONTROL El ID]** de cuenta es el ID de su cuenta de publicidad de Facebook. Puede encontrar este ID en el Administrador de publicidades de Facebook. Póngale el prefijo ID con `act_` como se muestra a continuación:

   ![Conectar con destino de red social: paso de configuración](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos en redes](#activate-segments)sociales, para el resto del flujo de trabajo.

## Activar segmentos en redes sociales {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en redes sociales, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)