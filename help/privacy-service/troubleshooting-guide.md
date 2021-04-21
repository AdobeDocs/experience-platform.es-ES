---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de solución de problemas del Privacy Service
topic-legacy: troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el Privacy Service, así como información sobre los errores encontrados con frecuencia en la API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# [!DNL Privacy Service] guía de solución de problemas

Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudar a las empresas a administrar las solicitudes de privacidad de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y de la organización.

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Privacy Service], así como información sobre errores encontrados con frecuencia en la API.

## Al realizar solicitudes de privacidad en la API, ¿cuál es la diferencia entre un usuario y un ID de usuario? {#user-ids}

Para realizar un nuevo trabajo de privacidad en la API, la carga útil JSON de la solicitud debe contener una matriz `users` que enumere información específica para cada usuario al que se aplique la solicitud de privacidad. Cada elemento de la matriz `users` es un objeto que representa a un usuario en particular, identificado por su valor `key`.

A su vez, cada objeto de usuario (o `key`) contiene su propia matriz `userIDs`. Esta matriz enumera los valores de ID específicos **para ese usuario** en particular.

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

La matriz contiene dos objetos que representan a usuarios individuales identificados por sus valores `key` (&quot;DavidSmith&quot; y &quot;user12345&quot;). &quot;DavidSmith&quot; solo tiene un ID enumerado (su dirección de correo electrónico), mientras que &quot;user12345&quot; tiene dos (su dirección de correo electrónico y ECID).

Para obtener más información sobre cómo proporcionar información de identidad de usuario, consulte la guía sobre [datos de identidad para solicitudes de privacidad](identity-data.md).


## ¿Puedo usar [!DNL Privacy Service] para limpiar los datos que se enviaron accidentalmente a [!DNL Platform]?

Adobe no admite el uso de [!DNL Privacy Service] para borrar datos que se hayan enviado por error a un producto. [!DNL Privacy Service] está diseñado para ayudarle a cumplir con sus obligaciones en cuanto a solicitudes de acceso o eliminación del interesado (o del consumidor). Estas solicitudes distinguen el tiempo y se completan en relación con la legislación de privacidad aplicable. El envío de solicitudes que no sean solicitudes de acceso o eliminación de sujetos/consumidores de datos afecta a todos los clientes [!DNL Privacy Service] y a la capacidad de [!DNL Privacy Service] de soportar los plazos legales adecuados.

Póngase en contacto con su administrador de cuentas para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier PII o problema de datos.

## ¿Cómo obtengo información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar detalles sobre un trabajo concreto utilizando la API [!DNL Privacy Service] o la interfaz de usuario.

### Uso de la API

Para recuperar el estado de un trabajo concreto mediante la API [!DNL Privacy Service], realice una solicitud al extremo raíz (`GET /`) utilizando el ID del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para desarrolladores de [!DNL Privacy Service].

### Uso de la interfaz de usuario

Todas las solicitudes de trabajo activas se enumeran en el widget **[!UICONTROL Job Requests]** del panel de IU [!DNL Privacy Service]. El estado de cada solicitud de trabajo se muestra en la columna **[!UICONTROL Status]**. Para obtener más información sobre la visualización de solicitudes de trabajo en la interfaz de usuario, consulte la [guía del usuario del Privacy Service](ui/user-guide.md).

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

La API [!DNL Privacy Service] y la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP.

### Uso de la API

Realice una solicitud al extremo raíz (`GET /`) de la API [!DNL Privacy Service] utilizando el ID del trabajo cuyos resultados desee descargar en la ruta de solicitud. Si se completa el estado del trabajo, la API incluirá un atributo `downloadURL` en el cuerpo de respuesta. Este atributo contiene una dirección URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre [búsqueda de un trabajo por su ID](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para desarrolladores de [!DNL Privacy Service].

### Uso de la interfaz de usuario

En el tablero de la interfaz de usuario [!DNL Privacy Service], busque el trabajo que desea descargar del widget **Solicitudes de trabajo**. Seleccione el ID del trabajo para abrir la página Detalles del trabajo . Desde aquí, seleccione **Download** en la esquina superior derecha para descargar el archivo ZIP. Consulte la [guía del usuario del Privacy Service](ui/user-guide.md) para ver los pasos más detallados.

## Mensajes de error frecuentes

La siguiente tabla describe algunos errores comunes en [!DNL Privacy Service], con descripciones que ayudan a resolver sus respectivos problemas.

| Mensaje de error | Descripción |
| --- | --- |
| No se encontraron los ID de usuario. | Algunos de los ID de usuario proporcionados en la solicitud no se encontraron y se omitieron. Asegúrese de que está utilizando los espacios de nombres y valores de ID correctos en la carga útil de la solicitud. Consulte el documento sobre [proporcionar datos de identidad](./identity-data.md) para obtener una explicación más detallada. |
| Espacio de nombres no válido | Un espacio de nombres de identidad proporcionado para un ID de usuario no era válido. Consulte la sección sobre [áreas de nombres de identidad estándar](./api/appendix.md#standard-namespaces) en el apéndice de la guía para desarrolladores de [!DNL Privacy Service] para obtener una lista de áreas de nombres aceptadas. Si utiliza un área de nombres personalizada, asegúrese de que está configurando la propiedad `type` del ID en &quot;personalizada&quot;. |
| Finalizado parcialmente | El trabajo se completó correctamente, pero algunos datos no eran aplicables para la solicitud dada y se omitieron. |
| Los datos no tienen el formato requerido. | Uno o más de los valores de datos de la aplicación especificada tenían un formato incorrecto. Consulte los detalles del trabajo para obtener más información. |
| La organización IMS no se ha aprovisionado. | Este mensaje se produce cuando la organización IMS no se ha aprovisionado para [!DNL Privacy Service]. Póngase en contacto con su administrador para obtener más información. |
| Se necesitan permisos y acceso. | Se necesitan permisos y acceso para utilizar [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener acceso. |
| Hubo un problema al cargar y archivar los datos de acceso. | Cuando se produzca este error, vuelva a cargar los datos de acceso e inténtelo de nuevo. |
| Se superó la carga de trabajo para el límite actual de la tasa de documentos. | Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo. |
