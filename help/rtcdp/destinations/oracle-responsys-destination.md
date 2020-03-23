---
title: Destino de Oracle Responsys
seo-title: Destino de Oracle Responsys
description: Responsys es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, pantallas y medios sociales.
seo-description: Responsys es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, pantallas y medios sociales.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## Información general

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.

Para enviar datos de segmentos a Oracle Responsys, primero debe [conectar el destino](#connect-destination) en la plataforma de datos del cliente en tiempo real de Adobe y, a continuación, [configurar una importación](#import-data-into-responsys) de datos desde su ubicación de almacenamiento en Oracle Responsys.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione Oracle Responsys y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar a Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. En el asistente de destino de Connect, seleccione la ubicación **[!UICONTROL Connection type]** de almacenamiento. Para Oracle Responsys, puede seleccionar entre **SFTP con contraseña** y **SFTP con clave** SSH. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect]**.

   ![Configurar el asistente de Responsys](/help/rtcdp/destinations/assets/responsys-wizard.png)

   Para **SFTP con conexiones de contraseña** , debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **SFTP con conexiones SSH Key** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Responsys](/help/rtcdp/destinations/assets/responsys-step2.png)

1. En Información **** básica, rellene la información relevante para su destino, como se muestra a continuación:
   * **Nombre**: Elija un nombre relevante para el destino.
   * **Descripción**: Escriba una descripción para el destino.
   * **Ruta** de carpeta: Proporcione la ruta en su ubicación de almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **Formato** de archivo: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.
   ![Información básica de Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. Haga clic en **Crear** después de rellenar los campos en Información **** básica. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Oracle Responsys, le recomendamos que seleccione un identificador único del esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se utilizarán como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de marketing por correo electrónico.

## Configurar la importación de datos en Oracle Responsys {#import-data-into-responsys}

Después de conectar CDP en tiempo real con su almacenamiento de Amazon S3 o SFTP, debe configurar la importación de datos desde su ubicación de almacenamiento de información en Oracle Responsys. Para obtener más información sobre cómo realizar esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en el Centro de ayuda de Oracle Responsys.