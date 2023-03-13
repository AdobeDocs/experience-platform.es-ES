---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API;informes;informe de superposición de conjuntos de datos;datos de perfil
title: Generar el informe de superposición de conjuntos de datos
type: Tutorial
description: Este tutorial describe los pasos necesarios para generar el informe de superposición de conjuntos de datos mediante la API de perfil del cliente en tiempo real.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# Generar el informe de superposición de conjuntos de datos

El informe de superposición de conjuntos de datos proporciona visibilidad sobre la composición de la [!DNL Profile] almacene al exponer los conjuntos de datos que más contribuyen a su audiencia direccionable (perfiles).

Además de proporcionar perspectivas sobre sus datos, este informe puede ayudarle a tomar medidas para optimizar el uso de la licencia, como establecer un límite en la duración de ciertos datos.

Este tutorial describe los pasos necesarios para generar el informe de superposición de conjuntos de datos utilizando [!DNL Real-Time Customer Profile] API e interpretar los resultados para su organización.

## Primeros pasos

Para utilizar las API de Adobe Experience Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para recopilar los valores que necesita para los encabezados necesarios. Para obtener más información sobre las API de Experience Platform, consulte la [introducción a la documentación de las API de Platform](../../landing/api-guide.md).

Los encabezados necesarios para todas las llamadas de API de este tutorial son:

* `Authorization: Bearer {ACCESS_TOKEN}`: La `Authorization` El encabezado de requiere un token de acceso precedido de la palabra `Bearer`. Se debe generar un nuevo valor de token de acceso cada 24 horas.
* `x-api-key: {API_KEY}`: La `API Key` también se conoce como `Client ID` y es un valor que solo debe generarse una vez.
* `x-gw-ims-org-id: {ORG_ID}`: La `IMS Org` también se conoce como `Organization ID` y solo debe generarse una vez.

Después de completar el tutorial de autenticación y recopilar los valores de los encabezados necesarios, está listo para empezar a realizar llamadas a la API del cliente en tiempo real.

## Generar informe de superposición de conjuntos de datos mediante la línea de comandos

GET Si está familiarizado con el uso de la línea de comandos, puede utilizar la siguiente solicitud cURL para generar el informe de superposición de conjuntos de datos realizando una solicitud a `/previewsamplestatus/report/dataset/overlap`.

**Solicitud**

La siguiente solicitud utiliza el `date` para devolver el informe más reciente de la fecha especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la fecha, se devuelve el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se devuelve el error de estado HTTP 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

**Respuesta**

Una solicitud correcta devuelve el estado HTTP 200 (OK) y el informe de superposición de conjuntos de datos. El informe incluye un `data` que contiene listas de conjuntos de datos separados por comas y su respectivo recuento de perfiles. Para obtener más información sobre cómo leer el informe, consulte la sección sobre [interpretación de los datos del informe de superposición de conjuntos de datos](#interpret-the-report) más adelante en este tutorial.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Generar informe de superposición de conjuntos de datos mediante Postman

Postman es una plataforma colaborativa para el desarrollo de API y resulta útil para visualizar llamadas a la API. Se puede descargar de forma gratuita desde el [sitio web de Postman](https://www.postman.com) y proporciona una interfaz de usuario fácil de usar para realizar llamadas a la API. Las siguientes capturas de pantalla utilizan la interfaz de Postman.

**Solicitud**

Para solicitar el informe de superposición de conjuntos de datos mediante Postman, complete los siguientes pasos:

* En el menú desplegable, seleccione GET como tipo de solicitud.
* Introduzca los encabezados necesarios en la variable `KEY` columna:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Introduzca los valores generados durante la autenticación en la variable `VALUE` columna, reemplazando las llaves (`{{ }}`) y cualquier contenido dentro de las llaves.
* Introduzca la ruta de solicitud con o sin el opcional `date` parámetro:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   o
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parámetro | Descripción |
|---|---|
| `date` | Especifique la fecha del informe que desea devolver. Si se han ejecutado varios informes en la fecha, se devuelve el informe más reciente de esa fecha. Si no existe un informe para la fecha especificada, se devuelve el error de estado HTTP 404 (no encontrado). Si no se especifica ninguna fecha, se devuelve el informe más reciente. <br/>Formato: AAAA-MM-DD. Ejemplo: `date=2024-12-31` |

Una vez completados el tipo de solicitud, los encabezados, los valores y la ruta, seleccione **Enviar** para enviar la solicitud de API y generar el informe.

![](../images/dataset-overlap-report/postman-request.png)

**Respuesta**

Una solicitud correcta devuelve el estado HTTP 200 (OK) y el informe de superposición de conjuntos de datos. El informe incluye un `data` que contiene listas de conjuntos de datos separados por comas y su respectivo recuento de perfiles. Para obtener más información sobre cómo leer el informe, consulte la sección sobre [interpretación de los datos del informe de superposición de conjuntos de datos](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpretación de los datos del informe de superposición de conjuntos de datos {#interpret-the-report}

El informe de superposición de conjuntos de datos generado proporciona una marca de tiempo que muestra la fecha y la hora del informe y un objeto de datos que incluye combinaciones únicas de ID de conjuntos de datos como listas separadas por comas. En las secciones siguientes se proporciona información adicional sobre los componentes del informe.

### Marca de tiempo del informe

El `reportTimestamp` coincide con la fecha proporcionada en la solicitud de API o, si no se proporcionó ninguna fecha, con la marca de tiempo del informe más reciente.

### Lista de ID de conjuntos de datos

El `data` incluye combinaciones únicas de ID de conjuntos de datos como listas separadas por comas con el recuento respectivo de perfiles para esa combinación de conjuntos de datos.

>[!NOTE]
>
>La suma de todos los recuentos de perfiles asociados a cada fila del informe de superposición de conjuntos de datos debe ser igual al número total de perfiles de su organización.

Para interpretar los resultados del informe, observe el siguiente ejemplo:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Este informe proporciona la siguiente información:

* Hay 123 perfiles compuestos de datos procedentes de los siguientes conjuntos de datos: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Hay 454 412 perfiles compuestos de datos procedentes de estos dos conjuntos de datos: `5d92921872831c163452edc8` y `5eb2cdc6fa3f9a18a7592a98`.
* Hay 107 perfiles que solo están compuestos por datos de conjuntos de datos `5eeda0032af7bb19162172a7`.
* Hay un total de 454.642 perfiles en la organización.

## Pasos siguientes

Después de completar este tutorial, ahora puede generar el informe de superposición de conjuntos de datos mediante la API de perfil del cliente en tiempo real. Para obtener más información sobre cómo trabajar con los datos de perfil tanto en la API como en la interfaz de usuario de Experience Platform, comience por leer la [Documentación de información general de perfil](../home.md).
