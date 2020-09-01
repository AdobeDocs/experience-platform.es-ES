---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type;Segmentation data types;Segmentation;segmentation;Segmentation Service;Segmentation service data types;
solution: Experience Platform
title: Tipos de datos del servicio de segmentación de Adobe Experience Platform
topic: overview
description: Todos los tipos de datos XDM son compatibles con el servicio de segmentación. Las reglas que constituyen una definición de segmento están contextualizadas por los siguientes tipos de datos.
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Tipos de datos admitidos por Adobe Experience Platform [!DNL Segmentation Service]

Todos los tipos de datos XDM son compatibles en [!DNL Segmentation Service]. Las reglas que constituyen una definición de segmento están contextualizadas por los siguientes tipos de datos.

## Datos de cadena

Las definiciones de segmentos utilizan datos de cadena para definir restricciones no numéricas para audiencias de segmentos, como &quot;nombre de país&quot; o &quot;nivel de programa de lealtad&quot;.

Los datos de cadena se incluyen en las definiciones de segmentos mediante sentencias lógicas, inclusivas/exclusivas y comparativas. Una vez que se agrega un atributo de cadena a la definición del segmento, puede utilizar afirmaciones relevantes para la cadena para evaluarlo con otros campos de cadena.

| Tipo de instrucción | Ejemplos |
| -------------- | -------- |
| Lógico | `and`, `or`, `not` |
| Incluido/exclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparación | `equals`, `does not equal`, `contains`, `starts with` |

## Datos de fecha

Los datos de fecha le permiten asignar un contexto basado en la hora a las definiciones de segmentos, ya sea mediante el uso de fechas de inicio/finalización específicas o mediante declaraciones de fecha relevantes, como se muestra en la tabla siguiente. Una implementación podría estar creando una audiencia de clientes que han interactuado con su marca en cualquier momento *este año* y que también han estado activos *en los* últimos días.

| Campo de ejemplo | Declaraciones pertinentes a la fecha | Escala de tiempo |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevante para el día en que se creó el segmento. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevante en cualquier semana/mes. |

## Eventos de experiencias

Como esquema de Adobe Experience Platform, [!DNL XDM ExperienceEvents] registre las interacciones explícitas e implícitas de los clientes con aplicaciones [!DNL Platform]integradas, incluida una instantánea del sistema en el momento en que se produjo la interacción. [!DNL ExperienceEvents] son registros de hechos. Por lo tanto, son una fuente de datos disponible durante la definición del segmento.

Como se muestra en la tabla siguiente, los datos de evento se representan utilizando palabras clave que ayudan a reducir el comportamiento de evento y a especificar atributos de evento.

| Palabra clave | Utilice  |
| ------- | --- |
| Incluir/excluir | Describe el comportamiento del evento mediante la inclusión u omisión de datos. |
| Cualquiera/todo | Ayuda a determinar el número de segmentos cualificados. |
| Botón de alternancia &quot;Aplicar regla de tiempo&quot; | Incorpora datos de fecha. |
| Es igual a, no es igual a, inicios con, no inicio con, termina con, no termina con, contiene, no contiene, existe, no existe | Incorpora datos de cadena. |

### Uso compartido de audiencias

Las audiencias externas también se pueden usar como componentes de una nueva definición de segmento, agregando sus reglas de atributos al nuevo segmento.

Actualmente, solo se admite Adobe Audience Manager como audiencia externa, y en el futuro se habilitarán fuentes adicionales. Encontrará más información sobre el uso de audiencias de Adobe Audience Manager con plataforma en la guía de uso compartido de [audiencias de la documentación](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)de Adobe Audience Manager.

### Uso compartido de segmentos

Los segmentos creados en la plataforma se pueden usar en otros servicios [principales de](https://docs.adobe.com/content/help/es-ES/core-services/interface/experience-cloud.html)Adobe Experience Cloud. Para habilitar esta función, deberá ponerse en contacto con su arquitecto de soluciones o con su asesor.

## Otros tipos de datos

Además de los tipos de datos mencionados anteriormente, la lista de los tipos de datos admitidos también incluye:

- Identificador uniforme de recursos (URI)
- Enum
- Número
- Largo
- Número entero
- Corto
- Byte
- Booleano
- Matriz
- Objeto
- Mapa