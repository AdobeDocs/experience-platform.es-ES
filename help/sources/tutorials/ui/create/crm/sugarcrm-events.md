---
title: Crear una conexión de origen de eventos de SugarCRM en la interfaz de usuario
description: Aprenda a crear una conexión de origen de eventos de SugarCRM mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL SugarCRM Events] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL SugarCRM Events] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL SugarCRM] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar credenciales necesarias

Para conectar [!DNL SugarCRM Events] a Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Host` | El punto final de la API de SugarCRM al que se conecta el origen. | `developer.salesfusion.com` |
| `Username` | Su nombre de usuario de cuenta de desarrollador de SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Contraseña de su cuenta de desarrollador de SugarCRM. | `123456789` |

### Crear un esquema de plataforma para [!DNL SugarCRM]

Antes de crear una conexión de origen de [!DNL SugarCRM], también debe asegurarse de crear primero un esquema de Platform para utilizarlo en el origen. Consulte el tutorial de [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para ver los pasos detallados sobre cómo crear un esquema.

![Captura de pantalla de IU de Platform que muestra un esquema de ejemplo para SugarCRM Events](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Al asignar el esquema, asegúrese de asignar también los campos obligatorios `event_id` y `timestamp` requeridos por Platform.

## Conectar su cuenta de [!DNL SugarCRM Events]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *CRM*, seleccione **[!UICONTROL Eventos de SugarCRM]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![Captura de pantalla de la interfaz de usuario de Platform para el catálogo con SugarCRM Events card](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de eventos de SugarCRM]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL SugarCRM Events] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la IU de Platform para conectar la cuenta de eventos de SugarCRM con una cuenta existente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Captura de pantalla de la IU de Platform para conectar la cuenta de eventos de SugarCRM con una nueva cuenta](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL SugarCRM Events]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en la plataforma](../../dataflow/crm.md).

## Recursos adicionales

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al usar el origen [!DNL SugarCRM].

### Mecanismos de protección {#guardrails}

Las velocidades de aceleración de API [!DNL SugarCRM] son de 90 llamadas por minuto o 2000 llamadas por día, lo que suceda primero. Sin embargo, esta restricción se ha eludido añadiendo un parámetro a la especificación de conexión que retrasará el tiempo de solicitud para que nunca se alcance el límite de velocidad.

### Validación {#validation}

Para comprobar que ha configurado correctamente el origen y que se están ingiriendo los datos de [!DNL SugarCRM Events], siga los pasos a continuación:

* En la interfaz de usuario de Platform, seleccione **[!UICONTROL Ver flujos de datos]** junto al menú de tarjeta [!DNL SugarCRM Events] en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Previsualizar conjunto de datos]** para verificar los datos ingeridos.

* Según el tipo de objeto con el que esté trabajando, puede comprobar los datos agregados con los recuentos visibles en la página [!DNL SugarMarket] eventos a continuación:

![Captura de pantalla de la página de cuentas de SugarMarket que muestra la lista de cuentas](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Las páginas [!DNL SugarMarket] no incluyen los recuentos de objetos eliminados. Sin embargo, los datos recuperados a través de esta fuente también incluirán el recuento eliminado, que se marcaría con un indicador eliminado.
