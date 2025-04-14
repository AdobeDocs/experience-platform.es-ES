---
title: Conexión De MariaDB A Experience Platform Mediante La Interfaz De Usuario
description: Obtenga información sobre cómo conectar su cuenta de MariaDB a Experience Platform mediante el espacio de trabajo de fuentes en la interfaz de usuario de Experience Platform.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Conectar [!DNL MariaDB] a Experience Platform mediante la interfaz de usuario

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL MariaDB] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.

Si ya tiene una conexión de [!DNL MariaDB], puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Lea la [[!DNL MariaDB] descripción general](../../../../connectors/databases/mariadb.md#prerequisites) para obtener información sobre la autenticación.

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Seleccione la categoría adecuada en el panel *[!UICONTROL Categorías]*. También puede usar la barra de búsqueda para ir al origen específico que desee usar.

Para usar [!DNL MariaDB], seleccione la tarjeta de origen **[!UICONTROL MariaDB]** en *[!UICONTROL Bases de datos]* y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes de la interfaz de usuario con la tarjeta MariaDB seleccionada.](../../../../images/tutorials/create/maria-db/catalog.png)

## Usar una cuenta existente {#existing}

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL MariaDB] que desee usar.

![Interfaz de cuentas existentes en el flujo de trabajo de orígenes con la opción Cuenta existente seleccionada.](../../../../images/tutorials/create/maria-db/existing.png)

## Crear una nueva cuenta {#create}

Si no tiene una cuenta existente, debe crear una nueva cuenta proporcionando las credenciales de autenticación necesarias que se correspondan con su origen.

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y, a continuación, proporciona un nombre y, opcionalmente, agrega una descripción para tu cuenta.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes con un nombre de cuenta y una descripción opcional proporcionados.](../../../../images/tutorials/create/maria-db/new.png)

### Conectarse a Experience Platform en Azure {#azure}

Puede conectar su cuenta de [!DNL MariaDB] a Experience Platform en Azure mediante la clave de cuenta o la autenticación básica.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para usar la autenticación de clave de cuenta, selecciona **[!UICONTROL Autenticación de clave de cuenta]**, proporciona tu [cadena de conexión](../../../../connectors/databases/mariadb.md#azure) y, a continuación, selecciona **[!UICONTROL Conectarse al origen]**.

![Nueva interfaz de cuenta en el flujo de trabajo de orígenes con la opción &quot;Autenticación de clave de cuenta&quot; seleccionada.](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB Autenticación básica]

Para usar la autenticación básica, selecciona **[!UICONTROL Autenticación básica]**, proporciona valores para tus [credenciales de autenticación](../../../../connectors/databases/mariadb.md#azure) y, a continuación, selecciona **[!UICONTROL Conectarse al origen]**.

![Nueva interfaz de cuenta en el flujo de trabajo de orígenes con la opción Autenticación básica seleccionada.](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

### Conexión a Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Para crear una nueva cuenta de [!DNL MariaDB] y conectarse a Experience Platform en AWS, asegúrese de estar en una zona protegida de VA6 y, a continuación, proporcione las [credenciales necesarias para la autenticación](../../../../connectors/databases/mariadb.md#aws).

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes para conectarse a AWS.](../../../../images/tutorials/create/maria-db/basic-auth.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL MariaDB]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Experience Platform](../../dataflow/databases.md).
