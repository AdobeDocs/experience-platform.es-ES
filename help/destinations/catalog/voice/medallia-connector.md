---
title: Conexión de Medallia
description: Active perfiles para encuestas de Medallia y recopilación de comentarios para comprender mejor las necesidades y expectativas de los clientes.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

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
* **ID de cliente**
* **Secreto de cliente**
* **URL de puerta de enlace API**
* **Importar nombre de API**

Trabaje con su equipo de entrega de Medallia para obtener estos detalles.

## Identidades admitidas {#supported-identities}

Medallia apoya la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email | Dirección de correo electrónico | Seleccione la identidad del destinatario del correo electrónico cuando desee enviar encuestas de invitación por correo electrónico. Cuando un perfil está asociado con varias direcciones de correo electrónico, Medallia enviará en déclencheur la invitación solo al primer correo electrónico. |
| phone | Números de teléfono con hash en formato E.164 | Seleccione la identidad del destinatario del teléfono cuando desee enviar encuestas basadas en SMS. El número de teléfono debe tener el formato E.164, que incluye un signo más (+), un código de llamada de país internacional, un código de área local y un número de teléfono. Por ejemplo: (+)(código de país)(código de área)(número de teléfono). Cuando un perfil está asociado con varios números de teléfono, Medallia enviará la invitación al primer número de teléfono únicamente en déclencheur. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Está exportando todos los miembros recién calificados de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL URL de extremo de token de OAuth]**: Normalmente adopta la forma de https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID de cliente]**: obténgalo de su equipo de entrega de Medallia.
* **[!UICONTROL Secreto del cliente]**: obténgalo de su equipo de entrega de Medallia.

![Imagen que muestra la pantalla de autenticación de este destino.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL URL de puerta de enlace de API]**: obténgala a su equipo de entrega de Medallia. Normalmente adopta la forma de https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importar nombre de API]**: comuníquese con el equipo de entrega de Medallia. Nombre de la API de importación de Medallia (también conocida como fuente web) que se utilizará en esta conexión. Puede activar distintas audiencias en diferentes API de importación para almacenar en déclencheur diferentes programas de encuestas.

![Imagen que muestra la pantalla de detalles de destino de este destino.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Las siguientes áreas de nombres de identidad de destino deben asignarse según el caso de uso:
* Para las encuestas basadas en correo electrónico, **correo electrónico** debe asignarse como campo de destino mediante **Campo de destino** > **Seleccionar área de nombres de identidad** > **correo electrónico**
* Para las encuestas basadas en SMS, **teléfono** debe asignarse como campo de destino con **Campo de destino** > **Seleccionar área de nombres de identidad** > **teléfono**. Los números de teléfono deben tener el formato E.164, que incluye un signo más (+), un código de llamada de país internacional, un código de área local y un número de teléfono

Se recomienda asignar también atributos personalizados de destinatario adicionales para crear encuestas personalizadas y anexar información adicional sobre el cliente al registro de encuesta:

* Las encuestas personalizadas suelen dirigirse al cliente por su nombre
   * Asigne el nombre del cliente a **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre de atributo** > **nombre**
   * Asigne el apellido del cliente a **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre de atributo** > **apellido**
* Añada asignaciones para cualquier otro atributo personalizado de destino que desee

![Imagen que muestra una asignación de muestra para identidades y atributos.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Comparta con su equipo de entrega de Medallia los **nombres de atributo** exactos para cada atributo personalizado de destino que asigne con **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre de atributo**. Es posible que desee realizar una captura de pantalla de la página de asignación para compartirla directamente.

## Datos exportados {#exported-data}

Una vez que haya activado sus segmentos en el destino, informe a su equipo de entrega de Medallia, que podrá validar los datos exportados de Adobe Experience Platform a Medallia. Tenga en cuenta que las encuestas solo pueden activarse dentro de Medallia después de una verificación de datos correcta; antes de esto, los datos se exportarán a Medallia, pero no se almacenarán en déclencheur las encuestas a los clientes.

A continuación se proporciona un ejemplo de JSON de los datos exportados, que utiliza la asignación de ejemplo de la captura de pantalla anterior en la sección **Asignar atributos e identidades**:

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

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
