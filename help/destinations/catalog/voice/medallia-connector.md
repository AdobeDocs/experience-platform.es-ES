---
title: Conexión con Medallia
description: Active perfiles para encuestas de Medallia dirigidas y recopilación de comentarios para comprender mejor las necesidades y expectativas de los clientes.
source-git-commit: be2d4e5d1f204feefc7acb7cb4518044ab3f153a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 2%

---


# Conexión con Medallia

## Información general {#overview}

Active perfiles para encuestas de Medallia dirigidas y recopilación de comentarios para comprender mejor las necesidades y expectativas de los clientes.

>[!IMPORTANT]
>
>Esta página de documentación fue creada por el equipo de Medallia. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en adobe-integrations@medallia.com.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Medallia, estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Una marca B2B quiere evaluar y racionalizar su programa de incorporación. Les gustaría enviar encuestas personalizadas en tiempo real a los clientes que acaban de completar el proceso de incorporación.

### Caso de uso n.º 2

Un minorista busca comprender mejor las preferencias de los clientes para la realización de pedidos. Quieren enviar una breve encuesta SMS de 1 pregunta a los clientes que han realizado compras en línea y en la tienda durante el mes pasado.

## Requisitos previos {#prerequisites}

Se requiere la siguiente información para establecer la conexión con Medallia:
* **URL de extremo de tokens de OAuth**
* **ID del cliente**
* **Secreto del cliente**
* **URL de puerta de enlace de API**
* **Importar nombre de API**

Trabaje con su equipo de envío de Medallia para obtener estos detalles.

## Identidades compatibles {#supported-identities}

Medallia apoya la activación de las identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| email | Correo electrónico Dirección | Seleccione la identidad del destinatario de correo electrónico cuando desee enviar encuestas de invitación por correo electrónico. Cuando un perfil está asociado con varias direcciones de correo electrónico, Medallia envía la invitación únicamente por déclencheur al primer correo electrónico. |
| phone | Números de teléfono con hash en formato E.164 | Seleccione la identidad de destino del teléfono cuando desee enviar encuestas basadas en SMS. El número de teléfono debe tener el formato E.164, que incluye un signo más (+), un código de país internacional, un código de área local y un número de teléfono. Por ejemplo: (+) (código de país) (código de área) (número de teléfono). Cuando un perfil está asociado con varios números de teléfono, Medallia sólo dará el déclencheur de la invitación al primer número de teléfono. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros recién cualificados de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!UICONTROL URL de extremo de tokens de OAuth]**: Normalmente adopta la forma de https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID de cliente]**: Obtenga información de su equipo de envío de Medallia.
* **[!UICONTROL Secreto del cliente]**: Obtenga información de su equipo de envío de Medallia.

![Imagen que muestra la pantalla de autenticación de este destino.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL URL de puerta de enlace de API]**: Obtenga información de su equipo de envío de Medallia. Normalmente adopta la forma de https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importar nombre de API]**: Obtenga información de su equipo de envío de Medallia. Nombre de la API de importación de Medallia (también conocida como Fuente web) que se utilizará en esta conexión. Puede activar diferentes segmentos en diferentes API de importación para almacenar en déclencheur diferentes programas de encuestas.

![Imagen que muestra la pantalla de detalles de destino para este destino.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Asignación de atributos e identidades {#map}

Los siguientes espacios de nombres de identidad de destino deben asignarse según el caso de uso:
* Para encuestas basadas en correo electrónico, **email** debe asignarse como campo de destino mediante **Campo de destino** > **Seleccionar área de nombres de identidad** > **email**
* Para encuestas basadas en SMS, **phone** debe asignarse como campo de destino mediante **Campo de destino** > **Seleccionar área de nombres de identidad** > **phone**. Los números de teléfono deben tener el formato E.164, que incluye un signo más (+), un código de país internacional, un código de área local y un número de teléfono

Se recomienda encarecidamente que también asigne atributos personalizados de objetivo adicionales para crear encuestas personalizadas y anexe información adicional sobre el cliente al registro de encuesta:

* Las encuestas personalizadas suelen dirigirse al cliente por su nombre
   * Asigne el nombre del cliente a **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre del atributo** > **firstname**
   * Asigne el apellido del cliente a **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre del atributo** > **lastname**
* Agregue asignaciones para cualquier otro atributo personalizado de destino como desee

![Imagen que muestra una asignación de muestra para identidades y atributos.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Comparta con su equipo de entrega de Medallia la información exacta **Nombres de atributos** para cada atributo personalizado de destino que asigne con **Campo de destino** > **Seleccionar atributos personalizados** > **Nombre del atributo**. Puede que desee realizar una captura de pantalla de la página de asignación para compartirla directamente.

## Datos exportados {#exported-data}

Una vez que haya activado los segmentos en el destino, informe a su equipo de entrega de Medallia, que podrá validar los datos exportados de Adobe Experience Platform a Medallia. Tenga en cuenta que los estudios solo se pueden activar en Medallia después de verificar correctamente los datos; antes de esto, los datos se exportarán a Medallia, pero no se déclencheur las encuestas a los clientes.

A continuación se proporciona un JSON de muestra de los datos exportados, que utiliza la asignación de ejemplo de la captura de pantalla anterior en la **Asignación de atributos e identidades** sección:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).
