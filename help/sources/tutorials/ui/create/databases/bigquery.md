---
title: Creación de una conexión de Google Big Query Source en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Google Big Query mediante la interfaz de usuario de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Google BigQuery] en la interfaz de usuario

>[!IMPORTANT]
>
>El origen [!DNL Google BigQuery] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Lea este tutorial para aprender a conectar su cuenta de [!DNL Google BigQuery] a Adobe Experience Platform mediante la interfaz de usuario.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Google BigQuery] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Lea la [[!DNL Google BigQuery] guía de autenticación](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) para ver los pasos detallados sobre cómo recopilar las credenciales requeridas.

## Conecte su cuenta de Google BigQuery

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL Bases de datos], seleccione **[!UICONTROL Google BigQuery]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con Google BigQuery seleccionado.](../../../../images/tutorials/create/google-big-query/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a Google Big Query]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL Google BigQuery] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Página de la cuenta existente donde se presenta una lista de cuentas existentes.](../../../../images/tutorials/create/google-big-query/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva cuenta de [!DNL Google BigQuery].

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB Usar autenticación básica]

Para usar la autenticación básica, selecciona **[!UICONTROL Autenticación básica]** y proporciona valores para tu [proyecto, ID de cliente, secreto de cliente, token de actualización y (opcional) conjunto de datos de resultados grandes](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

![Interfaz de la nueva cuenta donde se ha seleccionado la autenticación básica.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB Usar autenticación de servicio]

Para usar la autenticación del servicio, selecciona **[!UICONTROL Autenticación del servicio]** y proporciona valores para tu [ID de proyecto, contenido de archivos de claves y (opcional) ID de conjuntos de datos de resultados grandes](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

![Interfaz de la nueva cuenta donde se ha seleccionado la autenticación del servicio.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

### Omitir vista previa de datos de ejemplo {#skip-preview-of-sample-data}

Durante el paso de selección de datos, puede encontrar un tiempo de espera al ingerir tablas o archivos de datos grandes. Puede omitir la previsualización de datos para evitar el tiempo de espera y seguir viendo el esquema, aunque sin datos de ejemplo. Para omitir la vista previa de datos, active la opción **[!UICONTROL Omitir vista previa de datos de ejemplo]**.

El resto del flujo de trabajo sigue siendo el mismo. La única advertencia es que omitir la previsualización de datos puede impedir que los campos calculados y requeridos se validen automáticamente durante el paso de asignación y, a continuación, tendrá que validar manualmente esos campos durante la asignación.

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Google BigQuery]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en la plataforma](../../dataflow/databases.md).
