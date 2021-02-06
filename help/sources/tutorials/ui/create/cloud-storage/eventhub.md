---
keywords: Experience Platform;inicio;temas populares;Centros de Evento de Azure;Centros de Evento;Centros de evento de azure
solution: Experience Platform
title: Creación de una conexión de origen de los centros de Evento de Azure en la interfaz de usuario
topic: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure Evento Hubs mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Azure Event Hubs] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Azure Event Hubs] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para autenticar un conector de origen [!DNL Azure Event Hubs] (en adelante denominado &quot;[!DNL Event Hubs]&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Event Hubs] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen [!DNL Event Hubs], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `sasKeyName` | El nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | Firma de acceso compartido generada. |
| `namespace` | La Área de nombres del [!DNL Event Hubs] al que está accediendo. |

Para obtener más información sobre estos valores, consulte [this [!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Conectar su cuenta [!DNL Event Hubs]

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta [!DNL Event Hubs] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]**. La ficha **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Cloud Almacenamiento]**, seleccione **[!UICONTROL Azure Evento Hubs]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector de concentradores de Evento.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Aparece el cuadro de diálogo **[!UICONTROL Conectar con los centros de Evento de Azure]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus credenciales [!DNL Event Hubs]. Cuando termine, seleccione **[!UICONTROL Conectar]** y, a continuación, deje transcurrir algún tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/eventhub/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Event Hubs] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha conectado su cuenta [!DNL Event Hubs] a [!DNL Platform]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).