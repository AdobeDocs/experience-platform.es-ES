---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen del Explorador de datos de Azure en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 1fb07723aedcf6dfd49765c10342b70b0a7d24f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Creación de un conector de origen del Explorador de datos de Azure en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen del Explorador de datos de Azure (en adelante, &quot;Explorador de datos&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida con el Explorador de datos, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta del Explorador de datos en la plataforma, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | Extremo del servidor del Explorador de datos. |
| `database` | Nombre de la base de datos del Explorador de datos. |
| `tenant` | ID de inquilino único que se utiliza para conectarse a la base de datos del Explorador de datos. |
| `servicePrincipalId` | ID principal de servicio único que se utiliza para conectarse a la base de datos del Explorador de datos. |
| `servicePrincipalKey` | Clave principal de servicio única utilizada para conectarse a la base de datos del Explorador de datos. |

Para obtener más información sobre cómo empezar, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)del Explorador de datos.

## Conectar la cuenta del Explorador de datos de Azure

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta del Explorador de datos para conectarse a la plataforma.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear una cuenta de entrada y cada origen muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría *[!UICONTROL Bases de datos]* , seleccione Explorador **[!UICONTROL de datos de]** Azure y haga clic **en el icono + (+)** para crear un nuevo conector del Explorador de datos.

![catálogo](../../../../images/tutorials/create/data-explorer/catalog.png)

Aparece la página *[!UICONTROL Conectar con el Explorador]* de datos de Azure. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión con un nombre, una descripción opcional y las credenciales del Explorador de datos. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva cuenta.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta del Explorador de datos con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/data-explorer/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta del Explorador de datos. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/databases.md).