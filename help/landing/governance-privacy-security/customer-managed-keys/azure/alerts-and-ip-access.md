---
title: Configuración de alertas y lista de permitidos IP para Azure CMK
description: Obtenga información sobre cómo almacenar en lista de permitidos la dirección IP estática de Adobe en Azure Key Vault y comprenda cómo las alertas de Experience Platform ayudan a detectar y resolver los problemas de acceso a claves administradas por el cliente.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# Configurar alertas y lista de permitidos IP para [!DNL Azure] CMK

Para mejorar la transparencia, Adobe proporciona un [servicio de supervisión](../../../../observability/alerts/ui.md){target="_blank"} que comprueba el estado de acceso de su almacén de claves y avisa de déclencheur en caso de que se produzcan problemas. Estas alertas le ayudan a responder rápidamente y evitar interrupciones en el servicio. Para habilitar este servicio, lista de permitidos la dirección IP estática de Adobe.

>[!IMPORTANT]
>
>Si deshabilitó el acceso a la red pública o configuró el Almacén de claves de [!DNL Azure] para permitir solo las redes seleccionadas, debe agregar la dirección IP estática de Adobe a la lista de permitidos. Sin ella, es posible que no se le notifiquen los problemas de acceso que podrían afectar a su instancia de Experience Platform.

## Lista de permitidos de la IP estática de Adobe en [!DNL Azure] Key Vault {#add-adobe-static-ip}

Para habilitar estas alertas mientras se mantienen las restricciones de red, vaya a su **[!DNL Azure Key Vault]** > **[!DNL Networking settings]**. En la pestaña **[!DNL Firewalls and virtual networks]**, seleccione **[!DNL Allow public access from specific virtual networks and IP addresses]**.

![[!DNL Azure]: pantalla de configuración de red de almacén de claves que muestra dónde agregar la dirección IP estática de Adobe y con la opción Permitir acceso desde resaltada.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Dirección IP estática de Adobe

>[!IMPORTANT]
>
>La dirección IP estática proporcionada por Adobe es: `20.88.123.53`.

A continuación, en la sección **[!DNL Firewall]**, seleccione **[!DNL Add your current IP address]** y sustitúyalo por la dirección IP estática de Adobe. Todas las conexiones salientes se tratan como entornos de producción, por lo que esta dirección IP estática debe estar incluida en la lista de permitidos para garantizar el acceso ininterrumpido al almacén de claves en configuraciones de red restringidas.

>[!NOTE]
>
>Después de agregar o actualizar la dirección IP estática en la configuración de [!DNL Azure] Key Vault, espere hasta 10 minutos para que el cambio surta efecto. Una vez añadida la IP, la aplicación CMK accede al almacén de claves para verificar los permisos.

Después de la inclusión en la lista de permitidos de la IP estática de Adobe, Experience Platform puede monitorizar el acceso a su almacén de claves y las alertas de déclencheur si surgen problemas. Estas alertas proporcionan advertencias tempranas para que pueda actuar antes de que el servicio se vea afectado. La siguiente sección detalla los tipos de alertas que puede recibir y cómo responder.

## Monitorización de alertas {#monitor-alerts}

Las alertas de plataforma le notifican de problemas que pueden interrumpir el acceso a claves, como **[!UICONTROL error de acceso a claves]** o **[!UICONTROL deshabilitación de claves]**. Estas alertas le ayudan a identificar rápidamente problemas como una IP estática eliminada o un cortafuegos mal configurado. Para restaurar el acceso, revise la configuración del firewall de [!DNL Azure] y vuelva a agregar la dirección IP requerida.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Suscríbase a las notificaciones de eventos de Adobe I/O para recibir alertas en tiempo real en sus herramientas de monitorización. Para obtener instrucciones de configuración, consulte [Suscribirse a las notificaciones de eventos de Adobe I/O](../../../../observability/alerts/subscribe.md). También puede consultar la [guía de la interfaz de usuario de alertas](../../../../observability/alerts/ui.md) para obtener información sobre cómo ver y administrar alertas en Experience Platform.

## Pasos siguientes

Ya ha configurado la inclusión en la lista de permitidos IP y la supervisión de alertas para su almacén de claves [!DNL Azure]. Para completar la instalación de las claves administradas por el cliente en [!DNL Azure], siga estas guías de configuración.

- [Configurar un [!DNL Azure] depósito de claves](./azure-key-vault-config.md)
- [Use la API para configurar CMK](./api-set-up.md)
- [Uso de la interfaz de usuario para configurar CMK](./ui-set-up.md)
