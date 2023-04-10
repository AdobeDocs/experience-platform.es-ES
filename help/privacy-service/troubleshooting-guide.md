---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de solución de problemas del Privacy Service
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el Privacy Service, así como información sobre los errores encontrados con frecuencia en la API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 1%

---

# [!DNL Privacy Service] guía de solución de problemas

Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudar a las empresas a administrar las solicitudes de privacidad de datos de los clientes. con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos de clientes personales o privados, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y de la organización.

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Privacy Service], así como información sobre los errores encontrados con frecuencia en la API.

## Al realizar solicitudes de privacidad en la API, ¿cuál es la diferencia entre un usuario y un ID de usuario? {#user-ids}

Para realizar un nuevo trabajo de privacidad en la API, la carga útil JSON de la solicitud debe contener un `users` matriz que enumera información específica para cada usuario al que se aplica la solicitud de privacidad. Cada elemento de la sección `users` array es un objeto que representa a un usuario en particular, identificado por su `key` valor.

A su vez, cada objeto de usuario (o `key`) contiene su propio `userIDs` matriz. Esta matriz enumera los valores de ID específicos **para ese usuario en particular**.

Consideremos el siguiente ejemplo `users` matriz:

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

La matriz contiene dos objetos que representan a usuarios individuales identificados por sus `key` (&quot;DavidSmith&quot; y &quot;user12345&quot;). &quot;DavidSmith&quot; solo tiene un ID enumerado (su dirección de correo electrónico), mientras que &quot;user12345&quot; tiene dos (su dirección de correo electrónico y ECID).

Para obtener más información sobre cómo proporcionar información de identidad de usuario, consulte la guía de [datos de identidad para solicitudes de privacidad](identity-data.md).


## ¿Puedo usar [!DNL Privacy Service] para limpiar los datos que se han enviado accidentalmente a [!DNL Platform]?

El Adobe no es compatible con el uso de [!DNL Privacy Service] para borrar datos que se hayan enviado accidentalmente a un producto. [!DNL Privacy Service] está diseñado para ayudarle a cumplir con sus obligaciones en cuanto a solicitudes de acceso o eliminación del interesado (o del consumidor). No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos.

Las solicitudes de privacidad distinguen el tiempo y se completan en relación con la legislación de privacidad aplicable. la presentación de solicitudes que no sean solicitudes de acceso o eliminación del interesado o del consumidor afecta a todas las [!DNL Privacy Service] clientes y la capacidad de [!DNL Privacy Service] para apoyar los plazos legales adecuados. Ahora existe un límite de carga diaria estricto para ayudar a evitar el uso indebido del servicio.

Póngase en contacto con el equipo de su cuenta de Adobe para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier problema de datos o PII.

## ¿Cómo obtengo información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar los detalles de un trabajo en particular utilizando la variable [!DNL Privacy Service] API o interfaz de usuario.

### Uso de la API

Para recuperar el estado de un trabajo en particular mediante la variable [!DNL Privacy Service] , realice una solicitud a la raíz (`GET /`), usando el ID del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en el [!DNL Privacy Service] Guía de API.

### Uso de la interfaz de usuario

Todas las solicitudes de trabajo activas se enumeran en la sección **[!UICONTROL Solicitudes de trabajo]** en el [!DNL Privacy Service] Panel de IU. El estado de cada solicitud de trabajo se muestra en la sección **[!UICONTROL Estado]** para abrir el Navegador. Para obtener más información sobre la visualización de solicitudes de trabajo en la interfaz de usuario, consulte la [Guía del usuario del Privacy Service](ui/user-guide.md).

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

La variable [!DNL Privacy Service] La API y la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP.

### Uso de la API

Realice una solicitud a la raíz (`GET /`) en la variable [!DNL Privacy Service] , empleando el ID del trabajo cuyos resultados desea descargar en la ruta de solicitud. Si se completa el estado del trabajo, la API incluirá un `downloadURL` en el cuerpo de respuesta. Este atributo contiene una dirección URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre [búsqueda de un trabajo por su ID](api/privacy-jobs.md#check-the-status-of-a-job) en el [!DNL Privacy Service] Guía de API.

### Uso de la interfaz de usuario

En el [!DNL Privacy Service] En el tablero IU, busque el trabajo que desea descargar de la **Solicitudes de trabajo** para abrir el Navegador. Seleccione el ID del trabajo para abrir la página Detalles del trabajo . Desde aquí, seleccione **Descargar** en la esquina superior derecha para descargar el archivo ZIP. Consulte la [Guía del usuario del Privacy Service](ui/user-guide.md) para ver los pasos más detallados.

## Mensajes de error frecuentes

La siguiente tabla describe algunos errores comunes en [!DNL Privacy Service], con descripciones para ayudar a resolver sus problemas respectivos.

| Mensaje de error | Descripción |
| --- | --- |
| No se encontraron los ID de usuario. | Algunos de los ID de usuario proporcionados en la solicitud no se encontraron y se omitieron. Asegúrese de que está utilizando los espacios de nombres y valores de ID correctos en la carga útil de la solicitud. Consulte el documento en [proporcionar datos de identidad](./identity-data.md) para obtener una explicación más detallada. |
| Espacio de nombres no válido | Un espacio de nombres de identidad proporcionado para un ID de usuario no era válido. Consulte la sección sobre [áreas de nombres de identidad estándar](./api/appendix.md#standard-namespaces) en el [!DNL Privacy Service] apéndice de la guía de API para obtener una lista de áreas de nombres aceptadas. Si utiliza un área de nombres personalizada, asegúrese de que está configurando el ID de `type` en &quot;custom&quot;. |
| Finalizado parcialmente | El trabajo se completó correctamente, pero algunos datos no eran aplicables para la solicitud dada y se omitieron. |
| Los datos no tienen el formato requerido. | Uno o más de los valores de datos de la aplicación especificada tenían un formato incorrecto. Consulte los detalles del trabajo para obtener más información. |
| La organización IMS no se ha aprovisionado. | Este mensaje se produce cuando la organización de IMS no se ha aprovisionado para [!DNL Privacy Service]. Póngase en contacto con su administrador para obtener más información. |
| Se necesitan permisos y acceso. | Se necesitan permisos y acceso para poder usar [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener acceso. |
| Hubo un problema al cargar y archivar los datos de acceso. | Cuando se produzca este error, vuelva a cargar los datos de acceso e inténtelo de nuevo. |
| Se superó la carga de trabajo para el límite actual de la tasa de documentos. | Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo. |
