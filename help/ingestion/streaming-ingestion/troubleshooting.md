---
keywords: Experience Platform;inicio;temas populares;transmisión;flujo continuo de ingestión;resolución de problemas;resolución de problemas;flujo continuo de problemas de ingestión;transmisión de preguntas frecuentes;preguntas frecuentes; preguntas más frecuentes;
solution: Experience Platform
title: Guía de solución de problemas de inserción de flujo continuo
topic: troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre la transmisión de la ingesta por flujo continuo en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---


# Guía de solución de problemas de inserción de flujo continuo

Este documento proporciona respuestas a las preguntas más frecuentes sobre la transmisión de la ingesta por flujo continuo en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros [!DNL Platform] servicios, incluidos los que se encuentran en todas las [!DNL Platform] API, consulte la [guía de solución de problemas del Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] proporciona API de RESTful que puede utilizar para ingestar datos en [!DNL Experience Platform]. Los datos ingestados se utilizan para actualizar perfiles de clientes individuales en tiempo casi real, lo que le permite ofrecer experiencias relevantes y personalizadas en varios canales. Lea la [información general sobre la ingestión de datos](../home.md) para obtener más información sobre el servicio y los diferentes métodos de ingestión. Para ver los pasos sobre cómo utilizar las API de inserción de flujo continuo, lea la [descripción general de la ingestión de flujo](../streaming-ingestion/overview.md).

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas más frecuentes sobre la transmisión por secuencias de la ingestión.

### ¿Cómo sé que la carga útil que envío tiene el formato correcto?

[!DNL Data Ingestion] aprovecha los esquemas  [!DNL Experience Data Model] (XDM) para validar el formato de los datos entrantes. El envío de datos que no se ajusten a la estructura de un esquema XDM predefinido provocará un error en la ingestión. Para obtener más información sobre XDM y su uso en [!DNL Experience Platform], consulte la [información general del sistema XDM](../../xdm/home.md).

La ingestión de flujo continuo admite dos modos de validación: sincrónico y asincrónico. Cada método de validación gestiona los datos fallidos de forma diferente.

**La** validación sincrónica debe utilizarse durante el proceso de desarrollo. Los registros en los que se ha producido un error al efectuar la validación se eliminan y se devuelve un mensaje de error en el que se indica por qué han fallado (por ejemplo: &quot;Formato de mensaje XDM no válido&quot;).

**La** validación asincrónica debe utilizarse en la producción. Los datos mal formados que no pasen la validación se envían a [!DNL Data Lake] como un archivo por lotes con errores, donde se pueden recuperar posteriormente para mayor análisis.

Para obtener más información sobre la validación sincrónica y asincrónica, consulte la [descripción general de la validación de flujo](../quality/streaming-validation.md). Para ver los pasos para la vista de lotes que no se pueden validar, consulte la guía sobre [recuperación de lotes fallidos](../quality/retrieve-failed-batches.md).

### ¿Puedo validar una carga útil de solicitud antes de enviarla a [!DNL Platform]?

Las cargas de solicitud solo se pueden evaluar después de que se hayan enviado a [!DNL Platform]. Al realizar la validación sincrónica, las cargas válidas devuelven objetos JSON rellenados mientras que las cargas no válidas devuelven mensajes de error. Durante la validación asincrónica, el servicio detecta y envía los datos mal formados al [!DNL Data Lake], donde posteriormente se pueden recuperar para su análisis. Consulte la [descripción general de validación de flujo](../quality/streaming-validation.md) para obtener más información.

### ¿Qué sucede cuando se solicita la validación sincrónica en una arista que no la admite?

Cuando no se admite la validación sincrónica para la ubicación solicitada, se devuelve una respuesta de error 501. Consulte la [descripción general de validación de flujo](../quality/streaming-validation.md) para obtener más información sobre la validación sincrónica.

### ¿Cómo puedo garantizar que los datos se recopilen únicamente a partir de fuentes de confianza?

[!DNL Experience Platform] admite la recopilación de datos segura. Cuando la recopilación de datos autenticada está habilitada, los clientes deben enviar un testigo web JSON (JWT) y su identificador de organización IMS como encabezados de solicitud. Para obtener más información sobre cómo enviar datos autenticados a [!DNL Platform], consulte la guía sobre [recopilación de datos autenticada](../tutorials/create-authenticated-streaming-connection.md).

### ¿Cuál es la latencia para transmitir datos a [!DNL Real-time Customer Profile]?

Los eventos de flujo generalmente se reflejan en [!DNL Real-time Customer Profile] en menos de 60 segundos. Las latencias reales pueden variar debido al volumen de datos, el tamaño del mensaje y las limitaciones de ancho de banda.

### ¿Puedo incluir varios mensajes en la misma solicitud de API?

Puede agrupar varios mensajes dentro de una única carga útil de solicitud y transmitirlos a [!DNL Platform]. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una sola solicitud es una manera excelente de optimizar las operaciones de datos. Lea el tutorial sobre [envío de varios mensajes en una solicitud](../tutorials/streaming-multiple-messages.md) para obtener más información.

### ¿Cómo sé si los datos que envío se están recibiendo?

Todos los datos que se envían a [!DNL Platform] (correctamente o de otro modo) se almacenan como archivos por lotes antes de persistir en los conjuntos de datos. El estado de procesamiento de los lotes aparece dentro del conjunto de datos al que se enviaron.

Puede comprobar si los datos se han ingestado correctamente comprobando la actividad del conjunto de datos mediante la [interfaz de usuario del Experience Platform](https://platform.adobe.com). Haga clic en **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para mostrar una lista de conjuntos de datos. Seleccione el conjunto de datos al que está transmitiendo desde la lista mostrada para abrir su página **[!UICONTROL actividad del conjunto de datos]**, mostrando todos los lotes enviados durante un período de tiempo seleccionado. Para obtener más información sobre el uso de [!DNL Experience Platform] para monitorear flujos de datos, consulte la guía sobre [monitoreo de flujos de datos de flujo](../quality/monitor-data-ingestion.md).

Si los datos no se han podido transferir y desea recuperarlos de [!DNL Platform], puede recuperar los lotes con errores enviando sus ID a [!DNL Data Access API]. Consulte la guía sobre [recuperación de lotes fallidos](../quality/retrieve-failed-batches.md) para obtener más información.

### ¿Por qué los datos de flujo continuo no están disponibles en el lago de datos?

Existen diversos motivos por los que la ingestión por lotes puede no alcanzar el [!DNL Data Lake], como formato no válido, datos que faltan o errores del sistema. Para determinar por qué falló el lote, debe recuperar el lote mediante [!DNL Data Ingestion Service API] y vista sus detalles. Para ver los pasos detallados sobre cómo recuperar un lote con errores, consulte la guía sobre [recuperación de lotes con errores](../quality/retrieve-failed-batches.md).

### ¿Cómo se analiza la respuesta devuelta para la solicitud de API?

Puede analizar una respuesta comprobando primero el código de respuesta del servidor para determinar si se aceptó la solicitud. Si se devuelve un código de respuesta correcto, puede revisar el objeto de matriz `responses` para determinar el estado de la tarea de ingestión.

Una solicitud de API de un solo mensaje correcta devuelve el código de estado 200. Una solicitud de API de mensaje por lotes correcta (o parcialmente correcta) devuelve el código de estado 207.

El siguiente JSON es un objeto de respuesta de ejemplo para una solicitud de API con dos mensajes: un éxito y otro fracaso. Los mensajes que se transmiten correctamente devuelven una propiedad `xactionId`. Los mensajes que no se pueden transmitir devuelven una propiedad `statusCode` y una respuesta `message` con más información.

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

### ¿Por qué los mensajes enviados no son recibidos por [!DNL Real-time Customer Profile]?

Si [!DNL Real-time Customer Profile] rechaza un mensaje, lo más probable es que se deba a una información de identidad incorrecta. Puede ser el resultado de proporcionar un valor o una Área de nombres no válidos para una identidad.

Existen dos tipos de Áreas de nombres de identidad: predeterminado y personalizado. Cuando utilice Áreas de nombres personalizadas, asegúrese de que la Área de nombres se ha registrado en [!DNL Identity Service]. Consulte la [información general de la Área de nombres de identidad](../../identity-service/namespaces.md) para obtener más información sobre el uso de Áreas de nombres predeterminadas y personalizadas.

Puede utilizar [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver más información sobre por qué un mensaje falló en la ingestión. Haga clic en **[!UICONTROL Monitoreo]** en el panel de navegación izquierdo y, a continuación, vista la ficha **[!UICONTROL Flujo de extremo a extremo]** para ver los lotes de mensajes transmitidos durante un período de tiempo seleccionado.
