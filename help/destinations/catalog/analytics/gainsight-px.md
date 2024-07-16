---
title: Conexión de Gainsight PX
description: Utilice el destino Gainsight PX para enviar información de segmentación a la plataforma Gainsight PX.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 3%

---

# Conexión de Gainsight PX {#gainsight-px}

## Información general {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) es una plataforma de experiencia del producto que permite a los equipos de productos comprender cómo utilizan los usuarios sus productos, recopilar comentarios y crear participaciones en la aplicación, como tutoriales de productos, para impulsar la incorporación del usuario y la adopción de productos.

>[!IMPORTANT]
>
>El equipo *Gainsight PX* crea y mantiene el conector de destino y la página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en *`pxsupport@gainsight.com`*.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar el destino *Gainsight PX*, aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Segmentación de participaciones en la aplicación {#targeting-in-app-engagements}

Una empresa SaaS quiere atraer a sus clientes a través de una guía en la aplicación creada en Gainsight PX. Se ha creado en Adobe Experience Platform una audiencia para recibir esta participación. El destino PX de Gainsight recibe la audiencia y la pone a disposición del entorno PX de Gainsight.

## Requisitos previos {#prerequisites}

* Póngase en contacto con el equipo de soporte técnico de [!DNL Gainsight] y solicite la activación de las características de segmentos externos para su suscripción.
* Genere un valor OAuth Secret para su suscripción PX, usando el botón **[!UICONTROL Generar nuevo secreto]** en la parte inferior de la [página Detalles de la compañía](https://app.aptrinsic.com/settings/subscription)
  ![Pantalla de detalles de la compañía en Gainsight PX que muestra el botón Generar nuevo secreto](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Identidades admitidas {#supported-identities}

Gainsight PX admite la activación de las identidades descritas en la siguiente tabla. Más información sobre [identidades](../../../identity-service/features/namespaces.md).

| Identidad de destino | Descripción |
|---|----|
| Identificar ID | Identificador de usuario común que identifica de forma exclusiva a un usuario en Gainsight PX y Adobe Experience Platform |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencia puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---|---|---|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---|---|---|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL Gainsight PX]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Experience Platform en función de la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL permiso Administrar destinos]** [control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Captura de pantalla de autenticación](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Contraseña]**: La contraseña usada para iniciar sesión en [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL ID de cliente]**: el ID de suscripción de Gainsight PX en la [página de detalles de la compañía](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Secreto de cliente]**: El secreto de OAuth generado en la parte inferior de [página Detalles de la compañía](https://app.aptrinsic.com/settings/subscription) en la interfaz de usuario de [!DNL Gainsight PX].
* **[!UICONTROL Nombre de usuario]**: El correo electrónico usado para iniciar sesión en la interfaz de usuario de [[!DNL Gainsight PX]](https://app.aptrinsic.com)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Pantalla de detalles de destino en la interfaz de usuario del Experience Platform que muestra cómo rellenar los campos Nombre y Descripción](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignación de identidades {#map}

Este destino admite la asignación de atributos de perfil y áreas de nombres de identidad. La asignación de destino siempre debe ser el área de nombres de identidad **[!UICONTROL IDENTIFY_ID]**.

Consulte los ejemplos siguientes para comprender mejor cómo configurar la asignación.

#### Asignación de un atributo de perfil {#map-profile-attribute}

En el ejemplo que se muestra a continuación, el campo de origen es un atributo de perfil XDM que se asigna al área de nombres de destino IDENTIFY_ID.

![Pantalla de asignación de ejemplo del área de nombres de identidad que muestra cómo seleccionar los valores de origen y destino](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Asignar un área de nombres de identidad {#map-identity-namespace}

En el ejemplo siguiente, el campo de origen es un área de nombres de identidad (**[!UICONTROL ECID]**) que se asigna al área de nombres de destino **[!UICONTROL IDENTIFY_ID]**.

![Pantalla de asignación de ejemplo de atributo que muestra cómo seleccionar los valores de origen y destino](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Los datos de segmentación se transmiten desde el Experience Platform a Gainsight PX.

Los metadatos del segmento se pueden ver en la pantalla Segmentos de la interfaz de usuario de [!DNL Gainsight PX].

![Pantalla de lista de segmentos en Gainsight PX que muestra segmentos externos.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

La información de abono a segmentos está visible en la ficha Segmentos de la pantalla del Audience Explorer de la interfaz de usuario de [!DNL Gainsight PX].

La pantalla de ![Audience Explorer en Gainsight PX muestra los segmentos asociados a un usuario.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
