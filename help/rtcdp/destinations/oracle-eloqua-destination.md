---
title: Destino de Oracle Eloqua
seo-title: Destino de Oracle Eloqua
description: Oracle Eloqua es una plataforma de software como servicio (SaaS) para la automatización de mercadotecnia ofrecida por Oracle que tiene como objetivo ayudar a los especialistas en mercadotecnia y a las organizaciones B2B a administrar las campañas de mercadotecnia y la generación de posibles clientes de ventas.
seo-description: Oracle Eloqua es una plataforma de software como servicio (SaaS) para la automatización de mercadotecnia ofrecida por Oracle que tiene como objetivo ayudar a los especialistas en mercadotecnia y a las organizaciones B2B a administrar las campañas de mercadotecnia y la generación de posibles clientes de ventas.
translation-type: tm+mt
source-git-commit: fe56fe71c36e06f2eeed45436cb36b5a371d0484

---


# Oracle Eloqua

## Información general

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) es una plataforma de software como servicio (SaaS) para la automatización de mercadotecnia ofrecida por Oracle que tiene como objetivo ayudar a los especialistas en mercadotecnia y las organizaciones B2B a administrar las campañas de mercadotecnia y la generación de posibles clientes de ventas.

Para enviar datos de segmentos a Oracle Eloqua, primero debe [conectar el destino](#connect-destination) en la plataforma de datos del cliente en tiempo real de Adobe y, a continuación, [configurar una importación](#import-data-into-eloqua) de datos desde la ubicación del almacenamiento en Oracle Eloqua.

## Conectar al destino {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione Oracle Eloqua y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar a Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. En el paso **Autenticación** , si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione **[!UICONTROL Existing Account]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** configurar una nueva conexión. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Connect to destination]**. Para Oracle Eloqua, puede seleccionar entre **SFTP con contraseña** y **SFTP con clave** SSH. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect to destination]**.

   Para **SFTP con conexiones de contraseña** , debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **SFTP con conexiones SSH Key** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Configurar el asistente para Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. En el paso **Configuración** , rellene la información relevante para su destino como se muestra a continuación:
   * **Nombre**: Elija un nombre relevante para el destino.
   * **Descripción**: Escriba una descripción para el destino.
   * **Ruta** de carpeta: Proporcione la ruta en la ubicación del almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **Formato** de archivo: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.
   ![Información básica de Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Haga clic en **Crear destino** después de rellenar los campos anteriores. El destino se ha creado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Oracle Eloqua, se recomienda seleccionar un identificador único en el esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se van a utilizar como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de mercadotecnia de correo electrónico.

## Configurar la importación de datos en Oracle Eloqua {#import-data-into-eloqua}

Después de conectar CDP en tiempo real con su almacenamiento Amazon S3 o SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento en Oracle Eloqua. Para obtener más información sobre cómo realizar esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) en el Centro de Ayuda de Oracle Eloqua.