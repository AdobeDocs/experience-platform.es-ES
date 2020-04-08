---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Preguntas más frecuentes sobre Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 64cb2de507921fcb4aaade67132024a3fc0d3dee

---


# Preguntas más frecuentes sobre Privacy Service

Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform Privacy Service.

Privacy Service proporciona una API RESTful y una interfaz de usuario para ayudar a las compañías a administrar las solicitudes de privacidad de datos de los clientes. Con Privacy Service, puede enviar solicitudes para acceder y eliminar datos de clientes personales o privados, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y de la organización.

## Al realizar solicitudes de privacidad en la API, ¿cuál es la diferencia entre un usuario y un ID de usuario? {#user-ids}

Para realizar un nuevo trabajo de privacidad en la API, la carga útil JSON de la solicitud debe contener una `users` matriz que lista información específica para cada usuario al que se aplique la solicitud de privacidad. Cada elemento de la `users` matriz es un objeto que representa a un usuario concreto, identificado por su `key` valor.

A su vez, cada objeto de usuario (o `key`) contiene su propia `userIDs` matriz. Esta matriz lista valores de ID específicos **para ese usuario** en particular.

Consider the following example `users` array:

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

La matriz contiene dos objetos que representan a usuarios individuales identificados por sus `key` valores (&quot;DavidSmith&quot; y &quot;user12345&quot;). &quot;DavidSmith&quot; solo tiene una ID de la lista (su dirección de correo electrónico), mientras que &quot;user12345&quot; tiene dos (su dirección de correo electrónico y ECID).

Para obtener más información sobre cómo proporcionar información de identidad de usuario, consulte la guía sobre datos de [identidad para solicitudes](identity-data.md)de privacidad.


## ¿Puedo utilizar Privacy Service para limpiar los datos que se enviaron accidentalmente a Platform?

Adobe no admite el uso de Privacy Service para eliminar datos enviados accidentalmente a un producto. Privacy Service está diseñado para ayudarle a cumplir con sus obligaciones en cuanto a solicitudes de acceso o eliminación del sujeto de datos (o del consumidor). Estas solicitudes tienen en cuenta el tiempo y se completan en relación con la ley de privacidad aplicable. La presentación de solicitudes que no son solicitudes de acceso al consumidor/sujeto a datos o de eliminación afecta a todos los clientes de Privacy Service y a la capacidad de Privacy Service para admitir los plazos legales adecuados.

Comuníquese con el administrador de cuentas (MDL) para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier PII o problema de datos.

## ¿Cómo puedo obtener información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar detalles sobre un trabajo concreto mediante la API de Privacy Service o la interfaz de usuario.

### Uso de la API

Para recuperar el estado de un trabajo concreto mediante la API de Privacy Service, realice una solicitud al extremo raíz (`GET /`) utilizando el ID del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre la [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para desarrolladores de Privacy Service.

### Uso de la interfaz de usuario

Todas las solicitudes de trabajo activas se enumeran en la utilidad Solicitudes **de** trabajo del panel de IU de Privacy Service. El estado de cada solicitud de trabajo se muestra en la columna **Estado** . Para obtener más información sobre la visualización de solicitudes de trabajo en la interfaz de usuario, consulte la guía [de usuario de](ui/user-guide.md)Privacy Service.

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

Tanto la API de Privacy Service como la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP.

### Uso de la API

Realice una solicitud al extremo raíz (`GET /`) en la API de Privacy Service, utilizando el ID del trabajo cuyos resultados desee descargar en la ruta de la solicitud. Si se completa el estado del trabajo, la API incluirá un `downloadURL` atributo en el cuerpo de respuesta. Este atributo contiene una URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre la [búsqueda de un trabajo mediante su ID](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para desarrolladores de Privacy Service.

### Uso de la interfaz de usuario

En el panel de la interfaz de usuario de Privacy Service, busque el trabajo que desea descargar desde la utilidad Solicitudes **de** trabajo. Haga clic en el ID del trabajo para abrir la página Detalles _del_ trabajo. Desde aquí, haga clic en **Descargar** en la esquina superior derecha para descargar el archivo ZIP. Consulte la guía [del usuario de](ui/user-guide.md) Privacy Service para obtener más detalles.