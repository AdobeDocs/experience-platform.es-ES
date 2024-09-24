---
title: Información general sobre el asistente de IA en Adobe Experience Platform
description: Obtenga información sobre el asistente de IA, sus matices y casos de uso, y cómo puede utilizarlo para acelerar el flujo de trabajo con Adobe Experience Platform y Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: 0926a0e8c7ae560bf5f4f9ff6853b191af047738
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 16%

---

# Asistente de IA en Adobe Experience Platform

El siguiente vídeo tiene como objetivo ayudarle a comprender el asistente de IA.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Lea este documento para obtener más información sobre el asistente de IA en Adobe Experience Platform.

El Asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el Asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El Asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

![Interfaz del asistente de IA con la primera experiencia de usuario desencadenada.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Debe aceptar un [acuerdo de usuario](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) para poder usar el Asistente para IA. El contrato de usuario también contiene el contrato de versión beta pública. Esto es para que pueda utilizar funciones adicionales del asistente de IA a medida que se implementan en una capacidad beta.

+++Seleccionar para ver la interfaz de acuerdo de usuario

![Primera página del acuerdo de usuario.](./images/user-agreement-1.png)

![Última página del acuerdo de usuario.](./images/user-agreement-2.png)

+++

## Explicación del asistente de IA {#understanding-ai-assistant}

El asistente de IA responde a las preguntas enviadas consultando una base de datos y luego traduciendo los datos de la base de datos a una respuesta legible en lenguaje natural.

Esta representación interna de datos subyacentes también se conoce como **[!DNL Knowledge Graph]**: una web completa de conceptos, datos y metadatos para una respuesta determinada.

[!DNL Knowledge Graph] consta de subgráficos a los que se hace referencia cada vez que se envían consultas:

* Perspectivas operativas del cliente.
* Perspectivas operativas del cliente en varias metatiendas.
* Documentación del Experience League.

Hay dos clases de preguntas que se deben tener en cuenta antes de consultar el Asistente de IA:

### Conocimiento del producto {#product-knowledge}

El conocimiento del producto hace referencia a conceptos y temas basados en la documentación del Experience League. Las preguntas sobre conocimientos del producto se pueden especificar en los siguientes subgrupos:

| Conocimiento del producto | Ejemplos |
| --- | --- |
| Aprendizaje puntual | <ul><li>¿Cuál es la diferencia entre una identidad y una clave principal o externa?</li><li>¿Qué es el Público similar?</li></ul> |
| Abrir detección | <ul><li>¿Cómo puedo exportar este conjunto de datos?</li><li>¿Existen esquemas para los clientes del sector sanitario?</li></ul> |
| Resolución de problemas | <ul><li>¿Por qué no puedo activar un esquema propiedad de Adobe para el perfil?</li><li>¿Por qué no puedo eliminar un segmento?</li></ul> |

{style="table-layout:auto"}

### Datos operativos {#operational-insights}

>[!IMPORTANT]
>
>Las respuestas de Operational Insights están en versión beta. Cualquier persona que tenga acceso al permiso **Ver perspectivas operativas** tendrá acceso a las respuestas de perspectivas operativas.

Perspectivas operativas se refiere a las respuestas que genera AI Assistant sobre los objetos de metadatos (atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes), incluidos los recuentos, las búsquedas y el impacto en el linaje. No observa ningún dato dentro de la zona protegida.

* ¿Cuántos conjuntos de datos tengo?
* ¿Cuántos atributos de esquema nunca se han utilizado?
* ¿Qué audiencias se han activado?

Puede hacer preguntas al asistente de IA sobre sus perspectivas operativas en los siguientes dominios:

| Dominio | Metadatos admitidos | Metadatos no admitidos |
| --- | --- | --- |
| Atributos | <ul><li>Búsqueda de nombre de atributo</li><li>Atributo: relación de esquema</li><li>Atributo: relación de conjunto de datos</li><li>Atributo: relación de audiencia</li><li>Atributo: relación de destino</li></ul> | <ul><li>Clase de atributo</li><li>Auditoría</li><li>Estado de obsolescencia</li><li>Etiquetas</li><li>Valor almacenado en atributos</li></ul> |
| Públicos | <ul><li>Recuento de público</li><li>Tipo de audiencia (flujo continuo o por lotes)</li><li>Fechas de creación/modificación</li><li>Estado de activación</li><li>Recuento de perfiles</li><li>Duplicar audiencias</li><li>Búsqueda de definición de audiencia</li><li>Audiencia: relación de audiencia</li><li>Audiencia: relación de atributos</li><li>Audiencia: relación entre conjuntos de datos</li><li>Audiencia: relación de destino</li><li>Búsqueda de nombres</li><li>Búsqueda de nombre e ID | <ul><li>Superposiciones de audiencias</li><li>Activación de público</li><li>Audiencia: relaciones de campaña</li><li>Auditoría</li><li>Crear/modificar</li><li>Etiquetas</li><li>Tendencias de calificación de perfiles</li></ul> |
| Flujos de datos | <ul><li>Recuentos de flujo de datos</li><li>Estado de flujo de datos</li><li>Flujo de datos: relación de conjunto de datos</li><li>Flujo de datos: relación de origen</li></ul> | <ul><li>Creación/modificación</li><li>Relaciones entre flujo de datos y lotes</li><li>Ingesta de recuento de perfiles</li></ul> |
| Conjuntos de datos | <ul><li>Recuento de conjuntos de datos</li><li>Estado de habilitación de perfil</li><li>Fecha de creación/modificación</li><li>Conjunto de datos: relación de esquema</li><li>Conjunto de datos: relación de audiencia</li><li>Conjunto de datos: relación de atributos</li><li>Conjunto de datos: relación de flujo de datos</li><li>Búsqueda de nombres </li><li>Búsqueda de nombre e ID</li></ul> | <ul><li>Auditoría</li><li>Creado por</li><li>Conjunto de datos: relación por lotes</li><li>Creación/modificación de conjuntos de datos</li><li>Tamaño del conjunto de datos</li><li>Número de perfiles</li><li>Número de filas</li><li>Búsqueda de valores</li></ul> |
| Destinos | <ul><li>Recuentos de destino configurados</li><li>Destino: relación de audiencia</li><li>Relación de atributo de destino</li></ul> | <ul><li>Configuración de cuenta</li><li>Información de credenciales de cuenta</li><li>Perfiles únicos activados</li></ul> |
| Recorridos | <ul><li>Recuentos</li><li>Búsqueda de nombres</li><li>Búsqueda de nombre e ID</li><li>Estado del recorrido</li><li>Estado de activación (audiencia frente a eventos)</li><li>Fechas de creación/modificación</li><li>Frecuencia recurrente</li></ul> | <ul><li>Atributos: relaciones de recorrido</li><li>Auditoría</li><li>Creación/modificación</li><li>Creado por</li><li>Eventos</li><li>Recorrido: conjunto de datos</li><li>Recorrido - esquema</li><li>Ofertas</li><li>Tendencias de calificación de perfiles</li><li>Eventos de paso</li></ul> |
| Esquemas | <ul><li>Recuentos de esquemas</li><li>Fecha de creación/modificación</li><li>Esquema: relación de atributos</li><li>Esquema: relación del conjunto de datos</li><li>Esquema: relación de audiencia</li><li>Estado de habilitación de perfil</li><li>Búsqueda de nombres</li><li>Búsqueda de nombre e ID</li></ul> | <ul><li>Auditoría</li><li>Creación/modificación</li><li>Creado por</li><li>Grupos de campo</li><li>Identidades</li><li>Áreas de nombres de identidad</li><li>Etiquetas</li><li>Número de perfiles</li></ul> |
| Fuentes | <ul><li>Recuentos de cuentas</li><li>Estado de cuenta</li><li>Flujos de datos activos/inactivos para cada cuenta</li><li>Conector de Source: relación de flujo de datos</li><li>cuenta de Source: relación de flujo de datos</li></ul> | <ul><li>Información de credenciales de cuenta</li><li>Configuración de cuenta</li><li>Métricas de ingesta de datos</li><li>Número de perfiles</li><li>Source: relaciones por lotes</li></ul> |

{style="table-layout:auto"}

Para las preguntas de información operativa, es posible que las respuestas no reflejen el estado actual de la interfaz de usuario. Los datos que respaldan estas preguntas se actualizan una vez cada 24 horas. Por ejemplo, los cambios que los usuarios realizan en Real-Time CDP durante el día se sincronizan con los almacenes de datos por la noche y, a continuación, están disponibles para que los usuarios formulen preguntas por la mañana. Deberá iniciar sesión en una zona protegida para consultar sobre datos específicos relacionados con los objetos.

### Funcionalidad del ámbito {#feature-scope}

En la actualidad, el ámbito del asistente de IA es el siguiente:

* [Conocimiento del producto](./home.md#product-knowledge): el Asistente de IA puede responder preguntas de conocimiento del producto para Experience Platform, Real-time Customer Data Platform y Adobe Journey Optimizer. También puede profundizar en los temas de conocimiento del producto para Customer Journey Analytics, pero solo a través de la interfaz de usuario de Customer Journey Analytics.
* [Perspectivas operativas](./home.md#operational-insights): puede hacer preguntas al Asistente de IA sobre perspectivas operativas en los siguientes objetos de datos: atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes.

## Pasos siguientes

Ahora que tiene una comprensión general de AI Assistant, puede continuar y utilizar AI Assistant durante los flujos de trabajo. Consulte la siguiente documentación para obtener más información:

* [Guía de IU del asistente de IA](./ui-guide.md)
* [Acceso a funciones](./access.md)
* [Guía de preguntas](./questions.md)
* [Privacidad, seguridad y administración en el asistente de IA](./privacy.md)
* [Preguntas frecuentes](./faq.md)
