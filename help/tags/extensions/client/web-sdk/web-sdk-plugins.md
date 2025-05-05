---
title: Información general sobre la extensión Common Web SDK Plugins
description: Obtenga información acerca de la extensión de etiquetas Common Web SDK Plugins en Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# Información general sobre la extensión Common Web SDK Plugins

>[!IMPORTANT]
>
>La extensión está pensada para utilizarse con la extensión SDK para web de Adobe Experience Platform. Para ver información sobre la versión que se va a usar con AppMeasurement, consulte la descripción general de la [extensión de complementos de Analytics comunes](../plugins/overview.md).

Este documento explica cómo configurar la extensión de etiquetas Web SDK Plugins y cómo utilizarla para aumentar la [extensión de SDK web de Adobe Experience Platform](../web-sdk/overview.md).

## Configurar la extensión de complementos de SDK web comunes

Esta sección proporciona una referencia sobre las opciones disponibles al configurar la extensión de complementos del SDK web.

>[!IMPORTANT]
>
>La extensión de complementos de SDK web comunes está diseñada para aumentar la extensión de SDK web de Adobe Experience Platform, pero no es necesario tenerla instalada para que la extensión funcione según lo esperado.

## Añadir complementos a la extensión SDK para web de Adobe Experience Platform

No es necesario realizar ninguna configuración para inicializar o agregar un complemento a la biblioteca fuera de mediante los siguientes elementos de datos nativos que proporciona la extensión de complementos de SDK web comunes:

* [getAndPersistValue](#getAndPersistValue)
* [getGeoCoordinates](#getGeoCoordinates)
* [getNewRepeat](#getNewRepeat)
* [&quot;getPagename&quot;](#getPagename)
* [&quot;getPreviousValue&quot;](#getPreviousValue)
* [getQueryParam](#getQueryParam)
* [getTimeParting](#getTimeParting)
* [&quot;getTimeSinceLastVisit&quot;](#getTimeSInceLastVisit)
* [getValOnce](#getValOnce)
* [getVisitDuration](#getVisitDuration)
* [getVisitNum](#getVisitNum)
* [&quot;pFo&quot;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies y permite almacenar valores generados por el usuario en cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getAndPersistValue` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html?lang=es). El elemento de datos `getAndPersistValue` almacena un valor en una cookie que se puede recuperar posteriormente durante una visita.

El elemento de datos `getAndPersistValue` proporciona los siguientes argumentos:

* `vtp` (obligatorio): El valor que se va a mantener de página en página.
* `cn` (opcional): el nombre de la cookie para almacenar el valor. Si no se establece este argumento, la cookie se llamará `"s_gapv"`
* `ex` (opcional): número de días antes de que caduque la cookie. Si este argumento es `0` o no está establecido, la cookie caduca al final de la visita (a los 30 minutos de inactividad).

Si se establece la variable en el argumento `vtp`, el elemento de datos establece la cookie y devuelve el valor de la cookie. Si no se establece la variable en el argumento `vtp`, el elemento de datos solo devolverá el valor de la cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Este complemento requiere acceso a la ubicación en el cliente, pero no genera una excepción si no la obtiene.

Permite configurar el complemento [`getGeoCoordinates` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html?lang=es). El elemento de datos `getGeoCoordinates` captura la latitud y longitud de los dispositivos de los visitantes.

El elemento de datos `getGeoCoordinates` no utiliza ningún argumento. Devuelve uno de los siguientes valores:

* `"geo coordinates not available"`: para dispositivos que no tienen datos de ubicación geográfica disponibles en el momento en que se ejecuta el complemento. Este valor es común en la primera visita, especialmente cuando los visitantes deben consentir por primera vez que se rastree su ubicación.
* `"error retrieving geo coordinates"`: cuando el complemento encuentra algún error al intentar recuperar la ubicación del dispositivo
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: donde [LATITUDE]/[LONGITUDE] son la latitud y longitud, respectivamente

### `getNewRepeat`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getNewRepeat` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html?lang=es). El elemento de datos `getNewRepeat` determina si un visitante del sitio accede por primera vez o si repite dentro de un número determinado de días.

El elemento de datos `getNewRepeat` utiliza los siguientes argumentos:

* `d` (entero, opcional): el número mínimo de días entre visitas que restablece a los visitantes a `"New"`. Si no se establece este argumento, el valor predeterminado es de 30 días.

Este elemento de datos devuelve el valor de `"New"` si la cookie configurada por el elemento de datos no existe o ha caducado. Devuelve el valor de `"Repeat"` si la cookie configurada por el elemento de datos existe y el tiempo desde la visita actual y el tiempo establecido en la cookie supera los 30 minutos. Este método devuelve el mismo valor para una visita completa.

### `getPageName`

Permite configurar el complemento [`getPageName` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html?lang=es). El elemento de datos `getPageName` crea una versión fácil de leer y con formato sencillo de la dirección URL actual.

El elemento de datos `getPageName` utiliza los siguientes argumentos:

* `si` (opcional, cadena): ID insertado al principio de la cadena que representa el ID del sitio. Este valor puede ser un ID numérico o un nombre descriptivo. Si no se establece, el valor predeterminado es el dominio actual.
* `qv` (opcional, cadena): una lista delimitada por comas de parámetros de cadena de consulta que, si se encuentran en la dirección URL, se agregan a la cadena
* `hv` (opcional, cadena): una lista delimitada por comas de parámetros encontrados en el hash de la dirección URL que, si se encuentran en la dirección URL, se agregan a la cadena
* `de` (opcional, cadena): el delimitador para dividir partes individuales de la cadena. El valor predeterminado es una barra vertical (`|`).

El elemento de datos devuelve una cadena que contiene una versión de la dirección URL con formato sencillo. Esta cadena se suele asignar a la variable `pageName`, pero también se puede utilizar en otras variables.

### `getPreviousValue`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies y permite almacenar valores generados por el usuario en cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getPreviousValue` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html?lang=es). El elemento de datos `getPreviousValue` establece una variable en un valor establecido en una visita anterior.

El elemento de datos `getPreviousValue` utiliza los siguientes argumentos:

* `v` (cadena, obligatorio): La variable que tiene el valor que desea pasar a la siguiente solicitud de imagen. Una variable común utilizada es `s.pageName` para recuperar el valor de la página anterior.
* `c` (cadena, opcional): El nombre de la cookie que almacena el valor.  Si no se establece este argumento, el valor predeterminado es `"s_gpv"`.

Al llamar a este elemento de datos, devuelve el valor de cadena contenido en la cookie. A continuación, el complemento restablece la caducidad de la cookie y le asigna el valor de variable del argumento `v`. La cookie caduca tras 30 minutos de inactividad.

### `getQueryParam`

Permite configurar el complemento [`getQueryParam` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html?lang=es). El elemento de datos `getQueryParam` extrae el valor de cualquier parámetro de cadena de consulta contenido en una dirección URL. Resulta útil para extraer códigos de campaña, tanto internos como externos, de las direcciones URL de las páginas de aterrizaje. También resulta útil al extraer términos de búsqueda u otros parámetros de cadena de consulta. Este elemento de datos proporciona funciones sólidas para analizar direcciones URL complejas, incluidos hashes y direcciones URL que contienen varios parámetros de cadena de consulta.

El elemento de datos `getQueryParam` utiliza los siguientes argumentos:

* `qsp` (obligatorio): Una lista delimitada por comas de parámetros de cadena de consulta que se buscarán en la dirección URL. No distingue entre mayúsculas y minúsculas.
* `de` (opcional): El delimitador que se usará si coinciden varios parámetros de cadena de consulta. El valor predeterminado es una cadena vacía.
* `url` (opcional): una dirección URL, cadena o variable personalizada desde la que extraer los valores de parámetro de cadena de consulta. El valor predeterminado es `window.location`.

Llamar a este elemento de datos devuelve un valor según los argumentos anteriores y la dirección URL:

* Si no se encuentra un parámetro de cadena de consulta coincidente, el método devuelve una cadena vacía.
* Si se encuentra un parámetro de cadena de consulta coincidente, el método devuelve el valor del parámetro de cadena de consulta.
* Si se encuentra un parámetro de cadena de consulta coincidente pero el valor está vacío, el método devuelve `true`.
* Si se encuentran varios parámetros de cadena de consulta coincidentes, el método devuelve una cadena con el valor de cada parámetro delimitado por la cadena en el argumento `de`.

### `getTimeParting`

Permite configurar el complemento [`getTimeParting` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html?lang=es). El elemento de datos `getTimeParting` captura los detalles del momento en que se produce cualquier actividad que se pueda medir en el sitio. Este elemento de datos es útil cuando desea desglosar métricas para cualquier división de tiempo repetible en un intervalo de fechas determinado. Por ejemplo: puede comparar las tasas de conversión entre dos días diferentes de la semana, como los domingos frente a los jueves. También puede comparar periodos del día, como las mañanas frente a las noches.

El elemento de datos `getTimeParting` utiliza el argumento siguiente:

`t` (opcional pero recomendado, cadena): Nombre del huso horario al que convertir la hora local del visitante.  El valor predeterminado es UTC/GMT. Consulte la [Lista de husos horarios de la base de datos TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) en Wikipedia para obtener una lista completa de los valores válidos.

Los valores válidos comunes incluyen:

* `"America/New_York"` para la hora del este
* `"America/Chicago"` para la hora central
* `"America/Denver"` para la hora de la montaña
* `"America/Los_Angeles"` para la hora del Pacífico

Llamar a este elemento de datos devuelve una cadena que contiene lo siguiente, delimitado por una barra vertical (`|`):

* El año en curso
* El mes actual
* El día del mes
* El día de la semana
* La hora actual (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getTimeSinceLastVisit` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html?lang=es). El elemento de datos `getTimeSinceLastVisit` realiza el seguimiento del tiempo que un visitante ha tardado en regresar al sitio después de su última visita.

El elemento de datos `getTimeSinceLastVisit` no utiliza ningún argumento. Devuelve el tiempo transcurrido desde la última vez que el visitante accedió al sitio, agrupado en el siguiente formato:

* Un valor entre 30 minutos y una hora desde la última visita se establece en la referencia de medio minuto más cercana. Por ejemplo, `"30.5 minutes"`, `"53 minutes"`
* Un valor entre una hora y un día se redondea a la referencia de cuarto de hora más cercana. Por ejemplo, `"2.25 hours"`, `"7.5 hours"`
* Un valor mayor que un día se redondea a la referencia del día más próximo. Por ejemplo, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Si un visitante no ha realizado ninguna visita anteriormente o si el tiempo transcurrido supera los dos años, el valor se establece en `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies y permite almacenar valores generados por el usuario en cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getValOnce` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html?lang=es). El elemento de datos `getValOnce` evita que una variable se establezca en el mismo valor más de una vez.

El elemento de datos `getValOnce` utiliza los siguientes argumentos:

* `vtc` (obligatorio, cadena): La variable para comprobar y ver si anteriormente se ha establecido en un valor idéntico
* `cn` (opcional, cadena): El nombre de la cookie que contiene el valor que se va a comprobar. Valores predeterminados de `"s_gvo"`
* `et` (opcional, entero): La caducidad de la cookie en días (o minutos, según el argumento `ep`). El valor predeterminado es `0`, que caduca al final de la sesión del explorador
* `ep` (opcional, cadena): Establezca este argumento solo si también establece el argumento `et`. Establezca este argumento en `"m"` si desea que el argumento `et` caduque en minutos en lugar de en días. El valor predeterminado es `"d"`, que establece el argumento `et` en días.

Si el argumento `vtc` y el valor de la cookie coinciden, este método devuelve una cadena vacía. Si el argumento `vtc` y el valor de la cookie no coinciden, el método devuelve el argumento `vtc` como una cadena.

### `getVisitDuration`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getVisitDuration` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html?lang=es). El elemento de datos `getVisitDuration` realiza el seguimiento del tiempo en minutos que el visitante ha pasado en el sitio hasta ese momento.

El elemento de datos `getVisitDuration` no utiliza ningún argumento. Devuelve uno de los siguientes valores:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (donde `[x]` es el número de minutos transcurridos desde que el visitante accedió al sitio)

### `getVisitNum`

>[!IMPORTANT]
>
>Este elemento de datos establece cookies. Consulte la documentación específica del complemento para obtener más información.

Permite configurar el complemento [`getVisitNum` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html?lang=es). El elemento de datos `getVisitNum` devuelve el número de la visita de todos los visitantes que acceden al sitio dentro del número de días deseado.

El elemento de datos `getVisitNum` utiliza los siguientes argumentos:

* `rp` (opcional, entero O cadena): el número de días antes de que se restablezca el contador de números de visitas.  Si no se establece, el valor predeterminado es `365`.
   * Cuando este argumento es `"w"`, el contador se restablece al final de la semana (este sábado a las 23:59 h)
   * Cuando este argumento es `"m"`, el contador se restablece al final del mes (el último día del mes en curso)
   * Cuando este argumento es `"y"`, el contador se restablece al final del año (31 de diciembre)
* `erp` (opcional, booleano): Cuando el argumento `rp` es un número, este argumento determina si se debe ampliar la caducidad del número de visita. Si se establece en `true`, las posteriores visitas al sitio restablecerán el contador de número de visitas. Si se establece en `false`, las posteriores visitas al sitio no se amplían cuando se restablece el contador de número de visitas. El valor predeterminado es `true`. Este argumento no es válido cuando el argumento `rp` es una cadena.

El número de visitas aumenta cada vez que el visitante regresa al sitio después de 30 minutos de inactividad. Llamar a este método devuelve un entero que representa el número de visita actual del visitante.

### `p_fo` (Page First Only)

Permite configurar el complemento [`p_fo` de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html?lang=es). El elemento de datos `p_fo` es una utilidad que comprueba la existencia de un objeto JavaScript específico. Si el objeto no existe, el complemento crea el objeto y devuelve `true`. Si el objeto JavaScript ya existe en la página, devuelve `false`. Este elemento de datos es útil para ejecutar código exactamente una vez en una página.

El elemento de datos `p_fo` utiliza los siguientes argumentos:

* `on` (obligatorio, cadena): El nombre del objeto JavaScript que crea el elemento de datos si el objeto aún no existe en la página.

Si el objeto aún no existe, este método devuelve `true` y crea el objeto. Si el objeto ya existe, este método devuelve `false`.
