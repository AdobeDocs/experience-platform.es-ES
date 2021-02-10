---
keywords: correo electrónico;correo electrónico;correo electrónico;destinos de correo electrónico;campaña de adobe;campaña
title: Conexión Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---


# Conexión Adobe Campaign

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y ofrecer campañas en todos sus canales en línea y sin conexión. Consulte [Acerca de Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obtener más información.

Para enviar datos de segmentos a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en Adobe Experience Platform y luego [configurar una importación de datos](#import-data-into-campaign) desde la ubicación del almacenamiento en Adobe Campaign.

## Tipo de exportación {#export-type}

**Basado**  en perfiles: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [ de activación de ](../../ui/activate-destinations.md#select-attributes)destino.

## Destino de Connect {#connect-destination}

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione Adobe Campaign y, a continuación, seleccione **[!UICONTROL Destino de Connect]**.

![Conectar con la campaña de adobe](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

En el flujo de trabajo de destino de Connect, seleccione el **[!UICONTROL tipo de conexión]** para la ubicación del almacenamiento. Para Adobe Campaign, puede seleccionar **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP con contraseña]**, **[!UICONTROL SFTP con clave SSH]** y **[!UICONTROL Azure Blob]**. Rellene la información siguiente, según el tipo de conexión, luego seleccione **[!UICONTROL Conectar]**.

![Configuración del asistente para Campañas](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Para las conexiones **[!UICONTROL Amazon S3]**, debe proporcionar el ID de clave de acceso y la clave de acceso secreto.
- Para conexiones **[!UICONTROL SFTP con contraseña]**, debe proporcionar dominio, puerto, nombre de usuario y contraseña.
- Para conexiones **[!UICONTROL SFTP con clave SSH]**, debe proporcionar dominio, puerto, nombre de usuario y clave SSH.
- Para las conexiones **[!UICONTROL Blob de Azure]**, debe proporcionar una cadena de conexión.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado con PGP/GPG a sus archivos exportados en la sección **[!UICONTROL Clave]**. Tenga en cuenta que esta clave pública **debe** escribirse como una cadena con codificación Base64.

![Rellenar información de Campaña](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

En **[!UICONTROL Información básica]**, rellene la información relevante para su destino, como se muestra a continuación:
- **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
- **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
- **[!UICONTROL Nombre]** del contenedor:  *Para conexiones* S3. Introduzca la ubicación del bucket S3 donde Platform depositará los datos de exportación como archivos CSV o delimitados por tabuladores.
- **[!UICONTROL Ruta]** de carpeta: Proporcione la ruta en la ubicación del almacenamiento donde Platform depositará los datos de exportación como archivos CSV o separados por tabuladores.
- **[!UICONTROL Contenedor]**:  *Para conexiones* Blob. El contenedor que contiene el Blob en el que se encuentra la ruta de la carpeta.
- **[!UICONTROL Formato]** de archivo:  **** CSVo  **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.

![Información básica de campaña](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Haga clic en **[!UICONTROL Crear]** después de completar los campos anteriores. El destino está ahora conectado y puede [activar segmentos](../../ui/activate-destinations.md) en el destino.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](../../ui/activate-destinations.md) en el destino de Adobe Campaign, le recomendamos que seleccione un identificador único en su esquema [de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Seleccionar los campos de esquema que se usarán como atributos de destino en los archivos exportados](./overview.md#destination-attributes) en la documentación de destinos de mercadotecnia de correo electrónico.

## Datos exportados {#exported-data}

Para los destinos [!DNL Adobe Campaign], Platform crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de Marketing por correo electrónico y destinos de almacenamiento de Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.

## Configurar la importación de datos en Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Tenga en cuenta los límites de almacenamiento SFTP, los límites de almacenamiento de la base de datos y los límites de perfil activos según su contrato de Adobe Campaign mientras realiza esta integración.
>- Debe programar, importar y asignar los segmentos exportados en Adobe Campaign mediante flujos de trabajo [!DNL Campaign]. Consulte [Configuración de una importación recurrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) en la documentación de Adobe Campaign.



Después de conectar Platform con su [!DNL Amazon S3] o almacenamiento SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento en Adobe Campaign. Para obtener más información sobre cómo hacerlo, consulte [Importación de datos](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) en la documentación de Adobe Campaign.