---
keywords: streaming, destino de Qualtrics
title: Automatizaciones de Qualtrics
description: Sincronice la experiencia y los datos operativos del cliente para desbloquear la personalización a escala. Utilice la agregación de varias fuentes de datos operativos en Adobe Experience Platform como entrada en Qualtrics Experience ID para comprender mejor a sus clientes y permitir que el alcance dirigido cierre la brecha cuando se trata de comprender los impulsores de la intención, la emoción y la experiencia.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# Automatizaciones de Qualtrics

## Información general {#overview}

Sincronice la experiencia y los datos operativos del cliente para desbloquear la personalización a escala.

Utilice la agregación de varias fuentes de datos operativos en Adobe Experience Platform como entrada en Qualtrics Experience ID para comprender mejor a sus clientes y permitir que el alcance dirigido cierre la brecha cuando se trata de comprender los impulsores de la intención, la emoción y la experiencia.

>[!IMPORTANT]
>
>El equipo de Qualtrics crea y mantiene el conector de destino y la página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente iniciando sesión en [Centro de éxito del cliente](https://support-portal.qualtrics.com/).

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el *Automatizaciones de Qualtrics* Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1 {#use-case-1}

**Escenario**: una empresa quiere medir la satisfacción del cliente en varios puntos de contacto digitales, como su sitio web y su aplicación móvil. Utilizan Adobe Experience Platform para almacenar en déclencheur las encuestas de Qualtrics basadas en las interacciones de los usuarios, como completar una compra o visitar una página web específica.

**Resultado**: Al recopilar comentarios en tiempo real, la empresa puede realizar mejoras en la experiencia del cliente basadas en datos, lo que produce una mayor satisfacción y lealtad.

### Caso de uso #2 {#use-case-2}

**Escenario**: una organización tiene como objetivo mejorar su proceso de incorporación de empleados. Utilizan Adobe Experience Platform para recopilar comentarios de las nuevas contrataciones a través de encuestas de Qualtrics. Las encuestas se activan automáticamente después de un período de incorporación predefinido.

**Resultado**: La retroalimentación continua permite a la organización adaptar y mejorar el proceso de incorporación, lo que resulta en una mejor participación y productividad entre los nuevos empleados.

## Requisitos previos

Antes de configurar el destino de Qualtrics en Adobe Experience Platform, asegúrese de que se hayan cumplido los siguientes requisitos previos:

* Tiene una cuenta de Qualtrics.
* Ha obtenido el token de API necesario de Qualtrics.

### Obtención de un token de API

A continuación se indican los pasos necesarios para obtener un token de API de Qualtrics.

1. Inicie sesión en su cuenta de Qualtrics.
2. Ir a **Configuración de cuenta**.
3. Seleccionar **ID de Qualtrics**.
4. En esta página, busque la variable **API** contiene una sección, **Token** field. Este es el token de API y será necesario durante la configuración de destino.

## Identidades admitidas {#supported-identities}

*Automatizaciones de Qualtrics* admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email | Direcciones de correo electrónico de texto sin formato | Qualtrics solo admite direcciones de correo electrónico de texto sin formato. |
| external_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en *Automatizaciones de Qualtrics* destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Como parte de la autenticación, deberá proporcionar un **Nombre de usuario** y **Contraseña**. El nombre de usuario es su nombre de usuario de Qualtrics y la contraseña es el token de API de su cuenta de Qualtrics. Para recuperar el token de API, siga las instrucciones de la **Requisitos previos** sección anterior.

![Autenticación](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL URL]**: La dirección URL encontrada en la variable [Evento JSON](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) que déclencheur su [flujo de trabajo en Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Vea la siguiente captura de pantalla para ver un ejemplo.

![Dirección URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Este destino tiene un esquema abierto, por lo que puede enviar cualquier propiedad a Qualtrics.

#### Asignar atributos

Para añadir un atributo a la asignación, simplemente seleccione **atributos personalizados** al añadir una nueva asignación. Puede introducir cualquier nombre para el atributo. Qualtrics promueve la *camelCase* convención de nombres de atributos (consulte la siguiente captura de pantalla para ver un ejemplo).

![Atributo personalizado](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Consulte la siguiente captura de pantalla para ver un ejemplo de posibles asignaciones de atributos.

![Asignaciones de ejemplo](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Asignación de identidades

Es obligatorio seleccionar un área de nombres de identidad para este destino. Las dos asignaciones posibles de campos de origen a campos de destino son:

| Campo de origen | Campo de destino |
|--------------------|-----------------------|
| IdentityMap: correo electrónico | Identity: email |
| IdentityMap: ECID | Identidad: external_id |

Vea la siguiente captura de pantalla para ver un ejemplo.

![Espacio de nombre de identidad](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Como se ha mencionado anteriormente, este destino utiliza un esquema abierto, por lo que cualquier propiedad puede enviarse a Qualtrics. Sin embargo, los datos enviados a Qualtrics seguirán la siguiente estructura:

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Para verificar que los datos se han introducido en Qualtrics, vaya al flujo de trabajo que contiene su **Evento JSON**, desde allí, vaya a **Ejecutar historial** donde debería ver las ejecuciones del flujo de trabajo. Cada flujo de trabajo tiene un estado de **Correcto** o **Error**. Si se selecciona una ejecución determinada, se muestra más información al respecto, lo que le permite solucionar problemas si encuentra algún problema.

Si no hay ejecuciones visibles en **Ejecutar historial**, significa que el flujo de trabajo aún no se ha activado, lo que indica que puede haber un problema. Asegúrese de que el flujo de trabajo esté habilitado y de que la variable **URL** en el destino en Adobe Experience Platform es correcto. Las ejecuciones del flujo de trabajo no son instantáneas, por lo que es posible que tenga que esperar un poco antes de que se complete.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).
