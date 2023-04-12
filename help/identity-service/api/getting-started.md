---
keywords: Experience Platform;inicio;temas populares;api de servicio de identidad;guía para desarrolladores de servicios de identidad;región
solution: Experience Platform
title: Guía de API del servicio de identidad
description: La API del servicio de identidad permite a los desarrolladores administrar la identificación de clientes entre dispositivos, canales cruzados y casi en tiempo real mediante gráficos de identidad en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Guía de la API de [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] administra la identificación de sus clientes en varios dispositivos, canales cruzados y casi en tiempo real en lo que se conoce como gráfico de identidad dentro de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Resuelve el desafío fundamental que supone la fragmentación de los datos de perfil del cliente. Para ello, combina identidades entre dispositivos y sistemas en los que los clientes interactúan con su marca.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil unificado y de cliente en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que debe conocer o tener disponible para realizar llamadas correctamente al [!DNL Identity Service] API.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

### Enrutamiento basado en regiones

La variable [!DNL Identity Service] La API emplea extremos específicos de la región que requieren la inclusión de un `{REGION}` como parte de la ruta de solicitud. Durante el aprovisionamiento de su organización, se determina y almacena una región dentro del perfil de su organización. El uso de la región correcta con cada extremo garantiza que todas las solicitudes realizadas con la variable [!DNL Identity Service] Las API de se dirigen a la región adecuada.

Actualmente hay dos regiones que cuentan con el apoyo de [!DNL Identity Service] API: VA7 y NLD2.

La tabla siguiente muestra rutas de ejemplo que utilizan regiones:

| Service | Región: VA7 | Región: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Las solicitudes realizadas sin especificar una región pueden dar como resultado que las llamadas se dirijan a una región incorrecta o que las llamadas fallen de forma inesperada.

Si no puede localizar la región dentro del perfil de su organización, póngase en contacto con el administrador del sistema para obtener asistencia técnica.

## Al usar la variable [!DNL Identity Service] API

Los parámetros de identidad utilizados en estos servicios pueden expresarse de una de las dos maneras siguientes: compuesto o XID.

Las identidades compuestas son construcciones que incluyen tanto el valor de ID como el área de nombres. Cuando se utilizan identidades compuestas, el área de nombres se puede proporcionar mediante cualquiera de los nombres (`namespace.code`) o ID (`namespace.id`).

Cuando persiste una identidad, [!DNL Identity Service] genera y asigna un ID a esa identidad, denominada ID nativo o XID. Todas las variaciones de las API de clúster y asignación admiten tanto identidades compuestas como XID en sus solicitudes y respuestas. Se requiere uno de los parámetros: `xid` o combinación de [`ns` o `nsid`] y `id` para usar estas API.

Para limitar la carga útil en las respuestas, las API adaptan sus respuestas al tipo de construcción de identidad utilizada. Es decir, si pasa XID, las respuestas tendrán XID, si pasa identidades compuestas, la respuesta seguirá la estructura utilizada en la solicitud.

Los ejemplos de este documento no abarcan toda la funcionalidad del [!DNL Identity Service] API. Para obtener la API completa, consulte la [Referencia de la API de Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Todas las identidades devueltas se encuentran en un formulario XID nativo cuando se utiliza XID nativo en la solicitud. Se recomienda utilizar el formulario ID/namespace. Para obtener más información, consulte la sección sobre [obtención del XID para una identidad](./create-custom-namespace.md).

## Pasos siguientes

Ahora que ha reunido las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante con respecto a sus extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.
