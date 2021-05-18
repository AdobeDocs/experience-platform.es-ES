---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;destino de responsys de oracle
title: Conexión de Responsys de oracle
description: Responsys es una herramienta de marketing por correo electrónico para campañas de marketing en canales múltiples que ofrece Oracle para personalizar las interacciones entre correo electrónico, móvil, visualización y social.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# [!DNL Oracle Responsys] connection

## Información general {#overview}

[](https://www.oracle.com/cx/marketing/campaign-management/) Responsya es una herramienta de marketing por correo electrónico para campañas de marketing en canales múltiples que ofrece  [!DNL Oracle] para personalizar las interacciones entre correo electrónico, móvil, visualización y social.

Para enviar datos de segmentos a [!DNL Oracle Responsys], primero debe [conectarse al destino](#connect-destination) en Adobe Experience Platform y luego [configurar una importación de datos](#import-data-into-responsys) desde su ubicación de almacenamiento a [!DNL Oracle Responsys].

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

## LISTA DE PERMITIDOS de dirección IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, Adobe recomienda que agregue ciertos rangos de IP a la lista de permitidos.

Consulte la [lista de permitidos de direcciones IP para destinos de almacenamiento en la nube](../cloud-storage/ip-address-allow-list.md) si necesita agregar IP de Adobe a su lista de permitidos.

## Conectar destino {#connect-destination}

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL Oracle Responsys] y, a continuación, seleccione **[!UICONTROL Connect destination]**.

![Conectarse a Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

En el paso **[!UICONTROL Cuenta]**, si anteriormente ha configurado una conexión con su destino de almacenamiento en la nube, seleccione **[!UICONTROL Cuenta existente]** y elija una de las conexiones existentes. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión. Complete las credenciales de autenticación de la cuenta y seleccione **[!UICONTROL Connect to destination]**. Para [!DNL Oracle Responsys], puede seleccionar entre **[!UICONTROL SFTP con contraseña]** y **[!UICONTROL SFTP con clave SSH]**.

![Conectar la cuenta de Responsys](../../assets/catalog/email-marketing/oracle-responsys/connection-type.png)

Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Configurar]**.

- Para conexiones **[!UICONTROL SFTP con contraseña]**, debe proporcionar [!UICONTROL Dominio], [!UICONTROL Puerto], [!UICONTROL Nombre de usuario] y [!UICONTROL Contraseña].
- Para conexiones **[!UICONTROL SFTP con clave SSH]**, debe proporcionar [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL User name] y [!UICONTROL SSH Key].

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en la sección **[!UICONTROL Clave]**. La clave pública debe escribirse como una cadena codificada [!DNL Base64].

![Rellene la información de Responsys](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

En el paso **[!UICONTROL Authentication]** , rellene la información relevante para su destino como se muestra a continuación:
- **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
- **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
- **[!UICONTROL Ruta]** de carpeta: Proporcione la ruta en su ubicación de almacenamiento donde Platform depositará sus datos de exportación como archivos CSV o delimitados por tabuladores.
- **[!UICONTROL Formato]** de archivo:  **** CSVo  **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a su ubicación de almacenamiento.
- **[!UICONTROL Acciones]** de marketing: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Información básica de Responsys](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Haga clic en **[!UICONTROL Crear destino]** después de rellenar los campos anteriores. El destino ahora está conectado y puede [activar segmentos](../../ui/activate-destinations.md) en el destino.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](../../ui/activate-destinations.md) en el destino [!DNL Oracle Responsys], Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Seleccionar qué campos de esquema utilizar como atributos de destino en los archivos exportados](./overview.md#destination-attributes).

## Datos exportados {#exported-data}

Para destinos [!DNL Oracle Responsys], Platform crea un archivo `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.

## Configurar la importación de datos en [!DNL Oracle Responsys] {#import-data-into-responsys}

Después de conectar [!DNL Platform] al almacenamiento [!DNL SFTP], debe configurar la importación de datos desde su ubicación de almacenamiento en [!DNL Oracle Responsys]. Para obtener información sobre cómo lograr esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en [!DNL Oracle Responsys Help Center].
