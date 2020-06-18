---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen OData genérico en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Creación de un conector de origen OData genérico en la interfaz de usuario

> [!NOTE]
> El conector OData genérico está en fase beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen genérico de protocolo de datos abiertos (en adelante, &quot;OData&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión OData válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de conjuntos de datos de protocolos](../../dataflow/protocols.md)

### Recopilar las credenciales necesarias

Para acceder a su cuenta de OData en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | Dirección URL raíz del servicio OData. |

Para obtener más información sobre cómo empezar, consulte [este documento](https://www.odata.org/getting-started/basic-tutorial/)de OData.

## Conectar la cuenta de OData

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de OData para conectarse a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear una cuenta de entrada. Cada fuente muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría *Protocolos* , seleccione **Generic OData** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión de entrada, seleccione Origen **de** Connect.

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

Aparece la página *Conectar con OData* genérico. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, proporcione la conexión con un nombre, una descripción opcional y sus credenciales de OData. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva cuenta.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de OData con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de OData. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de conjuntos de datos para traer datos de protocolos a Platform](../../dataflow/protocols.md).