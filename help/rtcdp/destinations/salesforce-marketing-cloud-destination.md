---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud es una suite de marketing digital anteriormente conocida como ExactTarget que le permite crear y personalizar viajes para que los visitantes y clientes puedan personalizar su experiencia.
seo-description: Salesforce Marketing Cloud es una suite de marketing digital anteriormente conocida como ExactTarget que le permite crear y personalizar viajes para que los visitantes y clientes puedan personalizar su experiencia.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Información general

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) es una suite de marketing digital anteriormente conocida como ExactTarget que le permite crear y personalizar viajes para que los visitantes y clientes puedan personalizar su experiencia.

Para enviar datos de segmentos a Salesforce Marketing Cloud, primero debe [conectar el destino](#connect-destination) en Adobe Real-time CDP y, a continuación, [configurar una importación](#import-data-into-salesforce) de datos desde su ubicación de almacenamiento en Salesforce Marketing Cloud.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione Salesforce Marketing Cloud y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar a Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. En el asistente de destino de Connect, seleccione la ubicación **[!UICONTROL Connection type]** de almacenamiento. En Salesforce Marketing Cloud, puede seleccionar entre **SFTP con contraseña** y **SFTP con clave** SSH. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect]**.

   ![Configurar el asistente de Salesforce](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Para **SFTP con conexiones de contraseña** , debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **SFTP con conexiones SSH Key** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Salesforce](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. En Información **** básica, rellene la información relevante para su destino, como se muestra a continuación:
   * **Nombre**: Elija un nombre relevante para el destino.
   * **Descripción**: Escriba una descripción para el destino.
   * **Ruta** de carpeta: Proporcione la ruta en su ubicación de almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **Formato** de archivo: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.
   ![Información básica de Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Haga clic en **Crear** después de rellenar los campos en Información **** básica. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Salesforce Marketing Cloud, le recomendamos que seleccione un identificador único del esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se utilizarán como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de marketing por correo electrónico.

## Configurar la importación de datos en Salesforce Marketing Cloud {#import-data-into-salesforce}

Después de conectar CDP en tiempo real al almacenamiento de Amazon S3 o SFTP, debe configurar la importación de datos desde su ubicación de almacenamiento en Salesforce Marketing Cloud. Para obtener información sobre cómo realizar esto, consulte [Importación de suscriptores a Marketing Cloud desde un archivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) en el Centro de ayuda de Salesforce.