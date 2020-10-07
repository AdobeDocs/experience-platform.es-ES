---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Preguntas más frecuentes sobre Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# [!DNL Privacy Service] guía de solución de problemas

Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudar a las compañías a administrar las solicitudes de privacidad de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales o privados de clientes, facilitando así el cumplimiento automatizado de las normas de privacidad legales y de la organización.

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Privacy Service], así como información sobre los errores encontrados más frecuentemente en la API.

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


## ¿Puedo usar [!DNL Privacy Service] para limpiar datos a los que se envió accidentalmente [!DNL Platform]?

Adobe no admite el uso [!DNL Privacy Service] para eliminar datos enviados accidentalmente a un producto. [!DNL Privacy Service] está diseñado para ayudarle a cumplir con sus obligaciones de acceso al sujeto de datos (o consumidor) o para eliminar solicitudes. Estas solicitudes tienen en cuenta el tiempo y se completan en relación con la ley de privacidad aplicable. La presentación de solicitudes que no son solicitudes de acceso al consumidor o sujeto a datos o de eliminación afecta a todos [!DNL Privacy Service] los clientes y la capacidad de [!DNL Privacy Service] admitir los plazos legales adecuados.

Comuníquese con el administrador de cuentas (MDL) para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier PII o problema de datos.

## ¿Cómo puedo obtener información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar detalles sobre un trabajo concreto mediante la API o la interfaz de usuario [!DNL Privacy Service] .

### Uso de la API

Para recuperar el estado de un trabajo concreto mediante la [!DNL Privacy Service] API, realice una solicitud al extremo raíz (`GET /`) utilizando el ID del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre la [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para [!DNL Privacy Service] desarrolladores.

### Uso de la interfaz de usuario

Todas las solicitudes de trabajo activas se muestran en la utilidad Solicitudes **[!UICONTROL de]** trabajo del panel de la [!DNL Privacy Service] interfaz de usuario. El estado de cada solicitud de trabajo se muestra en la columna **[!UICONTROL Estado]** . Para obtener más información sobre la visualización de solicitudes de trabajo en la interfaz de usuario, consulte la guía [de usuario del](ui/user-guide.md)Privacy Service.

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

Tanto la API como la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP. [!DNL Privacy Service]

### Uso de la API

Realice una solicitud al extremo raíz (`GET /`) en la [!DNL Privacy Service] API, utilizando el ID del trabajo cuyos resultados desee descargar en la ruta de la solicitud. Si se completa el estado del trabajo, la API incluirá un `downloadURL` atributo en el cuerpo de respuesta. Este atributo contiene una URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre la [búsqueda de un trabajo por su ID](api/privacy-jobs.md#check-the-status-of-a-job) en la guía para [!DNL Privacy Service] desarrolladores.

### Uso de la interfaz de usuario

En el panel de la [!DNL Privacy Service] interfaz de usuario, busque el trabajo que desea descargar desde la utilidad Solicitudes **de** trabajo. Haga clic en el ID del trabajo para abrir la página Detalles del trabajo. Desde aquí, haga clic en **Descargar** en la esquina superior derecha para descargar el archivo ZIP. Consulte la guía [del usuario del](ui/user-guide.md) Privacy Service para obtener más detalles.

## Mensajes de error comunes

La siguiente tabla describe algunos errores comunes en [!DNL Privacy Service], con descripciones que ayudan a resolver sus respectivos problemas.

| Mensaje de error | Descripción |
| --- | --- |
| No se encontraron los ID de usuario. | Algunos de los ID de usuario proporcionados en la solicitud no se encontraron y se omitieron. Asegúrese de que está utilizando las Áreas de nombres y los valores de ID correctos en la carga útil de la solicitud. Consulte el documento sobre [proporcionar datos](./identity-data.md) de identidad para obtener una explicación más detallada. |
| Área de nombres no válida | La Área de nombres de identidad proporcionada para un ID de usuario no era válida. Consulte la sección sobre Áreas de nombres [de identidad](./api/appendix.md#standard-namespaces) estándar en el apéndice de la guía para [!DNL Privacy Service] desarrolladores para ver una lista de Áreas de nombres aceptadas. Si utiliza una Área de nombres personalizada, asegúrese de que está configurando la propiedad del ID en `type` &quot;custom&quot;. |
| Finalizado parcialmente | El trabajo se completó correctamente, pero algunos datos no se aplicaron a la solicitud dada y se omitieron. |
| Los datos no tienen el formato requerido. | Uno o más de los valores de datos de la aplicación especificada tenían un formato incorrecto. Consulte los detalles del trabajo para obtener más información. |
| No se ha aprovisionado la organización IMS. | Este mensaje se produce cuando la organización de IMS no se ha aprovisionado para [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener más información. |
| Se requiere acceso y permisos. | Se requieren permisos y acceso para poder utilizarlos [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener acceso. |
| Hubo un problema al cargar y archivar los datos de acceso. | Cuando se produzca este error, vuelva a cargar los datos de acceso e inténtelo de nuevo. |
| Se excedió la carga de trabajo para el límite actual de la tasa de documento. | Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo. |