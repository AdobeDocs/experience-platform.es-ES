---
keywords: Experience Platform;inicio;temas populares;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;conector adls
solution: Experience Platform
title: Crear una conexión de origen Gen2 de Azure Data Lake Storage en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure Data Lake Storage Gen2 mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Crear un [!DNL Azure Data Lake Storage Gen2] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un [!DNL Azure Data Lake Storage Gen2] (en lo sucesivo, &quot;[!DNL ADLS Gen2]&quot;) utilizando el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión ADLS Gen2 válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL ADLS Gen2] conector de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | El punto final para [!DNL ADLS Gen2]. |
| `servicePrincipalId` | ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene su aplicación. |

Para obtener más información, consulte [esta [!DNL ADLS Gen2] documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Conecte su [!DNL ADLS Gen2] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL ADLS Gen2] cuenta a la que conectarse [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Azure Data Lake Gen2]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

El **[!UICONTROL Conectar con Azure Data Lake Gen2]** aparece el cuadro de diálogo. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL ADLS Gen2] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL ADLS Gen2] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL ADLS Gen2] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
