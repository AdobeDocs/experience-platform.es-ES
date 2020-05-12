---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Azure Data Lake Almacenamiento Gen2 en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 799445eca080175e2bffc49c6714f0c812b9bbea
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Creación de un conector de origen de Azure Data Lake Almacenamiento Gen2 en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para autenticar un conector de origen de Azure Data Lake Almacenamiento Gen2 (en adelante, &quot;ADLS Gen2&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión base ADLS Gen2, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen ADLS Gen2, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | Extremo para ADLS Gen2. |
| `servicePrincipalId` | El ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene la aplicación. |

Para obtener más información sobre estos valores, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

## Conectar la cuenta de ADLS Gen2

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular su cuenta de ADLS Gen2 a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La ficha *Catálogo* muestra una serie de orígenes para los que se pueden utilizar para crear conexiones base de entrada. Cada origen muestra el número de conexiones base existentes asociadas a ellas.

En la categoría *Cloud Almacenamiento* , seleccione **Azure Data Lake Gen2** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la vista de origen de la misma. Para crear una nueva conexión base de entrada, haga clic en **Conectar origen**.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Aparece el cuadro de diálogo *Conectar con Azure Data Lake Gen2* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de ADLS Gen2. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta ADLS Gen2 con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base con su cuenta de ADLS Gen2. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento de nube a la plataforma](../../dataflow/batch/cloud-storage.md).