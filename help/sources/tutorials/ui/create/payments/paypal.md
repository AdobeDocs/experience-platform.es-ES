---
keywords: Experience Platform;home;popular topics;paypal;Paypal
solution: Experience Platform
title: Creación de un conector de origen de PayPal en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un conector de origen de PayPal mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Creación de un conector [!DNL PayPal] de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL PayPal] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de [!DNL PayPal] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [!DNL PayPal] [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL PayPal] cuenta [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | The URL of the [!DNL PayPal] instance. |
| `clientID` | ID de cliente asociado a la [!DNL PayPal] aplicación. |
| `clientSecret` | El secreto de cliente asociado a la [!DNL PayPal] aplicación. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conectar su [!DNL PayPal] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL PayPal] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Pagos]** , seleccione **[!UICONTROL PayPal]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo [!DNL PayPal] conector.

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

Aparece la página **[!UICONTROL Conectar con PayPal]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL PayPal] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL PayPal] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su [!DNL PayPal] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incluir [!DNL Platform]](../../dataflow/payments.md)datos de pago.