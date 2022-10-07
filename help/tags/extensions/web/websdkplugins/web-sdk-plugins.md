---
title: Información general sobre la extensión de complementos de SDK web comunes
description: Obtenga información sobre la extensión de etiqueta de complementos de SDK web comunes en Adobe Experience Platform.
exl-id: null
source-git-commit: 482ea64e25c7bbbb2eef772fb97064e34f0689e7
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 49%

---

# Información general sobre la extensión de complementos de SDK web comunes

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../launch-term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

>[!IMPORTANT]
>
>La extensión está pensada para utilizarse con la variable [!DNL Adobe Experience Platform Web SDK] extensión. Para ver información sobre la versión que debe utilizarse con AppMeasurement, consulte este vínculo.

Utilice esta referencia para obtener información sobre cómo configurar la extensión de complementos de SDK web y las opciones disponibles al utilizar esta extensión para aumentar la variable [!DNL Adobe Experience Platform Web SDK] Extensión.

## Configurar la extensión de complementos de SDK web comunes

Esta sección proporciona una referencia sobre las opciones disponibles al configurar la extensión de complementos de SDK web.

>[!IMPORTANT]
>
>La extensión de complementos de SDK web comunes está pensada para aumentar la variable [!DNL Adobe Experience Platform Web SDK] sin embargo, no es necesario que esté instalado para que la extensión funcione según lo esperado.

No se requiere ninguna configuración adicional en el nivel de extensión.

## Añadir complementos a la extensión de [!DNL Adobe Experience Platform Web SDK]

A diferencia del homólogo de AppMeasurement, no se necesita ninguna configuración para inicializar o agregar un complemento a la biblioteca fuera del uso de los elementos de datos nativos que se proporcionan. Consulte a continuación para obtener información adicional sobre cada elemento de datos.

## Elementos de datos de extensión de complementos de SDK web comunes

La extensión Common Web SDK Plugins proporciona los siguientes elementos de datos:

* [getAndPersistValue](#getAndPersistValue)
* [getGeoCoordinates](#getGeoCoordinates)
* [getNewRepeat](#getNewRepeat)
* [getPagename](#getPagename)
* [getPreviousValue](#getPreviousValue)
* [getQueryParam](#getQueryParam)
* [getTimeParting](#getTimeParting)
* [getTimeSinceLastVisit](#getTimeSInceLastVisit)
* [getValOnce](#getValOnce)
* [getVisitDuration](#getVisitDuration)
* [getVisitNum](#getVisitNum)
* [o](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### getAndPersistValue

>[!IMPORTANT]
>
>Este elemento de datos establece cookies y permite almacenar valores generados por el usuario en cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos en Adobe Experience Platform para configurar y configurar el [getAndPersistValue plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). La variable `getAndPersistValue` el elemento de datos le permite almacenar un valor en una cookie que se puede recuperar más adelante durante una visita. Cumple una función similar a la de [!UICONTROL duración del almacenamiento] en Adobe Experience Platform Launch.

La variable `getAndPersistValue` El elemento de datos proporciona los siguientes argumentos:

* **`vtp`** (obligatorio): El valor que se va a mantener de página en página.
* **`cn`** (opcional): El nombre de la cookie para almacenar el valor. Si no se establece este argumento, se llamará a la cookie `"s_gapv"`.
* **`ex`** (opcional): Número de días antes de que caduque la cookie. Si este argumento está establecido en `0` o no, la cookie caduca al final de la visita (a los 30 minutos de inactividad).

Si la variable en la variable `vtp` está configurado, el elemento de datos establece la cookie y devuelve el valor de la cookie. Si la variable en la variable `vtp` no está establecido, el elemento de datos solo devuelve el valor de la cookie.

### getGeoCoordinates

>[!IMPORTANT]
>
>Este complemento requiere acceso a la ubicación en el cliente, pero no genera una excepción si no lo consigue.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos en Adobe Experience Platform para configurar y configurar el [getGeoCoordinates plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). La variable `getGeoCoordinates` elemento de datos le permite capturar la latitud y longitud de los dispositivos de los visitantes.

La variable `getGeoCoordinates` El elemento de datos no utiliza ningún argumento. Devuelve uno de los siguientes valores:

* `"geo coordinates not available"`: Para dispositivos que no tienen datos de localización geográfica disponibles cuando se ejecuta el complemento. Este valor es habitual en la primera visita, especialmente cuando los visitantes deben consentir por primera vez que se rastree su ubicación.
* `"error retrieving geo coordinates"`: Cuando el complemento encuentra algún error al intentar recuperar la ubicación del dispositivo.
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Donde [LATITUDE]/[LONGITUDE] representan la latitud y la longitud, respectivamente.

### getNewRepeat

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getNewRepeat plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). La variable `getNewRepeat` el elemento de datos le permite determinar si un visitante del sitio es un visitante nuevo o uno habitual dentro de un número deseado de días.

La variable `getNewRepeat` el elemento de datos utiliza los siguientes argumentos:

* **`d`** (entero, opcional): el número mínimo de días entre visitas que restablece a los visitantes de nuevo como `"New"`. Si no se establece este argumento, el valor predeterminado es de 30 días.

Este elemento de datos devuelve el valor de `"New"` si la cookie configurada por el elemento de datos no existe o ha caducado. Devuelve el valor de `"Repeat"` si la cookie configurada por el elemento de datos existe y la cantidad de tiempo desde la visita actual y el tiempo establecido en la cookie es de buenos 30 minutos. Este método devuelve el mismo valor para una visita completa.

### getPageName

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getPageName plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). La variable `getPageName` el elemento de datos crea una versión fácil de leer y con formato sencillo de la dirección URL actual.

La variable `getPageName` el elemento de datos utiliza los siguientes argumentos:

* **`si`** (opcional, cadena): un ID insertado al principio de la cadena que representa el ID del sitio. Este valor puede ser un ID numérico o un nombre sencillo. Si no se establece, el valor predeterminado es el dominio actual.
* **`qv`** (opcional, cadena): una lista delimitada por comas de parámetros de cadena de consulta que, si se encuentran en la dirección URL, se agregan a la cadena
* **`hv`** (opcional, cadena): una lista delimitada por comas de parámetros encontrados en el hash de la URL que, si se encuentran en la dirección URL, se agregan a la cadena
* **`de`** (opcional, cadena): el delimitador para dividir partes individuales de la cadena. Valores predeterminados de una barra vertical (`|`).

El elemento de datos devuelve una cadena que contiene una versión de la URL con formato sencillo. Esta cadena se suele asignar a la variable `pageName`, pero también se puede utilizar en otras variables.

### getPreviousValue

>[!IMPORTANT]
>
>Este elemento de datos establece cookies y permite almacenar valores generados por el usuario en cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getPreviousValue plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). La variable `getPreviousValue` elemento de datos le permite establecer una variable en un valor establecido en una visita anterior.

La variable `getPreviousValue` el elemento de datos utiliza los siguientes argumentos:

* **`v`** (cadena, obligatorio): La variable que tiene el valor que desea pasar a la siguiente solicitud de imagen. Una variable común es `s.pageName` y se utiliza para recuperar el valor de la página anterior.
* **`c`** (cadena, opcional): El nombre de la cookie que almacena el valor.  Si no se establece este argumento, el valor predeterminado es `"s_gpv"`.

Cuando llama a este elemento de datos, devuelve el valor de cadena contenido en la cookie. A continuación, el complemento restablece la caducidad de la cookie y le asigna el valor de variable del argumento `v`. La cookie caduca tras 30 minutos de inactividad.

### getQueryParam

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getQueryParam plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). La variable `getQueryParam` el elemento de datos le permite extraer el valor de cualquier parámetro de cadena de consulta contenido en una dirección URL. Resulta útil para extraer códigos de campaña, tanto internos como externos, de las direcciones URL de las páginas de aterrizaje. También resulta útil al extraer términos de búsqueda u otros parámetros de cadena de consulta. Este elemento de datos proporciona funciones sólidas para analizar direcciones URL complejas, incluidos hashes y direcciones URL que contienen varios parámetros de cadena de consulta.

La variable `getQueryParam` el elemento de datos utiliza los siguientes argumentos:

* **`qsp`** (obligatorio): Una lista delimitada por comas de parámetros de cadena de consulta que se buscarán en la dirección URL. Sin distinción de mayúsculas y minúsculas.
* **`de`** (opcional): El delimitador que se usará si coinciden varios parámetros de cadena de consulta. El valor predeterminado es una cadena vacía.
* **`url`** (opcional): Una dirección URL, cadena o variable personalizada desde la que extraer los valores de parámetro de cadena de consulta. El valor predeterminado es `window.location`.

Llamar a este elemento de datos devuelve un valor según los argumentos anteriores y la dirección URL:

* Si no se encuentra un parámetro de cadena de consulta coincidente, el método devuelve una cadena vacía.
* Si se encuentra un parámetro de cadena de consulta coincidente, el método devuelve el valor del parámetro de cadena de consulta.
* Si se encuentra un parámetro de cadena de consulta coincidente pero el valor está vacío, el método devuelve `true`.
* Si se encuentran varios parámetros de cadena de consulta coincidentes, el método devuelve una cadena con cada valor de parámetro delimitado por la cadena en el argumento `de`.

### getTimeParting

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getTimeParting plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). La variable `getTimeParting` el elemento de datos le permite capturar los detalles del momento en que se produce cualquier actividad que se pueda medir en el sitio. Este elemento de datos es útil cuando desea desglosar métricas por cualquier división de tiempo repetible en un intervalo de fechas determinado. Por ejemplo: puede comparar las tasas de conversión entre dos días diferentes de la semana, como los domingos frente a los jueves. También puede comparar periodos del día, como las mañanas frente a las noches.

La variable `getTimeParting` el elemento de datos utiliza el siguiente argumento:

**`t`** (opcional pero recomendado, cadena): Nombre del huso horario al que convertir la hora local del visitante.  El valor predeterminado es UTC/GMT. Consulte la [lista de husos horarios de la base de datos TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) en Wikipedia para obtener una lista completa de los valores válidos.

Los valores válidos comunes incluyen:

* `"America/New_York"` para la hora del este
* `"America/Chicago"` para la hora central
* `"America/Denver"` para la hora de montaña
* `"America/Los_Angeles"` para la hora del Pacífico

Llamar a este elemento de datos devuelve una cadena que contiene lo siguiente delimitado por una barra vertical (`|`):

* El año en curso
* El mes en curso
* El día del mes
* El día de la semana
* La hora (AM/PM)

### getTimeSinceLastVisit

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getTimeSinceLastVisit plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). La variable `getTimeSinceLastVisit` El elemento de datos le permite rastrear cuánto tiempo ha tardado un visitante en regresar a su sitio después de su última visita.

La variable `getTimeSinceLastVisit` El elemento de datos no utiliza ningún argumento. Devuelve el tiempo transcurrido desde la última vez que el visitante accedió al sitio, agrupado en el siguiente formato:

* Un valor entre 30 minutos y una hora desde la última visita se establece en la referencia de medio minuto más cercana. Por ejemplo, `"30.5 minutes"`, `"53 minutes"`
* Un valor entre una hora y un día se redondea a la referencia de cuarto de hora más cercana. Por ejemplo, `"2.25 hours"`, `"7.5 hours"`
* Un valor mayor que un día se redondea a la referencia del día más próximo. Por ejemplo, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Si es la primera visita de un visitante o si el tiempo transcurrido supera los dos años, el valor se establece en `"New Visitor"`.

### getValOnce

>[!IMPORTANT]
>
>Este elemento de datos establece cookies y permite almacenar valores generados por el usuario en cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getValOnce plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). La variable `getValOnce` el elemento de datos evita que una variable se establezca en el mismo valor más de una vez.

La variable `getValOnce` el elemento de datos utiliza los siguientes argumentos:

* **`vtc`** (obligatorio, cadena): La variable para comprobar y ver si anteriormente se ha definido en un valor idéntico
* **`cn`** (opcional, cadena): El nombre de la cookie que contiene el valor que se va a comprobar. El valor predeterminado es `"s_gvo"`
* **`et`** (opcional, entero): La caducidad de la cookie en días (o minutos, según el argumento `ep`). El valor predeterminado es `0`, que caduca al final de la sesión del explorador
* **`ep`** (opcional, cadena): Establezca este argumento solo si también establece el argumento `et`. Establezca este argumento en `"m"` si desea que el argumento `et` caduque en minutos en lugar de en días. El valor predeterminado es `"d"`, que establece el argumento `et` en días.

Si el argumento `vtc` y el valor de la cookie coinciden, este método devuelve una cadena vacía. Si el argumento `vtc` y el valor de la cookie no coinciden, el método devuelve el argumento `vtc` como una cadena.

### getVisitDuration

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getVisitDuration plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). La variable `getVisitDuration` el elemento de datos rastrea la cantidad de tiempo en minutos que el visitante ha estado en el sitio hasta ese momento.

La variable `getVisitDuration` El elemento de datos no utiliza ningún argumento. Devuelve uno de los siguientes valores:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (donde `[x]` es el número de minutos transcurridos desde que el visitante accedió al sitio)

### getVisitNum

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [getVisitNum plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). La variable `getVisitNum` elemento de datos devuelve el número de visita de todos los visitantes que acceden al sitio dentro del número de días deseado.

La variable `getVisitNum` el elemento de datos utiliza los siguientes argumentos:

* **`rp`** (opcional, entero O cadena): El número de días antes de que se restablezca el contador de números de visitas.  Si no se configura de forma distinta, el valor predeterminado es `365`.
   * Cuando este argumento es `"w"`, el contador se restablece al final de la semana (este sábado a las 23:59 h)
   * Cuando este argumento es `"m"`, el contador se restablece al final del mes (el último día del mes en curso)
   * Cuando este argumento es `"y"`, el contador se restablece al final del año (31 de diciembre)
* **`erp`** (opcional, booleano): Cuando el argumento `rp` es un número, este argumento determina si se debe ampliar la caducidad del número de visita. Si se establece en `true`, las posteriores visitas al sitio restablecerán el contador de número de visitas. Si se establece en `false`, las posteriores visitas al sitio no se amplían cuando se restablece el contador de número de visitas. El valor predeterminado es `true`. Este argumento no es válido cuando el argumento `rp` es una cadena.

El número de visitas aumenta cada vez que el visitante regresa al sitio después de 30 minutos de inactividad. Llamar a este método devuelve un entero que representa el número de visita actual.

### p_fo (Page First Only)

Permite a los usuarios aprovechar la IU nativa de recopilación de datos para configurar y configurar el [complemento p_fo](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). La variable `p_fo` el elemento de datos es una utilidad que comprueba la existencia de un objeto JavaScript específico. Si el objeto no existe, el complemento crea el objeto y lo devuelve `true`. Si el objeto JavaScript ya existe en la página, devuelve `false`. Este elemento de datos es útil para ejecutar código exactamente una vez en una página.

La variable `p_fo` el elemento de datos utiliza los siguientes argumentos:

* **en** (obligatorio, cadena): Nombre del objeto JavaScript que crea el elemento de datos si el objeto aún no existe en la página.

Si el objeto aún no existe, este método devuelve `true` y crea el objeto. Si el objeto ya existe, este método devuelve `false`.
