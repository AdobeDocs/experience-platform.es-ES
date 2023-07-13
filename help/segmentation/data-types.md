---
solution: Experience Platform
title: Tipos de datos admitidos en el servicio de segmentación
description: Todos los tipos de datos del modelo de datos de experiencia (XDM) son compatibles con el servicio de segmentación de Adobe. Las reglas que constituyen una definición de segmento se contextualizan con los siguientes tipos de datos.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# Tipos de datos admitidos en el servicio de segmentación

Todos los tipos de datos del Modelo de datos de experiencia (XDM) son compatibles con el servicio de segmentación de Adobe Experience Platform. Las reglas que constituyen una definición de segmento se contextualizan con los siguientes tipos de datos.

## Datos de cadena

Las definiciones de segmentos utilizan datos de cadena para definir restricciones no numéricas para audiencias, como &quot;nombre de país&quot; o &quot;nivel de programa de lealtad&quot;.

Los datos de cadena se incluyen en las definiciones de segmentos mediante instrucciones lógicas, inclusivas/exclusivas y de comparación. Una vez agregado un atributo de cadena a la definición del segmento, puede utilizar instrucciones relevantes para la cadena para evaluarlo con otros campos de cadena.

| Tipo de instrucción | Ejemplos |
| -------------- | -------- |
| Lógico | `and`, `or`, `not` |
| Inclusivo/exclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparación | `equals`, `does not equal`, `contains`, `starts with` |

## Datos de fecha

Los datos de fecha le permiten asignar un contexto basado en el tiempo a sus definiciones de segmento, ya sea mediante el uso de fechas de inicio/fin específicas o mediante el uso de instrucciones relevantes por fecha, como se muestra en la tabla siguiente. Una implementación podría crear una audiencia de clientes que hayan interactuado con su marca en cualquier momento *este año* y también ha estado activo *dentro* los últimos días.

| Campo de ejemplo | Declaraciones relevantes para la fecha | Escala de cronología |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevante para el día en que se creó la definición del segmento. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevante en cualquier semana/mes dado. |

## Eventos de experiencia

Como esquema de Adobe Experience Platform, [!DNL XDM ExperienceEvents] registrar interacciones explícitas e implícitas de clientes con [!DNL Platform]aplicaciones integradas por el usuario, incluida una instantánea del sistema en el momento en que tuvo lugar la interacción. [!DNL ExperienceEvents] son registros de hechos. Como tal, son una fuente de datos disponible durante la definición del segmento.

Como se ve en la tabla siguiente, los datos de evento se representan con palabras clave que ayudan a refinar el comportamiento del evento y especificar atributos de evento.

| Palabra clave | Utilice  |
| ------- | --- |
| Incluir/excluir | Describe el comportamiento del evento mediante la inclusión u omisión de datos. |
| Cualquiera/todos | Ayuda a determinar el número de definiciones de segmento aptas. |
| Botón de alternancia &quot;Aplicar regla de tiempo&quot; | Incorpora datos de fecha. |
| Es igual a, no es igual a, comienza con, no comienza con, termina con, no termina con, contiene, no contiene, existe, no existe | Incorpora datos de cadena. |

### Uso compartido de audiencias

Las audiencias externas también se pueden utilizar como componentes de una nueva definición de segmento y añadir sus reglas de atributos a las nuevas definiciones de segmento.

Actualmente, solo se admite Adobe Audience Manager como audiencia externa y las fuentes adicionales se habilitarán en el futuro. Encontrará más información sobre el uso de audiencias de Adobe Audience Manager con Platform en la [guía de uso compartido de audiencias en la documentación de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Uso compartido de definiciones de segmento

Las definiciones de segmentos creadas en Platform se pueden usar en otros [Servicios principales de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=es). Para habilitar esta función, deberá ponerse en contacto con el arquitecto de la solución o con el consultor.

## Otros tipos de datos

Además de los tipos de datos mencionados anteriormente, la lista de tipos de datos admitidos también incluye:

- Identificador uniforme de recursos (URI)
- Enumeración
- Número
- Largo
- Número entero
- corto
- Byte
- Booleano
- Matriz
- Objeto
- Mapa
