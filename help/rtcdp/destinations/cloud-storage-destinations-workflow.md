---
title: Flujo de trabajo de destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de destinos de almacenamiento en la nube
description: Instrucciones para conectarse a las ubicaciones de almacenamiento en la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento en la nube
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

Esta página explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en la plataforma de datos del cliente en tiempo real de Adobe.

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione el destino de almacenamiento en la nube preferido y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

   ![Conectar con destino de almacenamiento en la nube](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. En el paso **Autenticación** , si ya ha configurado una conexión con el destino de almacenamiento en la nube, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de almacenamiento en la nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**.

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la ubicación de almacenamiento en la nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. En el paso **[!UICONTROL Configuración]** , escriba un **[!UICONTROL Nombre]** y un **[!UICONTROL Destino]** para el flujo de activación e inserte la ruta **[!UICONTROL de]** carpeta en el destino de almacenamiento en la nube donde se entregarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo,

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.