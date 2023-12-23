---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de resolución de problemas del Privacy Service
description: Este documento proporciona respuestas a las preguntas frecuentes sobre Privacy Service, así como información sobre los errores más comunes encontrados en la API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 1%

---

# [!DNL Privacy Service] guía de solución de problemas

Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudar a las empresas a administrar las solicitudes de privacidad de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

Este documento proporciona respuestas a las preguntas frecuentes acerca de [!DNL Privacy Service], así como información sobre errores más comunes encontrados en la API.

## Al realizar solicitudes de privacidad en la API, ¿cuál es la diferencia entre un usuario y un ID de usuario? {#user-ids}

Para poder realizar un nuevo trabajo de privacidad en la API, la carga útil JSON de la solicitud debe contener un `users` matriz que enumera información específica de cada usuario al que se aplica la solicitud de privacidad. Cada elemento de la `users` matriz es un objeto que representa a un usuario en particular, identificado por su `key` valor.

A su vez, cada objeto de usuario (o `key`) contiene su propio `userIDs` matriz. Esta matriz enumera valores de ID específicos **para ese usuario en particular**.

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

La matriz contiene dos objetos que representan a usuarios individuales identificados por su `key` valores (&quot;DavidSmith&quot; y &quot;user12345&quot;). &quot;DavidSmith&quot; solo tiene un ID en la lista (su dirección de correo electrónico), mientras que &quot;user12345&quot; tiene dos (su dirección de correo electrónico y ECID).

Para obtener más información sobre cómo proporcionar información de identidad de usuario, consulte la guía de [datos de identidad para solicitudes de privacidad](identity-data.md).


## ¿Puedo usar [!DNL Privacy Service] para limpiar los datos que se enviaron accidentalmente a [!DNL Platform]?

El Adobe no admite el uso de [!DNL Privacy Service] para borrar datos que se hayan enviado accidentalmente a un producto. [!DNL Privacy Service] está diseñado para ayudarle a cumplir con sus obligaciones en relación con las solicitudes de acceso o eliminación de los interesados (o consumidores). No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos.

Las solicitudes de privacidad son sensibles al tiempo y se completan en relación con la ley de privacidad aplicable. el envío de solicitudes que no sean solicitudes de acceso o eliminación de los interesados/consumidores afecta a todo [!DNL Privacy Service] clientes y la capacidad para [!DNL Privacy Service] para cumplir los plazos legales adecuados. Ahora se establece un límite diario de carga estricto para ayudar a evitar el abuso del servicio.

Póngase en contacto con el equipo de su cuenta de Adobe para coordinar y proporcionar un nivel de esfuerzo para eliminar cualquier PII o problema de datos.

## ¿Cómo obtengo información sobre el estado de mi solicitud de privacidad o trabajo?

Puede recuperar detalles sobre un trabajo en particular utilizando la variable [!DNL Privacy Service] API o interfaz de usuario.

### Uso de la API

Para recuperar el estado de un trabajo concreto utilizando [!DNL Privacy Service] API, realice una solicitud a la raíz (`GET /`) punto final, con el ID del trabajo en la ruta de solicitud. Para obtener más información, consulte la sección sobre [comprobación del estado de un trabajo](api/privacy-jobs.md#check-the-status-of-a-job) en el [!DNL Privacy Service] Guía de API.

### Uso de la IU

Todas las solicitudes de trabajo activas se enumeran en la **[!UICONTROL Solicitudes de trabajo]** widget en el [!DNL Privacy Service] Panel de IU. El estado de cada solicitud de trabajo se muestra en **[!UICONTROL Estado]** columna. Para obtener más información sobre la visualización de solicitudes de trabajo en la IU, consulte la [Guía del usuario del Privacy Service](ui/user-guide.md).

## ¿Cómo puedo descargar los resultados de mis trabajos de privacidad completados?

El [!DNL Privacy Service] Tanto la API como la interfaz de usuario proporcionan métodos para descargar los resultados de los trabajos completados en formato ZIP.

### Uso de la API

Realice una solicitud a la raíz (`GET /`) punto final en [!DNL Privacy Service] API, con el ID del trabajo cuyos resultados desea descargar en la ruta de solicitud. Si el estado del trabajo es Completo, la API incluirá un `downloadURL` en el cuerpo de la respuesta. Este atributo contiene una dirección URL que puede pegar en la barra de direcciones del explorador para descargar el archivo ZIP.

Para obtener más información, consulte la sección sobre [búsqueda de un trabajo por su ID](api/privacy-jobs.md#check-the-status-of-a-job) en el [!DNL Privacy Service] Guía de API.

### Uso de la IU

En el [!DNL Privacy Service] En el panel de la interfaz de usuario, busque el trabajo que desea descargar desde **Solicitudes de trabajo** widget. Seleccione el ID del trabajo para abrir la página Detalles del trabajo. Desde aquí, seleccione **Descargar** en la esquina superior derecha para descargar el archivo ZIP. Consulte la [Guía del usuario del Privacy Service](ui/user-guide.md) para ver los pasos más detallados.

## Mensajes de error frecuentes {#common-error-messages}

En la tabla siguiente se describen algunos errores comunes de [!DNL Privacy Service], con descripciones para ayudar a resolver sus respectivos problemas.

| Mensaje de error | Descripción |
| --- | --- |
| No se han encontrado los ID de usuario. | Algunos de los ID de usuario proporcionados en la solicitud no se encontraron y se omitieron. Asegúrese de que está utilizando los espacios de nombres y los valores de ID correctos en la carga útil de la solicitud. Consulte el documento sobre [proporcionar datos de identidad](./identity-data.md) para obtener una explicación más detallada. |
| Área de nombres no válida | Un área de nombres de identidad proporcionada para un ID de usuario no era válida. Consulte la sección sobre [áreas de nombres de identidad estándar](./api/appendix.md#standard-namespaces) en el [!DNL Privacy Service] Anexo de la guía de API para obtener una lista de áreas de nombres aceptadas. Si utiliza un área de nombres personalizada, asegúrese de que está configurando el ID de `type` propiedad en &quot;custom&quot;. |
| Completado parcialmente | El trabajo se ha completado correctamente, pero algunos datos no eran aplicables a la solicitud determinada y se omitieron. |
| Los datos no tienen el formato requerido. | Uno o varios valores de datos de la aplicación especificada tenían un formato incorrecto. Consulte los detalles del trabajo para obtener más información. |
| No se ha aprovisionado la organización de IMS. | Este mensaje se produce cuando su organización no se ha aprovisionado para [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener más información. |
| El acceso y los permisos son obligatorios. | El acceso y los permisos son necesarios para utilizar [!DNL Privacy Service]. Póngase en contacto con el administrador para obtener acceso. |
| Se ha producido un error al cargar y archivar los datos de acceso. | Cuando se produzca este error, vuelva a cargar los datos de acceso e inténtelo de nuevo. |
| Se ha superado la carga de trabajo para el límite actual de tasa de documentos. | Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo. |
| Demasiadas solicitudes<br>(Errores HTTP 429) | Si los patrones de envío superan el límite monitorizado de trabajos de sujetos de datos permitidos, recibirá un error HTTP 429 en respuesta al tráfico continuo de su organización. Privacy Service está diseñado para el procesamiento de las solicitudes de privacidad de los sujetos de datos. No debe utilizarse para la limpieza de datos. Si recibe errores HTTP 429, se implementan límites de restricción y solicitud para proteger el Adobe de abusos que podrían poner en riesgo el trabajo de conformidad legítimo.<br>Los métodos alternativos para minimizar sus datos son proporcionados por [establecer programaciones de caducidad de conjuntos de datos](../hygiene/ui/dataset-expiration.md) y el uso de [función de eliminación de registros](../hygiene/ui/record-delete.md). Consulte su documentación correspondiente para obtener más información sobre cómo aplicar estas funcionalidades. |
