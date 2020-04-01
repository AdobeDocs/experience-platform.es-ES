---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Información general sobre el servicio de privacidad de Adobe Experience Platform

Para ofrecer mejores experiencias de cliente, debe recopilar y almacenar los datos personales de sus clientes. Al utilizar estos datos, es importante comprender y respetar la privacidad de sus clientes. Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan.

Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con Privacy Service, puede enviar solicitudes para acceder a los datos personales o privados de los clientes y eliminarlos de las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas de privacidad legales y de la organización.

## ¿Por qué Privacy Service?

Privacy Service se desarrolló en respuesta a un cambio fundamental en la manera en que las empresas deben administrar los datos personales de sus clientes. El objetivo central de Privacy Service es automatizar el cumplimiento de las regulaciones de privacidad de datos que, cuando se violan, pueden resultar en multas importantes y en interrumpir las operaciones de datos de su empresa.

### Privacy Service y GDPR

El Reglamento [](https://eugdpr.org/) General de Protección de Datos (RGPD) introdujo varios nuevos derechos de privacidad de datos para los miembros de la Unión Europea, incluidos el **derecho de acceso** y el **derecho a ser olvidado**. Esto significa que cualquier ciudadano de la UE cuyos datos personales hayan sido recopilados por su empresa puede solicitar el acceso o la eliminación de sus datos en cualquier momento. El incumplimiento de estas solicitudes en un plazo de 30 días puede resultar en multas de varios millones de dólares para su organización.

Privacy Service admite solicitudes de acceso y eliminación del RGPD, y las rastrea por separado de las solicitudes de conformidad con el reglamento del CCPA. Consulte las preguntas más frecuentes [y los documentos](gdpr/faq.md) terminológicos [del](gdpr/terminology.md) RGPD para obtener más información.

### Privacy Service y CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. La CCPA otorga nuevos derechos de privacidad de datos a los residentes de California, incluido el derecho a acceder y eliminar sus datos personales, a saber si sus datos personales se venden o revelan (y a quién) y a exclusión que sus datos se venden a terceros.

Privacy Service acepta las solicitudes de acceso y eliminación de la regulación de CCPA, y las rastrea por separado de las solicitudes de RGPD. Privacy Service también admite el envío de solicitudes de exclusión de venta para aplicaciones de Experience Cloud que las admitan. Consulte las preguntas más frecuentes [de](ccpa/faq.md) CCPA para obtener más información.

## Cómo utilizar Privacy Service para administrar solicitudes de trabajos de privacidad

Privacy Service proporciona una API RESTful y una interfaz de usuario que le permiten administrar las solicitudes de sus clientes para acceder o eliminar sus datos privados o exclusión la venta (también conocidos como trabajos **de** privacidad). El servicio también proporciona un mecanismo central de auditoría y registro que le permite realizar vistas del estado y los resultados de los trabajos de privacidad que involucran aplicaciones de Experience Cloud.

>[!NOTE] Actualmente, las solicitudes de exclusión solo son compatibles con la API de Privacy Service.

### Uso de la API

La API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service le permite crear y administrar trabajos de privacidad mediante llamadas de API RESTful, lo que le permite abordar mediante programación la conformidad con la normativa de privacidad de sus aplicaciones de Experience Cloud. Para ver los pasos detallados sobre cómo utilizar la API, consulte la guía para desarrolladores de la API de [Privacy Service](api/getting-started.md).

### Uso de la interfaz de usuario

La interfaz de usuario de Privacy Service permite crear y supervisar trabajos de privacidad mediante una interfaz gráfica. La interfaz de usuario incluye un widget de informe **de** estado que proporciona una representación visual del estado de todas las solicitudes activas y le permite crear nuevas solicitudes mediante el creador **de** solicitudes integrado o cargando archivos JSON. Para obtener más información sobre el uso de la interfaz de usuario, consulte la guía [del usuario de](ui/overview.md)Privacy Service.