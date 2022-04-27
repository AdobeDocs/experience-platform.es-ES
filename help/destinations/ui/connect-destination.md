---
keywords: conectar destino;conexión de destino;cómo conectar destino
title: Crear una nueva conexión de destino
type: Tutorial
description: Este tutorial enumera los pasos para conectarse a un destino en Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: b275621d9c6552327e0e55c00c8fcf0397088168
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Crear una nueva conexión de destino

## Información general {#overview}

Para poder enviar datos de audiencia a un destino, debe configurar una conexión con la plataforma de destino. Este artículo muestra cómo configurar un nuevo destino mediante la interfaz de usuario de Adobe Experience Platform.

## Crear una nueva conexión de destino {#setup}

1. Vaya a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione **[!UICONTROL Catálogo]** pestaña .

   ![Página Catálogo](../assets/ui/connect-destinations/catalog.png)

1. En función de si tiene una conexión existente con el destino, puede ver una **[!UICONTROL Configuración]** o **[!UICONTROL Activar segmentos]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar segmentos]** y **[!UICONTROL Configuración]**, consulte [Catálogo](../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

   Seleccione: **[!UICONTROL Configuración]** o **[!UICONTROL Activar segmentos]**, según el botón que esté disponible.

   ![Página Catálogo](../assets/ui/connect-destinations/set-up.png)

   ![Activar segmentos](../assets/ui/connect-destinations/activate-segments.png)

1. Si ha seleccionado **[!UICONTROL Configuración]**, vaya al paso siguiente.

   Si ha seleccionado **[!UICONTROL Activar segmentos]**, ahora puede ver una lista de conexiones de destino existentes.

   Select **[!UICONTROL Configurar nuevo destino]**.

   ![Configurar nuevo destino](../assets/ui/connect-destinations/configure-new-destination.png)

1. Introduzca los detalles de conexión de la plataforma de destino y, a continuación, seleccione **[!UICONTROL Conectarse al destino]**.

   >[!NOTE]
   >
   >La siguiente imagen se utiliza solo con fines ilustrativos. Los detalles de la conexión de destino varían según el destino. Para obtener información detallada sobre los detalles de conexión de su destino, consulte la **Parámetros de conexión** en cada [catálogo de destino](../catalog/overview.md) (por ejemplo, [Coincidencia de clientes de Google](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Conectarse al destino](../assets/ui/connect-destinations/connect-destination.png)

1. (Opcional) Seleccione las alertas de flujo de datos de destino a las que desee suscribirse. Puede suscribirse a las alertas al crear un flujo de datos para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo. Consulte [Suscripción a alertas de destino en contexto](alerts.md) para obtener información detallada sobre las alertas de flujo de datos de destino.

   ![Imagen de interfaz de usuario que muestra las opciones de suscripción de alertas de destino en contexto](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. Seleccione **[!UICONTROL Siguiente]**.

   ![Conectarse al destino](../assets/ui/connect-destinations/next.png)

1. Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la [información general sobre las políticas de uso de datos](../../data-governance/policies/overview.md) página.

   ![Seleccionar acciones de marketing](../assets/ui/connect-destinations/governance.png)

1. Select **[!UICONTROL Guardar y salir]** para guardar la configuración de destino o seleccione **[!UICONTROL Siguiente]** para continuar con los datos de audiencia [flujo de activación](activation-overview.md).