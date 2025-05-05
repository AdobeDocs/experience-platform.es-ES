---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de resolución de problemas de Privacy Service
description: Este documento proporciona respuestas a las preguntas más frecuentes acerca de Privacy Service, así como información sobre los errores más comunes encontrados en la API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---

# [!DNL Privacy Service] guía de solución de problemas

Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudar a las empresas a administrar las solicitudes de privacidad de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y de la organización.

Este documento proporciona respuestas a las preguntas más frecuentes acerca de [!DNL Privacy Service], así como información sobre los errores más comunes encontrados en la API.

## Al realizar solicitudes de privacidad en la API, ¿cuál es la diferencia entre un usuario y un ID de usuario? {#user-ids}

Para poder realizar un nuevo trabajo de privacidad en la API, la carga útil JSON de la solicitud debe contener una matriz `users` que enumere la información específica de cada usuario al que se aplique la solicitud de privacidad. Cada elemento de la matriz `users` es un objeto que representa a un usuario en particular, identificado por su valor `key`.

A su vez, cada objeto de usuario (o `key`) contiene su propia matriz `userIDs`. Esta matriz enumera valores de id. específicos **para ese usuario en particular**.

Consideremos el siguiente ejemplo de matriz `users`:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

La matriz contiene dos objetos que representan a los usuarios individuales identificados por sus valores de `key` (&quot;DavidSmith&quot; y &quot;user12345&quot;). &quot;DavidSmith&quot; solo tiene un ID en la lista (su dirección de correo electrónico), mientras que &quot;user12345&quot; tiene dos (su dirección de correo electrónico y ECID).

Para obtener más información sobre cómo proporcionar información de identidad de usuario, consulte la guía sobre [datos de identidad para solicitudes de privacidad](identity-data.md).


## ¿Puedo usar [!DNL Privacy Service] para limpiar datos que se enviaron accidentalmente a [!DNL Experience Platform]?

Adobe no admite el uso de [!DNL Privacy Service] para borrar datos que se hayan enviado accidentalmente a un producto. [!DNL Privacy Service] se ha diseñado para ayudarle a cumplir con sus obligaciones en relación con las solicitudes de acceso o eliminación de los interesados (o consumidores). No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos.

Las solicitudes de privacidad son sensibles al tiempo y se completan en relación con la ley de privacidad aplicable. el envío de solicitudes que no son solicitudes de eliminación o de acceso del sujeto de datos/consumidor afecta a todos los clientes de [!DNL Privacy Service] y a la capacidad de [!DNL Privacy Service] de admitir los plazos legales adecuados. Ahora se establece un límite diario de carga estricto para ayudar a evitar el abuso del servicio.

Póngase en contacto con el equipo de su cuenta de Adobe para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier PII o problema de datos.

## ¿Cómo obtengo información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar detalles sobre un trabajo en particular mediante la API o la interfaz de usuario de [!DNL Privacy Service].

### Uso de la API

Para recuperar el estado de un trabajo en particular mediante la API [!DNL Privacy Service], realice una solicitud al extremo raíz (`GET /`) utilizando el identificador del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en la guía de API de [!DNL Privacy Service].

### Uso de la IU

Todas las solicitudes de trabajo activas se enumeran en el widget **[!UICONTROL Solicitudes de trabajo]** del panel de interfaz de usuario [!DNL Privacy Service]. El estado de cada solicitud de trabajo se muestra en la columna **[!UICONTROL Estado]**. Para obtener más información sobre la visualización de solicitudes de trabajo en la interfaz de usuario, consulte la [guía del usuario de Privacy Service](ui/user-guide.md).

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

La API [!DNL Privacy Service] y la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP.

### Uso de la API

Realice una solicitud al extremo raíz (`GET /`) en la API [!DNL Privacy Service], utilizando el identificador del trabajo cuyos resultados desea descargar en la ruta de solicitud. Si el estado del trabajo es Completo, la API incluirá un atributo `downloadURL` en el cuerpo de respuesta. Este atributo contiene una dirección URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre [buscar un trabajo por su ID](api/privacy-jobs.md#check-the-status-of-a-job) en la guía de API [!DNL Privacy Service].

### Uso de la IU

En el panel de la interfaz de usuario [!DNL Privacy Service], busque el trabajo que desee descargar del widget **Solicitudes de trabajo**. Seleccione el ID del trabajo para abrir la página Detalles del trabajo. Aquí, selecciona **Descargar** en la esquina superior derecha para descargar el archivo ZIP. Consulte la [guía del usuario de Privacy Service](ui/user-guide.md) para ver los pasos más detallados.

## Mensajes de error comunes {#common-error-messages}

En la tabla siguiente se describen algunos errores comunes de [!DNL Privacy Service], con descripciones que ayudan a resolver sus respectivos problemas.

| Mensaje de error | Descripción |
| --- | --- |
| No se ha podido encontrar la ID de usuario. | Algunos de los ID de usuario proporcionados en la solicitud no se encontraron y se omitieron. Asegúrese de que está utilizando los espacios de nombres y los valores de ID correctos en la carga útil de la solicitud. Consulte el documento sobre [proporcionar datos de identidad](./identity-data.md) para obtener una explicación más detallada. |
| Área de nombres no válida | Un área de nombres de identidad proporcionada para un ID de usuario no era válida. Consulte la sección sobre [áreas de nombres de identidad estándar](./api/appendix.md#standard-namespaces) en el apéndice de la guía de API [!DNL Privacy Service] para obtener una lista de áreas de nombres aceptadas. Si utiliza un área de nombres personalizada, asegúrese de establecer la propiedad `type` del identificador en &quot;custom&quot;. |
| Completado parcialmente | El trabajo se ha completado correctamente, pero algunos datos no eran aplicables a la solicitud determinada y se omitieron. |
| Los datos no tienen el formato requerido. | Uno o varios valores de datos de la aplicación especificada tenían un formato incorrecto. Consulte los detalles del trabajo para obtener más información. |
| No se ha aprovisionado la organización de IMS. | Este mensaje se produce cuando su organización no se ha aprovisionado para [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener más información. |
| El acceso y los permisos son obligatorios. | El acceso y los permisos son necesarios para poder usar [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener acceso. |
| Error al cargar y archivar los datos de acceso. | Cuando se produzca este error, vuelva a cargar los datos de acceso e inténtelo de nuevo. |
| Se ha superado la carga de trabajo para el límite actual de tasa de documentos. | Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo. |
| Demasiadas solicitudes<br> (errores HTTP 429) | Si los patrones de envío superan el límite monitorizado de trabajos de sujetos de datos permitidos, recibirá un error HTTP 429 en respuesta al tráfico continuo de su organización. Privacy Service está diseñado para el procesamiento de las solicitudes de privacidad de los interesados. No debe utilizarse para la limpieza de datos. Si recibe errores HTTP 429, se implementan límites de restricción y solicitud para proteger Adobe de abusos que podrían poner en riesgo el trabajo de conformidad legítimo.<br>La configuración de las programaciones de caducidad de los conjuntos de datos[&#128279;](../hygiene/ui/dataset-expiration.md) y el uso de la [característica de eliminación de registros](../hygiene/ui/record-delete.md) proporcionan métodos alternativos para minimizar los datos.  Consulte su documentación correspondiente para obtener más información sobre cómo aplicar estas funcionalidades. |
