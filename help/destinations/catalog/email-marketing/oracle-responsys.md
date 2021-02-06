---
keywords: correo electrónico;correo electrónico;correo electrónico;destinos de correo electrónico;destino de responsys de oracle
title: Destino de conexión de oracle Responsys
description: Responsys es una herramienta empresarial de marketing por correo electrónico para campañas de marketing entre canales ofrecidas por Oracle con el fin de personalizar las interacciones entre correo electrónico, dispositivos móviles, visualización y redes sociales.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# [!DNL Oracle Responsys] connection

[](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) Responsysis es una herramienta de marketing por correo electrónico para campañas de marketing en varios canales ofrecida por  [!DNL Oracle] para personalizar las interacciones en correo electrónico, dispositivos móviles, pantallas y redes sociales.

Para enviar datos de segmentos a [!DNL Oracle Responsys], primero debe [conectarse al destino](#connect-destination) en Adobe Experience Platform y luego [configurar una importación de datos](#import-data-into-responsys) desde la ubicación del almacenamiento a [!DNL Oracle Responsys].

## Tipo de exportación {#export-type}

**Basado**  en perfiles: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [ de activación de ](../../ui/activate-destinations.md#select-attributes)destino.

## Destino de Connect {#connect-destination}

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL Oracle Responsys] y, a continuación, seleccione **[!UICONTROL Destino de Connect]**.

![Conectar a Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

En el paso **[!UICONTROL Autenticación]**, si anteriormente había configurado una conexión con el destino de almacenamiento de nube, seleccione **[!UICONTROL Cuenta existente]** y seleccione una de las conexiones existentes. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**. Para [!DNL Oracle Responsys], puede seleccionar entre **[!UICONTROL SFTP con contraseña]** y **[!UICONTROL SFTP con clave SSH]**. Rellene la información siguiente, según el tipo de conexión, y seleccione **[!UICONTROL Conectar con destino]**.

Para conexiones **[!UICONTROL SFTP con contraseña]**, debe proporcionar dominio, puerto, nombre de usuario y contraseña.

Para conexiones **[!UICONTROL SFTP con clave SSH]**, debe proporcionar dominio, puerto, nombre de usuario y clave SSH.

![Rellenar información de Responsys](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

En el paso **[!UICONTROL Configuración]**, rellene la información relevante para su destino como se muestra a continuación:
- **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
- **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
- **[!UICONTROL Ruta]** de carpeta: Proporcione la ruta en la ubicación del almacenamiento donde Platform depositará los datos de exportación como archivos CSV o separados por tabuladores.
- **[!UICONTROL Formato]** de archivo:  **** CSVo  **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a la ubicación de almacenamiento.

![Información básica de Responsys](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Haga clic en **[!UICONTROL Crear destino]** después de completar los campos anteriores. El destino está ahora conectado y puede [activar segmentos](../../ui/activate-destinations.md) en el destino.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](../../ui/activate-destinations.md) en el destino [!DNL Oracle Responsys], le recomendamos que seleccione un identificador único en su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Seleccionar los campos de esquema que se usarán como atributos de destino en los archivos exportados](./overview.md#destination-attributes) en Destinos de mercadotecnia de correo electrónico.

## Datos exportados {#exported-data}

Para los destinos [!DNL Oracle Responsys], Platform crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de Marketing por correo electrónico y destinos de almacenamiento de Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.

## Configurar la importación de datos en [!DNL Oracle Responsys] {#import-data-into-responsys}

Después de conectar Platform con su [!DNL Amazon S3] o almacenamiento SFTP, debe configurar la importación de datos desde la ubicación del almacenamiento en [!DNL Oracle Responsys]. Para obtener más información sobre cómo lograr esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en la [!DNL Oracle Responsys Help Center].