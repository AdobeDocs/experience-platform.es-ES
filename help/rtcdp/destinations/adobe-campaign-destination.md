---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
seo-description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 1%

---


# Adobe Campaign

## Información general

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión. Consulte [Acerca de Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obtener más información.

Para enviar datos de segmentos a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en la plataforma de datos del cliente en tiempo real y, a continuación, [configurar una importación](#import-data-into-campaign) de datos desde la ubicación del almacenamiento en Adobe Campaign.

## Tipo de exportación {#export-type}

**Basado** en perfiles: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [de activación de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destino.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione Adobe Campaign y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

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

   ![Información básica de campaña](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Haga clic en **[!UICONTROL Crear]** después de rellenar los campos anteriores. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Adobe Campaign, le recomendamos que seleccione un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se utilizarán como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados de la documentación de destinos de marketing por correo electrónico.

## Datos exportados {#exported-data}

Para [!DNL Adobe Campaign] los destinos, Adobe Real-time CDP crea un archivo delimitado por tabuladores `.txt` o `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte Destinos de [correo electrónico de Marketing y Destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de almacenamiento de Cloud en el tutorial de activación de segmentos.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Configurar la importación de datos en Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tenga en cuenta los límites de almacenamiento SFTP, los límites de almacenamiento de la base de datos y los límites de perfil activos según su contrato de Adobe Campaign mientras realiza esta integración.
>* Debe programar, importar y asignar los segmentos exportados en Adobe Campaign mediante [!DNL Campaign] flujos de trabajo. Consulte [Configuración de una importación](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#setting-up-a-recurring-import) recurrente en la documentación de Adobe Campaign.



Después de conectar CDP en tiempo real con su almacenamiento [!DNL Amazon S3] o SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento a Adobe Campaign. Para obtener información sobre cómo realizar esto, consulte [Importación de datos](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) en la documentación de Adobe Campaign.