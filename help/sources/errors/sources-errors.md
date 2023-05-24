---
title: Mensajes de error de origen
description: Obtenga información acerca de los mensajes de error que pueden surgir al utilizar Flow Service para las fuentes.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# Mensajes de error de fuentes

Este documento proporciona un catálogo de mensajes de error, descripciones y resoluciones sugeridas para las fuentes.

## Errores genéricos

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1000-400` | Solicitud incorrecta | Solicitud no válida. Compruebe la solicitud e inténtelo de nuevo. |
| `1001-401` | No autorizado | El usuario no está autorizado. Póngase en contacto con el administrador para obtener acceso al recurso. |
| `1002-403` | Prohibido | No se permite la operación solicitada. Compruebe la operación solicitada e inténtelo de nuevo. |
| `1003-404` | Recurso no encontrado | No se ha encontrado el recurso solicitado. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1004-415` | Tipo de medio no compatible | El formato de carga útil proporcionado no es compatible. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1005-500` | Error interno | Se ha producido un error interno. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1006-408` | Tiempo de espera de solicitud | Se ha producido un error al procesar la solicitud. Se ha agotado el tiempo de espera de la solicitud. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1007-400` | Parámetro de encabezado no válido | Se ha recibido un parámetro de encabezado no válido: {headerName}. Compruebe los parámetros del encabezado e inténtelo de nuevo. |
| `1008-401` |  | Token de autorización no válido | El token de autorización no tiene acceso a esta organización o la organización no existe. Asegúrese de que la organización existe o póngase en contacto con el administrador para obtener acceso. |
| `1009-403` | Falta el ID de organización de IMS o está vacío | Falta el encabezado de solicitud del ID de organización o está vacío. Actualice el valor del encabezado e inténtelo de nuevo. |
| `1010-500` | Mensaje detallado no válido | El parámetro del mensaje detallado no se ha proporcionado correctamente. Compruebe el parámetro en el mensaje detallado e inténtelo de nuevo. |
| `1011-503` | Servicio no disponible | El servicio no está disponible temporalmente. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1012-504` | Tiempo de espera de puerta | Se agotó el tiempo de espera de puerta de enlace. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1013-412` | Error de condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. Compruebe e inténtelo de nuevo. |
| `1014-400` | Argumento no válido de solicitud incorrecto | No se ha podido procesar la solicitud. {detailedMessage} |

## Errores de marco

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1100-400` | Solicitud incorrecta | No se ha podido procesar la solicitud. {detailedMessage} |
| `1101-500` | Error interno | Se ha producido un error interno. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1102-404` | Recurso no encontrado | No se ha encontrado el recurso solicitado. {detailedMessage} |
| `1103-503` | Servicio no disponible | El servicio no está disponible temporalmente. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1104-504` | Tiempo de espera de puerta | Se agotó el tiempo de espera de puerta de enlace. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1105-401` | No autorizado | El usuario no está autorizado. {detailedMessage} |
| `1106-403` | Prohibido | No se permite la operación solicitada. {detailedMessage} |
| `1107-412` | Error de condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. {detailedMessage} |

## Errores de cifrado

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1200-500` | Error interno | Se ha producido un error interno. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1201-400` | Solicitud incorrecta | flowId no puede ser nulo ni estar vacío. Proporcione un flowId válido en la solicitud e inténtelo de nuevo. |
| `1202-400` | Solicitud incorrecta | Falta publicKeyId en las transformaciones del flujo={transformations}. Proporcione publicKeyId en la solicitud e inténtelo de nuevo. |
| `1203-400` | Solicitud incorrecta | La clave de cifrado no existe con respecto a keyID={keyID} en las transformaciones={transformations} del flujo. Compruebe el KeyID proporcionado e inténtelo de nuevo. |
| `1204-400` | Solicitud incorrecta | El algoritmo de cifrado proporcionado no es válido. Proporcione un algoritmo de cifrado válido e inténtelo de nuevo. |
| `1205-400` | Solicitud incorrecta | Falta la frase de contraseña en la sección de parámetros de la solicitud proporcionada. Proporcione passPhrase en parámetros e inténtelo de nuevo. |

## Errores de API de REST

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1300-400` | Solicitud incorrecta | La solicitud de conexión de parche no es compatible con el conector {connectorType}. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1301-400` | Solicitud incorrecta | El parámetro authSpecType proporcionado: {authSpecType} no es compatible. Proporcione un tipo de especificación de autenticación válido e inténtelo de nuevo. |
| `1302-400` | Solicitud incorrecta | El tipo de autenticación proporcionado = {authType} no es compatible con connector={connectorType}. Proporcione un tipo de autenticación válido para el conector determinado. |
| `1303-400` | Solicitud incorrecta | La URL no se ha podido codificar con los parámetros de autenticación proporcionados porque la codificación de la URL no es compatible con {value}. Compruebe los parámetros de autenticación e inténtelo de nuevo. |
| `1304-400` | Solicitud incorrecta | No se proporciona el campo obligatorio {field}. Proporcione el {field} e inténtelo de nuevo. |
| `1305-400` | Solicitud incorrecta | El tipo de conector proporcionado = {connectorType} no es compatible con esta operación. |
| `1306-400` | Solicitud incorrecta | La conexión de destino no puede ser nula al validar el ID de especificación de conexión de destino. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1307-400` | Solicitud incorrecta | La ID de especificación de conexión de destino no es válida={targetConnectionSpecId}. El valor permitido es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Solicitud incorrecta | No se ha podido procesar la solicitud. Mensaje de error: {msftErrorMessage} |
| `1309-400` | Solicitud incorrecta | La transformación de cifrado proporcionada no es válida porque falta {requiredParam} en los parámetros. Proporcione {requiredParam} e inténtelo de nuevo. |
| `1310-400` | Solicitud incorrecta | El publicKeyId proporcionado en los parámetros ha caducado. Proporcione un publicKeyId válido e inténtelo de nuevo. |
| `1311-400` | Solicitud incorrecta | El publicKeyId proporcionado en los parámetros no es válido. Proporcione un publicKeyId válido e inténtelo de nuevo. |
| 1312-400 | Solicitud incorrecta | El valor de parámetro proporcionado {paramValue} no es una entrada válida para property={requestParam}. Proporcione un valor de parámetro válido e inténtelo de nuevo. |
| `1313-400` | Solicitud incorrecta | El atributo de ruta {attribute} no existe. Asegúrese de que el atributo exista e inténtelo de nuevo. |
| `1314-400` | Solicitud incorrecta | Se ha proporcionado una ruta compleja, pero no está permitida. Asegúrese de que no se proporcione una ruta compleja e inténtelo de nuevo. |
| `1315-400` | Solicitud incorrecta | La ruta proporcionada {path} debe señalar a una matriz de registros. Asegúrese de que la ruta proporcionada apunta a la matriz de registros e inténtelo de nuevo. |
| `1316-400` | Solicitud incorrecta | Los parámetros de paginación proporcionados no deben estar vacíos. Proporcione parámetros de paginación válidos e inténtelo de nuevo. |
| `1317-400` | Solicitud incorrecta | Los parámetros de programación proporcionados están vacíos, pero no deben estar vacíos. Proporcione parámetros de programación válidos e inténtelo de nuevo. |
| `1318-400` | Solicitud incorrecta | {mergedMessage}. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1319-400` | Solicitud incorrecta | {param} debe formar parte de la colección principal. Proporcione {param} en la colección principal e inténtelo de nuevo. |
| `1320-400` | Solicitud incorrecta | {idType} no puede ser nulo ni estar vacío. Proporcione un {idType} válido e inténtelo de nuevo. |
| `1321-400` | Solicitud incorrecta | La longitud de {idType} debe ser una, el tamaño proporcionado es {size}. Proporcione un tamaño válido e inténtelo de nuevo. |
| `1322-400` | Solicitud incorrecta | La conexión de origen no puede ser nula para generar la referencia de esquema. Proporcione una conexión de origen válida e inténtelo de nuevo. |
| `1323-400` | Solicitud incorrecta | {entity} no puede ser nulo ni estar vacío en la conexión de origen: {sourceConnection}. Proporcione una {entity} válida e inténtelo de nuevo. |
| `1324-400` | Solicitud incorrecta | La conexión de destino no puede ser nula al extraer el ID del conjunto de datos. Proporcione una conexión de destino válida e inténtelo de nuevo. |
| `1325-400` | Solicitud incorrecta | El parámetro dataSetId no puede ser nulo ni estar vacío en la conexión de destino: {TargetConnection}. Proporcione un parámetro dataSetId válido e inténtelo de nuevo. |
| `1326-400` | Solicitud incorrecta | La conexión de origen no puede ser nula al recuperar el formato de origen. Proporcione una conexión de origen válida e inténtelo de nuevo. |
| `1327-400` | Solicitud incorrecta | No se admite el formato de los datos de origen proporcionados={sourceFormat} en SourceConnection. Los valores permitidos son: {values}. Proporcione los valores permitidos e inténtelo de nuevo. |
| `1328-400` | Solicitud incorrecta | La transformación de la asignación no puede ser nula al extraer {param}. Proporcione una transformación de asignación válida e inténtelo de nuevo. |
| `1329-400` | Solicitud incorrecta | El parámetro: {param} no puede ser nulo ni estar vacío en la solicitud proporcionada. Proporcione un {param} válido e inténtelo de nuevo. |
| `1330-400` | Solicitud incorrecta | No se ha encontrado ninguna columna para la tabla {tableName}. Proporcione un nombre de tabla válido e inténtelo de nuevo. |
| `1331-400` | Solicitud incorrecta | El delimitador de columna no puede tener más de un carácter en SourceConnection: {sourceConnection}. Proporcione un delimitador de columna válido e inténtelo de nuevo. |
| `1332-400` | Solicitud incorrecta | La solicitud de conexión de origen con connectionSpecId: {connectionSpecId} no puede tener un baseConnectionId. Elimine baseConnectionId e inténtelo de nuevo. |
| `1333-400` | Solicitud incorrecta | flowRunAction={flowRunAction} no es compatible con el origen con la especificación id={specId}. Proporcione una acción de ejecución de flujo válida e inténtelo de nuevo. |
| `1334-400` | Solicitud incorrecta | El parámetro de consulta: {param} no puede estar vacío. Proporcione un {param} válido e inténtelo de nuevo. |
| `1335-400` | Solicitud incorrecta | Error al serializar los parámetros de filtro para la exploración. Compruebe la solicitud del parámetro de filtro e inténtelo de nuevo. |
| `1336-400` | Solicitud incorrecta | La conexión Explorar no es compatible con la ID de especificación de conexión: {connectionSpecId}. Proporcione el ID de especificación de conexión compatible e inténtelo de nuevo. |
| `1337-400` | Solicitud incorrecta | {QueryParam} no puede estar vacío para objectType={objectType}. Proporcione un {QueryParam} válido e inténtelo de nuevo. |
| `1338-400` | Solicitud incorrecta | La ID de conexión {connectionType} no puede ser nula en flowRequest. Proporcione un ID de conexión {connectionType} válido en flowRequest. |
| `1339-400` | Solicitud incorrecta | El formato de la organización={imsOrg} proporcionado en la solicitud no es válido. Proporcione un ID de organización válido e inténtelo de nuevo. |
| `1340-400` | Solicitud incorrecta | Error al analizar {time}. Compruebe el formato de hora proporcionado en la solicitud e inténtelo de nuevo. |
| `1341-400` | Solicitud incorrecta | El JSON de ODI proporcionado está vacío. Proporcione un JSON de ODI válido e inténtelo de nuevo. |
| `1342-400` | Solicitud incorrecta | Falta definición en el segmento &quot;dls:folder&quot; de &quot;odi.json&quot;. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1343-400` | Solicitud incorrecta | Faltan definiciones en los segmentos &quot;dls:entityReferences&quot; y &quot;dls:partitionSpec&quot; de &quot;odi.json&quot;. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1344-400` | Solicitud incorrecta | La definición de &quot;dls:partitionSpec&quot; en &quot;odi.json&quot; no es válida porque se encontraron más de un partitionSpec. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1345-400` | Solicitud incorrecta | Faltan definiciones en uno o más segmentos de las rutas: &quot;dls:partitionSpec/dls:fileFormat&quot;, &quot;dls:partitionSpec/dls:partitionTemplate&quot;, &quot;dls:partitionSpec/dls:fileFormat/@type&quot;, &quot;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&quot; en &quot;odi.json&quot;. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1346-400` | Solicitud incorrecta | La definición &quot;@type&quot; proporcionada en &quot;dls:fileFormat&quot; en &quot;odi.json&quot; no es válida. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1347-400` | Solicitud incorrecta | No se admite la definición de dls:csvDelimiters en &quot;odi.json&quot;. Los csvDelimiters admitidos son: [&#39;,&#39;]. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1348-400` | Solicitud incorrecta | Error al deserializar &quot;dls:entityReferences&quot;. Compruebe si los datos tienen un formato válido e inténtelo de nuevo. |
| `1349-400` | Solicitud incorrecta | Los parámetros de filtro proporcionados no son válidos. Proporcione parámetros de filtro válidos e inténtelo de nuevo. |
| `1350-400` | Solicitud incorrecta | No se ha proporcionado ningún operador para el filtro en origen. Proporcione una solicitud de filtro válida con el operador adecuado e inténtelo de nuevo. |
| `1351-400` | Solicitud incorrecta | El operador {operator} proporcionado no es compatible con el filtro en el origen para este conector. Proporcione un operador válido e inténtelo de nuevo. |
| `1352-400` | Solicitud incorrecta | El operador {operator} proporcionado no se puede asignar a ningún operador nativo admitido para {ql}. Proporcione un operador válido e inténtelo de nuevo. |
| `1353-400` | Solicitud incorrecta | El filtro en origen aún no es compatible con el conector {connectorType}. Compruebe los conectores admitidos en la documentación: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Solicitud incorrecta | El idioma de consulta {ql} aún no es compatible con el filtro en origen. Proporcione un idioma de consulta válido e inténtelo de nuevo. |
| `1355-400` | Solicitud incorrecta | El tipo de filtro proporcionado no es válido. El tipo de filtro admitido es: PQL. Proporcione un tipo de filtro válido e inténtelo de nuevo. |
| `1356-400` | Solicitud incorrecta | El formato de filtro proporcionado no es válido. El formato de filtro admitido es : pql/json. Proporcione un formato de filtro válido e inténtelo de nuevo. |
| `1357-400` | Solicitud incorrecta | El filtro proporcionado no es válido. El valor debe proporcionarse con filtros detallados. Proporcione un filtro válido e inténtelo de nuevo. |
| `1358-400` | Solicitud incorrecta | El parámetro proporcionado &quot;objectType&quot; no es válido. Proporcione un objectType válido e inténtelo de nuevo. |
| `1359-400` | Solicitud incorrecta | Falta el parámetro {param} en la solicitud. Proporcione un {param} válido e inténtelo de nuevo. |
| `1360-400` | Solicitud incorrecta | La hora de inicio no puede establecerse en el pasado. Proporcione una hora de inicio válida e inténtelo de nuevo. |
| `1361-400` | Solicitud incorrecta | El intervalo no se permite con la ingesta única. Elimine el intervalo o cambie la frecuencia e inténtelo de nuevo. |
| `1362-400` | Solicitud incorrecta | El intervalo no puede ser menor que {minInterval}. Proporcione un valor de intervalo válido e inténtelo de nuevo. |
| `1363-400` | Solicitud incorrecta | El intervalo {interval} no se permite con la frecuencia: {frequency}. Proporcione un valor de intervalo válido e inténtelo de nuevo. |
| `1364-400` | Solicitud incorrecta | No se permite el indicador de relleno cuando la frecuencia se establece en uno. Elimine el indicador de relleno cuando la frecuencia esté establecida en una vez e inténtelo de nuevo. |
| `1365-400` | Solicitud incorrecta | La ruta {path} proporcionada en operaciones no es válida. Proporcione una ruta válida {path} e inténtelo de nuevo. |
| `1366-400` | Solicitud incorrecta | Ha pasado el tiempo de inicio y ya no se permite la operación de actualización. |
| `1367-400` | Solicitud incorrecta | La columna delta es necesaria en la transformación de copia al crear un conector CRM. Proporcione una columna delta e inténtelo de nuevo. |
| `1368-400` | Solicitud incorrecta | El modo no está permitido en la solicitud de flujo. Compruebe su solicitud e inténtelo de nuevo. |
| `1369-400` | Solicitud incorrecta | La columna delta de la transformación de copia no está permitida cuando la frecuencia se establece en una vez. Elimine la columna delta e inténtelo de nuevo. |
| `1370-400` | Solicitud incorrecta | No se han podido recuperar las columnas de origen para la ingesta porque falta la transformación de asignación. Agregue la transformación de asignación e inténtelo de nuevo. |
| `1371-400` | Solicitud incorrecta | La detección de propiedades del archivo no es compatible con el conector {connectorType}. Proporcione las propiedades del archivo manualmente. |
| `1372-400` | Solicitud incorrecta | No se permite la operación actual. No se permite explorar mediante especificación de conexión para la especificación de conexión ID={connectionSpecId}. |
| `1373-400` | Solicitud incorrecta | Falta flowSpecType en la solicitud. Proporcione un flowSpecType válido e inténtelo de nuevo. |
| `1374-400` | Solicitud incorrecta | Los parámetros de consulta proporcionados no son válidos. No puede tener el indicador determineProperties y las propiedades definidas por el usuario en la misma solicitud. Corrija su solicitud e inténtelo de nuevo. |
| `1375-400` | Solicitud incorrecta | Error al detectar las propiedades del archivo. Introduzca las propiedades manualmente. |
| `1376-400` | Solicitud incorrecta | La detección de propiedades de archivo no es compatible con la especificación de conexión id={connectionSpecId}. Proporcione las propiedades del archivo manualmente. |
| `1377-400` | Solicitud incorrecta | El parámetro de valor proporcionado es nulo y no se puede comparar con el operador {operator}. Proporcione un parámetro de valor válido e inténtelo de nuevo. |
| `1378-400` | Solicitud incorrecta | Error al validar la columna de entrada {column} para el filtro en origen. El nombre de columna debe ser una columna válida de la tabla. Proporcione un nombre de columna válido e inténtelo de nuevo. |
| `1379-400` | Solicitud incorrecta | Error al validar la entrada {value} para el filtro en origen. La columna DataType en origen es {columnDataType} y el valor DataType [Cadena] no coincide con. Proporcione un {value} válido e inténtelo de nuevo. |
| `1380-400` | Solicitud incorrecta | Error al crear la ejecución del flujo. Mensaje de error: {message} |
| `1381-400` | Solicitud incorrecta | WindowEndTime={endTime} no puede ser anterior a Window StartTime={startTime}. Proporcione una hora de finalización válida e inténtelo de nuevo. |
| `1382-400` | Solicitud incorrecta | La columna delta debe coincidir con el valor presente en las transformaciones de copia del flujo. Proporcione una columna delta válida e inténtelo de nuevo. |
| `1383-400` | Solicitud incorrecta | Falta la columna delta en los parámetros recibidos para crear una ejecución de flujo. Proporcione la columna delta en parámetros e inténtelo de nuevo. |
| `1384-400` | Solicitud incorrecta | Los parámetros={params} proporcionados para crear una ejecución de flujo no son válidos o están vacíos. Proporcione parámetros válidos e inténtelo de nuevo. |
| `1385-400` | Solicitud incorrecta | El connectorType={connectorType} proporcionado no es compatible con la creación de ejecuciones de flujo. Proporcione un connectorType válido e inténtelo de nuevo. |
| `1386-400` | Solicitud incorrecta | flowId={flowId} con scheduleParams frequency={frequency} no es compatible con la creación de ejecuciones de flujo. Proporcione una frecuencia válida e inténtelo de nuevo. |
| `1387-400` | Solicitud incorrecta | flowRunId={flowRunId} no es válido={state} para reactivarlo. Vuelva a intentarlo después de un tiempo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1388-400` | Solicitud incorrecta | El flujo={flow} está en estado={state} y no se puede volver a activar. El flujo debe estar en estado habilitado para volver a activarse. |
| `1389-400` | Solicitud incorrecta | Error al analizar la cadena codificada en base64 proporcionada. Proporcione una cadena de filtro codificada válida e inténtelo de nuevo. |
| `1390-400` | Solicitud incorrecta | El operador &quot;not&quot; no puede tener más de una comparación. Proporcione un número válido de comparaciones e inténtelo de nuevo. |
| `1391-400` | Solicitud incorrecta | Error al analizar SchemaMetaData en sourceConnection para Id={sourceConnectionId}. Compruebe schemaMetaData en la solicitud e inténtelo de nuevo. |
| `1392-400` | Solicitud incorrecta | Error al analizar las transformaciones en la solicitud de flujo para flowId={flowId}. Compruebe las transformaciones en la solicitud e inténtelo de nuevo. |
| `1393-400` | Solicitud incorrecta | El parámetro {parameter} proporcionado es nulo o está vacío. Proporcione un {parameter} válido e inténtelo de nuevo. |
| `1394-400` | Solicitud incorrecta | El valor mínimo de un parámetro {parameter} es uno. Proporcione un {parameter} válido e inténtelo de nuevo. |
| `1395-400` | Solicitud incorrecta | La conexión de origen encontrada en el flujo es nula o está vacía. Proporcione una conexión de origen válida en el flujo e inténtelo de nuevo. |
| `1396-400` | Solicitud incorrecta | No se ha encontrado un formato coincidente. Proporcione un formato coincidente e inténtelo de nuevo. |
| `1397-400` | Solicitud incorrecta | La frecuencia proporcionada: {frequency} no es válida. Proporcione una frecuencia válida e inténtelo de nuevo. |
| `1398-400` | Solicitud incorrecta | La operación proporcionada: {action} no es compatible. Compruebe la operación proporcionada e inténtelo de nuevo. |
| `1399-400` | Solicitud incorrecta | No se ha encontrado requestFileType válido. Proporcione un requestFileType válido e inténtelo de nuevo. |
| `1400-400` | Solicitud incorrecta | El parámetro proporcionado &quot;templateType&quot; no es válido. Proporcione un tipo de plantilla válido e inténtelo de nuevo. |
| `1401-400` | Solicitud incorrecta | No se admite la acción de ejecución de flujo proporcionada={flowRunAction}. Proporcione una acción de ejecución de flujo válida e inténtelo de nuevo. |
| `1402-500` | Error interno | Se ha producido un error interno. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1403-400` | Solicitud incorrecta | El tiempo de inicio ha pasado y ya no puede cambiar la frecuencia a una vez. |
| `1404-400` | Solicitud incorrecta | El tiempo de inicio ha pasado y ya no puede actualizar el relleno. |

## Excepciones de Flow Service (1600-1699)

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1600-400` | Solicitud incorrecta | No se ha podido procesar la solicitud. {detailedMessage} |
| `1601-500` | Error interno | Se ha producido un error interno. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1602-404` | Recurso no encontrado | No se ha encontrado el recurso solicitado. {detailedMessage} |
| `1603-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo. Póngase en contacto con Atención al cliente si el problema persiste. |
| `1604-504` | Tiempo de espera de puerta | Se agotó el tiempo de espera de puerta de enlace. Inténtelo de nuevo. Póngase en contacto con Atención al cliente si el problema persiste. |
| `1605-401` | No autorizado | El usuario no está autorizado. {detailedMessage} |
| `1606-403` | Prohibido | No se permite la operación solicitada. {detailedMessage} |
| `1607-412` | Error de condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. {detailedMessage} |

## Errores de zona de aterrizaje de datos

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1700-500` | Error interno | Se ha producido un error interno. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1701-400` | Solicitud incorrecta | La zona de aterrizaje proporcionada está inactiva. Active la zona de aterrizaje e inténtelo de nuevo. |
| `1702-400` | Solicitud incorrecta | No se permite el tipo SAS={sasType} proporcionado para la zona de aterrizaje. Proporcione una SAS válida e inténtelo de nuevo. |
| `1703-400` | Solicitud incorrecta | No se permite actualizar las credenciales. |
| `1704-400` | Solicitud incorrecta | Las claves devueltas para storageAccountName={accountName} en subscriptionId={subscriptionId} y resourceGroupName={resourceGroupName} tienen un formato incorrecto. Compruebe su solicitud e inténtelo de nuevo. Póngase en contacto con el servicio de asistencia si el problema persiste. |
| `1705-400` | Solicitud incorrecta | La acción de zona de aterrizaje de datos proporcionada no es compatible. Proporcione una acción válida e inténtelo de nuevo. |
| `1706-400` | Solicitud incorrecta | La configuración de activaciones permitidas no está configurada correctamente para landing zone={landingZoneType}. Vuelva a intentarlo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1707-400` | Solicitud incorrecta | El servicio no se pudo iniciar porque la configuración de la zona de aterrizaje no puede ser nula ni estar vacía. Asegúrese de que la configuración de la zona de aterrizaje no sea nula e inténtelo de nuevo. |
| `1708-400` | Solicitud incorrecta | La configuración del contenedor no puede ser nula en landingZoneType={landingZoneType}. Asegúrese de que la configuración del contenedor no sea nula e inténtelo de nuevo. |
| `1709-400` | Solicitud incorrecta | Los detalles SAS no pueden ser nulos para {tokenConfig} en landingZoneType={landingZoneType}. Proporcione una SAS válida en la configuración e inténtelo de nuevo. |
| `1710-400` | Solicitud incorrecta | No se admite la zona de aterrizaje proporcionada del tipo: {landingZoneUseCase}. Proporcione un tipo de zona de aterrizaje válido e inténtelo de nuevo. |
| `1711-400` | Solicitud incorrecta | No se encontraron los detalles de SAS para la zona de aterrizaje de datos proporcionada del tipo: {landingZoneUseCase}. Compruebe si se proporcionan detalles SAS para el tipo de zona de aterrizaje proporcionado. |
| `1712-400` | Solicitud incorrecta | La acción de zona de aterrizaje proporcionada: {actionType} no está permitido. Proporcione una acción de zona de aterrizaje de datos válida e inténtelo de nuevo. |
| `1713-400` | Solicitud incorrecta | {OperationType} no está permitido para el {tokenType} proporcionado. Compruebe su solicitud e inténtelo de nuevo. |
| `1714-400` | Solicitud incorrecta | clientId={clientId} no tiene permiso para realizar esta operación. Compruebe su solicitud con permisos e inténtelo de nuevo. |
