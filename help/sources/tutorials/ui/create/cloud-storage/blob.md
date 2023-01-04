---
keywords: Experience Platform;inicio;temas populares;Azure Blob;azure blob;Conector Azure Blob
solution: Experience Platform
title: Crear una conexión de origen de Azure Blob en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear un conector de origen de Azure Blob mediante la interfaz de usuario de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# Cree un [!DNL Azure Blob] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Azure Blob] (en lo sucesivo, &quot;el[!DNL Blob]&quot;) utilizando la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Blob] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo que se van a introducir desde almacenes externos:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por coma. El valor de los encabezados de campo de los archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se admitirán los archivos DSV generales.
- Notación de objeto de JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
- Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Blob] en Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena que contiene la información de autorización necesaria para autenticarse [!DNL Blob] al Experience Platform. La variable [!DNL Blob] el patrón de cadena de conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información sobre cadenas de conexión, consulte esta [!DNL Blob] documento en [configuración de cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | El URI de firma de acceso compartido que puede usar como tipo de autenticación alternativo para conectar su [!DNL Blob] cuenta. La variable [!DNL Blob] El patrón de URI SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte [!DNL Blob] documento en [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Conecte su [!DNL Blob] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Blob] a Platform.

En el [Interfaz de usuario de Platform](https://platform.adobe.com), seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccione **[!UICONTROL Almacenamiento de Azure Blob]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

La variable **[!UICONTROL Conectarse al almacenamiento de Azure Blob]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Blob] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción de la opción para la nueva [!DNL Blob] cuenta.

**Autenticar mediante una cadena de conexión**

La variable [!DNL Blob] connector proporciona diferentes tipos de autenticación para el acceso. En [!UICONTROL Autenticación de la cuenta] select **[!UICONTROL ConnectionString]** para utilizar credenciales basadas en cadenas de conexión.

![cadena de conexión](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticar mediante un URI de firma de acceso compartido**

Un URI de firma de acceso compartido (SAS) permite una autorización delegada segura en su [!DNL Blob] cuenta. Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Select **[!UICONTROL SasURIAuthauthentication]** y, a continuación, proporcione la [!DNL Blob] URI SAS. Select **[!UICONTROL Conectar a origen]** para continuar.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Blob] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
