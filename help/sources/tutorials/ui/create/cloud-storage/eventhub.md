---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de los centros de Evento de Azure en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 75581529ede3772606bc18fea683da5d396996c5
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---


# Creación de un conector de origen de los centros de Evento de Azure en la interfaz de usuario

>[!NOTE]
> El conector de los centros de Evento de Azure está en versión beta. Las funciones y la documentación están sujetas a cambios.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para autenticar un conector de origen de los centros de Evento de Azure (en adelante, &quot;centros de Evento&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una cuenta de Evento Hubs, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen Evento Hubs, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `sasKeyName` | El nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| `sasKey` | Firma de acceso compartido generada. |
| `namespace` | La Área de nombres de los centros de Evento a los que está accediendo. |

Para obtener más información acerca de estos valores, consulte [este documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)de Evento Hubs.

## Conectar la cuenta de los centros de Evento

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular la cuenta de los centros de Evento a la plataforma.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La ficha *Catálogo* muestra una serie de orígenes para los que se puede conectar a Plataforma. Cada origen muestra el número de cuentas existentes asociadas a ellas.

En la categoría de Almacenamiento *de* Cloud, seleccione Hubs **de Evento de** Azure y haga clic **en el icono + (+)** para crear un nuevo conector Hubs de Evento.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Aparece el cuadro de diálogo *Conectar con los centros* de Evento de Azure. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y las credenciales de los centros de Evento. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/eventhub/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Evento Hubs con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha conectado su cuenta de Evento Hubs a Platform. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento de nube a la plataforma](../../dataflow/streaming/cloud-storage.md).