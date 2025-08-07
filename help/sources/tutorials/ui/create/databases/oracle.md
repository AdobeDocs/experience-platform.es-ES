---
title: Conexión De Oracle DB A Experience Platform Mediante La IU
description: Obtenga información sobre cómo conectar la instancia de Oracle DB a Experience Platform mediante la interfaz de usuario.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Crear una conexión de origen [!DNL Oracle DB] en la interfaz de usuario

Lea esta guía para obtener información sobre cómo conectar la instancia de [!DNL Oracle DB] a Adobe Experience Platform mediante el espacio de trabajo de orígenes en la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de [!DNL Oracle DB], puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Lea la [[!DNL Oracle DB] descripción general](../../../../connectors/databases/oracle.md#prerequisites) para obtener información sobre la autenticación.

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectarse a [!DNL Oracle DB], vaya a la categoría *[!UICONTROL Bases de datos]*, seleccione la tarjeta de origen de **[!UICONTROL Oracle DB]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Las fuentes muestran **[!UICONTROL Configurado]** para nuevas conexiones y **[!UICONTROL Agregar datos]** si ya existe una cuenta.

![El catálogo de orígenes con &quot;Oracle DB&quot; seleccionado.](../../../../images/tutorials/create/oracle/catalog.png)

## Usar una cuenta existente {#existing}

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL Oracle DB] que desee usar.

![Interfaz de cuentas existentes en el flujo de trabajo de orígenes con la opción Cuenta existente seleccionada.](../../../../images/tutorials/create/oracle/existing.png)

## Crear una nueva cuenta {#new}

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y, a continuación, proporciona un nombre y, opcionalmente, agrega una descripción para tu cuenta.

### Conectarse a Experience Platform en Azure {#azure}

Puede conectar su base de datos de [!DNL Oracle DB] a Experience Platform en Azure mediante una cadena de conexión.

Para usar la autenticación de cadena de conexión, proporcione su [cadena de conexión](../../../../connectors/databases/oracle.md#azure) y seleccione **[!UICONTROL Conectar con el origen]**.

![Nueva interfaz de cuenta en el flujo de trabajo de orígenes con la opción &quot;Autenticación de cadena de conexión&quot; seleccionada.](../../../../images/tutorials/create/oracle/azure.png)

### Conexión a Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Para crear una nueva cuenta de [!DNL Oracle DB] y conectarse a Experience Platform en AWS, asegúrese de estar en una zona protegida de VA6 y, a continuación, proporcione las [credenciales necesarias para la autenticación](../../../../connectors/databases/oracle.md#aws).

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes para conectarse a AWS.](../../../../images/tutorials/create/oracle/aws.png)

## Crear un flujo de datos para [!DNL Oracle DB] datos

Ahora que ha conectado correctamente su base de datos de [!DNL Oracle DB], puede [crear un flujo de datos e introducir datos de su base de datos en Experience Platform](../../dataflow/databases.md).
