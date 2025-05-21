---
title: Conectar MySQL a Experience Platform mediante la interfaz de usuario
description: Aprenda a conectar la base de datos MySQL a Experience Platform mediante la interfaz de usuario.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Conectar [!DNL MySQL] a Experience Platform mediante la interfaz de usuario

Lea esta guía para obtener información sobre cómo conectar la base de datos de [!DNL MySQL] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de [!DNL MySQL], puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Lea la [[!DNL MySQL] descripción general](../../../../connectors/databases/mysql.md#prerequisites) para obtener información sobre la autenticación.

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectarse a [!DNL MySQL], vaya a la categoría *[!UICONTROL Bases de datos]*, seleccione la tarjeta de origen **[!UICONTROL MySQL]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con la tarjeta de origen MySQL seleccionada.](../../../../images/tutorials/create/my-sql/catalog.png)

## Usar una cuenta existente {#existing}

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL MySQL] que desee usar.

![Interfaz de cuentas existentes en el flujo de trabajo de orígenes con la opción Cuenta existente seleccionada.](../../../../images/tutorials/create/my-sql/existing.png)

## Crear una nueva cuenta {#new}

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y, a continuación, proporciona un nombre y, opcionalmente, agrega una descripción para tu cuenta.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes con un nombre de cuenta y una descripción opcional proporcionados.](../../../../images/tutorials/create/my-sql/new.png)

### Conectarse a Experience Platform en Azure {#azure}

Puede conectar su base de datos de [!DNL MySQL] a Experience Platform en Azure mediante la clave de cuenta o la autenticación básica.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para usar la autenticación de clave de cuenta, selecciona **[!UICONTROL Autenticación de clave de cuenta]**, proporciona tu [cadena de conexión](../../../../connectors/databases/mysql.md#azure) y, a continuación, selecciona **[!UICONTROL Conectarse al origen]**.

![Nueva interfaz de cuenta en el flujo de trabajo de orígenes con la opción &quot;Autenticación de clave de cuenta&quot; seleccionada.](../../../../images/tutorials/create/my-sql/account-key.png)

>[!TAB Autenticación básica]

Para usar la autenticación básica, selecciona **[!UICONTROL Autenticación básica]**, proporciona valores para tus [credenciales de autenticación](../../../../connectors/databases/mysql.md#azure) y, a continuación, selecciona **[!UICONTROL Conectarse al origen]**.

![Nueva interfaz de cuenta en el flujo de trabajo de orígenes con la opción Autenticación básica seleccionada.](../../../../images/tutorials/create/my-sql/basic-auth.png)

>[!ENDTABS]

### Conexión a Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Para crear una nueva cuenta de [!DNL MySQL] y conectarse a Experience Platform en AWS, asegúrese de estar en una zona protegida de VA6 y, a continuación, proporcione las [credenciales necesarias para la autenticación](../../../../connectors/databases/mysql.md#aws).

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes para conectarse a AWS.](../../../../images/tutorials/create/my-sql/aws.png)

## Crear un flujo de datos para [!DNL MySQL] datos

Ahora que ha conectado correctamente su base de datos de [!DNL MySQL], puede [crear un flujo de datos e introducir datos de su base de datos en Experience Platform](../../dataflow/databases.md).
