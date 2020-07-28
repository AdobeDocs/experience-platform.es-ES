---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
seo-description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---


# Adobe Campaign

## Información general

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión. Consulte [Acerca de Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obtener más información.

Para enviar datos de segmentos a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en Adobe Real-time Customer Data Platform y, a continuación, [configurar una importación](#import-data-into-campaign) de datos desde la ubicación de almacenamiento en Adobe Campaign.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione Adobe Campaign y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

   ![Conectar con la campaña de adobe](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. En el flujo de trabajo de destino de Connect, seleccione el tipo **[!UICONTROL de]** conexión para la ubicación del almacenamiento. Para Adobe Campaign, puede seleccionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP con contraseña]** y **[!UICONTROL SFTP con clave]** SSH. Rellene la información siguiente, según el tipo de conexión y, a continuación, seleccione **[!UICONTROL Connect]**.

   ![Configuración del asistente para Campañas](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Para las conexiones **[!UICONTROL Amazon S3]** , debe proporcionar el ID de la clave de acceso y la clave de acceso secreto.
Para **[!UICONTROL SFTP con conexiones de contraseña]** , debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **[!UICONTROL SFTP con conexiones SSH Key]** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Campaña](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. En Información **** básica, rellene la información relevante para su destino, como se muestra a continuación:
   * **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
   * **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
   * **[!UICONTROL Nombre]** del contenedor: *Para conexiones* S3. Introduzca la ubicación del bucket S3 donde CDP en tiempo real depositará los datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL Ruta]** de carpeta: Proporcione la ruta en la ubicación del almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL Formato]** de archivo: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.

   ![Información básica de Campaña](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Haga clic en **[!UICONTROL Crear]** después de rellenar los campos anteriores. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Adobe Campaign, le recomendamos que seleccione un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se utilizarán como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de marketing por correo electrónico.


## Configurar la importación de datos en Adobe Campaign {#import-data-into-campaign}

Después de conectar CDP en tiempo real con su almacenamiento [!DNL Amazon S3] o SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento en Adobe Campaign. Para obtener información sobre cómo realizar esto, consulte [Importación de datos](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) en la documentación de la Ayuda de Adobe Campaign.