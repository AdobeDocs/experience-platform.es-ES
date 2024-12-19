---
keywords: Experience Platform;inicio;temas populares;RGPD;rgpd;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;faq;FAQ;regulación;regulaciones;regulaciones;privacidad;privacidad;
solution: Experience Platform
title: Preguntas frecuentes sobre normas de privacidad
description: Este documento proporciona respuestas a las preguntas más frecuentes acerca de las regulaciones legales de privacidad admitidas y su implementación en Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: d643b2aeadd4080fa89d6a7b0f84a9f6882d7b89
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 1%

---

# Preguntas frecuentes sobre normas de privacidad

Este documento proporciona respuestas a las preguntas más frecuentes acerca de las regulaciones legales de privacidad admitidas y su implementación en Adobe Experience Cloud.

>[!NOTE]
>
>Las definiciones de los distintos términos utilizados en este documento se encuentran en la guía [terminología de regulación de privacidad](terminology.md).

## Preguntas generales

Las siguientes preguntas están relacionadas con todas las regulaciones de privacidad admitidas por Experience Cloud.

### ¿A quién afectan las regulaciones de privacidad admitidas?

Las [regulaciones de privacidad que admite el Experience Cloud](./overview.md) se aplican a todas las organizaciones que almacenan y procesan los datos personales de los ciudadanos en las respectivas jurisdicciones de las regulaciones, independientemente de la ubicación geográfica de la organización.

### ¿Qué constituyen los datos personales?

Los datos personales son toda información relacionada con una persona física o un interesado que pueda utilizarse directa o indirectamente para identificar a la persona. Puede ser cualquier cosa, desde un nombre, una foto, una dirección de correo electrónico, datos bancarios, publicaciones en sitios de redes sociales, información médica o una dirección IP de computadora.

Los siguientes identificadores se utilizan comúnmente en aplicaciones Experience Cloud y podrían estar sujetos a requisitos de regulación de privacidad:

* Nombre
* Dirección postal
* Identificador personal único
* Identificador en línea
* Dirección IP
* Dirección de correo electrónico
* Nombre de la cuenta

La información personal también puede incluir información de actividad de Internet u otra red electrónica. Esto incluye, entre otras cosas:

* Historial de navegación
* Historial de búsqueda
* Información sobre la interacción de un consumidor con un sitio web, una aplicación o un anuncio

Aunque las regulaciones de privacidad cubren un amplio conjunto de información personal, los términos de contrato estándar de Adobe dictan que la información personal sensible (como el SSN, la información del permiso de conducir, la información de la cuenta financiera y los datos biométricos) generalmente tienen prohibido importarla y usarla en aplicaciones Experience Cloud.

### ¿Cuál es la diferencia entre un controlador de datos y un procesador de datos?

Un **controlador de datos** es la entidad que determina los propósitos, condiciones y medios de procesamiento de datos personales, mientras que el **procesador de datos** es una entidad que procesa datos personales en nombre del controlador de datos.

Un **controlador de datos** es la persona u organización que tiene el poder y la responsabilidad de tomar decisiones con respecto a la recopilación, el uso o la divulgación de datos personales. Un **procesador de datos** es la persona u organización que opera en relación con la recopilación, el uso o la divulgación de los datos personales y la dirección del controlador de datos.

### ¿Cuál es la diferencia entre el consentimiento explícito e inequívoco del interesado?

**El consentimiento explícito** se refiere a un estándar de consentimiento que implica una indicación específica, informada e inequívoca de los deseos del interesado en forma oral o escrita. En pocas palabras, el interesado debe decir literal y explícitamente &quot;Acepto&quot; o &quot;Acepto&quot; para que el consentimiento se considere explícito. Además, debe ser tan fácil retirar el consentimiento como darlo.

**El consentimiento inequívoco (implícito)** hace referencia a un consentimiento que no fue dado explícitamente por el interesado, pero que, sin embargo, es de naturaleza inequívoca. Por ejemplo, durante el proceso de registro en el sitio web de una empresa, se envía un aviso de que, al proporcionar una dirección de correo electrónico, el interesado consiente en recibir correos electrónicos en ofertas especiales. Si el interesado lee el aviso, la acción afirmativa de introducir su correo electrónico es suficiente para considerarse un consentimiento inequívoco.

Para muchas regulaciones como el RGPD, se requiere un consentimiento explícito para procesar datos personales confidenciales, donde nada menos que la opción de &quot;inclusión&quot; será suficiente. Sin embargo, para los datos no confidenciales es aceptable un consentimiento inequívoco (implícito).

### ¿Pueden dar su consentimiento los interesados menores de una edad determinada?

Muchas regulaciones de privacidad estipulan que si un sujeto de datos es menor de una cierta edad, no puede proporcionar legalmente consentimiento para la recopilación de sus datos personales. Algunas regulaciones permiten que el titular de la responsabilidad parental dé su consentimiento a ese interesado en estos casos, pero no en todos. En la tabla siguiente se enumera la edad mínima para que los interesados den su propio consentimiento con respecto a cada norma, con notas para más información:

| Regulación | Edad del consentimiento | Notas |
| --- | --- | --- |
| CCPA (California) | 16 | <ul><li>El consentimiento paterno solo se puede proporcionar a interesados de 13 años o más.</li><li>La recogida de datos personales de personas menores de 13 años está estrictamente prohibida.</li></ul> |
| RGPD (Unión Europea) | 16 | <ul><li>Algunos Estados miembros de la UE pueden establecer una ley para una edad más baja con este fin, pero no inferior a 13 años.</li><li>Se debe proporcionar el consentimiento paterno a todos los interesados por debajo del límite de edad.</li></ul> |
| LGPD (Brasil) | 13 | <ul><li>Se debe proporcionar el consentimiento paterno a todos los interesados por debajo del límite de edad.</li><li>El consentimiento puede ser dado por una persona física de 13 a 18 años de edad, siempre y cuando el procesamiento de sus datos personales se realice en su mejor interés.</li></ul> |
| PDPA (Tailandia) | 10 | <ul><li>Se debe proporcionar el consentimiento paterno a todos los interesados por debajo del límite de edad.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### ¿Cuántos días tiene una empresa para responder a una solicitud del consumidor de acceder o eliminar información personal?

Suponiendo que la empresa haya recopilado información personal y que pueda autenticar o verificar la identidad de un consumidor en particular, las regulaciones de privacidad permiten que se cumpla un período de tiempo específico para una solicitud del consumidor. En la siguiente tabla se desglosan los períodos de tiempo aplicables a cada regulación, con notas sobre algunas excepciones:

>[!NOTE]
>
>El periodo de tiempo para responder en &quot;días&quot; refleja los plazos establecidos por cada ley regulatoria para completar una solicitud de los consumidores.

| Regulación | Plazo de respuesta | Notas |
| --- | --- | --- |
| CCPA (California) | 45 días | |
| RGPD (Unión Europea) | 30 días | |
| LGPD (Brasil) | 15 días | |
| PDPA (Tailandia) | 30 días | Si una empresa no puede responder a la solicitud de un interesado dentro del período de cumplimiento, tendrá un plazo adicional de 30 días a partir de la fecha en la que no pudo cumplir la solicitud para responder por escrito al interesado. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### ¿Necesita mi empresa nombrar a un responsable de la protección de datos?

Si las operaciones de datos de su organización entran dentro de las jurisdicciones legales del RGPD, la LGPD o la PDPA, debe designar un responsable de la protección de datos (DPO) en los siguientes casos:

* Su organización es una autoridad pública
* Su organización realiza una monitorización sistemática a gran escala
* Su organización realiza un procesamiento a gran escala de datos personales confidenciales.

>[!IMPORTANT]
>
>A diferencia de otras regulaciones, la CCPA lo estipula como un requisito. Sin embargo, generalmente se recomienda que, para mantener el cumplimiento de la privacidad, una empresa debe tener una monitorización individual calificada de las actividades de recopilación de datos y el almacenamiento de datos de los consumidores, así como responder a las consultas de los clientes.

### ¿Cómo puedo admitir solicitudes de privacidad de consumidores si mantengo datos cubiertos por regulaciones de privacidad?

Una vez que haya tomado las medidas necesarias para autenticar a los consumidores que se encuentran dentro de las jurisdicciones legales adecuadas, Adobe Experience Platform Privacy Service le permite enviar solicitudes de privacidad de consumidores a aplicaciones de Experience Cloud compatibles. Consulte la [[!DNL Privacy Service] descripción general](../home.md) para obtener más información. Para obtener información sobre cómo las aplicaciones de Experience Cloud en particular pueden cumplir con las solicitudes de privacidad, consulte la guía sobre [aplicaciones de Privacy Service y Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Sigue habiendo más directrices del regulador de California sobre qué tipos de datos cumplen los requisitos para las solicitudes de privacidad del consumidor.

## Preguntas de CCPA

Las siguientes preguntas están relacionadas específicamente con la CCPA.

### ¿Cómo se aplican las diferentes funciones y responsabilidades de la CCPA a los Experience Cloud?

Según se define en la CCPA, las siguientes funciones se aplican a Adobe y sus clientes:

* Los clientes del Adobe (la parte que solicita la recopilación y el uso de información personal de los residentes de California) serían considerados un **negocio**.
* El Adobe, en su función de proporcionar el servicio, se consideraría **Proveedor de servicios**.

Como Proveedor de servicios, Adobe recopila y procesa información personal por cuenta de la Empresa y está obligado contractualmente a utilizar esa información solo para los fines específicos establecidos en el acuerdo.

Dada esta relación y el lenguaje contractual del Adobe, es probable que la divulgación al Adobe no se considere una &quot;venta&quot; para la cual las empresas necesitarían notificar y solicitar el consentimiento.

Sin embargo, los servicios de Adobe pueden utilizarse para habilitar el uso compartido de datos y las transferencias a terceros. Estas transferencias de terceros podrían considerarse una &quot;venta&quot; y requieren legalmente la divulgación y el consentimiento. Los clientes deben colaborar con sus asesores legales para evaluar casos de uso específicos y evaluar los requisitos aplicables.

### ¿Adobe ofrece otras herramientas que pueden ser útiles para cumplir los requisitos de la CCPA?

Las aplicaciones de Adobe Experience Cloud proporcionan funciones de administración y gestión de datos que pueden resultar útiles para las necesidades de privacidad de las empresas. Entre estas herramientas se encuentran el etiquetado del uso de datos, los controles de acceso basados en funciones, la ofuscación de IP y las capacidades de hash.

El Adobe ha recibido varias certificaciones sobre sus prácticas de privacidad y seguridad, como una certificación ISO 27001 y una validación del RGPD de TrustArc.

## Preguntas sobre RGPD

Las siguientes preguntas están relacionadas específicamente con el RGPD.

### ¿Cuál es la diferencia entre un reglamento y una directiva?

Una **regulación** es un acto legislativo vinculante y debe aplicarse en su totalidad en toda la UE. Una **directiva** es un acto legislativo que establece un objetivo que todos los países de la UE deben alcanzar, pero es decisión de cada país.

Es importante señalar que el RGPD es un reglamento, a diferencia de la legislación anterior (la Directiva de Protección de Datos), que es una directiva.

### ¿Cómo afecta el RGPD a la política en torno a las violaciones de datos?

Los reglamentos propuestos en relación con las violaciones de datos se refieren principalmente a las políticas de notificación de las empresas que han sido violadas. Las violaciones de datos que puedan suponer un riesgo para las personas deben notificarse a la autoridad de protección de datos en un plazo de 72 horas y a las personas afectadas sin demoras indebidas.

## Preguntas sobre PDPA

Las siguientes preguntas están relacionadas específicamente con la PDPA.

### ¿Qué constituyen los datos personales confidenciales?

La PDPA establece requisitos estrictos para la recopilación y el almacenamiento de datos personales sensibles que incluyen datos personales relativos a: origen racial o étnico, opiniones políticas, creencias religiosas o filosóficas, antecedentes penales, afiliación a sindicatos, datos genéticos, datos biométricos, registros de salud y orientación o preferencias sexuales.
