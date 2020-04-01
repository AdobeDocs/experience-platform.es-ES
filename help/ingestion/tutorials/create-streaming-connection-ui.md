---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de una conexión de flujo continuo mediante la interfaz de usuario
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182

---


# Creación de una conexión de flujo continuo mediante la interfaz de usuario

Esta guía de la interfaz de usuario le ayudará a crear una conexión de flujo continuo con Adobe Experience Platform.

## Primeros pasos

Para inicio de datos de flujo continuo a la plataforma de experiencia, primero debe crear una conexión HTTP de flujo. Al crear una conexión de flujo continuo, debe proporcionar detalles clave como, por ejemplo, el origen de los datos de flujo continuo y si desea o no enviar datos desde un origen de confianza (autenticado) o no de confianza (no autenticado).

Después de registrar una conexión de flujo, tendrá una dirección URL única que se puede utilizar para transmitir datos a Platform.

Tenga en cuenta que para completar esta guía, necesitará acceder a Adobe Experience Platform. Si no tiene acceso a Platform, póngase en contacto con el administrador del sistema antes de continuar.

## Creación de una conexión de flujo continuo

Después de iniciar sesión en la interfaz de usuario de la plataforma de experiencia, haga clic en **Fuentes** para abrir la ficha *Catálogo* . Esta página muestra los tipos de origen disponibles como tarjetas individuales, y cada tarjeta contiene una burbuja que muestra el número de flujos de datos que se han creado desde conexiones de flujo a conjuntos de datos.

![](../images/streaming-ingestion/ui/click-sources.png)

En la página *Fuentes* , haga clic en API **** HTTP y, a continuación, en **Connect source**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Aparece la pantalla *Conectar a HTTP* . En Detalles ** del servicio, proporcione el **nombre** y una **descripción** para la nueva conexión de flujo continuo.

En Autenticación *de cuenta*, seleccione las siguientes propiedades de configuración para la conexión de flujo continuo:

- **Autenticación:** Indica si la conexión de flujo requiere autenticación. La autenticación garantiza que los datos se recopilen a partir de fuentes de confianza. Se recomienda activarlo si se trata de información personal identificable (PII).
- **Compatibilidad de Esquema XDM:** Indica si esta conexión de transmisión enviará o no eventos compatibles con esquemas XDM. De forma predeterminada, esta propiedad está **activada**.

Una vez que haya terminado de seleccionar las propiedades de configuración, haga clic en **Connect**. La conexión HTTP de flujo se ha creado y ahora se puede ver en la ficha *Examinar* del espacio de trabajo *Fuentes* .

![](../images/streaming-ingestion/ui/http-sources-details.png)

Desde la ficha *Examinar* , puede hacer clic en la conexión HTTP de flujo recién creada y vista los detalles de esa conexión.

![](../images/streaming-ingestion/ui/browse-sources.png)

Al hacer clic en el hipervínculo del nombre de la conexión, puede seleccionar los datos que se mostrarán configurando qué conjunto de datos está conectado, haciendo clic en *Seleccionar datos*.

![](../images/streaming-ingestion/ui/select-data.png)

Puede [crear un nuevo conjunto de datos](#create-a-new-dataset) o [utilizar uno existente](#use-an-existing-dataset).

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos, proporcione el **Nombre**, la **Descripción** y el **Esquema** de destinatario para el conjunto de datos.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Después de insertar todos los detalles y hacer clic en **Siguiente**, puede revisar los detalles proporcionados antes de hacer clic en **Finalizar** para conectar el conjunto de datos a la conexión HTTP de flujo.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Usar un conjunto de datos existente

Para utilizar un conjunto de datos existente, seleccione el nombre **del conjunto de datos de** salida.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Después de hacer clic en **Siguiente**, puede revisar los detalles antes de hacer clic en **Finalizar** para conectar el conjunto de datos seleccionado a la conexión HTTP de flujo.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión HTTP de flujo que le permite utilizar el extremo de flujo para acceder a una variedad de API de inserción de datos. Para obtener instrucciones para crear una conexión de flujo en la API, lea el tutorial [de](../tutorials/create-streaming-connection.md)creación de una conexión de flujo.
