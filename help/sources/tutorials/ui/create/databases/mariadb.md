---
title: Conecte MariaDB a Experience Platform usando el IU
description: Aprenda a conectar su cuenta MariaDB a Experience Platform utilizando las fuentes espacio de trabajo en la interfaz de Experience Platform usuario.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Conéctese [!DNL MariaDB] a Experience Platform mediante el IU

Lea este guía para aprender a conectar su [!DNL MariaDB] cuenta a Adobe Experience Platform utilizando las fuentes espacio de trabajo en la interfaz de Experience Platform usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado por el cual Experience Platform organiza experiencia del cliente datos.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) esquema: aprenda sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición esquema.
   * [Editor de esquemas tutorial](../../../../../xdm/tutorials/create-schema-ui.md): aprenda a crear esquemas personalizados mediante el Editor de esquemas IU.
* [Perfil](../../../../../profile/home.md) del cliente en tiempo real: proporciona un perfil del consumidor unificado y en tiempo real basado en datos agregados de múltiples fuentes.

Si ya tiene una [!DNL MariaDB] conexión, puede omitir el resto de este documento y continuar con la tutorial de [configuración de un flujo](../../dataflow/databases.md) de datos.

### Recopile las credenciales necesarias

Lea la descripción general](../../../../connectors/databases/mariadb.md#prerequisites) para obtener información sobre la [[!DNL MariaDB] autenticación.

## Navegar por el catálogo de orígenes

En el IU Experience Platform, seleccione **[!UICONTROL Orígenes]** en el navegación izquierdo para acceder *[!UICONTROL al espacio de trabajo Orígenes]* . Seleccione el categoría adecuado en el *[!UICONTROL panel Categorías]* También puede utilizar la barra búsqueda para desplazarse hasta el origen específico que desee utilizar.

Para usar [!DNL MariaDB], seleccione el **[!UICONTROL tarjeta de origen MariaDB]** en *[!UICONTROL Bases de datos y, a continuación, seleccione **[!UICONTROL Configurar]*]**.

>[!TIP]
>
>Las fuentes del catálogo de fuentes muestran la **[!UICONTROL opción Configurar]** cuando una fuente determinada aún no tiene un cuenta autenticado. Una vez que se crea un cuenta autenticado, esta opción cambia a **[!UICONTROL añadir datos]**.

![El catálogo de fuentes en el IU con el tarjeta MariaDB seleccionado.](../../../../images/tutorials/create/maria-db/catalog.png)

## Utilizar un cuenta existente {#existing}

Para utilizar un cuenta existente, seleccione **[!UICONTROL cuenta]** existente y, a continuación, seleccione el [!DNL MariaDB] cuenta que desea utilizar.

![La interfaz de cuentas existentes en los orígenes flujo de trabajo con la opción &quot;cuenta existente&quot; seleccionada.](../../../../images/tutorials/create/maria-db/existing.png)

## Crear una nueva cuenta {#create}

Si no tiene un cuenta existente, debe crear un nuevo cuenta proporcionando las credenciales de autenticación necesarias que correspondan con su origen.

Para crear un nuevo cuenta, seleccione **[!UICONTROL Nuevo cuenta]** y, a continuación, proporcione un nombre y, opcionalmente, agregue una descripción para su cuenta.

![La nueva interfaz cuenta de los orígenes flujo de trabajo con un nombre cuenta y una descripción opcional.](../../../../images/tutorials/create/maria-db/new.png)

### Connect to Experience Platform on Azure {#azure}

Puede conectar su [!DNL MariaDB] cuenta a Experience Platform en Azure mediante cuenta clave o autenticación básica.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para usar cuenta autenticación de clave, seleccione **[!UICONTROL Autenticación]** de clave de cuenta, proporcione la [cadena](../../../../connectors/databases/mariadb.md#azure) de conexión y, a continuación, seleccione **[!UICONTROL Conectar al origen]**.

![La nueva interfaz cuenta de los orígenes flujo de trabajo con la opción &quot;Autenticación de clave de cuenta&quot; seleccionada.](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB Autenticación básica]

Para usar la autenticación básica, seleccione **[!UICONTROL Autenticación]** básica, proporcione valores para sus [credenciales](../../../../connectors/databases/mariadb.md#azure) de autenticación y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**.

![La nueva interfaz cuenta en los orígenes flujo de trabajo con la opción &quot;Autenticación básica&quot; seleccionada.](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

### Conéctese a Experience Platform en Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Services (AWS). Experience Platform que se ejecutan en AWS están disponibles actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura Experience Platform compatible, consulte la Experience Platform información general](../../../../../landing/multi-cloud.md) sobre varios [nube.

Para crear un nuevo [!DNL MariaDB] cuenta y conectarse a Experience Platform en AWS, asegúrese de estar en un entorno de pruebas VA6 y, a continuación, proporcione las credenciales necesarias [para la autenticación](../../../../connectors/databases/mariadb.md#aws).

![La nueva interfaz de cuenta en los orígenes flujo de trabajo para conectarse a AWS.](../../../../images/tutorials/create/maria-db/basic-auth.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL MariaDB] cuenta. Ahora puede continuar con la siguiente tutorial y [configurar un flujo de datos para llevar los datos a Experience Platform](../../dataflow/databases.md).
