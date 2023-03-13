---
keywords: Experience Platform;inicio;temas populares;PayPal;PayPal
solution: Experience Platform
title: Creación de una conexión de origen de PayPal en la IU
type: Tutorial
description: Aprenda a crear una conexión de origen de PayPal mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Crear un [!DNL PayPal] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL PayPal] conector de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL PayPal] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar credenciales necesarias

Para acceder a su [!DNL PayPal] En la plataforma de cuenta de, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección URL del [!DNL PayPal] ejemplo. |
| `clientID` | El ID de cliente asociado con su [!DNL PayPal] aplicación. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL PayPal] aplicación. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conecte su [!DNL PayPal] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL PayPal] a Platform.

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Pagos]** categoría, seleccionar **[!UICONTROL PayPal]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL PayPal] conector.

![catalogar](../../../../images/tutorials/create/paypal/catalog.png)

El **[!UICONTROL Conectar con PayPal]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL PayPal] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/paypal/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL PayPal] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL PayPal] cuenta. Ahora puede continuar con el siguiente tutorial y [Configuración de un flujo de datos para introducir datos de pago en Platform](../../dataflow/payments.md).
