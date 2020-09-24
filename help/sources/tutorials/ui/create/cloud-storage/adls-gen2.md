---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls connector
solution: Experience Platform
title: Creación de un conector de origen de Azure Data Lake Almacenamiento Gen2 en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona pasos para autenticar un conector de origen de Azure Data Lake Almacenamiento Gen2 (en adelante, "ADLS Gen2") mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# Creación de un conector [!DNL Azure Data Lake Storage Gen2] de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para autenticar un conector de origen [!DNL Azure Data Lake Storage Gen2] (en lo sucesivo denominado &quot;[!DNL ADLS Gen2]&quot;) mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión ADLS Gen2 válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector [!DNL ADLS Gen2] de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | El punto final para [!DNL ADLS Gen2]. |
| `servicePrincipalId` | El ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene la aplicación. |

Para obtener más información sobre estos valores, consulte [ [!DNL ADLS Gen2] este documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Conectar su [!DNL ADLS Gen2] cuenta

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL ADLS Gen2] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]** , seleccione **[!UICONTROL Azure Data Lake Gen2]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Aparece el cuadro de diálogo **[!UICONTROL Conectar con Azure Data Lake Gen2]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL ADLS Gen2] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL ADLS Gen2] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su [!DNL ADLS Gen2] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).