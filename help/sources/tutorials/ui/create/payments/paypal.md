---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de PayPal en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---


# Creación de un conector [!DNL PayPal] de origen en la interfaz de usuario

>[!NOTE]
> El [!DNL PayPal] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de [!DNL PayPal] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL PayPal] base, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL PayPal] cuenta [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Dirección URL de la [!DNL PayPal] instancia. |
| `clientID` | ID de cliente asociado a la [!DNL PayPal] aplicación. |
| `clientSecret` | El secreto de cliente asociado a la [!DNL PayPal] aplicación. |

Para obtener más información sobre cómo empezar, consulte este documento de [PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conectar su [!DNL PayPal] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada con la que vincular la [!DNL PayPal] cuenta a [!DNL Platform].

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *[!UICONTROL CRM]* , seleccione **[!UICONTROL PayPal]** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **[!UICONTROL de]** Connect.

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

Aparece la página *[!UICONTROL Conectar con PayPal]* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y sus [!DNL PayPal] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL PayPal] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión de base con su [!DNL PayPal] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar datos CRM a Platform](../../dataflow/payments.md).