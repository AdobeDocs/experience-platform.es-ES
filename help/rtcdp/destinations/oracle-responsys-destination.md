---
title: Destino de Oracle Responsys
seo-title: Destino de Oracle Responsys
description: Responsys es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.
seo-description: Responsys es una herramienta de mercadotecnia de correo electrónico empresarial para campañas de mercadotecnia entre canales ofrecidas por Oracle para personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## Información general

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) es una herramienta empresarial de marketing por correo electrónico para campañas de marketing entre canales ofrecida por [!DNL Oracle] para personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.

Para enviar datos de segmentos a [!DNL Oracle Responsys], primero debe [conectarse al destino](#connect-destination) en Platform de datos de clientes en tiempo real de Adobe y, a continuación, [configurar una importación](#import-data-into-responsys) de datos desde la ubicación del almacenamiento en [!DNL Oracle Responsys].

## Destino de Connect {#connect-destination}

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione [!DNL Oracle Responsys]y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

   ![Conectar a Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. En el paso **[!UICONTROL Autenticación]** , si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione Cuenta **** existente y seleccione una de las conexiones existentes. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**. Por [!DNL Oracle Responsys], puede seleccionar entre **[!UICONTROL SFTP con contraseña]** y **[!UICONTROL SFTP con clave]** SSH. Rellene la información siguiente, según el tipo de conexión, y seleccione **[!UICONTROL Conectar con destino]**.

   Para **[!UICONTROL SFTP con conexiones de contraseña]** , debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.
Para **[!UICONTROL SFTP con conexiones SSH Key]** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

   ![Rellenar información de Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. En el paso **[!UICONTROL Configuración]** , rellene la información relevante para su destino como se muestra a continuación:
   * **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
   * **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
   * **[!UICONTROL Ruta]** de carpeta: Proporcione la ruta en la ubicación del almacenamiento donde CDP en tiempo real depositará sus datos de exportación como archivos CSV o separados por tabuladores.
   * **[!UICONTROL Formato]** de archivo: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.

   ![Información básica de Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Haga clic en **[!UICONTROL Crear destino]** después de rellenar los campos anteriores. El destino ya está conectado y puede [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el destino.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](/help/rtcdp/destinations/activate-destinations.md) en el [!DNL Oracle Responsys] destino, le recomendamos que seleccione un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Selección de los campos de esquema que se utilizarán como atributos de destino en los archivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados en Destinos de marketing por correo electrónico.

## Configurar la importación de datos en [!DNL Oracle Responsys] {#import-data-into-responsys}

Después de conectar CDP en tiempo real con su almacenamiento Amazon S3 o SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento en [!DNL Oracle Responsys]. Para obtener información sobre cómo realizar esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en la [!DNL Oracle Responsys Help Center].