---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen HP Vertica en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Creación de un conector de origen HP Vertica en la interfaz de usuario

> [!NOTE]
> El conector HP Vertica está en versión beta. Las funciones y la documentación están sujetas a cambios.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen HP Vertica mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión HP Vertica válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a HP Vertica mediante la API de servicio de flujo.

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a su instancia de HP Vertica. El patrón de cadena de conexión para HP Vertica es `Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>` |

Para obtener más información sobre cómo empezar, consulte [este documento](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)HP Vertica.

## Conectar la cuenta de HP Vertica

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para crear una nueva cuenta de HP Vertica para conectarse a Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear una cuenta de entrada y cada origen muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría *[!UICONTROL Bases de datos]* , seleccione **[!UICONTROL HP Vertica]** y haga clic **en el icono + (+)** para crear un nuevo conector HP Vertica.

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

Aparece la página *[!UICONTROL Conectar con HP Vertica]* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión con un nombre, una descripción opcional y sus credenciales de HP Vertica. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva cuenta.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de HP Vertica con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de HP Vertica. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/databases.md).