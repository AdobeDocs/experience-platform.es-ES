---
title: Conexión de centro de decisión de clientes pega
description: Utilice el destino de Pega Customer decisions Hub en Adobe Experience Platform para enviar atributos de perfil y datos de pertenencia a segmentos a Pega Customer decisions Hub para la toma de decisiones de la mejor manera de actuar.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ae00b113308354e98f4448d2544e2a6e475c384e
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 1%

---

# Conexión de centro de decisión de clientes pega

## Información general {#overview}

Utilice la variable [!DNL Pega Customer Decision Hub] destino en Adobe Experience Platform para enviar atributos de perfil y datos de pertenencia a segmentos a [!DNL Pega Customer Decision Hub] para la toma de decisiones de la acción siguiente.

Pertenencia a segmentos de perfil desde Adobe Experience Platform, cuando se carga en [!DNL Pega Customer Decision Hub], se puede utilizar como predictor en modelos adaptables y ayudar a proporcionar los datos contextuales y de comportamiento adecuados para las decisiones de acción siguiente.

>[!IMPORTANT]
>
>Esta página de documentación fue creada por Pegasystems. Para cualquier consulta o actualización de solicitudes, contacte directamente con Pega [here](mailto:support@pega.com).

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL Customer Decision Hub] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Telecomunicaciones

Un especialista en marketing desea aprovechar las perspectivas de la siguiente mejor acción basada en el modelo de ciencia de datos que ofrece [!DNL Pega Customer Decision Hub] para la participación del cliente. [!DNL Pega Customer Decision Hub] depende en gran medida de la intención del cliente; por ejemplo, &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; o &quot;Interest_in_iPhone_Accessories&quot;.

### Servicios financieros

Un especialista en mercadotecnia desea optimizar las ofertas para los clientes que se suscribieron o cancelaron la suscripción a los boletines del Plan de Pensiones o del Plan de Jubilación. Las empresas de servicios financieros pueden introducir varios ID de cliente desde sus propios CRM en Adobe Experience Platform, crear segmentos a partir de sus propios datos sin conexión y enviar perfiles que entran y salen de los segmentos a [!DNL Pega Customer Decision Hub] para la toma de decisiones de acción siguiente (NBA) en canales salientes.

## Requisitos previos {#prerequisites}

Antes de usar este destino para exportar datos desde Adobe Experience Platform, asegúrese de completar los siguientes requisitos previos en [!DNL Pega Customer Decision Hub]:

* Configure las variables [Componente de integración de perfil y pertenencia a segmentos de Adobe Experience Platform](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) en su [!DNL Pega Customer Decision Hub] instancia.
* Configuración de OAuth 2.0 [Registro del cliente mediante credenciales del cliente](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) tipo de concesión en su [!DNL Pega Customer Decision Hub] instancia.
* Configurar [flujo de datos en tiempo real](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) para el flujo de datos de pertenencia a segmentos de Adobe en su [!DNL Pega Customer Decision Hub] instancia.

## Identidades compatibles {#supported-identities}

[!DNL Pega Customer Decision Hub] admite la activación de ID de usuario personalizados que se describen en la tabla siguiente. Para obtener más información, consulte [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción |
|---|---|
| *CustomerID* | Identificador de usuario común que identifica de forma exclusiva un perfil en [!DNL Pega Customer Decision Hub] y Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Exportar todos los miembros de un segmento con el identificador (*CustomerID*), atributos (apellidos, nombre, ubicación, etc.) y datos de pertenencia a segmentos. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API. Tan pronto como un perfil se actualiza en Experience Platform, según la evaluación del segmento, el conector envía la actualización descendente a la plataforma de destino. Para obtener más información, consulte [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

#### Autenticación de credenciales de cliente de OAuth 2 {#oauth-2-client-credentials-authentication}

![Imagen de la pantalla de la interfaz de usuario en la que puede conectarse al destino Pega CDH mediante OAuth 2 con autenticación de credenciales de cliente](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Complete los campos siguientes y seleccione **[!UICONTROL Conectarse al destino]**:

* **[!UICONTROL Dirección URL del token de acceso]**: La URL del token de acceso de OAuth 2 en su [!DNL Pega Customer Decision Hub] instancia.
* **[!UICONTROL ID de cliente]**: OAuth 2 [!DNL client ID] que ha generado en su [!DNL Pega Customer Decision Hub] instancia.
* **[!UICONTROL Secreto del cliente]**: OAuth 2 [!DNL client secret] que ha generado en su [!DNL Pega Customer Decision Hub] instancia.

### Rellenar detalles de destino {#destination-details}

Después de establecer la conexión de autenticación en la variable [!DNL Pega Customer Decision Hub], proporcione la siguiente información para el destino:

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino de la Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Para configurar los detalles del destino, rellene los campos obligatorios y seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Nombre del host]**: El nombre de host del centro de decisiones del cliente Pega al que se exporta el perfil como datos json.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#attributes}

En el [[!UICONTROL Seleccionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) paso, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

### Ejemplo de asignación: activación de actualizaciones de perfil en [!DNL Pega Customer Decision Hub] {#mapping-example}

A continuación se muestra un ejemplo de asignación de identidad correcta al exportar perfiles a [!DNL Pega Customer Decision Hub].

Selección de campos de origen:

* Seleccione un identificador (por ejemplo: CustomerID) como identidad de origen que identifica de forma exclusiva un perfil en Adobe Experience Platform y [!DNL Pega Customer Decision Hub].
* Seleccione los cambios en los atributos de perfil de origen XDM que deben exportarse y actualizarse en [!DNL Pega Customer Decision Hub].

Selección de campos de destino:

* Seleccione el `CustomerID` área de nombres como identidad de destino.
* Seleccione los nombres de atributos de perfil de destino que deben asignarse a los atributos de perfil de origen XDM correspondientes.

![Asignación de identidad](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Una actualización correcta de la pertenencia a un segmento para un perfil insertaría el identificador, el nombre y los estados del segmento en el almacén de datos de pertenencia a segmentos de Pega marketing. Los datos de pertenencia se asocian a un cliente mediante el Diseñador de perfiles de cliente en [!DNL Pega Customer Decision Hub], como se muestra a continuación.
![Imagen de la pantalla de la interfaz de usuario en la que se pueden asociar datos de pertenencia a segmentos de Adobe al cliente mediante el Diseñador de perfiles del cliente](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Los datos de pertenencia a segmentos se utilizan en las políticas de Participación del Diseñador de acciones siguientes para la toma de decisiones de la acción siguiente, como se muestra a continuación.
![Imagen de la pantalla de la interfaz de usuario en la que puede añadir campos de pertenencia a segmentos como condiciones en Políticas de participación del Diseñador de acciones más recientes](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Los campos de datos de pertenencia a segmentos de clientes se añaden como predictores en los modelos adaptables, como se muestra a continuación.
![Imagen de la pantalla de la interfaz de usuario en la que puede añadir campos de pertenencia a segmentos como predicadores en los modelos adaptables, utilizando Prediction Studio.](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Recursos adicionales {#additional-resources}

Consulte [Configuración de un registro de cliente de OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) en [!DNL Pega Customer Decision Hub].

Consulte [Creación de una ejecución en tiempo real para flujos de datos](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) en [!DNL Pega Customer Decision Hub].

Consulte [Administrar registros de cliente en el Diseñador de perfiles de cliente](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).
