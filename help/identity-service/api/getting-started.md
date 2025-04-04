---
keywords: Experience Platform;inicio;temas populares;api del servicio de identidad;guía para desarrolladores del servicio de identidad;región
solution: Experience Platform
title: Guía de API del servicio de identidad
description: La API del servicio de ID permite a los desarrolladores administrar la identificación de sus clientes en varios dispositivos, canales cruzados y casi en tiempo real mediante gráficos de identidad en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 14%

---

# Guía de la API de [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] administra la identificación de sus clientes en varios dispositivos, canales cruzados y casi en tiempo real en lo que se conoce como gráfico de identidad dentro de Adobe Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): resuelve el desafío fundamental que plantea la fragmentación de los datos de perfil del cliente. Para ello, une las identidades entre dispositivos y sistemas en los que los clientes interactúan con la marca.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado en tiempo real en función de los datos agregados de varios orígenes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que necesitará saber o tener disponible para realizar llamadas correctamente a la API [!DNL Identity Service].

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

### Enrutamiento basado en regiones

La API [!DNL Identity Service] emplea extremos específicos de región que requieren la inclusión de un `{REGION}` como parte de la ruta de solicitud. Durante el aprovisionamiento de la organización, se determina una región y se almacena dentro del perfil de la organización. El uso de la región correcta con cada extremo garantiza que todas las solicitudes realizadas mediante la API [!DNL Identity Service] se enruten a la región adecuada.

Actualmente hay dos regiones compatibles con las API de [!DNL Identity Service]: VA7 y NLD2.

En la tabla siguiente se muestran ejemplos de rutas que utilizan regiones:

| Servicio | Región: VA7 | Región: NLD2 |
| ------ | -------- |--------- |
| API [!DNL Identity Service] | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| API [!DNL Identity Namespace] | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Las solicitudes realizadas sin especificar una región pueden dar como resultado el enrutamiento de llamadas a la región incorrecta o provocar errores inesperados en las llamadas.

Si no puede localizar la región dentro del perfil de su organización, póngase en contacto con el administrador del sistema para obtener ayuda.

## Usando la API [!DNL Identity Service]

Los parámetros de identidad utilizados en estos servicios se pueden expresar de una de las dos maneras siguientes: compuesto o XID.

Las identidades compuestas son construcciones que incluyen el valor de ID y el área de nombres. Al utilizar identidades compuestas, el espacio de nombres se puede proporcionar mediante el nombre (`namespace.code`) o el identificador (`namespace.id`).

Cuando persiste una identidad, [!DNL Identity Service] genera y asigna un ID a esa identidad, denominado ID nativo o XID. Todas las variaciones de las API de clúster y asignación admiten identidades compuestas y XID en sus solicitudes y respuestas. Se requiere uno de los parámetros: `xid` o una combinación de [`ns` o `nsid`] y `id` para usar estas API.

Para limitar la carga útil en las respuestas, las API adaptan sus respuestas al tipo de construcción de identidad utilizada. Es decir, si pasa XID, las respuestas tendrán XID, si pasa identidades compuestas, la respuesta seguirá la estructura utilizada en la solicitud.

Los ejemplos de este documento no abarcan toda la funcionalidad de la API [!DNL Identity Service]. Para obtener la API completa, consulte [Referencia de la API de Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Todas las identidades devueltas estarán en formato XID nativo cuando se utilice XID nativo en la solicitud. Se recomienda utilizar el formulario ID/área de nombres. Para obtener más información, consulte la sección sobre [obtención del XID para una identidad](./create-custom-namespace.md).

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre sus puntos de conexión y muestra llamadas de API de ejemplo para realizar operaciones de CRUD. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, así como una respuesta de ejemplo para una llamada correcta.
