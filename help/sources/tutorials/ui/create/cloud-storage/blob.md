---
keywords: Experience Platform;inicio;temas populares;Azure Blob;azure blob;Conector Azure Blob
solution: Experience Platform
title: Crear una conexión de origen de Azure Blob en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear un conector de origen de Azure Blob mediante la interfaz de usuario de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Azure Blob] en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Azure Blob] (en adelante denominado &quot;[!DNL Blob]&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Blob] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo que se van a introducir desde almacenes externos:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por coma. El valor de los encabezados de campo de los archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se admitirán los archivos DSV generales.
- Notación de objeto de JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
- Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder al almacenamiento [!DNL Blob] en Platform, debe proporcionar un valor válido para la siguiente credencial:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena que contiene la información de autorización necesaria para autenticarse [!DNL Blob] en el Experience Platform. El patrón de cadena de conexión [!DNL Blob] es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información sobre cadenas de conexión, consulte este [!DNL Blob] documento sobre [configuración de cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | El URI de firma de acceso compartido que puede utilizar como tipo de autenticación alternativo para conectar su cuenta [!DNL Blob]. El patrón de URI SAS [!DNL Blob] es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte este [!DNL Blob] documento sobre [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Conecte su cuenta [!DNL Blob]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Blob] a Platform.

En la [Platform UI](https://platform.adobe.com), seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Cloud storage], seleccione **[!UICONTROL Azure Blob Storage]** y, a continuación, seleccione **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

Aparece la página **[!UICONTROL Connect to Azure Blob Storage]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta [!DNL Blob] con la que desea crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL New account]** y, a continuación, proporcione un nombre y una descripción de la opción para la nueva cuenta [!DNL Blob].

**Autenticar mediante una cadena de conexión**

El conector [!DNL Blob] le proporciona diferentes tipos de autenticación para el acceso. En [!UICONTROL Account authentication] seleccione **[!UICONTROL ConnectionString]** para utilizar credenciales basadas en cadenas de conexión.

![cadena de conexión](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticar mediante un URI de firma de acceso compartido**

Un URI de firma de acceso compartido (SAS) permite una autorización delegada segura en su cuenta [!DNL Blob]. Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Seleccione **[!UICONTROL SasURIAuthentication]** y, a continuación, proporcione el URI SAS [!DNL Blob]. Seleccione **[!UICONTROL Connect to source]** para continuar.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Blob]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para importar los datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
