---
keywords: Experience Platform;inicio;temas populares;API de servicio de identidad;guía para desarrolladores de servicios de identidad;región
solution: Experience Platform
title: Primeros pasos
topic: API guide
description: 'Adobe Experience Platform Identity Service gestiona la identificación de sus clientes entre dispositivos, entre canales y casi en tiempo real en lo que se conoce como gráfico de identidad dentro de Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---


# [!DNL Identity Service] Guía para desarrolladores de API

Adobe Experience Platform [!DNL Identity Service] administra la identificación entre dispositivos, entre canales y casi en tiempo real de sus clientes en lo que se conoce como un gráfico de identidad dentro de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md):: Resuelve el desafío fundamental que plantea la fragmentación de los datos de perfil de los clientes. Para ello, combina identidades entre dispositivos y sistemas en los que los clientes interactúan con su marca.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer o tener disponible para realizar llamadas exitosas a la API [!DNL Identity Service].

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

### Enrutamiento basado en la región

La API [!DNL Identity Service] emplea extremos específicos de la región que requieren la inclusión de `{REGION}` como parte de la ruta de solicitud. Durante el aprovisionamiento de la organización de IMS, se determina y almacena una región dentro del perfil de organización de IMS. El uso de la región correcta con cada extremo garantiza que todas las solicitudes realizadas mediante la API [!DNL Identity Service] se dirijan a la región adecuada.

Existen dos regiones actualmente admitidas por las API [!DNL Identity Service]: VA7 y NLD2.

La siguiente tabla muestra las rutas de ejemplo que utilizan regiones:

| Service | Región: VA7 | Región: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Las solicitudes realizadas sin especificar una región pueden dar como resultado un enrutamiento de llamadas a la región incorrecta o provocar un error inesperado en las llamadas.

Si no puede localizar la región dentro de su perfil de organización de IMS, póngase en contacto con el administrador del sistema para obtener ayuda.

## Uso de la API [!DNL Identity Service]

Los parámetros de identidad utilizados en estos servicios pueden expresarse de dos maneras: compuesto o XID.

Las identidades compuestas son construcciones que incluyen tanto el valor de ID como la Área de nombres. Al utilizar identidades compuestas, la Área de nombres se puede proporcionar con el nombre (`namespace.code`) o con el ID (`namespace.id`).

Cuando se persiste una identidad, [!DNL Identity Service] genera y asigna una ID a esa identidad, denominada ID nativa o XID. Todas las variaciones de las API de clúster y asignación admiten tanto identidades compuestas como XID en sus solicitudes y respuestas. Se requiere uno de los parámetros: `xid` o combinación de [`ns` o `nsid`] y `id` para utilizar estas API.

Para limitar la carga útil en las respuestas, las API adaptan sus respuestas al tipo de construcción de identidad utilizada. Es decir, si pasa XID, las respuestas tendrán XID, si pasa identidades compuestas, la respuesta seguirá la estructura utilizada en la solicitud.

Los ejemplos de este documento no cubren la funcionalidad completa de la API [!DNL Identity Service]. Para obtener la API completa, consulte la [Referencia de API de Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>Todas las identidades devueltas estarán en el formulario XID nativo cuando se utilice XID nativo en la solicitud. Se recomienda utilizar el formulario de ID/Área de nombres. Para obtener más información, consulte la sección sobre [obtención del XID para una identidad](./create-custom-namespace.md).

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre los extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.
