---
title: Kevel Connection
description: Utilice el destino de streaming de Kevel para activar audiencias directamente en las API de UserDB y Administración de segmentos de Kevel y admitir la segmentación en tiempo real en el momento de la decisión.
last-substantial-update: 2026-01-27T00:00:00Z
source-git-commit: 04d01b2deafb1b8f1b0c256f31475bb75989a2c4
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# [!DNL Kevel] conexión {#kevel}

## Información general {#overview}

[[!DNL Kevel]](https://www.kevel.com/) proporciona la tecnología habilitada para IA y la guía de expertos que ayudan a los líderes innovadores en comercio a lanzar, escalar y tener éxito en los medios minoristas. Retail Media Cloud de [!DNL Kevel] alimenta los formatos de anuncio personalizables, atribuibles y orientados para la publicidad dentro y fuera del sitio.

El destino de streaming de [!DNL Kevel] para Adobe Experience Platform permite a los clientes activar audiencias de Adobe directamente en las API de UserDB y Administración de segmentos de [!DNL Kevel] para admitir el direccionamiento en tiempo real en el momento de la decisión de anuncios.

>[!IMPORTANT]
> 
>Si tiene preguntas o desea solicitar una actualización con respecto al destino [!DNL Kevel] o su documentación, envíe un correo electrónico al equipo de [!DNL Kevel] a [support@kevel.com](mailto:support@kevel.com).

## Casos de uso {#use-cases}

Puede activar audiencias de comportamiento de origen enriquecidas en todas las experiencias de medios comerciales para ofrecer anuncios más relevantes y un rendimiento más sólido. En Experience Platform, puede generar audiencias de alto valor basadas en la intención, como compradores de categorías frecuentes o usuarios con interés en productos recientes, y sincronizar esas suscripciones a [!DNL Kevel] en tiempo real. [!DNL Kevel] pone inmediatamente estos segmentos a disposición para la toma de decisiones de anuncios, lo que permite un direccionamiento preciso para productos patrocinados y otros formatos en las experiencias de búsqueda, exploración y aplicación. Tan pronto como los usuarios cumplan los requisitos, puede actuar sobre estas señales para generar impresiones más relevantes, una mejor segmentación y una medición y un ROAS mejorados.

## Requisitos previos {#prerequisites}

Para prepararse para usar el destino [!DNL Kevel], asegúrese de que se cumplan los siguientes requisitos previos:

- Debe tener una red **[!DNL Kevel]** activa y acceso a la API.
- Necesita una clave de API **[!DNL Kevel]** con permisos para crear segmentos y actualizar registros de UserDB.
- Debe configurar áreas de nombres de identidad en Experience Platform que se asignen a las identidades que su sitio o aplicación envía durante [!DNL Kevel] solicitudes de publicidad (por ejemplo, ECID, GAID, IDFA, ID de fidelidad, etc.).
- Los clientes de Adobe solo deben asignar identidades que se utilicen durante las solicitudes de publicidad en tiempo real, ya que cada identidad generará un registro de UserDB.

## Identidades admitidas {#supported-identities}

El destino [!DNL Kevel] admite la activación de cualquier identidad que la aplicación pueda usar al enviar solicitudes de publicidad a [!DNL Kevel]. Puede asignar hasta tres áreas de nombres de identidad para generar los registros de UserDB correspondientes.

[!DNL Kevel] admite las siguientes áreas de nombres de identidad de Experience Platform:

| Espacio de nombres de identidad | Descripción | Uso habitual |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | Se utiliza para la personalización en el sitio y la identificación entre Adobe. |
| **GAID** | GOOGLE ADVERTISING ID | Se utiliza para el tráfico de aplicaciones/dispositivos de Android. |
| **IDFA** | APPLE ADVERTISING ID | Se utiliza para el tráfico de aplicaciones/dispositivos de iOS (sujeto al consentimiento de AT&amp;T). |
| **ID_EXTERNO** | ID externo (identificador personalizado) | Pasa los ID propietarios o generados por el servidor. |

{style="table-layout:auto"}

### Compatibilidad con áreas de nombres de identidad personalizadas

El destino [!DNL Kevel]0} también acepta áreas de nombres personalizadas **, tal como se definieron en su implementación de Experience Platform.**

Esto significa que:

- Puede asignar **áreas de nombres de identidad** específicas del cliente (por ejemplo: `loyalty_id`, `gigya_id` o cualquier identidad personalizada que haya definido en el servicio de identidad).
- Estas áreas de nombres se pueden asignar a `kevel_user_key1`, `kevel_user_key2` o `kevel_user_key3` de la misma manera que las áreas de nombres globales.
- [!DNL Kevel] generará **un registro UserDB por instancia de cada identidad asignada**, lo que permitirá la coincidencia en tiempo real en el momento de la decisión de anuncio para cada identificador que envíen sus sistemas.

### Comportamiento de asignación de identidad

- Puede asignar **hasta tres** áreas de nombres de identidad de Experience Platform a las tres ranuras de identidad de [!DNL Kevel].
- Para cada perfil activado, [!DNL Kevel] recibe **un registro UserDB por instancia de cada identidad asignada**.
- Los clientes solo deben asignar las identidades que realmente envían en solicitudes de publicidad a [!DNL Kevel] para evitar un almacenamiento innecesario de UserDB.

![Ejemplo de asignación para destino de kevel](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Audiencias compatibles {#supported-audiences}

| Origen de audiencia | Admitido | Descripción |
|-----------------------|-----------|---------------------------------------------------------- |
| Servicio de segmentación | Sí | Audiencias de perfil de Adobe evaluadas por el motor de segmentación. |
| Cargas personalizadas | No | No compatible en este momento. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

| Elemento | Tipo | Notas |
|------|------|-------|
| Tipo de exportación | **Exportación de segmentos** | [!DNL Kevel] recibe una actualización cada vez que un perfil califica para una audiencia o sale de ella. |
| Frecuencia de exportación | **Transmisión** | Las actualizaciones se envían en tiempo real mediante el marco de trabajo de flujo continuo de Destination SDK. |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

Siga el flujo de trabajo estándar de Experience Platform [connect a destination](../../ui/connect-destination.md).

>[!IMPORTANT]
> 
>Debe tener los permisos de **Ver destinos** y **Administrar destinos**.

### Autenticarse en el destino {#authenticate}

Al conectarse a [!DNL Kevel], proporcione el siguiente campo:

- **Token de portador** — Su clave de API [!DNL Kevel].

![Opciones de autenticación para Kevel Destination](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Rellenar detalles de destino {#destination-details}

Después de la autenticación, configure:

- **Nombre**: una etiqueta para identificar esta instancia de destino.
- **Descripción**: texto opcional para describir esta instancia de destino.
- **[!DNL Kevel]Id. de red** — Su identificador de red [!DNL Kevel].

![Detalles del destino de Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Activar segmentos en este destino {#activate}

Para enviar audiencias a [!DNL Kevel], siga el flujo de trabajo en\
[Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Desactivación de audiencias {#deactivate}

Cuando se desactiva o elimina una audiencia del destino [!DNL Kevel] en Experience Platform, Experience Platform deja de enviar más actualizaciones de calificación de perfiles para esa audiencia. Cualquier segmento existente creado en [!DNL Kevel] permanece disponible y no se elimina automáticamente.

Si el segmento [!DNL Kevel] se está usando actualmente en una campaña activa, [!DNL Kevel] impide la eliminación para evitar interrumpir la entrega en vivo. En este caso, la desactivación en Experience Platform resulta en lo siguiente:

- El flujo de datos de Experience Platform se detiene
- El segmento [!DNL Kevel] sigue existiendo y puede permanecer adjunto a las campañas hasta que se elimine manualmente o se actualice la campaña

Para detener completamente el direccionamiento en [!DNL Kevel], asegúrese de que el segmento se elimine de las campañas activas en el sistema de administración de campañas de [!DNL Kevel].

### Asignar atributos e identidades {#map}

[!DNL Kevel] requiere:

- **Áreas de nombres de identidad**: hasta tres áreas de nombres de identidad asignadas a [!DNL Kevel] ranuras de identidad.
- **Abono a segmentos**: no se requiere asignación manual; Experience Platform pasa automáticamente los alias e identificadores de abono a segmentos.

Durante la activación, seleccione las áreas de nombres de identidad que configuró para [!DNL Kevel]. Cada identidad generará su propia llamada de actualización de UserDB.

## Datos exportados / Validar exportación de datos {#exported-data}

Cuando un perfil califica para una audiencia o sale de ella, Experience Platform envía una actualización de flujo continuo a [!DNL Kevel].

### Carga útil de ejemplo recibida por [!DNL Kevel] UserDB

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Parámetro | Descripción |
|-----------|-------------|
| **claveDeUsuario** | Derivado de la identidad de Adobe asignada. |
| **segmentos** | El conjunto de [!DNL Kevel] ID de segmento correspondientes a las audiencias de Adobe para las que se realiza el perfil actualmente. |

{style="table-layout:auto"}

### Perfil de Experience Platform de muestra utilizado durante la exportación {#sample-profile}

Al activar audiencias en el destino [!DNL Kevel], Experience Platform envía fragmentos de perfil que contienen **cualificaciones de segmento** e **identidades asignadas por el cliente** a las ranuras de identidad de [!DNL Kevel].

A continuación se muestra un ejemplo de un perfil exportado que muestra:

- Varias áreas de nombres de identidad asignadas a `kevel_user_key1`, `kevel_user_key2` y `kevel_user_key3`
- Un solo segmento activado en el área de nombres `ups`

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Cómo [!DNL Kevel] interpreta este perfil

Con la configuración de destino [!DNL Kevel], cada identidad asignada genera un registro UserDB distinto, lo que significa que [!DNL Kevel] recibe:

- Una actualización para `ECID-fN1zo`
- Una actualización para `ECID-9Xr2p`
- Una actualización para `GAID-4oic4`
- Una actualización para `IDFA-nB5fU`

Esto permite que se reconozca a la misma persona en el momento de la decisión de anuncio utilizando cualquiera de sus identidades disponibles, y que cada identidad lleve un conjunto idéntico de pertenencias de segmentos.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

- [[!DNL Kevel] Referencia de UserDB](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] Segmentación de segmentos de usuario](https://dev.kevel.com/docs/segment-targeting)
