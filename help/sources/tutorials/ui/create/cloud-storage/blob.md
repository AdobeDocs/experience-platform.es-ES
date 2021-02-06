---
keywords: Experience Platform;inicio;temas populares;Blob de Azure;blob de Azure;Conector de blob de Azure
solution: Experience Platform
title: Creación de una conexión de origen de blob de Azure en la interfaz de usuario
topic: overview
type: Tutorial
description: Obtenga información sobre cómo crear un conector de origen de blob de Azure mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Azure Blob] en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Azure Blob] (en adelante denominado &quot;[!DNL Blob]&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Blob] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo para la ingesta desde almacenamientos externos:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se proporcionará compatibilidad con archivos DSV generales.
- Notación de objetos JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
- Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Blob] almacenamiento en la plataforma, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena que contiene la información de autorización necesaria para autenticar [!DNL Blob] al Experience Platform. El patrón de cadena de conexión [!DNL Blob] es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información acerca de las cadenas de conexión, consulte este [!DNL Blob] documento sobre [configuración de cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | El URI de firma de acceso compartido que puede utilizar como tipo de autenticación alternativo para conectar su cuenta [!DNL Blob]. El patrón de URI [!DNL Blob] SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte este [!DNL Blob] documento en [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Conectar su cuenta [!DNL Blob]

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta [!DNL Blob] a la plataforma.

En la [IU de la plataforma](https://platform.adobe.com), seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Cloud almacenamiento], seleccione **[!UICONTROL Azure Blob Almacenamiento]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

Aparece la página **[!UICONTROL Conectar con el Almacenamiento de blob de Azure]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta [!DNL Blob] con la que desea crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción de opción para la nueva cuenta [!DNL Blob].

**Autenticar mediante una cadena de conexión**

El conector [!DNL Blob] le proporciona diferentes tipos de autenticación para el acceso. En [!UICONTROL Autenticación de cuenta] seleccione **[!UICONTROL ConnectionString]** para utilizar las credenciales basadas en cadenas de conexión.

![cadena de conexión](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticar mediante un URI de firma de acceso compartido**

Un URI de firma de acceso compartido (SAS) permite una autorización delegada segura en su cuenta [!DNL Blob]. Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que una autenticación basada en SAS le permite establecer permisos, fechas de inicio y caducidad, así como provisiones para recursos específicos.

Seleccione **[!UICONTROL SasURIAuthauthentication]** y proporcione su URI [!DNL Blob] SAS. Seleccione **[!UICONTROL Conectar a origen]** para continuar.

![sa-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta [!DNL Blob]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a la plataforma](../../dataflow/batch/cloud-storage.md).
