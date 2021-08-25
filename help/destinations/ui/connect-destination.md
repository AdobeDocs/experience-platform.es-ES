---
keywords: conectar destino;conexión de destino;cómo conectar destino
title: Crear una nueva conexión de destino
type: Tutorial
description: Este tutorial enumera los pasos para conectarse a un destino en Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Crear una nueva conexión de destino

## Información general {#overview}

Para poder enviar datos de audiencia a un destino, debe configurar una conexión con la plataforma de destino. Este artículo muestra cómo configurar un nuevo destino mediante la interfaz de usuario de Adobe Experience Platform.

## Crear una nueva conexión de destino {#setup}

1. Vaya a **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** y seleccione la pestaña **[!UICONTROL Catalog]**.

   ![Página Catálogo](../assets/ui/connect-destinations/catalog.png)

1. Según si tiene una conexión existente con el destino, puede ver un botón **[!UICONTROL Configurar]** o **[!UICONTROL Activar segmentos]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate segments]** y **[!UICONTROL Set up]**, consulte la sección [Catalog](../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

   Seleccione **[!UICONTROL Set up]** o **[!UICONTROL Activate segments]**, según el botón que tenga disponible.

   ![Página Catálogo](../assets/ui/connect-destinations/set-up.png)

   ![Activar segmentos](../assets/ui/connect-destinations/activate-segments.png)

1. Si seleccionó **[!UICONTROL Configurar]**, vaya al paso siguiente.

   Si seleccionó **[!UICONTROL Activar segmentos]**, ahora puede ver una lista de conexiones de destino existentes.

   Seleccione **[!UICONTROL Configurar nuevo destino]**.

   ![Configurar nuevo destino](../assets/ui/connect-destinations/configure-new-destination.png)

1. Introduzca los detalles de conexión de la plataforma de destino y, a continuación, seleccione **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >La siguiente imagen se utiliza solo con fines ilustrativos. Los detalles de la conexión de destino varían según el destino. Para obtener información detallada sobre los detalles de conexión para el destino, consulte la sección **Connection parameters** en cada página [destination catalog](../catalog/overview.md) (por ejemplo, [Google Customer Match](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Conectarse al destino](../assets/ui/connect-destinations/connect-destination.png)

1. Seleccione **[!UICONTROL Siguiente]**.

   ![Conectarse al destino](../assets/ui/connect-destinations/next.png)

1. Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [información general sobre las políticas de uso de datos](../../data-governance/policies/overview.md).

   ![Seleccionar acciones de marketing](../assets/ui/connect-destinations/governance.png)

1. Seleccione **[!UICONTROL Guardar y salir]** para guardar la configuración de destino o seleccione **[!UICONTROL Siguiente]** para continuar con los datos de audiencia [flujo de activación](activation-overview.md).