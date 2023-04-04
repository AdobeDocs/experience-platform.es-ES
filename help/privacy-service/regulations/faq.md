---
keywords: Experience Platform;inicio;temas populares;RGPD;RGPD;RGPD;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;preguntas frecuentes;regulación;regulación;regulaciones;normativas;privacidad;privacidad;privacidad;
solution: Experience Platform
title: Preguntas frecuentes sobre las normas de privacidad
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre las regulaciones de privacidad legales compatibles y su implementación en Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: 7e86721f6dd6fd280ae7e7e67aca21b4258ffb66
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 1%

---

# Preguntas frecuentes sobre las normas de privacidad

Este documento proporciona respuestas a las preguntas más frecuentes sobre las regulaciones de privacidad legales compatibles y su implementación en Adobe Experience Cloud.

>[!NOTE]
>
>Las definiciones de los distintos términos utilizados en este documento se encuentran en la [terminología de regulación de privacidad](terminology.md) guía.

## Preguntas generales

Las siguientes preguntas están relacionadas con todas las normas de privacidad compatibles con el Experience Cloud.

### ¿A quién afectan las regulaciones de privacidad compatibles?

La variable [regulaciones de privacidad compatibles con el Experience Cloud](./overview.md) se aplican a todas las organizaciones que almacenan y procesan los datos personales de los ciudadanos dentro de las respectivas jurisdicciones de la organización, independientemente de su ubicación geográfica.

### ¿Qué constituye datos personales?

Los datos personales son toda información relacionada con una persona física o un interesado que puede utilizarse directa o indirectamente para identificar a la persona. Puede ser cualquier cosa, desde un nombre, una foto, una dirección de correo electrónico, detalles del banco, publicaciones en sitios web de redes sociales, información médica o una dirección IP de computadora.

Los siguientes identificadores se utilizan comúnmente en aplicaciones de Experience Cloud y podrían estar sujetos a los requisitos de regulación de la privacidad:

* Nombre
* Dirección postal
* Identificador personal único
* Identificador en línea
* Dirección IP
* Correo electrónico Dirección
* Nombre de la cuenta

La información personal también puede incluir información de actividades de Internet u otra red electrónica. Esto incluye, entre otras cosas:

* Historial de navegación
* Historial de búsqueda
* Información sobre la interacción de un consumidor con un sitio web, una aplicación o un anuncio

Aunque las normas de privacidad abarcan un amplio conjunto de información personal, los términos contractuales estándar del Adobe estipulan que la información personal confidencial (como SSN, información de licencia de conducir, información de cuentas financieras y datos biométricos) generalmente está prohibida de importar y usar en aplicaciones Experience Cloud.

### ¿Cuál es la diferencia entre un controlador de datos y un procesador de datos?

A **controlador de datos** es la entidad que determina los propósitos, condiciones y medios de tratamiento de datos personales, mientras que la variable **procesador de datos** es una entidad que procesa los datos personales en nombre del responsable del tratamiento de datos.

A **controlador de datos** es la persona u organización que tiene el poder y la responsabilidad de tomar decisiones relativas a la recopilación, uso o revelación de datos personales. A **procesador de datos** es la persona u organización que actúa en relación con la recopilación, el uso o la divulgación de los datos personales y la dirección del responsable del tratamiento de datos.

### ¿Cuál es la diferencia entre el consentimiento explícito y el del interesado?

**Consentimiento explícito** se refiere a una norma de consentimiento que implica una indicación específica, informada e inequívoca de los deseos del interesado en forma oral o escrita. En pocas palabras, el interesado debe decir literal y explícitamente &quot;consentido&quot; o &quot;estoy de acuerdo&quot; para que el consentimiento se considere explícito. Además, debe ser tan fácil retirar el consentimiento como concederlo.

**Consentimiento inequívoco (implícito)** se refiere al consentimiento que no fue expresamente dado por el interesado, pero que, sin embargo, es de naturaleza inequívoca. Por ejemplo, durante el proceso de registro de un sitio web de la empresa, se envía un aviso de que al proporcionar una dirección de correo electrónico, el sujeto de los datos consiente en recibir correos electrónicos en ofertas especiales. Si el interesado lee el aviso, la acción afirmativa de introducir su correo electrónico es suficiente para considerarse un consentimiento inequívoco.

Para muchas regulaciones como el RGPD, se requiere un consentimiento explícito para procesar datos personales confidenciales, donde nada menos que &quot;adhesión&quot; será suficiente. Sin embargo, para los datos no confidenciales, el consentimiento inequívoco (implícito) es aceptable.

### ¿Pueden dar su consentimiento los interesados menores de una edad determinada?

Muchas normas de privacidad estipulan que si un interesado es menor de una cierta edad, no puede dar su consentimiento legal para la recopilación de sus datos personales. Algunos reglamentos permiten que el titular de la patria potestad dé su consentimiento en esos casos, pero no en todos. En la tabla siguiente se indica la edad mínima para que los interesados den su propio consentimiento a cada reglamento, con notas para obtener más información:

| Reglamento | Edad del consentimiento | Notas |
| --- | --- | --- |
| CCPA (California) | 16 | <ul><li>El consentimiento paterno sólo puede proporcionarse a sujetos de datos de 13 años o más.</li><li>La recogida de datos personales de personas menores de 13 años está estrictamente prohibida.</li></ul> |
| RGPD (Unión Europea) | 16 | <ul><li>Algunos Estados miembros de la UE pueden establecer una ley para una edad inferior a tal efecto, pero no inferior a 13 años.</li><li>Se debe proporcionar consentimiento parental a todos los interesados por debajo del límite de edad.</li></ul> |
| LGPD (Brasil) | 13 | <ul><li>Se debe proporcionar consentimiento parental a todos los interesados por debajo del límite de edad.</li><li>El consentimiento puede ser otorgado por una persona física de 13 a 18 años, siempre que el tratamiento de sus datos personales se someta a su interés superior.</li></ul> |
| PDPA (Tailandia) | 10 | <ul><li>Se debe proporcionar consentimiento parental a todos los interesados por debajo del límite de edad.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### ¿Cuántos días tiene una empresa para responder a una solicitud del consumidor de acceder o eliminar información personal?

Suponiendo que la empresa haya recopilado información personal y que pueda autenticar o verificar la identidad de un consumidor en particular, las normas de privacidad permiten un periodo específico para que se cumpla una solicitud del consumidor. En el cuadro siguiente se detallan los plazos aplicables a cada reglamento, con notas sobre algunas excepciones:

>[!NOTE]
>
>El plazo para responder en &quot;días&quot; refleja los plazos establecidos por cada ley para completar una solicitud de los consumidores.

| Reglamento | Intervalo de tiempo para responder | Notas |
| --- | --- | --- |
| CCPA (California) | 45 días |  |
| RGPD (Unión Europea) | 30 días | Si la solicitud es compleja o el mismo interesado ha realizado numerosas solicitudes, se puede ampliar a 60 días. |
| LGPD (Brasil) | 15 días |  |
| PDPA (Tailandia) | 30 días | Si una empresa no puede responder a la solicitud de un interesado dentro de la ventana de cumplimiento de normas, la empresa tendrá 30 días adicionales desde la fecha en que no pudo cumplir la solicitud de respuesta por escrito al interesado. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### ¿Es necesario que mi empresa nombre un responsable de protección de datos?

Si las operaciones de datos de su organización entran dentro de las jurisdicciones legales del RGPD, la LGPD o la PDPA, debe designar un responsable de protección de datos (RPD) en los siguientes casos:

* Su organización es una autoridad pública
* Su organización realiza una monitorización sistemática a gran escala
* Su organización participa en el procesamiento a gran escala de datos personales confidenciales.

>[!IMPORTANT]
>
>A diferencia de otras normas, la CCPA sí lo estipula como requisito. Sin embargo, se recomienda generalmente que, para mantener el cumplimiento de la privacidad, una empresa tenga actividades de recopilación de datos de monitoreo individual calificadas y almacenamiento de datos de consumidores, así como responder a las preguntas de los clientes.

### ¿Cómo puedo admitir las solicitudes de privacidad del consumidor si mantengo datos que están cubiertos por las regulaciones de privacidad?

Una vez que haya realizado los pasos necesarios para autenticar a los consumidores que se encuentran dentro de las jurisdicciones legales apropiadas, Adobe Experience Platform Privacy Service le permite enviar solicitudes de privacidad del consumidor a aplicaciones Experience Cloud compatibles. Consulte la [[!DNL Privacy Service] información general](../home.md) para obtener más información. Para obtener información sobre cómo sus aplicaciones de Experience Cloud particulares pueden cumplir las solicitudes de privacidad, consulte la guía de [aplicaciones de Privacy Service y Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Todavía falta más información del regulador de California sobre qué tipos de datos cumplen los requisitos para solicitudes de privacidad del consumidor.

## Preguntas sobre la CCPA

Las siguientes preguntas se refieren específicamente a la CCPA.

### ¿Cómo se aplican las diferentes funciones y responsabilidades de la CCPA al Experience Cloud?

Como se define en la CCPA, las siguientes funciones se aplican a Adobe y a sus clientes:

* Los clientes de Adobe (la parte que solicita la recopilación y el uso de información personal de residentes de California) se considerarían como **Empresa**.
* El Adobe, en su función de prestar el servicio, se consideraría un **Proveedor de servicios**.

Como Proveedor de Servicios, Adobe recopila y procesa información personal en nombre de la Empresa y está obligado contractualmente a usar esa información solamente para los propósitos específicos establecidos en el acuerdo.

Dada esta relación y el lenguaje contractual del Adobe, las revelaciones de Adobe probablemente no se considerarían una &quot;venta&quot; para la que las empresas tendrían que notificar y solicitar el consentimiento.

Sin embargo, los servicios de Adobe se pueden utilizar para permitir cierto tipo de intercambio de datos y transferencias a terceros. Estas transferencias de terceros podrían considerarse una &quot;venta&quot; y exigir legalmente su divulgación y consentimiento. Los clientes deben colaborar con su asesor legal para evaluar casos de uso específicos y evaluar los requisitos aplicables.

### ¿Ofrece Adobe otras herramientas que pueden resultar útiles para cumplir los requisitos de la CCPA?

Las aplicaciones de Adobe Experience Cloud proporcionan funciones de administración y administración de datos que pueden ser útiles para las necesidades de privacidad de las empresas. Entre estas herramientas se encuentran el etiquetado del uso de los datos, los controles de acceso basados en roles, la confusión de IP y las capacidades de hash.

Adobe ha recibido varias certificaciones de sus prácticas de privacidad y seguridad, como la certificación ISO 27001 y la validación del RGPD TrustArc.

## Preguntas sobre el RGPD

Las siguientes preguntas se refieren específicamente al RGPD.

### ¿Cuál es la diferencia entre un reglamento y una directiva?

A **regulación** es un acto legislativo vinculante y debe aplicarse en su totalidad en toda la UE. A **directiva** es un acto legislativo que establece un objetivo que todos los países de la UE deben alcanzar, pero depende de cada país decidir cómo hacerlo.

Es importante señalar que el RGPD es un reglamento, a diferencia de la legislación anterior (la Directiva de protección de datos), que es una directiva.

### ¿Cómo afecta el RGPD a las políticas relativas a las infracciones de datos?

Las regulaciones propuestas en torno a las infracciones de datos se refieren principalmente a las políticas de notificación de las empresas que han sido violadas. Las infracciones de datos que puedan suponer un riesgo para las personas deben notificarse a la autoridad de protección de datos en un plazo de 72 horas y a las personas afectadas sin demora indebida.

## Preguntas sobre PDPA

Las siguientes preguntas están relacionadas específicamente con la PDPA.

### ¿Qué constituye datos personales confidenciales?

La PDPA establece requisitos estrictos para la recopilación y el almacenamiento de datos personales confidenciales, que incluyen datos personales relacionados con: origen racial o étnico, opiniones políticas, creencias religiosas o filosóficas, antecedentes penales, afiliación a sindicatos, datos genéticos, datos biométricos, registros de salud y orientación o preferencias sexuales.
