---
keywords: Experience Platform;inicio;temas populares;api de servicio de identidad;guía para desarrolladores de servicios de identidad;región
solution: Experience Platform
title: Guía de API del servicio de identidad
topic-legacy: API guide
description: La API del servicio de identidad permite a los desarrolladores administrar la identificación de clientes entre dispositivos, canales cruzados y casi en tiempo real mediante gráficos de identidad en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: f269a7b1584a6e4a0e1820a0c587a647c0c8f7b5
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 3%

---

# Guía de la API de [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] administra la identificación entre dispositivos, entre canales y casi en tiempo real de sus clientes en lo que se conoce como gráfico de identidad dentro de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Resuelve el desafío fundamental que supone la fragmentación de los datos de perfil del cliente. Para ello, combina identidades entre dispositivos y sistemas en los que los clientes interactúan con su marca.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil unificado y de cliente en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que debe conocer o tener disponible para realizar llamadas correctamente a la API [!DNL Identity Service] .

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

### Enrutamiento basado en regiones

La API [!DNL Identity Service] emplea extremos específicos de la región que requieren la inclusión de `{REGION}` como parte de la ruta de solicitud. Durante el aprovisionamiento de la organización IMS, se determina y almacena una región dentro del perfil de organización de IMS. El uso de la región correcta con cada extremo garantiza que todas las solicitudes realizadas con la API [!DNL Identity Service] se enruten a la región adecuada.

Actualmente existen dos regiones compatibles con las API [!DNL Identity Service]: VA7 y NLD2.

La tabla siguiente muestra rutas de ejemplo que utilizan regiones:

| Service | Región: VA7 | Región: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Las solicitudes realizadas sin especificar una región pueden dar como resultado que las llamadas se dirijan a una región incorrecta o que las llamadas fallen de forma inesperada.

Si no puede localizar la región dentro de su perfil de organización de IMS, póngase en contacto con el administrador del sistema para obtener asistencia.

## Uso de la API [!DNL Identity Service]

Los parámetros de identidad utilizados en estos servicios pueden expresarse de una de las dos maneras siguientes: compuesto o XID.

Las identidades compuestas son construcciones que incluyen tanto el valor de ID como el área de nombres. Cuando se utilizan identidades compuestas, el espacio de nombres se puede proporcionar mediante un nombre (`namespace.code`) o un ID (`namespace.id`).

Cuando se mantiene una identidad, [!DNL Identity Service] genera y asigna un ID a esa identidad, denominada ID nativo o XID. Todas las variaciones de las API de clúster y asignación admiten tanto identidades compuestas como XID en sus solicitudes y respuestas. Se requiere uno de los parámetros: `xid` o combinación de [`ns` o `nsid`] y `id` para utilizar estas API.

Para limitar la carga útil en las respuestas, las API adaptan sus respuestas al tipo de construcción de identidad utilizada. Es decir, si pasa XID, las respuestas tendrán XID, si pasa identidades compuestas, la respuesta seguirá la estructura utilizada en la solicitud.

Los ejemplos de este documento no abarcan toda la funcionalidad de la API [!DNL Identity Service]. Para obtener la API completa, consulte la [Referencia de API de Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Todas las identidades devueltas se encuentran en un formulario XID nativo cuando se utiliza XID nativo en la solicitud. Se recomienda utilizar el formulario ID/namespace. Para obtener más información, consulte la sección sobre [obtención del XID para una identidad](./create-custom-namespace.md).

## Pasos siguientes

Ahora que ha reunido las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante con respecto a sus extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.
