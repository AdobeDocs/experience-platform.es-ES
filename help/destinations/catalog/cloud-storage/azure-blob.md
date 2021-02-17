---
keywords: Blob de Azure;destino de Blob;s3;destino de blob de Azure
title: Conexión de blob de Azure
description: Cree una conexión directa de salida a su almacenamiento de blob de Azure para exportar periódicamente archivos de datos CSV o delimitados por tabuladores desde Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6d1960be886d12475603aeb79fe6283a1fd3030e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---


# [!DNL Azure Blob] connection

[!DNL Azure Blob] (en lo sucesivo, &quot;[!DNL Blob]&quot;) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona los pasos para crear un destino [!DNL Blob] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene un destino de Blob válido, puede omitir el resto de este documento y continuar con el tutorial sobre [activación de segmentos en su destino](../../ui/activate-destinations.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite el siguiente formato de archivo para exportar a  [!DNL Blob]:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. En el futuro se proporcionará compatibilidad con archivos DSV generales. Para obtener más información sobre los archivos admitidos, lea la sección de almacenamiento de nube en el tutorial sobre [activación de destinos](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Conectar la cuenta de Blob {#connect-destination}

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Destinations]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de destinos con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar el destino específico con el que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Cloud Almacenamiento]**, seleccione **[!UICONTROL Azure Blob Almacenamiento]**, seguido de **[!UICONTROL Configurar]**.

![Catalog](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

Aparece la página **[!UICONTROL Conectar con el Almacenamiento de blob de Azure]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta {#new-account}

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la cadena de conexión. La cadena de conexión es necesaria para acceder a los datos del almacenamiento Blob. El patrón de cadena de conexión [!DNL Blob] inicio con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

Para obtener más información sobre la configuración de la cadena de conexión [!DNL Blob], consulte [Configuración de una cadena de conexión para una cuenta de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar encriptación a sus archivos exportados. Tenga en cuenta que esta clave pública **debe** escribirse como una cadena con codificación Base64.

![Nueva cuenta](../../assets/catalog/cloud-storage/blob/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Blob] con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![Cuenta existente](../../assets/catalog/cloud-storage/blob/existing.png)

## Autenticación {#authentication}

Aparece la página **Autenticación**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional, la ruta de acceso a la carpeta y el contenedor de los archivos.

En este paso, también puede seleccionar cualquier **[!UICONTROL acción de mercadotecnia]** que deba aplicarse a este destino. Las acciones de marketing indican la intención de los datos que se exportarán al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o puede crear su propia acción de marketing. Para obtener más información acerca de las acciones de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

Cuando termine, seleccione **[!UICONTROL Crear destino]**.

![Autenticación](../../assets/catalog/cloud-storage/blob/authentication.png)

## Pasos siguientes {#activate-segments}

Siguiendo este tutorial, ha establecido una conexión con su cuenta [!DNL Blob]. Ahora puede continuar con el siguiente tutorial y [activar segmentos en su destino](../../ui/activate-destinations.md).
