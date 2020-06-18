---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen MariaDB en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Creación de un conector de origen MariaDB en la interfaz de usuario

> [!NOTE]
> El conector MariaDB está en fase beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen Maria DB mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión base de base de base de base de datos Maria, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta de Maria DB en Platform, debe proporcionar el siguiente valor:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada con la autenticación MariaDB. El patrón de cadena de conexión MariaDB es: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

Consulte [este documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/) para obtener más información sobre cómo empezar a usar MariaDB.

## Conectar la cuenta de Maria DB

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular su cuenta de Maria DB a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *Bases* de datos, seleccione **Maria DB** para mostrar una barra de información en la parte derecha de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **de** Connect.

![](../../../../images/tutorials/create/maria-db/catalog.png)

Aparece la página *Conectar con Maria DB* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de Maria DB. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/maria-db/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Maria DB con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![](../../../../images/tutorials/create/maria-db/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base con su cuenta de Maria DB. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/databases.md).