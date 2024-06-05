---
title: Información general sobre el asistente de IA en Adobe Experience Platform
description: Obtenga información sobre el asistente de IA, sus matices y casos de uso, y cómo puede utilizarlo para acelerar el flujo de trabajo con Adobe Experience Platform y Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: b51291e6c3663c6d6e6d416f0d2c37563c852155
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---

# Asistente de IA en Adobe Experience Platform

Lea este documento para obtener más información sobre el asistente de IA en Adobe Experience Platform.

El asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

![Interfaz del asistente de IA con la primera experiencia del usuario activada.](./images/blank.png)

>[!IMPORTANT]
>
>Debe aceptar una [acuerdo de usuario](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) antes de poder usar el asistente de IA. El contrato de usuario también contiene el contrato de versión beta pública. Esto es para que pueda utilizar funciones adicionales del asistente de IA a medida que se implementan en una capacidad beta.

+++Seleccionar para ver la interfaz de acuerdo de usuario

![Primera página del acuerdo de usuario.](./images/user-agreement-1.png)

![La última página del acuerdo de usuario.](./images/user-agreement-2.png)

+++

## Explicación del asistente de IA {#understanding-ai-assistant}

El asistente de IA responde a las preguntas enviadas consultando una base de datos y luego traduciendo los datos de la base de datos a una respuesta legible en lenguaje natural.

Esta representación interna de los datos subyacentes también se conoce como **[!DNL Knowledge Graph]** : una amplia red de conceptos, datos y metadatos para una respuesta determinada.

El [!DNL Knowledge Graph] consta de subgráficos a los que se hace referencia cada vez que se envían consultas:

* Perspectivas operativas del cliente.
* Perspectivas operativas del cliente en varias metatiendas.
* Documentación del Experience League.

Hay dos clases de preguntas que se deben tener en cuenta antes de consultar el Asistente de IA:

### Conocimiento del producto {#product-knowledge}

El conocimiento del producto hace referencia a conceptos y temas basados en la documentación del Experience League. Las preguntas sobre conocimientos del producto se pueden especificar en los siguientes subgrupos:

| Conocimiento del producto | Ejemplos |
| --- | --- |
| Aprendizaje puntual | <ul><li>¿Cuál es la diferencia entre una identidad y una clave principal o externa?</li><li>¿Cómo se calcula la riqueza de perfiles?</li></ul> |
| Abrir detección | <ul><li>¿Cómo puedo exportar este conjunto de datos?</li><li>¿Existen esquemas para los clientes del sector sanitario?</li></ul> |
| Resolución de problemas | <ul><li>¿Por qué no puedo activar un esquema propiedad de Adobe para el perfil?</li><li>¿Por qué no puedo eliminar un segmento?</li></ul> |

{style="table-layout:auto"}

### Perspectivas operativas {#operational-insights}

>[!IMPORTANT]
>
>Las respuestas de Operational Insights están en versión beta. Cualquier persona que tenga acceso a **Ver perspectivas operativas** El permiso de tendrá acceso a las respuestas de información operativa.

Perspectivas operativas se refiere a las respuestas que genera AI Assistant sobre los objetos de metadatos (atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes), incluidos los recuentos, las búsquedas y el impacto en el linaje. No observa ningún dato dentro de la zona protegida.

* ¿Cuántos conjuntos de datos tengo?
* ¿Cuántos atributos de esquema nunca se han utilizado?
* ¿Qué audiencias se han activado?

Puede hacer preguntas al asistente de IA sobre sus perspectivas operativas en los siguientes dominios:

* Atributos
* Públicos
* Flujos de datos
* Conjuntos de datos
* Destinos _(Las preguntas relativas a las cuentas y algunas preguntas sobre el flujo de datos no se pueden responder en este momento)._
* Recorridos
* Esquemas _(Las preguntas relativas a los grupos de campos no se pueden responder en este momento)._
* Fuentes _(Las preguntas relativas a las cuentas no se pueden responder en este momento)._

Para las preguntas de información operativa, es posible que las respuestas no reflejen el estado actual de la interfaz de usuario. Los datos que respaldan estas preguntas se actualizan una vez cada 24 horas. Por ejemplo, los cambios que los usuarios realizan en Real-Time CDP durante el día se sincronizan con los almacenes de datos por la noche y, a continuación, están disponibles para que los usuarios formulen preguntas por la mañana. Deberá iniciar sesión en una zona protegida para consultar sobre datos específicos relacionados con los objetos.

### Alcance de la función {#feature-scope}

En la actualidad, el ámbito del asistente de IA es el siguiente:

* [Conocimiento del producto](./home.md#product-knowledge): el asistente de IA puede responder preguntas de conocimiento del producto para Experience Platform, Real-time Customer Data Platform y Adobe Journey Optimizer. También puede profundizar en los temas de conocimiento del producto para Customer Journey Analytics, pero solo a través de la interfaz de usuario de Customer Journey Analytics.
* [Perspectivas operativas](./home.md#operational-insights): puede hacer preguntas al asistente de IA sobre las perspectivas operativas en los siguientes objetos de datos: atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes.

## Pasos siguientes

Ahora que tiene una comprensión general de AI Assistant, puede continuar y utilizar AI Assistant durante los flujos de trabajo. Consulte la siguiente documentación para obtener más información:

* [Guía de IU del asistente de IA](./ui-guide.md)
* [Acceso a funciones](./access.md)
* [Guía de preguntas](./questions.md)
* [Privacidad, seguridad y administración en el asistente de IA](./privacy.md)
* [Preguntas frecuentes](./faq.md)
