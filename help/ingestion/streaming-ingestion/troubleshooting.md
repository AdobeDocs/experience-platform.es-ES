---
keywords: Experience Platform;inicio;temas populares;transmisión;transmisión;ingesta de transmisión;resolución de problemas;resolución de problemas de ingesta de transmisión;preguntas frecuentes sobre ingesta de transmisión;preguntas frecuentes;
solution: Experience Platform
title: Guía de resolución de problemas de ingesta
description: Este documento proporciona respuestas a las preguntas frecuentes acerca de la ingesta de transmisión en Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# Guía de solución de problemas de ingesta

Este documento proporciona respuestas a las preguntas frecuentes acerca de la ingesta de transmisión en Adobe Experience Platform. Para preguntas y resolución de problemas relacionados con otros [!DNL Platform] servicios, incluidos los que se encuentran en todos los [!DNL Platform] API, consulte la [guía de solución de problemas del Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] proporciona API de RESTful que puede utilizar para introducir datos en [!DNL Experience Platform]. Los datos introducidos se utilizan para actualizar perfiles de clientes individuales en tiempo casi real, lo que le permite ofrecer experiencias personalizadas y relevantes en varios canales. Lea el [Resumen de ingesta de datos](../home.md) para obtener más información sobre el servicio y los diferentes métodos de ingesta. Para ver los pasos sobre cómo utilizar las API de ingesta de transmisión, lea la [información general sobre ingesta de streaming](../streaming-ingestion/overview.md).

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas frecuentes acerca de la ingesta de transmisión.

### ¿Cómo sé que la carga útil que estoy enviando tiene el formato correcto?

[!DNL Data Ingestion] aprovecha [!DNL Experience Data Model] (XDM) para validar el formato de los datos entrantes. Si se envían datos que no se ajustan a la estructura de un esquema XDM predefinido, la ingesta fallará. Para obtener más información sobre XDM y su uso en [!DNL Experience Platform], consulte la [Información general del sistema XDM](../../xdm/home.md).

La ingesta por transmisión admite dos modos de validación: sincrónico y asincrónico. Cada método de validación gestiona los datos con errores de forma diferente.

**Validación sincrónica** debe utilizarse durante el proceso de desarrollo. Los registros que no superan la validación se pierden y devuelven un mensaje de error sobre el motivo del error (por ejemplo: &quot;Formato de mensaje XDM no válido&quot;).

**Validación asincrónica** debe utilizarse en producción. Los datos mal formados que no superen la validación se envían a [!DNL Data Lake] como un archivo por lotes fallido, donde se puede recuperar más adelante para un análisis más detallado.

Para obtener más información sobre la validación sincrónica y asincrónica, consulte la [resumen de validación de streaming](../quality/streaming-validation.md). Para ver los pasos de los lotes que no superan la validación, consulte la guía sobre [recuperación de lotes fallidos](../quality/retrieve-failed-batches.md).

### ¿Puedo validar una carga útil de solicitud antes de enviarla a? [!DNL Platform]?

Las cargas útiles de solicitud solo se pueden evaluar después de enviarse a [!DNL Platform]. Al realizar la validación sincrónica, las cargas útiles válidas devuelven objetos JSON rellenados, mientras que las cargas útiles no válidas devuelven mensajes de error. Durante la validación asincrónica, el servicio detecta y envía los datos mal formados al [!DNL Data Lake] donde se puede recuperar posteriormente para su análisis. Consulte la [resumen de validación de streaming](../quality/streaming-validation.md) para obtener más información.

### ¿Qué sucede cuando se solicita una validación sincrónica en un perímetro que no la admite?

Cuando no se admite la validación sincrónica para la ubicación solicitada, se devuelve una respuesta de error 501. Consulte la [resumen de validación de streaming](../quality/streaming-validation.md) para obtener más información sobre la validación sincrónica.

### ¿Cómo puedo asegurarme de que los datos solo se recopilen de fuentes de confianza?

[!DNL Experience Platform] admite la recopilación de datos protegidos. Cuando la recopilación de datos autenticados está habilitada, los clientes deben enviar un token web JSON (JWT) y su ID de organización como encabezados de solicitud. Para obtener más información sobre cómo enviar datos autenticados a [!DNL Platform], consulte la guía de [recopilación de datos autenticados](../tutorials/create-authenticated-streaming-connection.md).

### ¿Cuál es la latencia para la transmisión de datos a [!DNL Real-Time Customer Profile]?

Los eventos transmitidos generalmente se reflejan en [!DNL Real-Time Customer Profile] en menos de 60 segundos. Las latencias reales pueden variar debido al volumen de datos, el tamaño del mensaje y las limitaciones de ancho de banda.

### ¿Puedo incluir varios mensajes en la misma solicitud de API?

Puede agrupar varios mensajes en una sola carga útil de solicitud y transmitirlos a [!DNL Platform]. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una sola solicitud es una forma excelente de optimizar las operaciones de datos. Lea el tutorial sobre [envío de varios mensajes en una solicitud](../tutorials/streaming-multiple-messages.md) para obtener más información.

### ¿Cómo sé si se están recibiendo los datos que estoy enviando?

Todos los datos que se envían a [!DNL Platform] (correctamente o de otro modo) se almacena como archivos por lotes antes de persistir en conjuntos de datos. El estado de procesamiento de los lotes aparece dentro del conjunto de datos al que se enviaron.

Puede comprobar si los datos se han introducido correctamente comprobando la actividad del conjunto de datos mediante el [Interfaz de usuario del Experience Platform](https://platform.adobe.com). Clic **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para mostrar una lista de conjuntos de datos. Seleccione el conjunto de datos al que está transmitiendo desde la lista mostrada para abrir su **[!UICONTROL Actividad de conjunto de datos]** página, que muestra todos los lotes enviados durante un período de tiempo seleccionado. Para obtener más información sobre el uso de [!DNL Experience Platform] para monitorizar flujos de datos, consulte la guía de [monitorización de flujos de datos de streaming](../quality/monitor-data-ingestion.md).

Si los datos no se han podido introducir y desea recuperarlos de [!DNL Platform], puede recuperar los lotes con errores enviando sus ID a [!DNL Data Access API]. Consulte la guía de [recuperación de lotes fallidos](../quality/retrieve-failed-batches.md) para obtener más información.

### ¿Por qué los datos de streaming no están disponibles en el lago de datos?

Existen varias razones por las que la ingesta por lotes puede no alcanzar el [!DNL Data Lake], como formato no válido, falta de datos o errores del sistema. Para determinar por qué ha fallado el lote, debe recuperar el lote utilizando [!DNL Data Ingestion Service API] y ver sus detalles. Para ver los pasos detallados sobre la recuperación de un lote fallido, consulte la guía de [recuperación de lotes fallidos](../quality/retrieve-failed-batches.md).

### ¿Cómo analizo la respuesta devuelta para la solicitud de API?

Puede analizar una respuesta comprobando primero el código de respuesta del servidor para determinar si su solicitud fue aceptada. Si se devuelve un código de respuesta correcto, puede revisar la `responses` objeto de matriz para determinar el estado de la tarea de ingesta.

Una solicitud correcta de API de un solo mensaje devuelve el código de estado 200. Una solicitud de API de mensaje por lotes correcta (o parcialmente correcta) devuelve el código de estado 207.

El siguiente JSON es un objeto de respuesta de ejemplo para una solicitud de API con dos mensajes: uno correcto y otro fallido. Los mensajes que se transmiten correctamente devuelven un `xactionId` propiedad. Los mensajes que no se transmiten devuelven un `statusCode` propiedad y una respuesta `message` con más información.

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

### ¿Por qué no reciben mis mensajes enviados [!DNL Real-Time Customer Profile]?

If [!DNL Real-Time Customer Profile] rechaza un mensaje, probablemente se deba a una información de identidad incorrecta. Esto puede deberse a que se ha proporcionado un valor o un área de nombres no válidos para una identidad.

Existen dos tipos de áreas de nombres de identidad: predeterminadas y personalizadas. Cuando utilice áreas de nombres personalizadas, asegúrese de que el área de nombres se ha registrado en [!DNL Identity Service]. Consulte la [información general del área de nombres de identidad](../../identity-service/features/namespaces.md) para obtener más información sobre el uso de áreas de nombres predeterminadas y personalizadas.

Puede usar el complemento [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver más información sobre el motivo por el que un mensaje ha fallado en la ingesta. Clic **[!UICONTROL Monitorización]** en el panel de navegación izquierdo y, a continuación, vea la **[!UICONTROL Transmisión de extremo a extremo]** para ver los lotes de mensajes transmitidos durante un período de tiempo seleccionado.
