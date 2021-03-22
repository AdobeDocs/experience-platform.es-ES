---
keywords: Azure Blob;destino de Blob;s3;destino de azure blob
title: Conexión de Azure Blob
description: Cree una conexión saliente en directo al almacenamiento del blob de Azure para exportar periódicamente archivos de datos de Adobe Experience Platform delimitados por tabulaciones o CSV.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---


# [!DNL Azure Blob] connection

## Información general {#overview}

[!DNL Azure Blob] (en adelante, &quot;[!DNL Blob]&quot;) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona pasos para crear un destino [!DNL Blob] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene un destino de Blob válido, puede omitir el resto de este documento y continuar con el tutorial sobre la [activación de segmentos a su destino](../../ui/activate-destinations.md).

## Formatos de archivo compatibles {#file-formats}

[!DNL Experience Platform] admite el siguiente formato de archivo para exportar a  [!DNL Blob]:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por coma. En el futuro se admitirán los archivos DSV generales. Para obtener más información sobre los archivos compatibles, lea la sección almacenamiento en la nube en el tutorial sobre [activación de destinos](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Conecte su cuenta de Blob {#connect-destination}

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Destinations]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de destinos con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar el destino específico con el que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Cloud Storage]**, seleccione **[!UICONTROL Azure Blob Storage]**, seguido de **[!UICONTROL Configure]**.

![Catalog](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

Aparece la página **[!UICONTROL Connect to Azure Blob Storage]**. En esta página, puede usar credenciales nuevas o existentes.

## Nueva cuenta {#new-account}

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, proporcione la cadena de conexión. La cadena de conexión es necesaria para acceder a los datos del almacenamiento del blob. El patrón de la cadena de conexión [!DNL Blob] comienza por: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

Para obtener más información sobre la configuración de la cadena de conexión [!DNL Blob], consulte [Configuración de una cadena de conexión para una cuenta de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. Tenga en cuenta que esta clave pública **debe** escribirse como una cadena codificada Base64.

![Nueva cuenta](../../assets/catalog/cloud-storage/blob/new.png)

## Cuenta existente {#existing-account}

Para conectar una cuenta existente, seleccione la cuenta [!DNL Blob] con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![Cuenta existente](../../assets/catalog/cloud-storage/blob/existing.png)

## Autenticación {#authentication}

Aparece la página **Autenticación**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional, la ruta de la carpeta y el contenedor de los archivos.

En este paso, también puede seleccionar cualquier **[!UICONTROL Marketing actions]** que deba aplicarse a este destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

Cuando termine, seleccione **[!UICONTROL Create destination]**.

![Autenticación](../../assets/catalog/cloud-storage/blob/authentication.png)

## Pasos siguientes {#activate-segments}

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Blob]. Ahora puede continuar con el siguiente tutorial y [activar segmentos en su destino](../../ui/activate-destinations.md).
