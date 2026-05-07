---
title: Conectar su cuenta de Salesforce Service Cloud mediante la interfaz de usuario de Experience Platform
description: Obtenga información sobre cómo conectar su cuenta de Salesforce Service Cloud y llevar los datos de éxito de los clientes a Experience Platform mediante la interfaz de usuario.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# Conecte su cuenta de [!DNL Salesforce Service Cloud] a Experience Platform mediante la interfaz de usuario

Siga esta guía paso a paso para conectar sin problemas su cuenta de [!DNL Salesforce Service Cloud] e importar los datos de éxito de los clientes en Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Salesforce Service Cloud] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para que el cliente se realice correctamente](../../dataflow/customer-success.md)

### Recopilar credenciales necesarias

Lea la [guía de autenticación](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials) para obtener más información sobre cómo recuperar sus credenciales.

## Conectar su cuenta de [!DNL Salesforce Service Cloud]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

Seleccione **[!DNL Salesforce Service Cloud]** en la categoría *[!UICONTROL Customer success]* y luego seleccione **[!UICONTROL Add data]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Add data]**.

![El catálogo de orígenes en la interfaz de usuario de Experience Platform con la tarjeta de origen de Salesforce Service Cloud seleccionada.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Aparecerá la página **[!UICONTROL Connect to Salesforce Service Cloud]**. En esta página, puede usar credenciales nuevas o existentes.

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Existing account]** y luego seleccione la cuenta que desee en la lista que aparece. Cuando termine, seleccione **[!UICONTROL Next]** para continuar.

![Una lista de cuentas autenticadas de Salesforce Service Cloud que ya existen en su organización.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Crear una nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL New account]** y proporcione un nombre y una descripción para la nueva cuenta de [!DNL Salesforce Service Cloud]. A continuación, seleccione **[!UICONTROL OAuth2 Client Credential]** y proporcione valores para las siguientes credenciales:

* URL de entorno
* ID de cliente
* Secreto del cliente
* Versión de API

Cuando termine, seleccione **[!UICONTROL Connect to source]**.

![Interfaz de OAuth para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

## Próximos pasos

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Salesforce Service Cloud]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar los datos de éxito del cliente a Experience Platform](../../dataflow/customer-success.md).
