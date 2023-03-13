---
keywords: Experience Platform;inicio;temas populares;Data Explorer de Azure;explorador de datos de Azure;explorador de datos;Data Explorer
solution: Experience Platform
title: Crear una conexión de origen de Azure Data Explorer en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Data Explorer de Azure mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Crear un [!DNL Azure Data Explorer] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Azure Data Explorer] (en lo sucesivo, &quot;[!DNL Data Explorer]&quot;) utilizando el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Data Explorer] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL Data Explorer] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | El punto final del [!DNL Data Explorer] servidor. |
| `database` | El nombre del [!DNL Data Explorer] base de datos. |
| `tenant` | ID único de inquilino utilizado para conectarse a [!DNL Data Explorer] base de datos. |
| `servicePrincipalId` | El ID principal de servicio único utilizado para conectarse a [!DNL Data Explorer] base de datos. |
| `servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse al [!DNL Data Explorer] base de datos. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Conecte su [!DNL Azure Data Explorer] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Data Explorer] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Azure Data Explorer]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector de Data Explorer.

![catalogar](../../../../images/tutorials/create/data-explorer/catalog.png)

El **[!UICONTROL Conectar con Data Explorer de Azure]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Data Explorer] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/data-explorer/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Data Explorer] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/data-explorer/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Data Explorer] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
