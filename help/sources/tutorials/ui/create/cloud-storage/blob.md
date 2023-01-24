---
title: Crear una conexión de origen de Azure Blob en la interfaz de usuario
description: Obtenga información sobre cómo crear un conector de origen de Azure Blob mediante la interfaz de usuario de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# Cree un [!DNL Azure Blob] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Azure Blob] (en lo sucesivo, &quot;el[!DNL Blob]&quot;) conexión de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado para organizar los datos de experiencia del cliente en Experience Platform.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Blob] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

Experience Platform admite los siguientes formatos de archivo que se van a ingerir desde almacenes externos:

* Valores separados por delimitadores (DSV): Puede utilizar cualquier delimitador de una sola columna, como una tabulación, una coma, una barra vertical, un punto y coma o un hash, para recopilar archivos planos en cualquier formato.
* Notación de objeto de JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Blob] en Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | Una cadena que contiene la información de autorización necesaria para autenticarse [!DNL Blob] al Experience Platform. La variable [!DNL Blob] el patrón de cadena de conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información sobre cadenas de conexión, consulte esta [!DNL Blob] documento en [configuración de cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| URI de SAS | El URI de firma de acceso compartido que puede usar como tipo de autenticación alternativo para conectar su [!DNL Blob] cuenta. La variable [!DNL Blob] El patrón de URI SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte [!DNL Blob] documento en [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contenedor | Nombre del contenedor al que desea designar el acceso. Al crear una cuenta nueva con el [!DNL Blob] fuente, puede proporcionar un nombre de contenedor para especificar el acceso del usuario a la subcarpeta que elija. |
| Ruta de carpeta | Ruta a la carpeta a la que desea proporcionar acceso. |

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Blob] a Platform.

## Conecte su [!DNL Blob] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccione **[!UICONTROL Almacenamiento de Azure Blob]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes del Experience Platform con el origen de almacenamiento del blob de Azure seleccionado.](../../../../images/tutorials/create/blob/catalog.png)

La variable **[!UICONTROL Conectarse al almacenamiento de Azure Blob]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Blob] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL Blob] cuenta.

![La nueva pantalla de cuenta para el origen de almacenamiento del blob de Azure.](../../../../images/tutorials/create/blob/new.png)

La variable [!DNL Blob] source admite autenticación de clave de cuenta y autenticación de firma de acceso compartido (SAS). Una autenticación basada en claves de cuenta requiere una cadena de conexión para la verificación, mientras que una autenticación SAS utiliza un URI que permite la autorización delegada segura de su cuenta.

Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre del contenedor y la ruta a la subcarpeta.

>[!BEGINTABS]

>[!TAB Cadena de conexión]

Para autenticarse con una clave de cuenta, seleccione **[!UICONTROL Autenticación de clave de cuenta]** y proporcione la cadena de conexión. Durante este paso, también puede designar el nombre del contenedor y la ruta a la subcarpeta a la que desea acceder. Cuando termine, seleccione **[!UICONTROL Conectar a origen]**.

![cadena de conexión](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI de SAS]

Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Para autenticarse con una firma de acceso compartido, seleccione **[!UICONTROL Autenticación de firma de acceso compartido]** y, a continuación, proporcione su URI SAS. Durante este paso, también puede designar el nombre del contenedor y la ruta a la subcarpeta a la que desea acceder. Cuando termine, seleccione **[!UICONTROL Conectar a origen]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Blob] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
