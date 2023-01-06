---
keywords: Experience Platform;inicio;temas populares;flujo continuo;ingesta de transmisión;solución de problemas;solución de problemas de ingesta de transmisión;preguntas frecuentes sobre ingesta de transmisión;preguntas frecuentes sobre transmisión;faq;
solution: Experience Platform
title: Guía de solución de problemas de ingesta de transmisión
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre la transmisión por secuencias de comandos en Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Guía de solución de problemas de ingesta de transmisión

Este documento proporciona respuestas a las preguntas más frecuentes sobre la transmisión por secuencias de comandos en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otras [!DNL Platform] servicios, incluidos los que se encuentran en todos los [!DNL Platform] API, consulte la [Guía de solución de problemas del Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] proporciona API de RESTful que puede usar para introducir datos en [!DNL Experience Platform]. Los datos introducidos se utilizan para actualizar perfiles de clientes individuales en tiempo casi real, lo que le permite ofrecer experiencias personalizadas y relevantes en varios canales. Lea el [Información general sobre la ingesta de datos](../home.md) para obtener más información sobre el servicio y los distintos métodos de ingesta. Para ver los pasos sobre cómo utilizar las API de ingesta de transmisión, lea la [información general sobre la ingesta de transmisión](../streaming-ingestion/overview.md).

## Preguntas frecuentes

A continuación se ofrece una lista de respuestas a las preguntas más frecuentes sobre la transmisión por secuencias de comandos.

### ¿Cómo sé que la carga útil que estoy enviando tiene el formato correcto?

[!DNL Data Ingestion] aprovecha [!DNL Experience Data Model] (XDM) esquemas para validar el formato de los datos entrantes. El envío de datos que no se ajuste a la estructura de un esquema XDM predefinido provocará errores de ingesta. Para obtener más información sobre XDM y su uso en [!DNL Experience Platform], consulte la [Información general del sistema XDM](../../xdm/home.md).

La introducción por transmisión admite dos modos de validación: sincrónico y asíncrono. Cada método de validación gestiona los datos con errores de forma diferente.

**Validación sincrónica** debe utilizarse durante el proceso de desarrollo. Los registros en los que se ha producido un error de validación se pierden y devuelven un mensaje de error en el que se indica por qué han fallado (por ejemplo: &quot;Formato de mensaje XDM no válido&quot;).

**Validación asincrónica** debe utilizarse en la producción. Los datos mal formados que no pasen la validación se envían al [!DNL Data Lake] como archivo por lotes con errores, donde se puede recuperar más adelante para su análisis posterior.

Para obtener más información sobre la validación sincrónica y asincrónica, consulte la [información general sobre validación de flujo continuo](../quality/streaming-validation.md). Para ver los pasos sobre cómo ver lotes que no se pueden validar, consulte la guía de [recuperación de lotes con errores](../quality/retrieve-failed-batches.md).

### ¿Puedo validar una carga útil de solicitud antes de enviarla a [!DNL Platform]?

Las cargas de solicitud solo se pueden evaluar una vez que se han enviado a [!DNL Platform]. Al realizar la validación sincrónica, las cargas válidas devuelven objetos JSON rellenados, mientras que las cargas no válidas devuelven mensajes de error. Durante la validación asíncrona, el servicio detecta y envía los datos mal formados al [!DNL Data Lake] donde se puede recuperar posteriormente para su análisis. Consulte la [información general sobre validación de flujo continuo](../quality/streaming-validation.md) para obtener más información.

### ¿Qué sucede cuando se solicita la validación sincrónica en un perímetro que no la admite?

Cuando no se admite la validación sincrónica para la ubicación solicitada, se devuelve una respuesta de error 501. Consulte la [información general sobre validación de flujo continuo](../quality/streaming-validation.md) para obtener más información sobre validación sincrónica.

### ¿Cómo me aseguro de que los datos solo se recopilen a partir de fuentes de confianza?

[!DNL Experience Platform] admite la recopilación de datos segura. Cuando la recopilación de datos autenticada está habilitada, los clientes deben enviar un token web JSON (JWT) y su ID de organización de IMS como encabezados de solicitud. Para obtener más información sobre cómo enviar datos autenticados a [!DNL Platform], consulte la guía de [recopilación de datos autenticada](../tutorials/create-authenticated-streaming-connection.md).

### ¿Cuál es la latencia para la transmisión de datos a [!DNL Real-Time Customer Profile]?

Los eventos de flujo continuo generalmente se reflejan en [!DNL Real-Time Customer Profile] en menos de 60 segundos. Las latencias reales pueden variar debido al volumen de datos, el tamaño del mensaje y las limitaciones de ancho de banda.

### ¿Puedo incluir varios mensajes en la misma solicitud de API?

Puede agrupar varios mensajes dentro de una única carga útil de solicitud y transmitirlos a [!DNL Platform]. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una única solicitud es una excelente manera de optimizar las operaciones de datos. Lea el tutorial en [envío de varios mensajes en una solicitud](../tutorials/streaming-multiple-messages.md) para obtener más información.

### ¿Cómo sé si los datos que envío se están recibiendo?

Todos los datos que se envían a [!DNL Platform] (correctamente o de otro modo) se almacena como archivos por lotes antes de persistir en los conjuntos de datos. El estado de procesamiento de los lotes aparece dentro del conjunto de datos al que se enviaron.

Puede verificar si los datos se han introducido correctamente comprobando la actividad del conjunto de datos mediante la variable [interfaz de usuario del Experience Platform](https://platform.adobe.com). Haga clic en **[!UICONTROL Conjuntos de datos]** en la navegación de la izquierda para mostrar una lista de conjuntos de datos. Seleccione el conjunto de datos al que está transmitiendo desde la lista mostrada para abrir su **[!UICONTROL Actividad del conjunto de datos]** , que muestra todos los lotes enviados durante un período de tiempo seleccionado. Para obtener más información sobre el uso de [!DNL Experience Platform] para monitorizar los flujos de datos, consulte la guía de [monitorización de flujos de datos de flujo continuo](../quality/monitor-data-ingestion.md).

Si los datos no se han podido ingerir y desea recuperarlos de [!DNL Platform], puede recuperar los lotes con errores enviando sus ID a la [!DNL Data Access API]. Consulte la guía de [recuperación de lotes con errores](../quality/retrieve-failed-batches.md) para obtener más información.

### ¿Por qué no están disponibles los datos de flujo continuo en el lago de datos?

Existen varias razones por las que la ingesta por lotes puede no alcanzar la variable [!DNL Data Lake], como formato no válido, datos que faltan o errores del sistema. Para determinar por qué ha fallado el lote, debe recuperar el lote mediante la variable [!DNL Data Ingestion Service API] y ver sus detalles. Para ver los pasos detallados sobre la recuperación de un lote con errores, consulte la guía de [recuperación de lotes con errores](../quality/retrieve-failed-batches.md).

### ¿Cómo se analiza la respuesta devuelta para la solicitud de API?

Puede analizar una respuesta comprobando primero el código de respuesta del servidor para determinar si la solicitud se aceptó. Si se devuelve un código de respuesta correcto, puede revisar la `responses` objeto array para determinar el estado de la tarea de ingesta.

Una solicitud de API de un solo mensaje correcta devuelve el código de estado 200. Una solicitud de API por lotes correcta (o parcialmente correcta) devuelve el código de estado 207.

El siguiente JSON es un objeto de respuesta de ejemplo para una solicitud de API con dos mensajes: un éxito y otro fracaso. Los mensajes que se retransmiten correctamente devuelven un `xactionId` propiedad. Los mensajes que no se pueden transmitir devuelven un `statusCode` propiedad y una respuesta `message` con más información.

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
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### ¿Por qué no reciben mis mensajes enviados? [!DNL Real-Time Customer Profile]?

If [!DNL Real-Time Customer Profile] rechaza un mensaje, lo más probable es que se deba a información de identidad incorrecta. Esto puede ser el resultado de proporcionar un valor o área de nombres no válida para una identidad.

Existen dos tipos de áreas de nombres de identidad: predeterminado y personalizado. Cuando utilice espacios de nombres personalizados, asegúrese de que el área de nombres se haya registrado en [!DNL Identity Service]. Consulte la [información general del área de nombres de identidad](../../identity-service/namespaces.md) para obtener más información sobre el uso de áreas de nombres predeterminadas y personalizadas.

Puede usar la variable [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver más información sobre por qué un mensaje falla en la ingesta. Haga clic en **[!UICONTROL Monitorización]** en el panel de navegación izquierdo, y luego vea la **[!UICONTROL Transmisión de extremo a extremo]** para ver los lotes de mensajes que se transmiten durante un período de tiempo seleccionado.
