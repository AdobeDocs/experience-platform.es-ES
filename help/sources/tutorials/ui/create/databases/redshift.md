---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen Amazon Redshift en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Creación de un conector [!DNL Amazon Redshift] de origen en la interfaz de usuario

>Las [!NOTE]
>El [!DNL Amazon Redshift] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Amazon Redshift] (en adelante denominado &quot;[!DNL Redshift]&quot;) mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Redshift] base, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Redshift] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| `server` | El servidor asociado a su [!DNL Redshift] cuenta. |
| `username` | El nombre de usuario asociado a su [!DNL Redshift] cuenta. |
| `password` | La contraseña asociada a su [!DNL Redshift] cuenta. |
| `database` | La [!DNL Redshift] base de datos a la que está accediendo. |

Para obtener más información sobre cómo empezar, consulte [este documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)Redshift.

## Conectar su [!DNL Redshift] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada con la que vincular la [!DNL Redshift] cuenta a [!DNL Platform].

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *[!UICONTROL Bases]* de datos, seleccione **[!UICONTROL Amazon Redshift]** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **[!UICONTROL de]** Connect.

![](../../../../images/tutorials/create/redshift/catalog.png)

Aparece la página *[!UICONTROL Conectar con Amazon Redshift]* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y sus [!DNL Redshift] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/redshift/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Redshift] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión de base con su [!DNL Redshift] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/databases.md).