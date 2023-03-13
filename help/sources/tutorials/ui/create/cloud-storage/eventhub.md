---
keywords: Experience Platform;inicio;temas populares;Azure Event Hubs;Event Hubs;azure event hubs
solution: Experience Platform
title: Crear una conexión de origen de Azure Event Hubs en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure Event Hubs mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Crear un [!DNL Azure Event Hubs] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un [!DNL Azure Event Hubs] (en lo sucesivo, &quot;[!DNL Event Hubs]&quot;) utilizando el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Event Hubs] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL Event Hubs] conector de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `sasKeyName` | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | La clave principal del [!DNL Event Hubs] namespace. El `sasPolicy` que el `sasKey` corresponde a debe tener `manage` derechos configurados para el [!DNL Event Hubs] lista que se va a rellenar. |
| `namespace` | El área de nombres del [!DNL Event Hubs] está accediendo a. |

Para obtener más información, consulte [esta [!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Conecte su [!DNL Event Hubs] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Event Hubs] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pestaña muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Almacenamiento en la nube]** categoría, seleccionar **[!UICONTROL Azure Event Hubs]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector de Event Hubs.

![](../../../../images/tutorials/create/eventhub/catalog.png)

El **[!UICONTROL Conectar con Azure Event Hubs]** aparece el cuadro de diálogo. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Event Hubs] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/eventhub/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Event Hubs] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha conectado su [!DNL Event Hubs] cuenta a [!DNL Platform]. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
