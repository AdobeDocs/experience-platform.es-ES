---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Preguntas más frecuentes sobre CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: d0fcae6b1b75584a2c26d6eee5b47e0d60a142ba

---


# Preguntas más frecuentes sobre CCPA

Este documento proporciona respuestas a las preguntas más frecuentes sobre la Ley de Protección del Consumidor de California (CCPA) y su implementación en Adobe Experience Cloud.

## ¿Qué es CCPA?

La Ley de Privacidad del Consumidor de California (CCPA, por sus siglas en inglés) es la nueva ley de privacidad de California que otorga a sus residentes nuevos derechos con respecto a su información personal e impone responsabilidades de protección de datos a ciertas entidades que realizan negocios en California.

>[!NOTE] Aunque técnicamente efectiva en enero de 2020, la CCPA sigue siendo perfeccionada por los legisladores. Además, en las normas que aún no han sido redactadas por el regulador de California se proporcionan importantes detalles de implementación y otras directrices.

Si bien la CCPA comparte algunos conceptos proporcionados en virtud del Reglamento General de Protección de Datos de la Unión Europea (RGPD), como el derecho de las personas a acceder y eliminar información personal, existen varias formas fundamentales en que la CCPA difiere del RGPD. Por ejemplo, la CCPA otorga a los consumidores el derecho de exclusión de ciertas actividades de intercambio de datos que pueden considerarse como &quot;vender&quot; información personal a terceros, en lugar de requerir el consentimiento previo.

## ¿Cuál es la definición de información personal en el marco de la CCPA?

La información personal es información &quot;que identifica, relaciona, describe, es capaz de estar asociada o razonablemente podría estar vinculada, directa o indirectamente, con un consumidor o un hogar&quot;.

## ¿Qué tipos de información personal o identificadores utilizados en Adobe Experience Cloud están sujetos a estos nuevos requisitos?

Los siguientes identificadores se utilizan comúnmente en las aplicaciones de Experience Cloud y podrían estar sujetos a los requisitos de CCPA:

- Nombre
- Dirección postal
- Identificador personal único
- Identificador en línea
- Dirección IP
- Correo electrónico Dirección
- Nombre de la cuenta

La información personal también puede incluir información de actividad de Internet u otra red electrónica. Esto incluye, entre otras cosas:

- Historial de exploración
- Historial de búsqueda
- Información sobre la interacción de un consumidor con un sitio web, una aplicación o un anuncio

Aunque CCPA abarca un amplio conjunto de información personal, las condiciones de contrato estándar de Adobe establecen que la información personal confidencial (como SSN, información de licencia de controlador, información de cuenta financiera y datos biométricos) generalmente no se puede importar ni utilizar en aplicaciones de Experience Cloud.

## ¿Cómo se aplican las diferentes funciones y responsabilidades de CCPA a Experience Cloud?

Según la definición de CCPA, las siguientes funciones se aplican a Adobe y a sus clientes:

- Los clientes de Adobe (la parte que solicita la recopilación y el uso de información personal de los residentes de California) se considerarían un **negocio**.
- Adobe, en su función de proporcionar el servicio, se consideraría un **Proveedor de servicio**.

Dada esta relación y el idioma del contrato de Adobe, las revelaciones a Adobe probablemente no se considerarían una &quot;venta&quot; para la que las empresas necesitarían proporcionar un aviso y una oferta de exclusión.

Sin embargo, los servicios de Adobe se pueden utilizar para habilitar determinados intercambios de datos y transferencias a terceros. Estas transferencias de terceros podrían considerarse una &quot;venta&quot; y exigir legalmente la divulgación y la exclusión.  Los clientes deben trabajar con su asesor legal para evaluar casos de uso específicos a fin de evaluar los requisitos aplicables.

## ¿Cuántos días tiene una empresa para responder a una solicitud del consumidor de acceder o eliminar información personal?

Suponiendo que la empresa ha recopilado información personal y que puede autenticar o verificar la identidad de un consumidor particular de California, la CCPA permite que las solicitudes de los consumidores se satisfagan en un plazo de 45 días (con algunas excepciones).

## ¿Cuál es la función de Adobe en el marco de CCPA?

Como Proveedor de servicio, Adobe recopila y procesa información personal en nombre de la empresa y está obligado por contrato a utilizar dicha información únicamente para los fines específicos establecidos en el acuerdo.

Dada esta relación y el idioma del contrato de Adobe, la divulgación a Adobe entra dentro de las disposiciones legales para Proveedores de servicio, y probablemente no se considere una &quot;venta&quot; para la cual las empresas necesitarían proporcionar un aviso y una oferta de exclusión.

Los servicios de Adobe se pueden utilizar para habilitar el uso compartido de determinados datos y las transferencias a terceros. Estas transferencias de terceros podrían considerarse una &quot;venta&quot; y exigir legalmente la divulgación y la exclusión.  Los clientes deben trabajar con su asesor legal para evaluar casos de uso específicos a fin de evaluar los requisitos aplicables.

## ¿Cómo puedo cumplir con los requisitos de privacidad del consumidor según la CCPA si mantengo ciertos tipos de datos que están cubiertos por los requisitos?

Una vez que haya realizado los pasos necesarios para autenticar a los consumidores de CA, Adobe Experience Platform Privacy Service le permite enviar solicitudes de privacidad de los consumidores a aplicaciones compatibles de Experience Cloud. Consulte la información general [de](../home.md) Privacy Service para obtener más información. Para obtener información sobre cómo sus aplicaciones de Experience Cloud en particular pueden cumplir las solicitudes de privacidad, consulte la guía sobre [Privacy Service y las aplicaciones](../experience-cloud-apps.md)de Experience Cloud.

>[!NOTE] Todavía se está dando más orientación por parte del regulador de California sobre qué tipos de datos son elegibles para solicitudes de privacidad de los consumidores.

## ¿oferta Adobe otras herramientas que pueden resultar útiles para cumplir los requisitos de CCPA?

Las aplicaciones de Adobe Experience Cloud proporcionan funciones de gestión de datos y control que pueden resultar útiles para las necesidades de privacidad de las compañías. Entre estas herramientas se encuentran el etiquetado del uso de datos, los controles de acceso basados en roles, la confusión de IP y las capacidades de hash.

Adobe ha recibido varias certificaciones de sus prácticas de privacidad y seguridad, como una certificación ISO 27001 y una validación de RGPD TrustArc.