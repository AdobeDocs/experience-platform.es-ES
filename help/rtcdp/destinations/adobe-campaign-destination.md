---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
seo-description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Adobe Campaign

## Información general

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión. Consulte [Acerca de Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obtener más información.

Para enviar datos de segmentos a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en la plataforma de datos del cliente en tiempo real de Adobe y, a continuación, [configurar una importación](#import-data-into-campaign) de datos desde la ubicación del almacenamiento en Adobe Campaign.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione Adobe Campaign y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar con la campaña de adobe](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. En el flujo de trabajo de destino de Connect, seleccione el **[!UICONTROL Connection type]** para la ubicación del almacenamiento. En Adobe Campaign, puede seleccionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** y **[!UICONTROL SFTP with SSH Key]**. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect]**.

   ![Configuración del asistente para Campañas](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Para **[!UICONTROL Amazon S3]** las conexiones, debe proporcionar el ID de clave de acceso y la clave de acceso secreto.
Para **[!UICONTROL SFTP with Password]** las conexiones, debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **[!UICONTROL SFTP with SSH Key]** las conexiones, debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Campaña](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. En **[!UICONTROL Basic Information]**, rellene la información relevante para su destino, como se muestra a continuación:
   * **[!UICONTROL Name]**:: Elija un nombre relevante para el destino.
   * **[!UICONTROL Description]**:: Escriba una descripción para el destino.
   * **[!UICONTROL Bucket Name]**:: *Para conexiones* S3. Introduzca la ubicación del bucket S3 donde CDP en tiempo real depositará los datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL Folder Path]**:: Proporcione la ruta en la ubicación del almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL File Format]**:: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.
   ![Información básica de Campaña](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Haga clic **[!UICONTROL Create]** después de rellenar los campos anteriores. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Adobe Campaign, le recomendamos que seleccione un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se van a utilizar como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de mercadotecnia de correo electrónico.


## Configurar la importación de datos en Adobe Campaign {#import-data-into-campaign}

Después de conectar CDP en tiempo real con su almacenamiento Amazon S3 o SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento en Adobe Campaign. Para obtener información sobre cómo realizar esto, consulte [Importación de datos](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) en la documentación de la Ayuda de Adobe Campaign.