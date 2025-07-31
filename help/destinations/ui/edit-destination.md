---
title: Editar destinos
type: Tutorial
description: Obtenga información sobre cómo editar y actualizar cuentas de destinos existentes en la IU de Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
exl-id: f3298836-668b-43fb-b4f3-85a650766f05
source-git-commit: 990fe9162c5b2970f269a5b0668916b7b6e61f44
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Editar destinos

Obtenga información sobre cómo editar varios componentes de una conexión de destino existente, incluido cómo actualizar las credenciales de autenticación, la ubicación de exportación y mucho más mediante la interfaz de usuario de Experience Platform.

>[!IMPORTANT]
>
>Esta funcionalidad está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con su representante de Adobe.

>[!NOTE]
>
> Las operaciones de edición descritas en este tutorial también se admiten mediante operaciones de API. Lea el tutorial sobre cómo [editar destinos en la API](/help/destinations/api/edit-destination.md) para obtener más información.

Para editar varios componentes de una conexión de destino existente:

1. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]**.
2. Seleccione el destino que desee editar.
3. Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Nombre] y use el control ![Editar control de destino](/help/images/icons/edit.png)**[!UICONTROL Editar destino &#x200B;]**&#x200B;para editar las conexiones de destino existentes.
4. En la ventana modal, edite la configuración que desee. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

En la ventana de edición de destino, puede actualizar cualquier configuración que haya configurado al conectarse inicialmente al destino. Esta configuración es diferente en función de la plataforma de destino que esté actualizando.

Según la configuración del destino, algunos campos podrían ser de solo lectura y no se pueden editar. Para cambiar el valor de los campos de solo lectura, debe [crear una nueva conexión de destino](../ui/connect-destination.md) con los nuevos valores de campo.

![Captura de pantalla que muestra un campo de solo lectura.](../assets/ui/edit-destinations/read-only.png)

A continuación se muestran algunos ejemplos de la configuración que puede actualizar para los destinos [Amazon S3](../catalog/cloud-storage/amazon-s3.md), [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md) y [Google Ads](../catalog/advertising/google-ads-destination.md).

<div style="display: flex; gap: 12px; justify-content: flex-start; align-items: flex-start;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-amazon-s3-connection.png" alt="Pantalla Editar destino para el destino de Amazon S3." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-eventhubs-connection.png" alt="Pantalla Editar destino para el destino de Azure EventHubs." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-google-ads-connection.png" alt="Pantalla Editar destino para el destino de Google Ads." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
</div>

>[!SUCCESS]
>
>Se ha actualizado la configuración de la conexión de destino.

## Otras opciones de edición

Mediante la interfaz de usuario de Experience Platform o la API de Flow Service, puede editar varias configuraciones de destino como se detalla en los vínculos siguientes:

| Uso de la IU de Experience Platform | Uso de la API de Flow Service |
|---------|----------|
| Editar conexiones de destino (esta página) | [Editar componentes de conexión de destino (ubicación de almacenamiento y otros componentes)](/help/destinations/api/edit-destination.md#patch-target-connection) |
| [Editar cuentas](/help/destinations/ui/update-accounts.md) | [Editar componentes de conexión base (parámetros de autenticación y otros componentes)](/help/destinations/api/edit-destination.md#patch-base-connection) |
| [Editar flujos de datos de activación](/help/destinations/ui/edit-activation.md) | [Actualizar flujos de datos de destino](/help/destinations/api/update-destination-dataflows.md) |

## Próximos pasos

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo **[!UICONTROL destinos]** para actualizar las conexiones de destino existentes.

Para obtener más información sobre los destinos, consulte la [descripción general de los destinos](../catalog/overview.md).
