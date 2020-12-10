---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestion;troubleshooting;streaming ingestion troubleshooting;streaming ingestion faq;faq;
solution: Experience Platform
title: Solución de problemas de ingestión de flujo continuo
topic: troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre la transmisión de la ingesta por flujo continuo en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cfdaf72b7f4bf190877006ccd4cc6a7fd014adc2
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 0%

---


# Guía de solución de problemas de inserción de flujo continuo

Este documento proporciona respuestas a las preguntas más frecuentes sobre la transmisión de la ingesta por flujo continuo en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros [!DNL Platform] servicios, incluidos los que se encuentran en todas [!DNL Platform] las API, consulte la guía de solución de problemas del [Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] proporciona API RESTful que puede utilizar para transferir datos a [!DNL Experience Platform]. Los datos ingestados se utilizan para actualizar perfiles de clientes individuales en tiempo casi real, lo que le permite ofrecer experiencias relevantes y personalizadas en varios canales. Lea la información general [sobre la ingestión de](../home.md) datos para obtener más información sobre el servicio y los diferentes métodos de ingestión. Para ver los pasos sobre cómo utilizar las API de inserción de flujo continuo, lea la descripción general [de](../streaming-ingestion/overview.md)la ingesta de flujo.

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas más frecuentes sobre la transmisión por secuencias de la ingestión.

### ¿Cómo sé que la carga útil que envío tiene el formato correcto?

[!DNL Data Ingestion] aprovecha los esquemas [!DNL Experience Data Model] (XDM) para validar el formato de los datos entrantes. El envío de datos que no se ajusten a la estructura de un esquema XDM predefinido provocará un error en la ingestión. Para obtener más información sobre XDM y su uso en [!DNL Experience Platform], consulte la descripción general [del sistema](../../xdm/home.md)XDM.

La ingestión de flujo continuo admite dos modos de validación: sincrónico y asincrónico. Cada método de validación gestiona los datos fallidos de forma diferente.

**La validación** sincrónica debe utilizarse durante el proceso de desarrollo. Los registros en los que se ha producido un error al efectuar la validación se eliminan y se devuelve un mensaje de error en el que se indica por qué han fallado (por ejemplo: &quot;Formato de mensaje XDM no válido&quot;).

**La validación** asincrónica debe usarse en la producción. Los datos mal formados que no pasen la validación se envían al archivo [!DNL Data Lake] como un archivo por lotes con errores, donde se pueden recuperar posteriormente para mayor análisis.

Para obtener más información sobre la validación sincrónica y asincrónica, consulte la descripción general [de la validación de](../quality/streaming-validation.md)flujo. Para ver los pasos para la vista de lotes en los que se han producido errores al efectuar la validación, consulte la guía para [recuperar lotes](../quality/retrieve-failed-batches.md)en los que se han producido errores.

### ¿Puedo validar una carga útil de solicitud antes de enviarla a [!DNL Platform]?

Las cargas de solicitud solo se pueden evaluar una vez que se han enviado a [!DNL Platform]. Al realizar la validación sincrónica, las cargas válidas devuelven objetos JSON rellenados mientras que las cargas no válidas devuelven mensajes de error. Durante la validación asincrónica, el servicio detecta y envía los datos mal formados a la [!DNL Data Lake] ubicación donde posteriormente se pueden recuperar para su análisis. See the [streaming validation overview](../quality/streaming-validation.md) for more information.

### ¿Qué sucede cuando se solicita la validación sincrónica en una arista que no la admite?

Cuando no se admite la validación sincrónica para la ubicación solicitada, se devuelve una respuesta de error 501. Consulte la descripción general [de validación de](../quality/streaming-validation.md) flujo para obtener más información sobre la validación sincrónica.

### ¿Cómo puedo garantizar que los datos se recopilen únicamente a partir de fuentes de confianza?

[!DNL Experience Platform] admite la recopilación de datos segura. Cuando la recopilación de datos autenticada está habilitada, los clientes deben enviar un testigo web JSON (JWT) y su identificador de organización IMS como encabezados de solicitud. Para obtener más información sobre cómo enviar datos autenticados a [!DNL Platform], consulte la guía sobre recopilación [de datos](../tutorials/create-authenticated-streaming-connection.md)autenticados.

### ¿Cuál es la latencia de transmisión de datos a [!DNL Real-time Customer Profile]?

Los eventos de flujo se reflejan generalmente [!DNL Real-time Customer Profile] en menos de 60 segundos. Las latencias reales pueden variar debido al volumen de datos, el tamaño del mensaje y las limitaciones de ancho de banda.

### ¿Puedo incluir varios mensajes en la misma solicitud de API?

Puede agrupar varios mensajes en una única carga útil de solicitud y transmitirlos a [!DNL Platform]. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una sola solicitud es una manera excelente de optimizar las operaciones de datos. Lea el tutorial sobre el [envío de varios mensajes en una solicitud](../tutorials/streaming-multiple-messages.md) para obtener más información.

### ¿Cómo sé si los datos que envío se están recibiendo?

Todos los datos que se envían a [!DNL Platform] (de forma satisfactoria o no) se almacenan como archivos por lotes antes de persistir en los conjuntos de datos. El estado de procesamiento de los lotes aparece dentro del conjunto de datos al que se enviaron.

Puede comprobar si los datos se han ingestado correctamente comprobando la actividad del conjunto de datos mediante la interfaz [de usuario del](https://platform.adobe.com)Experience Platform. Haga clic en **[!UICONTROL Conjuntos]** de datos en el panel de navegación izquierdo para mostrar una lista de conjuntos de datos. Seleccione el conjunto de datos al que está transmitiendo desde la lista mostrada para abrir la página de actividad **[!UICONTROL del]** conjunto de datos, mostrando todos los lotes enviados durante un período de tiempo seleccionado. Para obtener más información sobre el uso [!DNL Experience Platform] para supervisar flujos de datos, consulte la guía sobre [supervisión de flujos](../quality/monitor-data-ingestion.md)de datos de flujo continuo.

Si los datos no se han podido transferir y desea recuperarlos de [!DNL Platform], puede recuperar los lotes con errores enviando sus ID al [!DNL Data Access API]. Consulte la guía para [recuperar lotes](../quality/retrieve-failed-batches.md) con errores para obtener más información.

### ¿Por qué los datos de flujo continuo no están disponibles en el lago de datos?

Hay una variedad de razones por las que la ingestión por lotes puede no alcanzar el objetivo [!DNL Data Lake], como formato no válido, datos que faltan o errores del sistema. Para determinar por qué falló el lote, debe recuperar el lote mediante el [!DNL Data Ingestion Service API] y vista sus detalles. Para ver los pasos detallados sobre la recuperación de un lote dañado, consulte la guía sobre la [recuperación de lotes](../quality/retrieve-failed-batches.md)con errores.

### ¿Cómo se analiza la respuesta devuelta para la solicitud de API?

Puede analizar una respuesta comprobando primero el código de respuesta del servidor para determinar si se aceptó la solicitud. Si se devuelve un código de respuesta correcto, se puede revisar el objeto de `responses` matriz para determinar el estado de la tarea de ingesta.

Una solicitud de API de un solo mensaje correcta devuelve el código de estado 200. Una solicitud de API de mensaje por lotes correcta (o parcialmente correcta) devuelve el código de estado 207.

El siguiente JSON es un objeto de respuesta de ejemplo para una solicitud de API con dos mensajes: un éxito y otro fracaso. Los mensajes que se transmiten correctamente devuelven una `xactionId` propiedad. Los mensajes que no se pueden transmitir devuelven una `statusCode` propiedad y una respuesta `message` con más información.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### ¿Por qué mis mensajes enviados no son recibidos por [!DNL Real-time Customer Profile]?

Si [!DNL Real-time Customer Profile] rechaza un mensaje, lo más probable es que se deba a una información de identidad incorrecta. Puede ser el resultado de proporcionar un valor o una Área de nombres no válidos para una identidad.

Existen dos tipos de Áreas de nombres de identidad: predeterminado y personalizado. Cuando utilice Áreas de nombres personalizadas, asegúrese de que la Área de nombres se ha registrado en [!DNL Identity Service]. Consulte la descripción general [de la Área de nombres de](../../identity-service/namespaces.md) identidad para obtener más información sobre el uso de Áreas de nombres predeterminadas y personalizadas.

Puede usar el [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver más información sobre por qué un mensaje falló en la ingestión. Haga clic en **[!UICONTROL Monitoreo]** en el panel de navegación izquierdo y, a continuación, vista la ficha **[!UICONTROL Flujo de extremo a extremo]** para ver los lotes de mensajes transmitidos durante un período de tiempo seleccionado.
