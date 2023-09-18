---
title: Conexión de Medallia
description: Active perfiles para encuestas de Medallia y recopilación de comentarios para comprender mejor las necesidades y expectativas de los clientes.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# Conexión de Medallia

## Información general {#overview}

Active perfiles para encuestas de Medallia y recopilación de comentarios para comprender mejor las necesidades y expectativas de los clientes.

>[!IMPORTANT]
>
>El equipo de Medallia crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en adobe-integrations@medallia.com.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino Medallia, aquí tiene algunos casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1

Una marca B2B quiere evaluar y optimizar su programa de incorporación. Les gustaría enviar encuestas personalizadas en tiempo real a los clientes que acaban de completar el proceso de incorporación.

### Caso de uso #2

Un minorista busca comprender mejor las preferencias de los clientes para la realización de pedidos. Quieren enviar una breve encuesta SMS de 1 pregunta a los clientes que han realizado compras en línea y en la tienda durante el mes pasado.

## Requisitos previos {#prerequisites}

Se requiere la siguiente información para establecer la conexión con Medallia:
* **URL de extremo de token de OAuth**
* **ID del cliente**
* **Secreto de cliente**
* **URL de puerta API**
* **Importar nombre de API**

Trabaje con su equipo de entrega de Medallia para obtener estos detalles.

## Identidades admitidas {#supported-identities}

Medallia apoya la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email | Correo electrónico Dirección | Seleccione la identidad del destinatario del correo electrónico cuando desee enviar encuestas de invitación por correo electrónico. Cuando un perfil está asociado con varias direcciones de correo electrónico, Medallia enviará en déclencheur la invitación solo al primer correo electrónico. |
| phone | Números de teléfono con hash en formato E.164 | Seleccione la identidad del destinatario del teléfono cuando desee enviar encuestas basadas en SMS. El número de teléfono debe tener el formato E.164, que incluye un signo más (+), un código de llamada de país internacional, un código de área local y un número de teléfono. Por ejemplo: (+)(código de país)(código de área)(número de teléfono). Cuando un perfil está asociado con varios números de teléfono, Medallia enviará la invitación al primer número de teléfono únicamente en déclencheur. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros recién cualificados de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL URL de extremo de token de OAuth]**: Normalmente adopta la forma de https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID de cliente]**: Obtenga de su equipo de entrega de Medallia.
* **[!UICONTROL Secreto del cliente]**: Obtenga de su equipo de entrega de Medallia.

![Imagen que muestra la pantalla de autenticación de este destino.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL URL de puerta API]**: Obtenga de su equipo de entrega de Medallia. Normalmente adopta la forma de https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importar nombre de API]**: Obtenga de su equipo de entrega de Medallia. Nombre de la API de importación de Medallia (también conocida como fuente web) que se utilizará en esta conexión. Puede activar distintas audiencias en diferentes API de importación para almacenar en déclencheur diferentes programas de encuestas.

![Imagen que muestra la pantalla de detalles de destino de este destino.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Las siguientes áreas de nombres de identidad de destino deben asignarse según el caso de uso:
* Para encuestas basadas en correo electrónico, **email** debe asignarse como campo de destino mediante **Campo de destino** > **Seleccionar área de nombres de identidad** > **email**
* Para encuestas basadas en SMS, **phone** debe asignarse como campo de destino mediante **Campo de destino** > **Seleccionar área de nombres de identidad** > **phone**. Los números de teléfono deben tener el formato E.164, que incluye un signo más (+), un código de llamada de país internacional, un código de área local y un número de teléfono

Se recomienda asignar también atributos personalizados de destinatario adicionales para crear encuestas personalizadas y anexar información adicional sobre el cliente al registro de encuesta:

* Las encuestas personalizadas suelen dirigirse al cliente por su nombre
   * Asigne el nombre del cliente a **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre de atributo** > **firstname**
   * Asigne el apellido del cliente a **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre de atributo** > **apellido**
* Añada asignaciones para cualquier otro atributo personalizado de destino que desee

![Imagen que muestra una asignación de muestra para identidades y atributos.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Comparta con su equipo de entrega de Medallia la información exacta **Nombres de atributo** para cada atributo personalizado de destino asignado mediante **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre de atributo**. Es posible que desee realizar una captura de pantalla de la página de asignación para compartirla directamente.

## Datos exportados {#exported-data}

Una vez que haya activado sus segmentos en el destino, informe a su equipo de entrega de Medallia, que podrá validar los datos exportados de Adobe Experience Platform a Medallia. Tenga en cuenta que las encuestas solo pueden activarse dentro de Medallia después de una verificación de datos correcta; antes de esto, los datos se exportarán a Medallia, pero no se almacenarán en déclencheur las encuestas a los clientes.

A continuación se proporciona un JSON de muestra de los datos exportados, que utiliza la asignación de ejemplo de la captura de pantalla anterior en la **Asignar atributos e identidades** sección:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).
