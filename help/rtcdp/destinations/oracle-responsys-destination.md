---
title: Destino de Oracle Responsys
seo-title: Destino de Oracle Responsys
description: Responsys es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.
seo-description: Responsys es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Oracle Responsys

## Información general

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) es una herramienta de marketing de correo electrónico empresarial para campañas de marketing entre canales ofrecidas por Oracle con el fin de personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.

Para enviar datos de segmentos a Oracle Responsys, primero debe [conectarse al destino](#connect-destination) en la plataforma de datos del cliente en tiempo real de Adobe y, a continuación, [configurar una importación](#import-data-into-responsys) de datos desde la ubicación del almacenamiento en Oracle Responsys.

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione Oracle Responsys y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar a Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. En el **[!UICONTROL Authentication]** paso, si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione **[!UICONTROL Existing Account]** y seleccione una de las conexiones existentes. O bien, puede seleccionar **[!UICONTROL New Account]** configurar una nueva conexión. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Connect to destination]**. Para Oracle Responsys, puede seleccionar entre **[!UICONTROL SFTP with Password]** y **[!UICONTROL SFTP with SSH Key]**. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect to destination]**.

   Para **[!UICONTROL SFTP with Password]** las conexiones, debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **[!UICONTROL SFTP with SSH Key]** las conexiones, debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. En el **[!UICONTROL Setup]** paso, rellene la información relevante para su destino como se muestra a continuación:
   * **[!UICONTROL Name]**:: Elija un nombre relevante para el destino.
   * **[!UICONTROL Description]**:: Escriba una descripción para el destino.
   * **[!UICONTROL Folder Path]**:: Proporcione la ruta en la ubicación del almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL File Format]**:: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.
   ![Información básica de Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Haga clic **[!UICONTROL Create destination]** después de rellenar los campos anteriores. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino de Oracle Responsys, le recomendamos que seleccione un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se van a utilizar como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de mercadotecnia de correo electrónico.

## Configurar la importación de datos en Oracle Responsys {#import-data-into-responsys}

Después de conectar CDP en tiempo real con su almacenamiento Amazon S3 o SFTP, debe configurar la importación de datos desde la ubicación de almacenamiento en Oracle Responsys. Para obtener más información sobre cómo realizar esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en el Centro de ayuda de Oracle Responsys.