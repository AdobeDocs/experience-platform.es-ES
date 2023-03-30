---
title: Mensajes de error de fuentes
description: Obtenga información sobre los mensajes de error que pueden encontrarse al utilizar el servicio de flujo para los orígenes.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# Fuentes de mensajes de error

Este documento proporciona un catálogo de mensajes de error, descripciones y resoluciones sugeridas para las fuentes.

## Errores genéricos

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1000-400` | Solicitud incorrecta | La solicitud no es válida. Compruebe la solicitud e inténtelo de nuevo. |
| `1001-401` | No autorizado | El usuario no tiene autorización. Póngase en contacto con el administrador para obtener acceso al recurso. |
| `1002-403` | Prohibido | Se prohíbe la operación solicitada. Compruebe la operación solicitada e inténtelo de nuevo. |
| `1003-404` | Recurso no encontrado | No se encuentra el recurso solicitado. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1004-415` | Tipo de medio no admitido | El formato de carga útil proporcionado no es compatible. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1005-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1006-408` | Tiempo de espera de solicitud | Error al procesar la solicitud. Se ha agotado el tiempo de espera de la solicitud. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1007-400` | Parámetro de encabezado no válido | Un parámetro de encabezado no válido: Se ha recibido {headerName}. Compruebe los parámetros del encabezado e inténtelo de nuevo. |
| `1008-401` |  | Token de autorización no válido | El token de autorización no tiene acceso a esta organización o la organización no existe. Asegúrese de que la organización existe o póngase en contacto con el administrador para obtener acceso. |
| `1009-403` | Falta el id de organización de IMS o está vacío | Falta el encabezado de solicitud de ID de organización o está vacío. Actualice el valor del encabezado e inténtelo de nuevo. |
| `1010-500` | Mensaje detallado no válido | El parámetro del mensaje detallado no se ha proporcionado correctamente. Compruebe el parámetro en el mensaje detallado e inténtelo de nuevo. |
| `1011-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1012-504` | Tiempo de espera de la puerta de enlace | Se ha producido un tiempo de espera de puerta de enlace. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1013-412` | Error en la condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. Compruebe e inténtelo de nuevo. |
| `1014-400` | Argumento no válido de solicitud incorrecta | No se pudo procesar la solicitud. {detailMessage} |

## Errores de marco

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1100-400` | Solicitud incorrecta | No se pudo procesar la solicitud. {detailMessage} |
| `1101-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1102-404` | Recurso no encontrado | No se encuentra el recurso solicitado. {detailMessage} |
| `1103-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1104-504` | Tiempo de espera de la puerta de enlace | Se ha producido un tiempo de espera de puerta de enlace. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1105-401` | No autorizado | El usuario no tiene autorización. {detailMessage} |
| `1106-403` | Prohibido | Se prohíbe la operación solicitada. {detailMessage} |
| `1107-412` | Error en la condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. {detailMessage} |

## Errores de cifrado

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1200-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1201-400` | Solicitud incorrecta | El flowId no puede ser nulo ni estar vacío. Proporcione un flowId válido en la solicitud e inténtelo de nuevo. |
| `1202-400` | Solicitud incorrecta | Falta publicKeyId en las transformaciones del flujo={transformations}. Proporcione publicKeyId en la solicitud e inténtelo de nuevo. |
| `1203-400` | Solicitud incorrecta | La clave de cifrado no existe con keyID={keyID} en las transformaciones del flujo={transformations}. Compruebe el keyID proporcionado e inténtelo de nuevo. |
| `1204-400` | Solicitud incorrecta | El algoritmo de cifrado proporcionado no es válido. Proporcione un algoritmo de codificación válido e inténtelo de nuevo. |
| `1205-400` | Solicitud incorrecta | Falta la frase de contraseña en la sección params de la solicitud proporcionada. Proporcione passPhrase en parámetros e inténtelo de nuevo. |

## Errores de API de REST

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1300-400` | Solicitud incorrecta | La solicitud de conexión de parche no es compatible con el conector {connectorType}. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1301-400` | Solicitud incorrecta | El parámetro authSpecType proporcionado: {authSpecType} no es compatible. Proporcione un tipo de especificación de autenticación válido e inténtelo de nuevo. |
| `1302-400` | Solicitud incorrecta | El tipo de autenticación proporcionado = {authType} no es compatible con el conector={connectorType}. Proporcione un tipo de autenticación válido para el conector dado. |
| `1303-400` | Solicitud incorrecta | No se pudo codificar la dirección URL con los parámetros de autenticación dados porque la codificación URL no es compatible con {value}. Compruebe sus parámetros de autenticación e inténtelo de nuevo. |
| `1304-400` | Solicitud incorrecta | No se proporciona el campo obligatorio {field}. Proporcione el {field} e inténtelo de nuevo. |
| `1305-400` | Solicitud incorrecta | El tipo de conector proporcionado = {connectorType} no es compatible con esta operación. |
| `1306-400` | Solicitud incorrecta | La conexión de destino no puede ser nula al validar el ID de especificación de conexión de destino. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1307-400` | Solicitud incorrecta | El ID de especificación de conexión de destino no es válido={targetConnectionSpecId}. El valor permitido es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Solicitud incorrecta | No se pudo procesar la solicitud. Mensaje de error: {msftErrorMessage} |
| `1309-400` | Solicitud incorrecta | La transformación de cifrado proporcionada no es válida porque falta {requiredParam} en los parámetros. Proporcione {requiredParam} e inténtelo de nuevo. |
| `1310-400` | Solicitud incorrecta | El publicKeyId proporcionado en los parámetros ha caducado. Proporcione un publicKeyId válido e inténtelo de nuevo. |
| `1311-400` | Solicitud incorrecta | El valor de publicKeyId proporcionado en params no es válido. Proporcione un publicKeyId válido e inténtelo de nuevo. |
| 1312-400 | Solicitud incorrecta | El valor de parámetro proporcionado {paramValue} no es una entrada válida para la propiedad={requestParam}. Proporcione un valor de parámetro válido e inténtelo de nuevo. |
| `1313-400` | Solicitud incorrecta | El atributo de ruta {attribute} no existe. Asegúrese de que el atributo existe e inténtelo de nuevo. |
| `1314-400` | Solicitud incorrecta | Se ha proporcionado una ruta compleja, pero no se permite. Asegúrese de que no se proporcione la ruta compleja y vuelva a intentarlo. |
| `1315-400` | Solicitud incorrecta | La ruta de acceso proporcionada {path} debe apuntar a una matriz de registros. Asegúrese de que la ruta de acceso proporcionada señala a la matriz de registros e inténtelo de nuevo. |
| `1316-400` | Solicitud incorrecta | Los parámetros de paginación proporcionados no deben estar vacíos. Proporcione parámetros de paginación válidos e inténtelo de nuevo. |
| `1317-400` | Solicitud incorrecta | Los parámetros de programación proporcionados están vacíos, pero no deben estar vacíos. Proporcione parámetros de programación válidos e inténtelo de nuevo. |
| `1318-400` | Solicitud incorrecta | {MensajeCombinado}. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1319-400` | Solicitud incorrecta | El {param} debe formar parte de la colección principal. Proporcione {param} en la colección principal e inténtelo de nuevo. |
| `1320-400` | Solicitud incorrecta | {idType} no puede ser nulo ni estar vacío. Proporcione {idType} válido e inténtelo de nuevo. |
| `1321-400` | Solicitud incorrecta | La longitud de {idType} debe ser una, el tamaño proporcionado es {size}. Proporcione un tamaño válido e inténtelo de nuevo. |
| `1322-400` | Solicitud incorrecta | La conexión de origen no puede ser nula para crear el esquema ref. Proporcione una conexión de origen válida e inténtelo de nuevo. |
| `1323-400` | Solicitud incorrecta | La {entity} no puede ser nula ni estar vacía en la conexión de origen: {sourceConnection}. Proporcione una {entity} válida e inténtelo de nuevo. |
| `1324-400` | Solicitud incorrecta | La conexión de destino no puede ser nula al extraer el ID del conjunto de datos. Proporcione una conexión de destino válida e inténtelo de nuevo. |
| `1325-400` | Solicitud incorrecta | El parámetro dataSetId no puede ser nulo ni estar vacío en la conexión de destino: {TargetConnection}. Proporcione un parámetro dataSetId válido e inténtelo de nuevo. |
| `1326-400` | Solicitud incorrecta | La conexión de origen no puede ser nula al recuperar el formato de origen. Proporcione una conexión de origen válida e inténtelo de nuevo. |
| `1327-400` | Solicitud incorrecta | El formato de los datos de origen suministrados={sourceFormat} en SourceConnection no es compatible. Los valores permitidos son: {valores}. Proporcione los valores permitidos e inténtelo de nuevo. |
| `1328-400` | Solicitud incorrecta | La transformación de la asignación no puede ser nula al extraer {param}. Proporcione una transformación de asignación válida e inténtelo de nuevo. |
| `1329-400` | Solicitud incorrecta | El parámetro: {param} no puede ser nulo ni estar vacío en la solicitud proporcionada. Proporcione {param} válido e inténtelo de nuevo. |
| `1330-400` | Solicitud incorrecta | No se encontraron columnas para la tabla {tableName}. Proporcione un nombre de tabla válido e inténtelo de nuevo. |
| `1331-400` | Solicitud incorrecta | El delimitador de columna no puede tener más de un carácter en SourceConnection: {sourceConnection}. Proporcione un delimitador de columna válido e inténtelo de nuevo. |
| `1332-400` | Solicitud incorrecta | La solicitud de conexión de origen con connectionSpecId: {connectionSpecId} no puede tener un baseConnectionId. Elimine baseConnectionId e inténtelo de nuevo. |
| `1333-400` | Registros malos | El flowRunAction={flowRunAction} no es compatible con el origen con especificación id={specId}. Proporcione una acción de ejecución de flujo válida e inténtelo de nuevo. |
| `1334-400` | Solicitud incorrecta | El parámetro de consulta : {param} no puede estar vacío. Proporcione {param} válido e inténtelo de nuevo. |
| `1335-400` | Solicitud incorrecta | Error al serializar los parámetros de filtro para explorarlos. Compruebe su solicitud de parámetro de filtro e inténtelo de nuevo. |
| `1336-400` | Solicitud incorrecta | Explorar conexión no es compatible con el ID de especificación de conexión: {connectionSpecId}. Proporcione un id de especificación de conexión compatible e inténtelo de nuevo. |
| `1337-400` | Solicitud incorrecta | {QueryParam} no puede estar vacío para objectType={objectType}. Proporcione {QueryParam} válido e inténtelo de nuevo. |
| `1338-400` | Solicitud incorrecta | El ID de conexión {connectionType} no puede ser nulo en flowRequest. Proporcione un ID de conexión {connectionType} válido en flowRequest. |
| `1339-400` | Solicitud incorrecta | El formato de la organización={imsOrg} proporcionado en la solicitud no es válido. Proporcione un ID de organización válido e inténtelo de nuevo. |
| `1340-400` | Solicitud incorrecta | Error al analizar {time}. Compruebe el formato de hora proporcionado en la solicitud e inténtelo de nuevo. |
| `1341-400` | Solicitud incorrecta | El archivo Json ODI proporcionado está vacío. Proporcione un Json de ODI válido e inténtelo de nuevo. |
| `1342-400` | Solicitud incorrecta | Al segmento &quot;dls:folder&quot; de &quot;odi.json&quot; le faltan definiciones. Proporcione las definiciones adecuadas en &quot;odi.json&quot; y vuelva a intentarlo. |
| `1343-400` | Solicitud incorrecta | Faltan definiciones para los segmentos &quot;dls:entityReferences&quot; y &quot;dls:particiónSpec&quot; en &quot;odi.json&quot;. Proporcione las definiciones adecuadas en &quot;odi.json&quot; y vuelva a intentarlo. |
| `1344-400` | Solicitud incorrecta | La definición de &#39;dls:particiónSpec&#39; en &#39;odi.json&#39; no es válida porque se encontraron más de una particiónSpecs. Proporcione las definiciones adecuadas en &quot;odi.json&quot; y vuelva a intentarlo. |
| `1345-400` | Solicitud incorrecta | Faltan definiciones en 1 o más segmentos de las rutas: &#39;dls:particiónSpec/dls:fileFormat&#39;, &#39;dls:particiónSpec/dls:particiónTemplate&#39;,&#39;dls:particiónSpec/dls:fileFormat/@type&#39;, &#39;dls:particiónSpec/dls:fileFormat/dls:csvDelimiters&#39; en &#39;odi.json&#39;. Proporcione las definiciones adecuadas en &quot;odi.json&quot; y vuelva a intentarlo. |
| `1346-400` | Solicitud incorrecta | La definición &#39;@type&#39; proporcionada en &#39;dls:fileFormat&#39; en &#39;odi.json&#39; no es válida. Proporcione las definiciones adecuadas en &quot;odi.json&quot; y vuelva a intentarlo. |
| `1347-400` | Solicitud incorrecta | La definición de dls:csvDelimiters en &quot;odi.json&quot; no es compatible. Los delimitadores csvDelimiters admitidos son: [&#39;,&#39;]. Proporcione las definiciones adecuadas en &quot;odi.json&quot; y vuelva a intentarlo. |
| `1348-400` | Solicitud incorrecta | Error al deserializar &quot;dls:entityReferences&quot;. Compruebe si los datos tienen un formato válido e inténtelo de nuevo. |
| `1349-400` | Solicitud incorrecta | Los parámetros de filtro proporcionados no son válidos. Proporcione parámetros de filtro válidos e inténtelo de nuevo. |
| `1350-400` | Solicitud incorrecta | No se proporcionó ningún operador para filtrar en el origen. Proporcione una solicitud de filtro válida con el operador adecuado e inténtelo de nuevo. |
| `1351-400` | Solicitud incorrecta | El operador proporcionado {operator} no es compatible con el filtro de origen de este conector. Proporcione un operador válido e inténtelo de nuevo. |
| `1352-400` | Solicitud incorrecta | El operador proporcionado {operator} no se puede asignar a ningún operador nativo admitido para {ql}. Proporcione un operador válido e inténtelo de nuevo. |
| `1353-400` | Solicitud incorrecta | El filtro en el origen aún no es compatible con el conector {connectorType}. Compruebe los conectores compatibles en la documentación: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Solicitud incorrecta | El idioma de consulta {ql} aún no es compatible con el filtro en el origen. Proporcione un idioma de consulta válido e inténtelo de nuevo. |
| `1355-400` | Solicitud incorrecta | El tipo de filtro proporcionado no es válido. El tipo de filtro admitido es: PQL. Proporcione un tipo de filtro válido e inténtelo de nuevo. |
| `1356-400` | Solicitud incorrecta | El formato de filtro proporcionado no es válido. El formato de filtro admitido es : pql/json. Proporcione un formato de filtro válido e inténtelo de nuevo. |
| `1357-400` | Solicitud incorrecta | El filtro proporcionado no es válido. El valor debe proporcionarse con filtros detallados. Proporcione un filtro válido e inténtelo de nuevo. |
| `1358-400` | Solicitud incorrecta | El parámetro proporcionado &#39;objectType&#39; no es válido. Proporcione un objectType válido e inténtelo de nuevo. |
| `1359-400` | Solicitud incorrecta | Falta el parámetro {param} en la solicitud. Proporcione un {param} válido e inténtelo de nuevo. |
| `1360-400` | Solicitud incorrecta | La hora de inicio no se puede establecer en el pasado. Proporcione una hora de inicio válida e inténtelo de nuevo. |
| `1361-400` | Solicitud incorrecta | No se permite el intervalo con una ingesta única. Elimine el intervalo o cambie la frecuencia e inténtelo de nuevo. |
| `1362-400` | Solicitud incorrecta | El intervalo no puede ser menor que {minInterval}. Proporcione un valor de intervalo válido e inténtelo de nuevo. |
| `1363-400` | Solicitud incorrecta | No se permite el intervalo {intervalo} con frecuencia: {frecuencia}. Proporcione un valor de intervalo válido e inténtelo de nuevo. |
| `1364-400` | Solicitud incorrecta | No se permite el indicador de relleno cuando la frecuencia se establece en uno. Quite el indicador de relleno cuando la frecuencia esté establecida en una vez e inténtelo de nuevo. |
| `1365-400` | Solicitud incorrecta | La ruta de acceso {path} proporcionada en ops no es válida. Proporcione una ruta de acceso válida {path} e inténtelo de nuevo. |
| `1366-400` | Solicitud incorrecta | Ha pasado el tiempo de inicio y ya no se permite la operación de actualización. |
| `1367-400` | Solicitud incorrecta | La columna delta es necesaria en la transformación de copia al crear un conector CRM. Proporcione una columna delta e inténtelo de nuevo. |
| `1368-400` | Solicitud incorrecta | No se permite el modo en la solicitud de flujo. Compruebe su solicitud e inténtelo de nuevo. |
| `1369-400` | Solicitud incorrecta | La columna delta de la transformación de copia no está permitida cuando la frecuencia se establece en una sola vez. Elimine la columna delta e inténtelo de nuevo. |
| `1370-400` | Solicitud incorrecta | No se pudieron recuperar las columnas de origen para su ingesta porque falta la transformación de la asignación. Añada la transformación de la asignación e inténtelo de nuevo. |
| `1371-400` | Solicitud incorrecta | La detección de propiedades de archivo no es compatible con el conector {connectorType}. Proporcione las propiedades del archivo manualmente. |
| `1372-400` | Solicitud incorrecta | No se permite la operación actual. No se permite explorar mediante especificación de conexión para el ID de especificación de conexión={connectionSpecId}. |
| `1373-400` | Solicitud incorrecta | Falta flowSpecType en la solicitud. Proporcione un flowSpecType válido e inténtelo de nuevo. |
| `1374-400` | Solicitud incorrecta | Los parámetros de consulta proporcionados no son válidos. No puede tener el indicador determineProperties y las propiedades definidas por el usuario en la misma solicitud. Corrija la solicitud e inténtelo de nuevo. |
| `1375-400` | Solicitud incorrecta | Error en la detección de las propiedades del archivo. Escriba las propiedades manualmente. |
| `1376-400` | Solicitud incorrecta | La detección de propiedades de archivo no es compatible con el id. de especificación de conexión={connectionSpecId}. Proporcione las propiedades del archivo manualmente. |
| `1377-400` | Solicitud incorrecta | El parámetro de valor proporcionado es nulo y no se puede comparar con el operador {operator}. Proporcione un parámetro de valor válido e inténtelo de nuevo. |
| `1378-400` | Solicitud incorrecta | Error al validar la columna de entrada {column} para el filtro en el origen. El nombre de la columna debe ser una columna válida de la tabla. Proporcione un nombre de columna válido e inténtelo de nuevo. |
| `1379-400` | Solicitud incorrecta | Error al validar la entrada {value} para el filtro en el origen. La columna DataType en el origen es {columnDataType} y el valor DataType [Cadena] no coincide. Proporcione un {valor} válido e inténtelo de nuevo. |
| `1380-400` | Solicitud incorrecta | No se pudo crear la ejecución del flujo. Mensaje de error: {message} |
| `1381-400` | Solicitud incorrecta | WindowEndTime={endTime} no puede ser anterior a Window StartTime={startTime}. Proporcione una hora de finalización válida e inténtelo de nuevo. |
| `1382-400` | Solicitud incorrecta | La columna delta debe coincidir con el valor presente en las transformaciones Copy del flujo. Proporcione una columna delta válida e inténtelo de nuevo. |
| `1383-400` | Solicitud incorrecta | Falta la columna delta en los parámetros recibidos para crear una ejecución de flujo. Proporcione la columna delta en params y vuelva a intentarlo. |
| `1384-400` | Solicitud incorrecta | Los parámetros={params} proporcionados para crear la ejecución de flujo no son válidos o están vacíos. Proporcione parámetros válidos e inténtelo de nuevo. |
| `1385-400` | Solicitud incorrecta | El conectorType={connectorType} proporcionado no es compatible para crear ejecuciones de flujo. Proporcione un conectorType válido e inténtelo de nuevo. |
| `1386-400` | Solicitud incorrecta | El flowId={flowId} con scheduleParams frequency={frequency} no es compatible para la creación de ejecuciones de flujo. Proporcione una frecuencia válida e inténtelo de nuevo. |
| `1387-400` | Solicitud incorrecta | El flowRunId={flowRunId} está en un estado no válido={state} para la reactivación. Inténtelo de nuevo más tarde y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1388-400` | Solicitud incorrecta | El flujo={flow} está en estado={state} y no se puede volver a activar. El flujo debe estar en estado habilitado para volver a activarse. |
| `1389-400` | Solicitud incorrecta | Error al analizar la cadena codificada base64 proporcionada. Proporcione una cadena de filtro codificada válida e inténtelo de nuevo. |
| `1390-400` | Solicitud incorrecta | El operador &quot;not&quot; no puede tener más de una comparación. Proporcione un número válido de comparaciones e inténtelo de nuevo. |
| `1391-400` | Solicitud incorrecta | No se pudo analizar SchemaMetaData en sourceConnection para Id={sourceConnectionId}. Compruebe schemaMetaData en la solicitud e inténtelo de nuevo. |
| `1392-400` | Solicitud incorrecta | No se pudieron analizar las transformaciones en la solicitud de flujo para flowId={flowId}. Compruebe las transformaciones de su solicitud e inténtelo de nuevo. |
| `1393-400` | Solicitud incorrecta | El parámetro proporcionado {parameter} es nulo o está vacío. Proporcione un {parámetro} válido e inténtelo de nuevo. |
| `1394-400` | Solicitud incorrecta | El valor mínimo de un parámetro {parameter} es uno. Proporcione un {parámetro} válido e inténtelo de nuevo. |
| `1395-400` | Solicitud incorrecta | La conexión de origen encontrada en el flujo es nula o está vacía. Proporcione una conexión de origen válida en el flujo e inténtelo de nuevo. |
| `1396-400` | Solicitud incorrecta | No se encontró un formato coincidente. Proporcione un formato coincidente e inténtelo de nuevo. |
| `1397-400` | Solicitud incorrecta | La frecuencia proporcionada : {frecuencia} no es válida. Proporcione una frecuencia válida e inténtelo de nuevo. |
| `1398-400` | Solicitud incorrecta | La operación proporcionada : {action} no es compatible. Compruebe la operación proporcionada e inténtelo de nuevo. |
| `1399-400` | Solicitud incorrecta | No se encontró un requestFileType válido. Proporcione un requestFileType válido e inténtelo de nuevo. |
| `1400-400` | Solicitud incorrecta | El parámetro proporcionado &#39;templateType&#39; no es válido. Proporcione un tipo de plantilla válido e inténtelo de nuevo. |
| `1401-400` | Solicitud incorrecta | No se admite la acción de ejecución de flujo proporcionada={flowRunAction}. Proporcione una acción de ejecución de flujo válida e inténtelo de nuevo. |
| `1402-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1403-400` | Solicitud incorrecta | La hora de inicio ha pasado y ya no puede cambiar la frecuencia a una vez. |
| `1404-400` | Solicitud incorrecta | La hora de inicio ha pasado y ya no puede actualizar el relleno. |

## Excepciones de servicio de flujo (1600-1699)

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1600-400` | Solicitud incorrecta | No se pudo procesar la solicitud. {detailMessage} |
| `1601-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1602-404` | Recurso no encontrado | No se encuentra el recurso solicitado. {detailMessage} |
| `1603-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo. Póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1604-504` | Tiempo de espera de la puerta de enlace | Se ha producido un tiempo de espera de puerta de enlace. Inténtelo de nuevo. Póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1605-401` | No autorizado | El usuario no tiene autorización. {detailMessage} |
| `1606-403` | Prohibido | Se prohíbe la operación solicitada. {detailMessage} |
| `1607-412` | Error en la condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. {detailMessage} |

## Errores en la zona de aterrizaje de datos

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1700-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1701-400` | Solicitud incorrecta | La zona de aterrizaje proporcionada está inactiva. Active la zona de aterrizaje e inténtelo de nuevo. |
| `1702-400` | Solicitud incorrecta | No se permite el tipo SAS={sasType} proporcionado para la zona de aterrizaje. Proporcione un SAS válido e inténtelo de nuevo. |
| `1703-400` | Solicitud incorrecta | No se permite la actualización de Credenciales. |
| `1704-400` | Solicitud incorrecta | Las claves devueltas para storageAccountName={accountName} en subscriptionId={subscriptionId} y resourceGroupName={resourceGroupName} tienen un formato incorrecto. Compruebe su solicitud e inténtelo de nuevo. Póngase en contacto con el servicio de asistencia técnica si el problema persiste. |
| `1705-400` | Solicitud incorrecta | No se admite la acción de zona de aterrizaje de datos proporcionada. Proporcione una acción válida e inténtelo de nuevo. |
| `1706-400` | Solicitud incorrecta | La configuración de activaciones permitidas no está configurada correctamente para landing zone={landingZoneType}. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1707-400` | Solicitud incorrecta | No se pudo iniciar el servicio porque la configuración de la zona de aterrizaje no puede ser nula ni estar vacía. Asegúrese de que la configuración de la zona de aterrizaje no sea nula e inténtelo de nuevo. |
| `1708-400` | Solicitud incorrecta | La configuración del contenedor no puede ser nula en landingZoneType={landingZoneType}. Asegúrese de que la configuración del contenedor no sea nula e inténtelo de nuevo. |
| `1709-400` | Solicitud incorrecta | Los detalles de SAS no pueden ser nulos para {tokenConfig} en landingZoneType={landingZoneType}. Proporcione un SAS válido en la configuración e inténtelo de nuevo. |
| `1710-400` | Solicitud incorrecta | La zona de aterrizaje del tipo proporcionada: {landingZoneUseCase} no es compatible. Proporcione un tipo de zona de aterrizaje válido e inténtelo de nuevo. |
| `1711-400` | Solicitud incorrecta | No se encontraron los detalles de SAS para la zona de aterrizaje de datos proporcionada del tipo : {landingZoneUseCase}. Compruebe si se proporcionan detalles SAS para el tipo de zona de aterrizaje proporcionado. |
| `1712-400` | Solicitud incorrecta | La acción de zona de aterrizaje proporcionada : {actionType} no está permitido. Proporcione una acción de zona de aterrizaje de datos válida e inténtelo de nuevo. |
| `1713-400` | Solicitud incorrecta | No se permite {OperationType} para el {tokenType} proporcionado. Compruebe su solicitud e inténtelo de nuevo. |
| `1714-400` | Solicitud incorrecta | No se permite que clientId={clientId} realice esta operación. Compruebe su solicitud con permisos e inténtelo de nuevo. |