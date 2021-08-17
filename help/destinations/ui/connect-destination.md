---
keywords: conectar destino;conexión de destino;cómo conectar destino
title: Crear una nueva conexión de destino
type: Tutorial
description: Este tutorial enumera los pasos para conectarse a un destino en Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 1c67d9eb1b7762ecfcad5b0b7db5c317621f144e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Crear una nueva conexión de destino

## Información general {#overview}

Para poder enviar datos de audiencia a un destino, debe configurar una conexión con la plataforma de destino. Este artículo muestra cómo configurar un nuevo destino mediante la interfaz de usuario de Adobe Experience Platform.

## Crear una nueva conexión de destino {#setup}

### Seleccionar destino {#select-destination}

1. Vaya a **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** y seleccione la pestaña **[!UICONTROL Catalog]**.

   ![Página Catálogo](../assets/ui/connect-destinations/catalog.png)

1. Según si tiene una conexión existente con el destino, puede ver un botón **[!UICONTROL Configurar]** o **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino. Seleccione **[!UICONTROL Configure]** o **[!UICONTROL Activate]**, en función de qué botón esté disponible.

   ![Página Catálogo](../assets/ui/connect-destinations/set-up.png)

   ![Activar segmentos](../assets/ui/connect-destinations/activate-segments.png)

<!-- 1. If you selected **[!UICONTROL Set up]**, skip this step. If you selected **[!UICONTROL Activate segments]**, you can now see a list of the existing destination connections. Select **[!UICONTROL Configure new destination]**.

   ![Configure new destination](../assets/ui/connect-destinations/configure-new-destination.png) -->

### Paso de la cuenta {#account}

Seleccione **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino. O bien, si anteriormente ha configurado una conexión con su destino, seleccione **[!UICONTROL Cuenta existente]** y seleccione la conexión existente.

Las credenciales que debe introducir en el paso de cuenta varían según el destino y el tipo de autenticación.

* Para los destinos de almacenamiento en la nube, debe proporcionar las credenciales para que el Experience Platform se conecte a su ubicación de almacenamiento.

   ![Seleccionar tipo de cuenta para destinos de almacenamiento en la nube](../assets/ui/connect-destinations/new-account-cloud-storage.png)

* Para Facebook y otros destinos sociales y publicitarios, seleccione **[!UICONTROL New account]** y luego seleccione **[!UICONTROL Connect to destination]**. Esto lo llevará a la página de inicio de sesión de destino, para que pueda conectar el Experience Platform al destino.

   ![Seleccionar tipo de cuenta para destinos sociales](../assets/ui/connect-destinations/new-account.png)

>[!IMPORTANT]
>
>Consulte la sección **[!UICONTROL Connection parameters]** de cada página del catálogo de destino para obtener información detallada sobre los parámetros requeridos en este paso (por ejemplo, [Azure Blob](../catalog/cloud-storage/azure-blob.md#parameters) requiere una cadena de conexión).

### Paso de autenticación {#authentication}

Introduzca los detalles de conexión de la plataforma de destino y seleccione **[!UICONTROL Crear destino]**.

1. Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [información general sobre las políticas de uso de datos](../../data-governance/policies/overview.md).

   >[!IMPORTANT]
   >
   >La siguiente imagen se utiliza solo con fines ilustrativos. Los detalles de la conexión de destino varían según el destino. Para obtener información detallada sobre los detalles de conexión para el destino, consulte la sección **[!UICONTROL Connection parameters]** en cada página [destination catalog](../catalog/overview.md) (por ejemplo, [Google Customer Match](../catalog/advertising/google-customer-match.md#parameters)).

   ![Conectarse al destino](../assets/ui/connect-destinations/connect-destination.png)

1. Seleccione **[!UICONTROL Guardar y salir]** para guardar la configuración de destino o seleccione **[!UICONTROL Siguiente]** para continuar con los datos de audiencia [flujo de activación](activate-destinations.md).