---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;destino de responsys de oracle
title: Conexión de Responsys de oracle
description: Responsys es una herramienta de marketing por correo electrónico para campañas de marketing en canales múltiples que ofrece Oracle para personalizar las interacciones entre correo electrónico, móvil, visualización y social.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# [!DNL Oracle Responsys] connection

## Información general {#overview}

[](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) Responsya es una herramienta de marketing por correo electrónico para campañas de marketing en canales múltiples que ofrece  [!DNL Oracle] para personalizar las interacciones entre correo electrónico, móvil, visualización y social.

Para enviar datos de segmentos a [!DNL Oracle Responsys], primero debe [conectarse al destino](#connect-destination) en Adobe Experience Platform y luego [configurar una importación de datos](#import-data-into-responsys) desde su ubicación de almacenamiento a [!DNL Oracle Responsys].

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conectar destino {#connect-destination}

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL Oracle Responsys] y, a continuación, seleccione **[!UICONTROL Connect destination]**.

![Conectarse a Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

En el paso **[!UICONTROL Authentication]**, si ha configurado anteriormente una conexión con su destino de almacenamiento en la nube, seleccione **[!UICONTROL Existing Account]** y elija una de las conexiones existentes. O bien, puede seleccionar **[!UICONTROL New Account]** para configurar una nueva conexión. Complete las credenciales de autenticación de la cuenta y seleccione **[!UICONTROL Connect to destination]**. Para [!DNL Oracle Responsys], puede seleccionar entre **[!UICONTROL SFTP with Password]** y **[!UICONTROL SFTP with SSH Key]**. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect to destination]**.

Para las conexiones **[!UICONTROL SFTP with Password]**, debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.

Para las conexiones **[!UICONTROL SFTP with SSH Key]**, debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

![Rellene la información de Responsys](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

En el paso **[!UICONTROL Setup]**, rellene la información relevante para su destino como se muestra a continuación:
- **[!UICONTROL Name]**: Elija un nombre relevante para el destino.
- **[!UICONTROL Description]**: Escriba una descripción para el destino.
- **[!UICONTROL Bucket name]**: El espacio de Amazon S3, en el que Platform depositará la exportación de datos. La entrada debe tener entre 3 y 63 caracteres de longitud. Debe comenzar y terminar con una letra o un número. Solo debe contener letras minúsculas, números o guiones ( - ). No se debe dar formato a una dirección IP (por ejemplo, 192.100.1.1).
- **[!UICONTROL Folder Path]**: Proporcione la ruta en su ubicación de almacenamiento donde Platform depositará sus datos de exportación como archivos CSV o delimitados por tabuladores.
- **[!UICONTROL File Format]**:  **** CSVo  **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a su ubicación de almacenamiento.
- **[!UICONTROL Marketing actions]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [Control de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre las acciones de marketing definidas por el Adobe, consulte la [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

![Información básica de Responsys](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Haga clic en **[!UICONTROL Create destination]** después de rellenar los campos anteriores. El destino ahora está conectado y puede [activar segmentos](../../ui/activate-destinations.md) en el destino.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](../../ui/activate-destinations.md) en el destino [!DNL Oracle Responsys], le recomendamos que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Seleccionar qué campos de esquema utilizar como atributos de destino en los archivos exportados](./overview.md#destination-attributes) en Destinos de marketing por correo electrónico.

## Datos exportados {#exported-data}

Para destinos [!DNL Oracle Responsys], Platform crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.

## Configurar la importación de datos en [!DNL Oracle Responsys] {#import-data-into-responsys}

Después de conectar Platform al almacenamiento [!DNL Amazon S3] o SFTP, debe configurar la importación de datos desde la ubicación de almacenamiento en [!DNL Oracle Responsys]. Para obtener información sobre cómo lograr esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en [!DNL Oracle Responsys Help Center].