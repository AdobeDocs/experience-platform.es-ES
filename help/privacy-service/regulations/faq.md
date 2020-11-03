---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;faq;FAQ;regulation;Regulation;regulations;Regulations;privacy;Privacy;
solution: Experience Platform
title: Preguntas más frecuentes sobre la regulación de la privacidad
topic: troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre las normativas de privacidad legales admitidas y su implementación en Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: b36e6c4e92d6591f87c2cc4f5e1e607056b0957c
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 1%

---


# Preguntas más frecuentes sobre la regulación de la privacidad

Este documento proporciona respuestas a las preguntas más frecuentes sobre las normativas de privacidad legales admitidas y su implementación en Adobe Experience Cloud.

>[!NOTE]
>
>Las definiciones de los distintos términos utilizados en este documento se encuentran en la guía terminológica [de regulación de la](terminology.md) privacidad.

## Preguntas generales

Las siguientes preguntas se relacionan con todas las regulaciones de privacidad admitidas por el Experience Cloud.

### ¿A quién afectan las regulaciones de privacidad admitidas?

Las normas de [privacidad respaldadas por el Experience Cloud](./overview.md) se aplican a todas las organizaciones que almacenan y procesan los datos personales de los ciudadanos dentro de las respectivas jurisdicciones de la organización, independientemente de su ubicación geográfica.

### ¿Qué constituye los datos personales?

Datos personales es toda información relacionada con una persona física o con un interesado que puede utilizarse para identificar directa o indirectamente a la persona. Puede ser cualquier cosa desde un nombre, una foto, una dirección de correo electrónico, detalles del banco, publicaciones en sitios web de redes sociales, información médica o una dirección IP del equipo.

Los siguientes identificadores se utilizan comúnmente en aplicaciones Experience Cloud y podrían estar sujetos a los requisitos de la normativa de privacidad:

* Nombre
* Dirección postal
* Identificador personal único
* Identificador en línea
* Dirección IP
* Correo electrónico Dirección
* Nombre de la cuenta

La información personal también puede incluir información de actividad de Internet u otra red electrónica. Esto incluye, entre otras cosas:

* Historial de exploración
* Historial de búsqueda
* Información sobre la interacción de un consumidor con un sitio web, una aplicación o un anuncio

Aunque las regulaciones de privacidad cubren un amplio conjunto de información personal, los términos de contrato estándar de Adobe dictan que la información personal delicada (como SSN, información de licencia de conducir, información de cuenta financiera y datos biométricos) generalmente está prohibida de importar y utilizar en aplicaciones Experience Cloud.

### ¿Cuál es la diferencia entre un controlador de datos y un procesador de datos?

Un controlador **de** datos es la entidad que determina los fines, las condiciones y los medios para procesar los datos personales, mientras que el procesador **de** datos es una entidad que procesa los datos personales en nombre del controlador de datos.

Un controlador **de datos** es la persona u organización que tiene el poder y la responsabilidad de tomar decisiones con respecto a la recopilación, el uso o la divulgación de datos personales. Un procesador **de** datos es la persona u organización que trabaja en relación con la recopilación, el uso o la divulgación de los datos personales y la dirección del controlador de datos.

### ¿Cuál es la diferencia entre el consentimiento explícito y sin ambigüedades del sujeto de datos?

**El consentimiento** explícito se refiere a una norma de consentimiento que implica una indicación específica, informada e inequívoca de los deseos del interesado en forma oral o escrita. En pocas palabras, el sujeto de los datos debe decir literal y explícitamente &quot;Acepto&quot; o &quot;Acepto&quot; para que el consentimiento se considere explícito. Además, debe ser tan fácil retirar el consentimiento como concederlo.

**El consentimiento** inequívoco (implícito) se refiere al consentimiento que el interesado no dio explícitamente, pero que, sin embargo, es de naturaleza inequívoca. Por ejemplo, durante el proceso de registro de un sitio web de compañía, se notifica que al proporcionar una dirección de correo electrónico, el sujeto de datos consiente en recibir correos electrónicos en ofertas especiales. Si el interesado lee la notificación, la acción afirmativa de introducir su correo electrónico es suficiente para que se considere un consentimiento inequívoco.

Para muchas regulaciones como el RGPD, se requiere el consentimiento explícito para procesar datos personales sensibles, donde nada menos que &quot;adhesión&quot; será suficiente. Sin embargo, en el caso de los datos no sensibles, se acepta el consentimiento inequívoco (implícito).

### ¿Pueden dar su consentimiento los sujetos de datos menores de cierta edad?

Todas las regulaciones de privacidad estipulan que si una persona de datos es menor de cierta edad, no puede dar su consentimiento legal para la recopilación de sus datos personales. Algunos reglamentos permiten que el titular de la patria potestad dé su consentimiento respecto de ese interesado en estos casos, pero no en todos. En el cuadro siguiente se lista la edad mínima para que los interesados den su consentimiento para cada reglamento, con notas para obtener más información:

| Reglamento | Edad del consentimiento | Notas |
| --- | --- | --- |
| CCPA (California) | 16 | <ul><li>El consentimiento paterno sólo puede proporcionarse para personas de 13 años o más.</li><li>La recogida de datos personales de personas menores de 13 años está estrictamente prohibida.</li></ul> |
| RGPD (Unión Europea) | 16 | <ul><li>Algunos Estados miembros de la UE pueden promulgar una ley para una edad inferior con ese fin, pero no inferior a los 13 años.</li><li>Se debe proporcionar el consentimiento paterno para todos los sujetos de datos por debajo del límite de edad.</li></ul> |
| LGPD (Brasil) | 13 | <ul><li>Se debe proporcionar el consentimiento paterno para todos los sujetos de datos por debajo del límite de edad.</li><li>El consentimiento puede ser otorgado por una persona física de entre 13 y 18 años, siempre que el tratamiento de sus datos personales se someta a su interés superior.</li></ul> |
| PDPA (Tailandia) | 10 | <ul><li>Se debe proporcionar el consentimiento paterno para todos los sujetos de datos por debajo del límite de edad.</li></ul> |

### ¿Cuántos días tiene una empresa para responder a una solicitud del consumidor de acceder o eliminar información personal?

Suponiendo que la empresa ha recopilado información personal y que puede autenticar o verificar la identidad de un consumidor en particular, las normas de privacidad permiten un período de tiempo específico para que se cumpla una solicitud de consumidor. En el cuadro siguiente se desglosan los plazos aplicables a cada reglamento, con notas sobre algunas excepciones:

| Reglamento | Ventana Cumplimiento | Notas |
| --- | --- | --- |
| CCPA (California) | 45 días |  |
| RGPD (Unión Europea) | 30 días | Si la solicitud es compleja o el mismo sujeto de datos ha realizado numerosas solicitudes, la solicitud puede ampliarse a 60 días. |
| LGPD (Brasil) | 15 días |  |
| PDPA (Tailandia) | 30 días | Si una compañía no puede responder a la solicitud de un sujeto de datos dentro de la ventana de cumplimiento, la compañía tendrá 30 días adicionales a partir de la fecha en que no pudo cumplir la solicitud de respuesta por escrito al sujeto de datos. |

### ¿Mi empresa necesita designar un oficial de protección de datos?

Si las operaciones de datos de su organización se encuentran dentro de las jurisdicciones legales del RGPD, la LGPD o la PDPA, debe designar un responsable de protección de datos (RPD) en los siguientes casos:

* Su organización es una autoridad pública
* Su organización realiza un monitoreo sistemático a gran escala
* Su organización se dedica al procesamiento a gran escala de datos personales confidenciales.

>[!IMPORTANT]
>
>A diferencia de otros reglamentos, la CCPA sí estipula que esto es un requisito. Sin embargo, se recomienda generalmente que para mantener el cumplimiento de la privacidad, una compañía tenga actividades individuales de recopilación de datos de monitoreo y el almacenamiento de los datos de los consumidores, así como responder a las consultas de los clientes.

### ¿Cómo puedo apoyar las solicitudes de privacidad de los consumidores si mantengo datos que están cubiertos por las regulaciones de privacidad?

Una vez que haya tomado las medidas necesarias para autenticar a los consumidores que se encuentran dentro de las jurisdicciones legales correspondientes, Adobe Experience Platform Privacy Service le permite enviar solicitudes de privacidad de los consumidores a aplicaciones Experience Cloud compatibles. See the [[!DNL Privacy Service] overview](../home.md) for more information. Para obtener información sobre cómo sus aplicaciones Experience Cloud particulares pueden cumplir con las solicitudes de privacidad, consulte la guía sobre aplicaciones [para](../experience-cloud-apps.md)Privacy Service y Experience Cloud.

>[!NOTE]
>
>Todavía se está dando más orientación por parte del regulador de California sobre qué tipos de datos son elegibles para solicitudes de privacidad de los consumidores.

### ¿oferta el Adobe de otras herramientas que pueden ser útiles para cumplir los requisitos de la CCPA?

Las aplicaciones de Adobe Experience Cloud proporcionan funciones de gestión de datos y control que pueden resultar útiles para las necesidades de privacidad de las compañías. Entre estas herramientas se encuentran el etiquetado del uso de datos, los controles de acceso basados en roles, la confusión de IP y las capacidades de hash.

Adobe ha recibido varias certificaciones de sus prácticas de privacidad y seguridad, como la certificación ISO 27001 y la validación de la RGPD TrustArc.

## Preguntas de CCPA

Las siguientes preguntas se refieren específicamente a la CCPA.

### ¿Cómo se aplican las diferentes funciones y responsabilidades del CCPA al Experience Cloud?

Según la definición de CCPA, las siguientes funciones se aplican a Adobe y sus clientes:

* Los clientes de Adobe (la parte que solicita la recopilación y el uso de información personal de los residentes de California) se considerarían un **negocio**.
* El Adobe, en su función de prestar el servicio, se consideraría un **Proveedor de servicio**.

Como Proveedor de servicio, Adobe recopila y procesa información personal en nombre de la Empresa y está obligado contractualmente a utilizar esa información únicamente para los fines específicos establecidos en el acuerdo.

Dada esta relación y el lenguaje del contrato del Adobe, la divulgación de información sobre el Adobe probablemente no se consideraría una &quot;venta&quot; para la cual las empresas tendrían que notificar y solicitar el consentimiento.

No obstante, los servicios de Adobe pueden utilizarse para permitir determinados intercambios de datos y transferencias a terceros. Estas transferencias de terceros podrían considerarse una &quot;venta&quot; y exigir legalmente la divulgación y el consentimiento. Los clientes deben trabajar con su asesor legal para evaluar casos de uso específicos a fin de evaluar los requisitos aplicables.

## Preguntas del GDPR

Las siguientes cuestiones se refieren específicamente al RGPD.

### ¿Cuál es la diferencia entre un reglamento y una directiva?

Un **reglamento** es un acto legislativo vinculante y debe aplicarse en toda la UE. Una **directiva** es un acto legislativo que establece un objetivo que todos los países de la UE deben alcanzar, pero depende de cada país decidir cómo hacerlo.

Es importante señalar que el RGPD es un reglamento, a diferencia de la legislación anterior (la Directiva sobre protección de datos), que es una directiva.

### ¿Cómo afecta el RGPD la política relativa a las infracciones de datos?

Los reglamentos propuestos en relación con las infracciones de datos se refieren principalmente a las políticas de notificación de compañías que se han infringido. Las violaciones de datos que puedan suponer un riesgo para las personas deben notificarse a la autoridad de protección de datos en un plazo de 72 horas y a las personas afectadas sin demora indebida.

## Preguntas de PDPA

Las siguientes preguntas se refieren específicamente al PDPA.

### ¿Qué constituye datos personales confidenciales?

El PDPA establece requisitos estrictos para la recogida y el almacenamiento de datos personales confidenciales, que incluyen datos personales relativos a: origen racial o étnico, opiniones políticas, creencias religiosas o filosóficas, antecedentes penales, pertenencia a uniones comerciales, datos genéticos, datos biométricos, registros de salud y orientación o preferencias sexuales.