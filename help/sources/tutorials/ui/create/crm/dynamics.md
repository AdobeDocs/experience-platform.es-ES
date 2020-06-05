---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Microsoft Dynamics en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# Creación de un conector de origen de Microsoft Dynamics en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten transferir datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen de Microsoft Dynamics (en adelante denominado &quot;Dynamics&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una cuenta de Dynamics válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La dirección URL del servicio de la instancia de Dynamics. |
| `username` | El nombre de usuario de su cuenta de usuario de Dynamics. |
| `password` | La contraseña de su cuenta de Dynamics. |

Para obtener más información sobre cómo empezar, visite [este documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)de Dynamics.

## Conectar la cuenta de Dynamics

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de Dynamics para conectarse a Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear una cuenta de entrada y cada origen muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría *[!UICONTROL Bases de datos]* , seleccione **[!UICONTROL Dinámica]** y haga clic **en el icono + (+)** para crear un nuevo conector de Dynamics.

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Aparece la página *[!UICONTROL Conectar con Dynamics]* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión con un nombre, una descripción opcional y sus credenciales de Dynamics. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva cuenta.

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Dynamics con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de Dynamics. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/crm.md).