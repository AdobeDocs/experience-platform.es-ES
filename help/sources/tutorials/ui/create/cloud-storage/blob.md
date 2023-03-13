---
title: Crear una conexión de origen de Azure Blob en la interfaz de usuario
description: Obtenga información sobre cómo crear un conector de origen de Azure Blob mediante la interfaz de usuario de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# Crear un [!DNL Azure Blob] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL Azure Blob] (en lo sucesivo, &quot;[!DNL Blob]&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): el marco de trabajo estandarizado para organizar los datos de experiencia del cliente en Experience Platform.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Blob] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

Experience Platform admite la ingesta de los siguientes formatos de archivo desde almacenes externos:

* Valores separados por delimitadores (DSV): puede utilizar cualquier delimitador de columna individual, como una tabulación, una coma, una barra vertical, un punto y coma o un hash, para recopilar archivos planos en cualquier formato.
* Notación de objetos JavaScript (JSON): los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato Parquet deben ser compatibles con XDM.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Blob] en Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | Cadena que contiene la información de autorización necesaria para la autenticación [!DNL Blob] al Experience Platform. El [!DNL Blob] el patrón de cadena de conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información acerca de las cadenas de conexión, consulte esto [!DNL Blob] documento en [configurar cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| URI de SAS | El URI de firma de acceso compartido que puede utilizar como tipo de autenticación alternativo para conectar su [!DNL Blob] cuenta. El [!DNL Blob] El patrón de URI de SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte [!DNL Blob] documento en [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contenedor | El nombre del contenedor al que desea designar el acceso. Al crear una cuenta nueva con [!DNL Blob] origen, puede proporcionar un nombre de contenedor para especificar el acceso del usuario a la subcarpeta que elija. |
| Ruta de carpeta | La ruta a la carpeta a la que desea proporcionar acceso. |

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Blob] a Platform.

## Conecte su [!DNL Blob] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL Almacenamiento de Azure Blob]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes del Experience Platform con la fuente de almacenamiento de Azure Blob seleccionada.](../../../../images/tutorials/create/blob/catalog.png)

El **[!UICONTROL Conectar con Azure Blob Storage]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Blob] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL Blob] cuenta.

![La nueva pantalla de cuenta para el origen de almacenamiento del blob de Azure.](../../../../images/tutorials/create/blob/new.png)

El [!DNL Blob] El origen admite la autenticación de clave de cuenta y la autenticación de firma de acceso compartido (SAS). Una autenticación basada en claves de cuenta requiere una cadena de conexión para la verificación, mientras que una autenticación SAS utiliza un URI que permite la autorización delegada y segura de su cuenta.

Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre del contenedor y la ruta de acceso a la subcarpeta.

>[!BEGINTABS]

>[!TAB Cadena de conexión]

Para autenticarse con una clave de cuenta, seleccione **[!UICONTROL Autenticación de clave de cuenta]** y proporcione la cadena de conexión. Durante este paso, también puede designar el nombre del contenedor y la ruta de acceso a la subcarpeta a la que desea acceder. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![cadena de conexión](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI de SAS]

Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS le permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Para autenticarse con una firma de acceso compartido, seleccione **[!UICONTROL Autenticación de firma de acceso compartido]** y proporcione el URI de SAS. Durante este paso, también puede designar el nombre del contenedor y la ruta de acceso a la subcarpeta a la que desea acceder. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Blob] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
