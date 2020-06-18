---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Analytics de sincronización de Azure en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Creación de un conector de origen de Analytics de sincronización de Azure en la interfaz de usuario

> [!NOTE]
> El conector Analytics de la sinapsis de Azure está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen de Analytics de sinapsis de Azure (en adelante denominado &quot;Sinapsis&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya dispone de una conexión base Synapse, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta de Synapse en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada con la autenticación de Synapse. El patrón de la cadena de conexión Synapse es `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Para obtener más información sobre este valor, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse)de Sinapsis.

## Conectar la cuenta de Synapse

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular la cuenta de Sinapse a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *Bases* de datos, seleccione **Azure Synapse Analytics** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **de** Connect.

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

Aparece la página *Conectar con Azure Synapse de Analytics* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de sincronización. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de sintaxis con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base con su cuenta de Synapse. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/databases.md).