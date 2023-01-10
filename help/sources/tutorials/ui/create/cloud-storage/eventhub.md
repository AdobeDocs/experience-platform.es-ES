---
keywords: Experience Platform;inicio;temas populares;centros de eventos de Azure;centros de eventos;centros de eventos de azure
solution: Experience Platform
title: Crear una conexión de origen de los centros de eventos de Azure en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de los centros de eventos de Azure mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Cree un [!DNL Azure Event Hubs] conexión de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un [!DNL Azure Event Hubs] (en lo sucesivo, &quot;el[!DNL Event Hubs]&quot;) conector de origen que utiliza la variable [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Event Hubs] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar las credenciales necesarias

Para autenticar su [!DNL Event Hubs] conector de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `sasKeyName` | El nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | La clave principal de la variable [!DNL Event Hubs] espacio de nombres. La variable `sasPolicy` que `sasKey` corresponde a debe tener `manage` derechos configurados en orden para la variable [!DNL Event Hubs] para rellenar. |
| `namespace` | El espacio de nombres de la variable [!DNL Event Hubs] está accediendo. |

Para obtener más información sobre estos valores, consulte [this [!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Conecte su [!DNL Event Hubs] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Event Hubs] cuenta para [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Fuentes]** espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL Almacenamiento en la nube]** categoría, seleccione **[!UICONTROL Centros de eventos de Azure]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector de centros de eventos.

![](../../../../images/tutorials/create/eventhub/catalog.png)

La variable **[!UICONTROL Conectarse a los centros de eventos de Azure]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL Event Hubs] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![](../../../../images/tutorials/create/eventhub/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Event Hubs] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha conectado su [!DNL Event Hubs] cuenta para [!DNL Platform]. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para incorporar datos del almacenamiento en la nube a [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
