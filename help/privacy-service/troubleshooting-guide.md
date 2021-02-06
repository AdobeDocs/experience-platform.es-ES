---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de solución de problemas de Privacy Service
topic: troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el Privacy Service, así como información sobre los errores encontrados más frecuentemente en la API.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---


# [!DNL Privacy Service] guía de solución de problemas

Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudar a las compañías a administrar las solicitudes de privacidad de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales o privados de los clientes, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y de la organización.

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Privacy Service], así como información sobre los errores encontrados más frecuentemente en la API.

## Al realizar solicitudes de privacidad en la API, ¿cuál es la diferencia entre un usuario y un ID de usuario? {#user-ids}

Para realizar un nuevo trabajo de privacidad en la API, la carga útil JSON de la solicitud debe contener una matriz `users` que lista información específica para cada usuario al que se aplique la solicitud de privacidad. Cada elemento de la matriz `users` es un objeto que representa a un usuario en particular, identificado por su valor `key`.

A su vez, cada objeto de usuario (o `key`) contiene su propia matriz `userIDs`. Esta matriz lista valores de ID específicos **para ese usuario en particular**.

Considere la siguiente matriz de ejemplo `users`:

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

La matriz contiene dos objetos que representan a usuarios individuales identificados por sus valores `key` (&quot;DavidSmith&quot; y &quot;user12345&quot;). &quot;DavidSmith&quot; solo tiene una ID de la lista (su dirección de correo electrónico), mientras que &quot;user12345&quot; tiene dos (su dirección de correo electrónico y ECID).

Para obtener más información sobre cómo proporcionar información de identidad de usuario, consulte la guía sobre [datos de identidad para solicitudes de privacidad](identity-data.md).


## ¿Puedo utilizar [!DNL Privacy Service] para limpiar los datos que se enviaron accidentalmente a [!DNL Platform]?

Adobe no admite el uso de [!DNL Privacy Service] para borrar datos que se enviaron accidentalmente a un producto. [!DNL Privacy Service] está diseñado para ayudarle a cumplir con sus obligaciones de acceso al sujeto de datos (o consumidor) o para eliminar solicitudes. Estas solicitudes tienen en cuenta el tiempo y se completan en relación con la ley de privacidad aplicable. El envío de solicitudes que no son solicitudes de acceso al consumidor/sujeto a datos o de eliminación afecta a todos los [!DNL Privacy Service] clientes y a la capacidad de [!DNL Privacy Service] para soportar los cronogramas legales adecuados.

Comuníquese con el administrador de cuentas (MDL) para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier PII o problema de datos.

## ¿Cómo puedo obtener información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar detalles sobre un trabajo concreto mediante la API [!DNL Privacy Service] o la interfaz de usuario.

### Uso de la API

Para recuperar el estado de un trabajo concreto mediante la API [!DNL Privacy Service], realice una solicitud al extremo raíz (`GET /`) mediante el identificador del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para desarrolladores de [!DNL Privacy Service].

### Uso de la interfaz de usuario

Todas las solicitudes de trabajo activas se enumeran en la utilidad **[!UICONTROL Solicitudes de trabajo]** del panel de la interfaz de usuario [!DNL Privacy Service]. El estado de cada solicitud de trabajo se muestra en la columna **[!UICONTROL Estado]**. Para obtener más información sobre la visualización de solicitudes de trabajo en la interfaz de usuario, consulte la [guía del usuario del Privacy Service](ui/user-guide.md).

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

Tanto la API [!DNL Privacy Service] como la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP.

### Uso de la API

Realice una solicitud al extremo raíz (`GET /`) en la API [!DNL Privacy Service], utilizando el ID del trabajo cuyos resultados desee descargar en la ruta de la solicitud. Si se completa el estado del trabajo, la API incluirá un atributo `downloadURL` en el cuerpo de respuesta. Este atributo contiene una URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre [búsqueda de un trabajo por su ID](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para desarrolladores de [!DNL Privacy Service].

### Uso de la interfaz de usuario

En el panel de la interfaz de usuario [!DNL Privacy Service], busque el trabajo que desea descargar de la utilidad **Solicitudes de trabajo**. Seleccione el ID del trabajo para abrir la página Detalles del trabajo. Desde aquí, seleccione **Descargar** en la esquina superior derecha para descargar el archivo ZIP. Consulte la [guía del usuario del Privacy Service](ui/user-guide.md) para ver los pasos más detallados.

## Mensajes de error frecuentes

La siguiente tabla describe algunos errores comunes en [!DNL Privacy Service], con descripciones que ayudan a resolver sus respectivos problemas.

| Mensaje de error | Descripción |
| --- | --- |
| No se encontraron los ID de usuario. | Algunos de los ID de usuario proporcionados en la solicitud no se encontraron y se omitieron. Asegúrese de que está utilizando las Áreas de nombres y los valores de ID correctos en la carga útil de la solicitud. Consulte el documento sobre [proporcionar datos de identidad](./identity-data.md) para obtener una explicación más detallada. |
| Área de nombres no válida | La Área de nombres de identidad proporcionada para un ID de usuario no era válida. Consulte la sección sobre [Áreas de nombres de identidad estándar](./api/appendix.md#standard-namespaces) en el apéndice de la guía para desarrolladores [!DNL Privacy Service] para obtener una lista de Áreas de nombres aceptadas. Si utiliza una Área de nombres personalizada, asegúrese de que está configurando la propiedad `type` del ID en &quot;custom&quot;. |
| Finalizado parcialmente | El trabajo se completó correctamente, pero algunos datos no se aplicaron a la solicitud dada y se omitieron. |
| Los datos no tienen el formato requerido. | Uno o más de los valores de datos de la aplicación especificada tenían un formato incorrecto. Consulte los detalles del trabajo para obtener más información. |
| No se ha aprovisionado la organización IMS. | Este mensaje se produce cuando la organización de IMS no se ha aprovisionado para [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener más información. |
| Se requiere acceso y permisos. | Se requieren permisos y acceso para poder utilizar [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener acceso. |
| Hubo un problema al cargar y archivar los datos de acceso. | Cuando se produzca este error, vuelva a cargar los datos de acceso e inténtelo de nuevo. |
| Se excedió la carga de trabajo para el límite actual de la tasa de documento. | Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo. |