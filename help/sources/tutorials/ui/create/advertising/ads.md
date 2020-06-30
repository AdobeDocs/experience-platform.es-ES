---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Google AdWords en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Creación de un conector [!DNL Google AdWords] de origen en la interfaz de usuario

>[!NOTE]
>El [!DNL Google AdWords] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de [!DNL Google AdWords] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Google AdWords] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Google AdWords] cuenta [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | ID de cliente de la cuenta de AdWords. |
| `developerToken` | El testigo del programador asociado a la cuenta del administrador. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] para autorizar el acceso a AdWords. |
| `clientId` | El ID de cliente de la [!DNL Google] aplicación utilizada para adquirir el autentificador de actualización. |
| `clientSecret` | El secreto de cliente de la [!DNL Google] aplicación que se utiliza para adquirir el autentificador de actualización. |

Para obtener más información sobre cómo empezar, consulte este documento [de AdWords de](https://developers.google.com/adwords/api/docs/guides/authentication)Google.

## Conectar su [!DNL Google AdWords] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada con la que vincular la [!DNL Google AdWords] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *[!UICONTROL Publicidad]* , seleccione **[!UICONTROL Google AdWords]** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **[!UICONTROL de]** Connect.

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

Aparece la página *[!UICONTROL Conectar con Google AdWords]* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y sus [!DNL Google AdWords] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Google AdWords] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión de base con su [!DNL Google AdWords] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incluir datos de publicidad en Platform](../../dataflow/advertising.md).