---
title: Conecte su cuenta de Salesforce Marketing Cloud a Experience Platform a través de la interfaz de usuario de
description: Obtenga información sobre cómo conectar su cuenta de Salesforce Marketing Cloud a Experience Platform a través de la interfaz de usuario.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Conecte su cuenta de [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto en enero de 2026. Una nueva fuente se publicará a finales de este año como alternativa. Una vez lanzada la nueva fuente, debe planificar la migración a la nueva fuente creando nuevas conexiones de cuenta y flujos de datos antes de finales de enero de 2026.

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario de Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Salesforce Marketing Cloud], puede omitir el resto de este documento y continuar con el tutorial de [introducción de datos de automatización de marketing en Experience Platform mediante la interfaz de usuario](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Lea la [[!DNL Salesforce Marketing Cloud] descripción general](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites) para obtener información sobre la autenticación.

## Navegar por el catálogo de fuentes

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.


En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectar con [!DNL Salesforce Marketing Cloud], ve a la categoría *[!UICONTROL Automatización de mercadotecnia]*, selecciona la tarjeta de origen de **[!UICONTROL Salesforce Marketing Cloud]** y, a continuación, selecciona **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con la tarjeta de origen Marketing Cloud de Salesforce seleccionada.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## Usar una cuenta existente {#existing}

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL Salesforce Marketing Cloud] que desee usar.

![Interfaz de cuentas existentes en el flujo de trabajo de orígenes con la opción Cuenta existente seleccionada.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Crear una nueva cuenta {#new}

Puede usar el origen [!DNL Salesforce Marketing Cloud] para conectarse a Experience Platform en [!DNL Azure] o [!DNL Amazon Web Services] (AWS).

### Conectar con Experience Platform en [!DNL Azure] {#azure}

Para conectarse a Experience Platform en [!DNL Azure], proporcione un nombre de cuenta, una descripción opcional y sus [credenciales de autenticación de cuenta](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure). Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes para la conexión a Experience Platform en Azure.](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### Conexión a Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Para conectarse a Experience Platform en [!DNL AWS], asegúrese de que se encuentra en una zona protegida de VA6 y proporcione un nombre de cuenta, una descripción opcional y sus [credenciales de autenticación de cuenta](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws). Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes para la conexión a Experience Platform en AWS](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## Crear un flujo de datos para [!DNL Salesforce Marketing Cloud] datos

Ahora que ha conectado correctamente su [!DNL Salesforce Marketing Cloud] , puede [crear un flujo de datos e introducir datos de su proveedor de automatización de marketing en Experience Platform](../../dataflow/marketing-automation.md).
