---
title: Conexión de Pega Customer Decision Hub
description: Utilice el destino del centro de decisiones del cliente de Pega en Adobe Experience Platform para enviar atributos de perfil y datos de pertenencia a audiencias al centro de decisiones del cliente de Pega para la toma de decisiones de la mejor acción siguiente.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 3%

---

# Conexión de Pega Customer Decision Hub

## Información general {#overview}

Use el destino [!DNL Pega Customer Decision Hub] en Adobe Experience Platform para enviar atributos de perfil y datos de pertenencia a audiencias a [!DNL Pega Customer Decision Hub] para la toma de decisiones de la mejor acción siguiente.

El abono a audiencia de perfil de Adobe Experience Platform, cuando se carga en [!DNL Pega Customer Decision Hub], puede usarse como predictor en modelos adaptables y ayudar a entregar los datos contextuales y de comportamiento adecuados para la toma de decisiones de la siguiente mejor acción.

>[!IMPORTANT]
>
>Pegasystems crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con Pega [aquí](mailto:support@pega.com).

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Customer Decision Hub], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Telecomunicaciones

Un experto en marketing desea aprovechar las perspectivas de la siguiente mejor acción basada en el modelo de ciencia de datos según lo entregado por [!DNL Pega Customer Decision Hub] para la participación de los clientes. [!DNL Pega Customer Decision Hub] depende en gran medida de la intención del cliente; por ejemplo, &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; o &quot;Interest_in_iPhone_Accessories&quot;.

### Servicios financieros

Un experto en marketing desea optimizar las ofertas para los clientes que se suscribieron o cancelaron su suscripción a los boletines del Plan de pensiones o del Plan de jubilación. Las empresas de servicios financieros pueden ingerir varios ID de cliente desde sus propios CRM en Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar perfiles que entren y salgan de las audiencias a [!DNL Pega Customer Decision Hub] para la toma de decisiones de la mejor acción siguiente (NBA) en los canales salientes.

## Requisitos previos {#prerequisites}

Antes de poder usar este destino para exportar datos desde Adobe Experience Platform, asegúrese de completar los siguientes requisitos previos en [!DNL Pega Customer Decision Hub]:

* Configure [el perfil de Adobe Experience Platform y el componente de integración de pertenencia a audiencias](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) en su instancia de [!DNL Pega Customer Decision Hub].
* Configurar el registro de cliente OAuth 2.0 [mediante credenciales de cliente](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) tipo de concesión en su instancia [!DNL Pega Customer Decision Hub].
* Configure [flujo de datos en tiempo real](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) para el flujo de datos de pertenencia a audiencias de Adobe en su instancia de [!DNL Pega Customer Decision Hub].

## Identidades admitidas {#supported-identities}

[!DNL Pega Customer Decision Hub] admite la activación de los identificadores de usuario personalizados que se describen en la tabla siguiente. Para obtener más información, consulte [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| *CustomerID* | Identificador de usuario común que identifica de manera única un perfil en [!DNL Pega Customer Decision Hub] y Adobe Experience Platform |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Exportar todos los miembros de una audiencia con el identificador (*CustomerID*), atributos (apellidos, nombre, ubicación, etc.) y datos de pertenencia a audiencias. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas siempre en API. Tan pronto como se actualiza un perfil en Experience Platform, según la evaluación de audiencia, el conector envía la actualización de forma descendente a la plataforma de destino. Para obtener más información, consulte [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

#### Autenticación de credenciales de cliente de OAuth 2 {#oauth-2-client-credentials-authentication}

![Imagen de la pantalla de la interfaz de usuario donde puede conectarse al destino Pega CDH mediante OAuth 2 con autenticación de credenciales de cliente](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Rellene los campos siguientes y seleccione **[!UICONTROL Conectar con destino]**:

* **[!UICONTROL URL de token de acceso]**: La URL del token de acceso de OAuth 2 en su instancia de [!DNL Pega Customer Decision Hub].
* **[!UICONTROL ID de cliente]**: el OAuth 2 [!DNL client ID] que generó en su instancia de [!DNL Pega Customer Decision Hub].
* **[!UICONTROL Secreto de cliente]**: El OAuth 2 [!DNL client secret] que generó en su instancia de [!DNL Pega Customer Decision Hub].

### Rellenar detalles de destino {#destination-details}

Después de establecer la conexión de autenticación con [!DNL Pega Customer Decision Hub], proporcione la siguiente información para el destino:

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino de Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Para configurar los detalles del destino, rellena los campos obligatorios y selecciona **[!UICONTROL Siguiente]**.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Nombre de host]**: El nombre de host de Pega Customer Decision Hub al que se exporta el perfil como datos json.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Atributos de destino {#attributes}

En el paso [[!UICONTROL Seleccionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes), Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

### Ejemplo de asignación: activación de actualizaciones de perfil en [!DNL Pega Customer Decision Hub] {#mapping-example}

A continuación se muestra un ejemplo de asignación de identidad correcta al exportar perfiles a [!DNL Pega Customer Decision Hub].

Selección de campos de origen:

* Seleccione un identificador (por ejemplo: CustomerID) como identidad de origen que identifique de forma exclusiva un perfil en Adobe Experience Platform y [!DNL Pega Customer Decision Hub].
* Seleccione los cambios de atributo de perfil de origen de XDM que deben exportarse y actualizarse en [!DNL Pega Customer Decision Hub].

Selección de campos de destino:

* Seleccione el área de nombres `CustomerID` como identidad de destino.
* Seleccione los nombres de atributos de perfil de destino que deben asignarse a los atributos de perfil de origen XDM correspondientes.

![Asignación de identidad](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Una actualización correcta de la pertenencia a audiencias de un perfil insertaría el identificador de audiencia, el nombre y los estados en el almacén de datos de pertenencia a audiencias de marketing de Pega. Los datos de pertenencia están asociados a un cliente que usa Designer de perfil de cliente en [!DNL Pega Customer Decision Hub], como se muestra a continuación.
![Imagen de la pantalla de la interfaz de usuario donde puede asociar datos de pertenencia a audiencias de Adobe con el cliente mediante el Designer de perfil del cliente](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Los datos de pertenencia a audiencias se utilizan en las políticas de participación de Designer de la siguiente mejor acción de Pega para la toma de decisiones de la siguiente mejor acción, como se muestra a continuación.
![Imagen de la pantalla de la interfaz de usuario donde se pueden agregar campos de pertenencia a audiencias como condiciones en las directivas de participación de Pega Next-Best-Action Designer](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Los campos de datos de pertenencia a audiencias del cliente se agregan como predictores en los modelos adaptables, como se muestra a continuación.
![Imagen de la pantalla de la interfaz de usuario donde se pueden agregar campos de pertenencia a audiencias como predicadores en modelos adaptables mediante Prediction Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Recursos adicionales {#additional-resources}

Ver [Configuración de un registro de cliente OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) en [!DNL Pega Customer Decision Hub].

Ver [Creación de una ejecución en tiempo real para flujos de datos](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) en [!DNL Pega Customer Decision Hub].

Consulte [Administrar registros de clientes en el perfil de cliente de Designer](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
