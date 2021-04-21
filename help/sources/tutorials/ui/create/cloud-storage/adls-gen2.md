---
keywords: Experience Platform;inicio;temas populares;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;conector de adls
solution: Experience Platform
title: Crear una conexión de origen de Azure Data Lake Storage Gen2 en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure Data Lake Storage Gen2 mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Azure Data Lake Storage Gen2] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para autenticar un conector de origen [!DNL Azure Data Lake Storage Gen2] (en adelante denominado &quot;[!DNL ADLS Gen2]&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión ADLS Gen2 válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen [!DNL ADLS Gen2], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | El punto final para [!DNL ADLS Gen2]. |
| `servicePrincipalId` | El ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene su aplicación. |

Para obtener más información sobre estos valores, consulte [this [!DNL ADLS Gen2] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Conecte su cuenta [!DNL ADLS Gen2]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL ADLS Gen2] para conectarse a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL Azure Data Lake Gen2]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Aparece el cuadro de diálogo **[!UICONTROL Connect to Azure Data Lake Gen2]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New Account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL ADLS Gen2]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL ADLS Gen2] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL ADLS Gen2]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
