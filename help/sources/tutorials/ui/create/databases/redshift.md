---
title: Conectar AWS Redshift A Experience Platform Mediante La Interfaz De Usuario
description: Aprenda a conectar una cuenta de AWS Redshift a Experience Platform mediante la interfaz de usuario de fuentes.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# Conectar [!DNL AWS Redshift] a Experience Platform mediante la interfaz de usuario

>[!IMPORTANT]
>
>El origen [!DNL AWS Redshift] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL AWS Redshift] a Adobe Experience Platform mediante la interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL AWS Redshift] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

Seleccione **[!DNL AWS Redshift]** en la categoría *[!UICONTROL Bases de datos]* y luego seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con la tarjeta de origen AWS Redshift seleccionada.](../../../../images/tutorials/create/redshift/catalog.png)

## Usar una cuenta existente {#existing}

A continuación, se le redirige al paso de autenticación del flujo de trabajo de fuentes. Aquí puede usar una cuenta existente o crear una nueva cuenta.

Para usar una cuenta existente, seleccione la cuenta [!DNL AWS Redshift] del directorio de cuentas y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![El directorio de cuentas en el flujo de trabajo de orígenes donde se enumeran las cuentas existentes.](../../../../images/tutorials/create/redshift/existing.png)

## Crear una nueva cuenta {#create}

Si no tiene una cuenta existente, debe crear una nueva cuenta proporcionando las credenciales de autenticación necesarias que se correspondan con su origen.

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y, a continuación, proporciona un nombre y, opcionalmente, agrega una descripción para tu cuenta.

### Conectarse a Experience Platform en Azure {#azure}

Para conectar su cuenta de [!DNL AWS Redshift] a Experience Platform en Azure, proporcione las credenciales de autenticación en el formulario de entrada y, a continuación, seleccione **([!UICONTROL Conectarse al origen])**.

![La nueva interfaz de cuenta para conectar AWS Redshift a Experience Platform en Azure.](../../../../images/tutorials/create/redshift/new.png)

| Credencial | Descripción |
| --- | --- |
| Servidor | El nombre del servidor de su instancia [!DNL AWS Redshift]. |
| Puerto | El puerto TCP que usa un servidor [!DNL AWS Redshift] para detectar conexiones de cliente. |
| Nombre de usuario | El nombre de usuario de la cuenta a la que desea dar acceso. |
| Contraseña | La contraseña que corresponde a la cuenta de usuario. |
| Base de datos | Base de datos [!DNL AWS Redshift] de la que se van a obtener datos. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL AWS Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Conectarse a Experience Platform en AWS {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en AWS Web Services (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Para crear una nueva cuenta de [!DNL AWS Redshift] y conectarse a Experience Platform en AWS, asegúrese de que se encuentra en una zona protegida de VA6, proporcione las credenciales necesarias para la autenticación y, a continuación, seleccione **[!UICONTROL Conectarse al origen]**.

![La nueva interfaz de cuenta para conectar AWS Redshift a Experience Platform en AWS.](../../../../images/tutorials/create/redshift/aws-auth.png)

| Credencial | Descripción |
| --- | --- |
| Servidor | El nombre del servidor de su instancia [!DNL AWS Redshift]. |
| Puerto | El puerto TCP que usa un servidor [!DNL AWS Redshift] para detectar conexiones de cliente. |
| Nombre de usuario | El nombre de usuario de la cuenta a la que desea dar acceso. |
| Contraseña | La contraseña que corresponde a la cuenta de usuario. |
| Base de datos | Base de datos [!DNL AWS Redshift] de la que se van a obtener datos. |
| Esquema | Nombre del esquema asociado con la base de datos [!DNL AWS Redshift]. Debe asegurarse de que el usuario al que desea otorgar acceso a la base de datos también tenga acceso a este esquema. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL AWS Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión entre la base de datos [!DNL AWS Redshift] y Experience Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para introducir datos de su base de datos en Experience Platform](../../dataflow/databases.md).