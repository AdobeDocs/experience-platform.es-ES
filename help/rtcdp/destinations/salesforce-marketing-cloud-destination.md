---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud es una suite de marketing digital anteriormente conocida como ExactTarget que le permite crear y personalizar viajes para que los visitantes y clientes puedan personalizar su experiencia.
seo-description: Salesforce Marketing Cloud es una suite de marketing digital anteriormente conocida como ExactTarget que le permite crear y personalizar viajes para que los visitantes y clientes puedan personalizar su experiencia.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Salesforce Marketing Cloud

## Información general

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) es una suite de marketing digital anteriormente conocida como ExactTarget que le permite crear y personalizar viajes para que los visitantes y clientes puedan personalizar su experiencia.

Para enviar datos de segmentos a Salesforce Marketing Cloud, primero debe [conectar el destino](#connect-destination) en Adobe Real-time CDP y, a continuación, [configurar una importación](#import-data-into-salesforce) de datos desde la ubicación de almacenamiento en Salesforce Marketing Cloud.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione Salesforce Marketing Cloud y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar a Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. En el **[!UICONTROL Authentication]** paso, si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione **[!UICONTROL Existing Account]** y seleccione una de las conexiones existentes. O bien, puede seleccionar **[!UICONTROL New Account]** configurar una nueva conexión. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Connect to destination]**. En Salesforce Marketing Cloud, puede seleccionar entre **[!UICONTROL SFTP with Password]** y **[!UICONTROL SFTP with SSH Key]**. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect to destination]**.

   Para **[!UICONTROL SFTP with Password]** las conexiones, debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **[!UICONTROL SFTP with SSH Key]** las conexiones, debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. En el **[!UICONTROL Setup]** paso, rellene la información relevante para su destino como se muestra a continuación:
   * **[!UICONTROL Name]**:: Elija un nombre relevante para el destino.
   * **[!UICONTROL Description]**:: Escriba una descripción para el destino.
   * **[!UICONTROL Folder Path]**:: Proporcione la ruta en la ubicación del almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL File Format]**:: **[!UICONTROL CSV]** o **[!UICONTROL TAB_DELIMITED]**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.
   ![Información básica de Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Haga clic **[!UICONTROL Create destination]** después de rellenar los campos anteriores. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Salesforce Marketing Cloud, se recomienda seleccionar un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se van a utilizar como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de mercadotecnia de correo electrónico.

## Configurar la importación de datos en Salesforce Marketing Cloud {#import-data-into-salesforce}

Después de conectar CDP en tiempo real con su almacenamiento Amazon S3 o SFTP, debe configurar la importación de datos desde la ubicación de almacenamiento en Salesforce Marketing Cloud. Para obtener información sobre cómo realizar esto, consulte [Importación de suscriptores a Marketing Cloud desde un archivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) en el Centro de ayuda de Salesforce.