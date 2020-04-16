---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Microsoft Dynamics o Salesforce en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creación de un conector de origen de Microsoft Dynamics o Salesforce en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten transferir datos CRM de origen externo de forma programada. Este tutorial proporciona pasos para crear un conector de origen de Microsoft Dynamics (en adelante denominado &quot;Dynamics&quot;) o de Salesforce mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión base de Microsoft Dynamics o Salesforce, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta de Dynamics en Platform, debe proporcionar un URI **** de servicio, un **nombre de usuario** y una **contraseña**.

Del mismo modo, el acceso a su cuenta de Salesforce en Platform requiere que proporcione una URL **de** entorno, un **nombre de usuario**, una **contraseña** y un distintivo **de** seguridad.

## Conectar la cuenta de Dynamics o Salesforce

Con las credenciales del sistema CRM listas, puede seguir los pasos a continuación para crear una nueva conexión base de entrada para vincular su cuenta de Dynamics o Salesforce a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo de fuentes. La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *CRM* , seleccione **Microsoft Dynamics** o **Salesforce** para mostrar una barra de información en la parte derecha de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para la vista de la documentación o la conexión con la fuente. Para crear una nueva conexión base de entrada, haga clic en **Conectar origen**.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

En el formulario de entrada, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de Dynamics o Salesforce. Por último, haga clic en **Conectar** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

Una vez establecida la conexión base con el sistema CRM, puede continuar en la siguiente sección y configurar un flujo de datos para llevar los datos CRM a la plataforma.

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base a su cuenta de Dynamics o Salesforce. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/crm.md).