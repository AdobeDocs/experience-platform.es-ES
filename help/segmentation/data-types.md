---
keywords: Experience Platform;inicio;temas populares;tipo de datos;tipos de datos;Tipo de datos;Tipos de datos de segmentación;Segmentación;Segmentación;Servicio de segmentación;Tipos de datos del servicio de segmentación;
solution: Experience Platform
title: Tipos de datos compatibles con el servicio de segmentación
description: Todos los tipos de datos del Modelo de datos de experiencia (XDM) son compatibles con el servicio de segmentación de Adobe. Las reglas que constituyen una definición de segmento están contextualizadas por los siguientes tipos de datos.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Tipos de datos compatibles con el servicio de segmentación

Todos los tipos de datos del Modelo de datos de experiencia (XDM) son compatibles con el servicio de segmentación de Adobe Experience Platform. Las reglas que constituyen una definición de segmento están contextualizadas por los siguientes tipos de datos.

## Datos de cadena

Las definiciones de segmentos utilizan datos de cadena para definir restricciones no numéricas para audiencias de segmento, como &quot;nombre de país&quot; o &quot;nivel de programa de lealtad&quot;.

Los datos de cadena se incluyen en las definiciones de segmentos mediante instrucciones lógicas, inclusivas/exclusivas y de comparación. Una vez que se agrega un atributo de cadena a su definición de segmento, puede utilizar instrucciones relevantes para cadenas para evaluarlo en relación con otros campos de cadena.

| Tipo de instrucción | Ejemplos |
| -------------- | -------- |
| Lógica | `and`, `or`, `not` |
| Incluido/exclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparación | `equals`, `does not equal`, `contains`, `starts with` |

## Datos de fecha

Los datos de fecha le permiten asignar un contexto basado en el tiempo a sus definiciones de segmento, ya sea utilizando fechas de inicio/finalización específicas o utilizando instrucciones relevantes para la fecha como se muestra en la tabla siguiente. Una implementación podría estar creando una audiencia de clientes que han interactuado con su marca en cualquier momento *este año* y también ha estado activo *en* los últimos días.

| Campo de ejemplo | Declaraciones pertinentes a la fecha | Escala de cronología |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevante para el día en que se creó el segmento. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevante en cualquier semana/mes determinado. |

## Eventos de experiencias

Como esquema de Adobe Experience Platform, [!DNL XDM ExperienceEvents] registrar interacciones de clientes explícitas e implícitas con [!DNL Platform]- aplicaciones integradas, incluyendo una instantánea del sistema en el momento en que se realizó la interacción. [!DNL ExperienceEvents] son registros de hechos. Como tal, son una fuente de datos disponible durante la definición del segmento.

Como se ve en la tabla siguiente, los datos de evento se procesan con palabras clave que ayudan a refinar el comportamiento del evento y a especificar atributos de evento.

| Palabra clave | Utilice  |
| ------- | --- |
| Incluir/excluir | Describe el comportamiento del evento mediante la inclusión u omisión de datos. |
| Cualquiera/todo | Ayuda a determinar el número de segmentos aptos. |
| Botón de alternador &quot;Aplicar regla de tiempo&quot; | Incorpora datos de fecha. |
| Es igual a, no es igual a, empieza por, no comienza por, termina por, no termina por, contiene, no contiene, existe, no existe | Incorpora datos de cadenas. |

### Uso compartido de audiencias

Las audiencias externas también se pueden usar como componentes de una nueva definición de segmento, agregando sus reglas de atributos al nuevo segmento.

Actualmente, solo Adobe Audience Manager es compatible como audiencia externa, y en el futuro se habilitarán fuentes adicionales. Puede encontrar más información sobre el uso de audiencias de Adobe Audience Manager con Platform en la [guía de uso compartido de audiencias en la documentación de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Uso compartido de segmentos

Los segmentos creados en Platform se pueden usar en otros [Servicios principales de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=es). Para habilitar esta función, deberá ponerse en contacto con su arquitecto de soluciones o con su asesor.

## Otros tipos de datos

Además de los tipos de datos mencionados anteriormente, la lista de tipos de datos admitidos también incluye:

- Identificador uniforme de recursos (URI)
- Enum
- Número
- Largo
- Número entero
- corto
- Byte
- Booleano
- Matriz
- Objeto
- Mapa
