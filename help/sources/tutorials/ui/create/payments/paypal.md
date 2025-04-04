---
keywords: Experience Platform;inicio;temas populares;PayPal;PayPal
solution: Experience Platform
title: Creación de una conexión de Source con PayPal en la IU
type: Tutorial
description: Aprenda a crear una conexión de origen de PayPal mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL PayPal] en la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL PayPal] quedará obsoleto a finales de junio de 2025.

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL PayPal] mediante la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL PayPal] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar credenciales necesarias

Para tener acceso a la Experience Platform de su cuenta de [!DNL PayPal], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Dirección URL de la instancia [!DNL PayPal]. |
| `clientID` | Identificador de cliente asociado con la aplicación [!DNL PayPal]. |
| `clientSecret` | Secreto de cliente asociado a la aplicación [!DNL PayPal]. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conectar su cuenta de [!DNL PayPal]

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de [!DNL PayPal] a Experience Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Pagos]**, selecciona **[!UICONTROL PayPal]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL PayPal].

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con PayPal]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL PayPal]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/paypal/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL PayPal] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL PayPal]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de pago en Experience Platform](../../dataflow/payments.md).
