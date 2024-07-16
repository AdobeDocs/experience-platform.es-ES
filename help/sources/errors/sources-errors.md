---
title: Mensajes de error de origen
description: Obtenga información acerca de los mensajes de error que pueden surgir al utilizar Flow Service para las fuentes.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3188'
ht-degree: 90%

---

# Mensajes de error de fuentes

Este documento proporciona un catálogo de mensajes de error, descripciones y resoluciones sugeridas para las fuentes.

## Errores genéricos

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1000-400` | Solicitud incorrecta | La solicitud no es válida. Compruébela e inténtelo de nuevo. |
| `1001-401` | No autorizado | El usuario no está autorizado. Póngase en contacto con el administrador para obtener acceso al recurso. |
| `1002-403` | Prohibido | No se permite la operación solicitada. Compruébela e inténtelo de nuevo. |
| `1003-404` | Recurso no encontrado | No se encontró el recurso solicitado. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1004-415` | Tipo de medios no compatible | El formato de carga útil proporcionado no es compatible. Compruebe la solicitud e inténtelo de nuevo. |
| `1005-500` | Error interno | Se ha producido un error interno desconocido. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1006-408` | Se ha agotado el tiempo de espera de la solicitud | Error al procesar la solicitud. Se agotó el tiempo de espera. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1007-400` | Parámetro de encabezado no válido | Se ha recibido un parámetro de encabezado no válido: {headerName}. Compruebe los parámetros del encabezado e inténtelo de nuevo. |
| `1008-401` | | Token de autorización no válido | El token de autorización no tiene acceso a esta organización o la organización no existe. Asegúrese de que la organización existe o póngase en contacto con el administrador para obtener acceso. |
| `1009-403` | Falta el ID de organización de IMS o está vacío | El encabezado de la solicitud de ID de la organización falta o está vacío. Actualice el valor del encabezado e inténtelo de nuevo. |
| `1010-500` | detailed-message no válido | El parámetro del mensaje detallado no se ha proporcionado correctamente. Compruébelo e inténtelo de nuevo. |
| `1011-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1012-504` | Se ha agotado el tiempo de espera de la puerta de enlace | Se ha agotado el tiempo de espera de la puerta de enlace. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1013-412` | Error de condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. Verifíquelo e inténtelo de nuevo. |
| `1014-400` | Solicitud incorrecta, argumento ilegal | No se pudo procesar la solicitud. {detailedMessage} |

## Errores de marco

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1100-400` | Solicitud incorrecta | No se pudo procesar la solicitud. {detailedMessage} |
| `1101-500` | Error interno | Se ha producido un error interno desconocido. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1102-404` | Recurso no encontrado | No se ha encontrado el recurso solicitado. {detailedMessage} |
| `1103-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1104-504` | Se ha agotado el tiempo de espera de la puerta de enlace | Se ha agotado el tiempo de espera de la puerta de enlace. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1105-401` | No autorizado | El usuario no está autorizado. {detailedMessage} |
| `1106-403` | Prohibido | No se permite la operación solicitada. {detailedMessage} |
| `1107-412` | Error de condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. {detailedMessage} |

## Errores de cifrado

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1200-500` | Error interno | Se ha producido un error interno desconocido. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1201-400` | Solicitud incorrecta | El flowId no puede ser nulo ni estar vacío. Proporcione uno válido en la solicitud e inténtelo de nuevo. |
| `1202-400` | Solicitud incorrecta | Falta publicKeyId en transformations={transformations} del flujo. Proporciónelo en la solicitud e inténtelo de nuevo. |
| `1203-400` | Solicitud incorrecta | La clave de cifrado no existe en keyID={keyID} en las transformations={transformations} del flujo. Compruebe el keyID proporcionado e inténtelo de nuevo. |
| `1204-400` | Solicitud incorrecta | El algoritmo de cifrado proporcionado no es válido. Indique uno válido e inténtelo de nuevo. |
| `1205-400` | Solicitud incorrecta | Falta la frase de contraseña en la sección de parámetros de la solicitud proporcionada. Indique passPhrase en los parámetros e inténtelo de nuevo. |

## Errores de API de REST

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1300-400` | Solicitud incorrecta | La solicitud de conexión de revisión no es compatible con el conector {connectorType}. Compruébela e inténtelo de nuevo. |
| `1301-400` | Solicitud incorrecta | El authSpecType param : {authSpecType} proporcionado no es compatible. Indique un tipo de especificación de autenticación válido e inténtelo de nuevo. |
| `1302-400` | Solicitud incorrecta | El tipo de autenticación proporcionado = {authType} no es compatible con connector={connectorType}. Indique uno válido para el conector dado. |
| `1303-400` | Solicitud incorrecta | La URL no se pudo codificar con los parámetros de autenticación dados porque la codificación de la URL no es compatible con {value}. Compruebe los parámetros de autenticación e inténtelo de nuevo. |
| `1304-400` | Solicitud incorrecta | No se proporciona el campo obligatorio {field}. Indíquelo e inténtelo de nuevo. |
| `1305-400` | Solicitud incorrecta | El tipo de conector proporcionado = {connectorType} no es compatible con esta operación. |
| `1306-400` | Solicitud incorrecta | La conexión de público destinatario no puede ser nula al validar el ID de especificación de conexión de público destinatario. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1307-400` | Solicitud incorrecta | El id. de especificación de conexión de destino no es válido={targetConnectionSpecId}. El valor permitido es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Solicitud incorrecta | No se pudo procesar la solicitud. Mensaje de error: {msftErrorMessage} |
| `1309-400` | Solicitud incorrecta | La transformación de cifrado proporcionada no es válida porque falta {requiredParam} en los parámetros. Indique {requiredParam} e inténtelo de nuevo. |
| `1310-400` | Solicitud incorrecta | El publicKeyId proporcionado en los parámetros ha caducado. Indique uno válido e inténtelo de nuevo. |
| `1311-400` | Solicitud incorrecta | El publicKeyId proporcionado en parámetros no es válido. Indique uno válido e inténtelo de nuevo. |
| 1312-400 | Solicitud incorrecta | El valor de parámetro proporcionado {paramValue} no es una entrada válida para property={requestParam}. Indique uno válido e inténtelo de nuevo. |
| `1313-400` | Solicitud incorrecta | El atributo de ruta {attribute} no existe. Asegúrese de que exista e inténtelo de nuevo. |
| `1314-400` | Solicitud incorrecta | Se ha proporcionado una ruta compleja, pero no se permite. Asegúrese de no indicarla e inténtelo de nuevo. |
| `1315-400` | Solicitud incorrecta | La ruta de acceso proporcionada {path} debe señalar a una matriz de registros. Asegúrese de que lo haga e inténtelo de nuevo. |
| `1316-400` | Solicitud incorrecta | Los parámetros de paginación proporcionados no deben estar vacíos. Indique unos válidos e inténtelo de nuevo. |
| `1317-400` | Solicitud incorrecta | Los parámetros de programación proporcionados están vacíos, pero no deberían estarlo. Indique unos válidos e inténtelo de nuevo. |
| `1318-400` | Solicitud incorrecta | {combinedMessage}. Compruebe la solicitud proporcionada e inténtelo de nuevo. |
| `1319-400` | Solicitud incorrecta | El parámetro {param} debe formar parte de la colección principal. Proporciónelo e inténtelo de nuevo. |
| `1320-400` | Solicitud incorrecta | El {idType} no puede ser nulo ni estar vacío. Proporcione uno válido e inténtelo de nuevo. |
| `1321-400` | Solicitud incorrecta | La longitud de {idType} debe ser uno, el tamaño proporcionado es {size}. Indique uno válido e inténtelo de nuevo. |
| `1322-400` | Solicitud incorrecta | La conexión de origen no puede ser nula para generar la referencia de esquema. Proporcione una válida e inténtelo de nuevo. |
| `1323-400` | Solicitud incorrecta | La {entity} no puede ser nula o estar vacía en la conexión de origen: {sourceConnection}. Proporcione una {entity} válida e inténtelo de nuevo. |
| `1324-400` | Solicitud incorrecta | La conexión de público destinatario no puede ser nula al extraer el ID del conjunto de datos. Proporcione una válida e inténtelo de nuevo. |
| `1325-400` | Solicitud incorrecta | El parámetro dataSetId no puede ser nulo ni estar vacío en la conexión de público destinatario: {TargetConnection}. Proporcione uno válido e inténtelo de nuevo. |
| `1326-400` | Solicitud incorrecta | La conexión de origen no puede ser nula al recuperar el formato de origen. Proporcione una válida e inténtelo de nuevo. |
| `1327-400` | Solicitud incorrecta | No se admite el formato de los datos de origen supplied={sourceFormat} en SourceConnection. Los valores permitidos son: {values}. Indíquelos e inténtelo de nuevo. |
| `1328-400` | Solicitud incorrecta | La transformación de asignación no puede ser nula al extraer {param}. Proporcione una válida e inténtelo de nuevo. |
| `1329-400` | Solicitud incorrecta | El parámetro: {param} no puede ser nulo ni estar vacío en la solicitud proporcionada. Indique uno válido e inténtelo de nuevo. |
| `1330-400` | Solicitud incorrecta | No se ha encontrado ninguna columna para la tabla {tableName}. Proporcione un nombre de tabla válido e inténtelo de nuevo. |
| `1331-400` | Solicitud incorrecta | El delimitador de columnas no puede tener más de un carácter en SourceConnection: {sourceConnection}. Proporcione un delimitador de columna válido e inténtelo de nuevo. |
| `1332-400` | Solicitud incorrecta | La solicitud de conexión de origen con connectionSpecId: {connectionSpecId} no puede tener baseConnectionId. Quítelo e inténtelo de nuevo. |
| `1333-400` | Solicitud incorrecta | flowRunAction={flowRunAction} no es compatible con el origen con spec id={specId}. Proporcione una acción de ejecución de flujo válida e inténtelo de nuevo. |
| `1334-400` | Solicitud incorrecta | El parámetro de consulta : {param} no puede estar vacío. Proporcione uno válido e inténtelo de nuevo. |
| `1335-400` | Solicitud incorrecta | Error al serializar los parámetros de filtro para explorar. Compruebe la solicitud e inténtelo de nuevo. |
| `1336-400` | Solicitud incorrecta | Explorar la conexión no es compatible con el ID de especificación de conexión: {connectionSpecId}. Proporcione uno compatible e inténtelo de nuevo. |
| `1337-400` | Solicitud incorrecta | {QueryParam} no puede estar vacío para objectType={objectType}. Proporcione un {QueryParam} válido e inténtelo de nuevo. |
| `1338-400` | Solicitud incorrecta | El ID de conexión {connectionType} no puede ser nulo en flowRequest. Proporcione un ID de conexión de {connectionType} válido en flowRequest. |
| `1339-400` | Solicitud incorrecta | El formato de la organización={imsOrg} proporcionado en la solicitud no es válido. Proporcione un ID de organización válido e inténtelo de nuevo. |
| `1340-400` | Solicitud incorrecta | Error al analizar {time}. Compruebe el formato de hora proporcionado en la solicitud e inténtelo de nuevo. |
| `1341-400` | Solicitud incorrecta | El JSON de ODI proporcionado está vacío. Indique uno válido e inténtelo de nuevo. |
| `1342-400` | Solicitud incorrecta | El segmento “dls:folder” en “odi.json” carece de definiciones. Proporcione las adecuadas en “odi.json” e inténtelo de nuevo. |
| `1343-400` | Solicitud incorrecta | Los segmentos “dls:entityReferences” y “dls:partitionSpec” en “odi.json” no tienen definiciones. Proporcione las definiciones adecuadas en “odi.json” e inténtelo de nuevo. |
| `1344-400` | Solicitud incorrecta | La definición para “dls:partitionSpec” en “odi.json” no es válida porque se encontraron más de un partitionSpecs. Proporcione las definiciones adecuadas en “odi.json” e inténtelo de nuevo. |
| `1345-400` | Solicitud incorrecta | Faltan definiciones en 1 o más segmentos de las rutas: “dls:partitionSpec/dls:fileFormat”, “dls:partitionSpec/dls:partitionTemplate”, “dls:partitionSpec/dls:fileFormat/@type”, “dls:partitionSpec/dls:fileFormat/dls:csvDelimiters” en “odi.json”. Proporcione las definiciones adecuadas en “odi.json” e inténtelo de nuevo. |
| `1346-400` | Solicitud incorrecta | La definición “@type” proporcionada en “dls:fileFormat” en “odi.json” no es válida. Indique las definiciones adecuadas en “odi.json” e inténtelo de nuevo. |
| `1347-400` | Solicitud incorrecta | No se admite la definición de dls:csvDelimiters en &quot;odi.json&quot;. Los csvDelimiters admitidos son: [&#39;,&#39;]. Proporcione las definiciones adecuadas en &quot;odi.json&quot; e inténtelo de nuevo. |
| `1348-400` | Solicitud incorrecta | Error al deserializar “dls:entityReferences”. Compruebe si los datos tienen un formato válido e inténtelo de nuevo. |
| `1349-400` | Solicitud incorrecta | Los parámetros de filtro proporcionados no son válidos. Indique unos válidos e inténtelo de nuevo. |
| `1350-400` | Solicitud incorrecta | No se ha proporcionado ningún operador para el filtro en origen. Proporcione una solicitud de filtro válida con el operador adecuado e inténtelo de nuevo. |
| `1351-400` | Solicitud incorrecta | El operador proporcionado {operator} no es compatible con el filtro en el origen para este conector. Proporcione un operador válido e inténtelo de nuevo. |
| `1352-400` | Solicitud incorrecta | El operador proporcionado {operator} no se puede asignar a ningún operador nativo admitido para {ql}. Proporcione un operador válido e inténtelo de nuevo. |
| `1353-400` | Solicitud incorrecta | El filtro en origen aún no es compatible con el conector {connectorType}. Compruebe los conectores compatibles en la documentación: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=es. |
| `1354-400` | Solicitud incorrecta | El idioma de consulta {ql} todavía no es compatible con el filtro en origen. Proporcione un idioma de consulta válido e inténtelo de nuevo. |
| `1355-400` | Solicitud incorrecta | El tipo de filtro proporcionado no es válido. El tipo de filtro admitido es: PQL. Indique uno válido e inténtelo de nuevo. |
| `1356-400` | Solicitud incorrecta | El formato de filtro proporcionado no es válido. El admitido es: pql/json. Indique uno válido e inténtelo de nuevo. |
| `1357-400` | Solicitud incorrecta | El filtro proporcionado no es válido. El valor debe suministrarse con filtros detallados. Indique uno válido e inténtelo de nuevo. |
| `1358-400` | Solicitud incorrecta | El parámetro “objectType” proporcionado no es válido. Indique uno válido e inténtelo de nuevo. |
| `1359-400` | Solicitud incorrecta | Falta el parámetro {param} en la solicitud. Proporcione uno válido e inténtelo de nuevo. |
| `1360-400` | Solicitud incorrecta | La hora de inicio no puede establecerse en el pasado. Proporcione una válida e inténtelo de nuevo. |
| `1361-400` | Solicitud incorrecta | No se permite el intervalo con la ingesta única. Elimínelo o cambie la frecuencia e inténtelo de nuevo. |
| `1362-400` | Solicitud incorrecta | El intervalo no puede ser menor que {minInterval}. Proporcione un valor válido e inténtelo de nuevo. |
| `1363-400` | Solicitud incorrecta | El intervalo {interval} no se permite con la frecuencia: {frequency}. Proporcione un valor válido e inténtelo de nuevo. |
| `1364-400` | Solicitud incorrecta | El indicador de relleno no está permitido cuando la frecuencia está establecida en una vez. Quítelo e inténtelo de nuevo. |
| `1365-400` | Solicitud incorrecta | La ruta {path} proporcionada en ops no es válida. Indique una válida e inténtelo de nuevo. |
| `1366-400` | Solicitud incorrecta | Ha pasado el tiempo de inicio y ya no se permite la operación de actualización. |
| `1367-400` | Solicitud incorrecta | La columna delta es necesaria en la transformación de copia al crear un conector CRM. Proporcione una e inténtelo de nuevo. |
| `1368-400` | Solicitud incorrecta | No se permite el modo en la solicitud de flujo. Compruebe su solicitud e inténtelo de nuevo. |
| `1369-400` | Solicitud incorrecta | La columna delta de la transformación de copia no está permitida cuando la frecuencia se establece en una vez. Elimínela e inténtelo de nuevo. |
| `1370-400` | Solicitud incorrecta | No se han podido recuperar las columnas de origen para la ingesta porque falta la transformación de asignación. Añádala e inténtelo de nuevo. |
| `1371-400` | Solicitud incorrecta | La detección de propiedades de archivo no es compatible con el conector {connectorType}. Proporciónelas manualmente. |
| `1372-400` | Solicitud incorrecta | No se permite la operación actual. La exploración mediante la especificación de conexión no está permitida para la especificación de conexión ID={connectionSpecId}. |
| `1373-400` | Solicitud incorrecta | Falta flowSpecType en la solicitud. Proporcione uno válido e inténtelo de nuevo. |
| `1374-400` | Solicitud incorrecta | Los parámetros de consulta proporcionados no son válidos. No puede tener el indicador determineProperties y propiedades definidas por el usuario en la misma solicitud. Corríjala e inténtelo de nuevo. |
| `1375-400` | Solicitud incorrecta | Error al detectar las propiedades del archivo. Introdúzcalas manualmente. |
| `1376-400` | Solicitud incorrecta | La detección de propiedades de archivo no es compatible con la especificación de conexión id={connectionSpecId}. Proporcione las propiedades del archivo manualmente. |
| `1377-400` | Solicitud incorrecta | El parámetro de valor proporcionado es nulo y no se puede comparar con el operador {operator}. Indique uno válido e inténtelo de nuevo. |
| `1378-400` | Solicitud incorrecta | Error al validar la columna de entrada {column} para el filtro en origen. El nombre de columna debe ser una columna válida de la tabla. Proporcione uno válido e inténtelo de nuevo. |
| `1379-400` | Solicitud incorrecta | Error al validar la entrada {value} para el filtro en origen. El DataType de columna en origen es {columnDataType} y el valor DataType [String] no coincide. Proporcione un {value} válido e inténtelo de nuevo. |
| `1380-400` | Solicitud incorrecta | Error al crear la ejecución de flujo. Mensaje de error: {message} |
| `1381-400` | Solicitud incorrecta | WindowEndTime={endTime} no puede ser anterior a Window StartTime={startTime}. Proporcione una hora de finalización válida e inténtelo de nuevo. |
| `1382-400` | Solicitud incorrecta | La columna delta debe coincidir con el valor presente en las transformaciones de copia del flujo. Proporcione una columna delta válida e inténtelo de nuevo. |
| `1383-400` | Solicitud incorrecta | Falta la columna delta en los parámetros recibidos para crear una ejecución de flujo. Proporcione una e inténtelo de nuevo. |
| `1384-400` | Solicitud incorrecta | Los params={params} proporcionados para crear una ejecución de flujo no son válidos o están vacíos. Indique unos válidos e inténtelo de nuevo. |
| `1385-400` | Solicitud incorrecta | El connectorType={connectorType} proporcionado no es compatible con la creación de ejecuciones de flujo. Indique uno válido e inténtelo de nuevo. |
| `1386-400` | Solicitud incorrecta | flowId={flowId} con scheduleParams frequency={frequency} no es compatible con la creación de ejecuciones de flujo. Proporcione una frecuencia válida e inténtelo de nuevo. |
| `1387-400` | Solicitud incorrecta | flowRunId={flowRunId} tiene un estado no válido={state} para volver a activarlo. Vuelva a intentarlo después de un tiempo y, si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1388-400` | Solicitud incorrecta | flow={flow} está en state={state} y no se puede volver a activar. El flujo debe estar en estado habilitado para volver a activarse. |
| `1389-400` | Solicitud incorrecta | Error al analizar la cadena con codificación base64 proporcionada. Indique una válida e inténtelo de nuevo. |
| `1390-400` | Solicitud incorrecta | El operador “no” no puede tener más de una comparación. Proporcione un número válido e inténtelo de nuevo. |
| `1391-400` | Solicitud incorrecta | Error al analizar SchemaMetaData en sourceConnection para Id={sourceConnectionId}. Compruébelo en la solicitud e inténtelo de nuevo. |
| `1392-400` | Solicitud incorrecta | Error al analizar las transformaciones en la solicitud de flujo para flowId={flowId}. Compruébelas e inténtelo de nuevo. |
| `1393-400` | Solicitud incorrecta | El parámetro proporcionado {parameter} es nulo o está vacío. Indique uno válido e inténtelo de nuevo. |
| `1394-400` | Solicitud incorrecta | El valor mínimo de un parámetro {parameter} es uno. Proporcione uno válido e inténtelo de nuevo. |
| `1395-400` | Solicitud incorrecta | La conexión de origen encontrada en el flujo es nula o está vacía. Proporcione una válida en el flujo e inténtelo de nuevo. |
| `1396-400` | Solicitud incorrecta | No se encontró un formato coincidente. Proporcione uno e inténtelo de nuevo. |
| `1397-400` | Solicitud incorrecta | La frecuencia proporcionada : {frequency} no es válida. Indique una válida e inténtelo de nuevo. |
| `1398-400` | Solicitud incorrecta | La operación proporcionada : {action} no es compatible. Compruébela e inténtelo de nuevo. |
| `1399-400` | Solicitud incorrecta | No se encontró un requestFileType válido. Proporcione uno e inténtelo de nuevo. |
| `1400-400` | Solicitud incorrecta | El parámetro proporcionado “templateType” no es válido. Indique un tipo de plantilla válido e inténtelo de nuevo. |
| `1401-400` | Solicitud incorrecta | No se admite la acción de ejecución de flujo proporcionada action={flowRunAction}. Indique una válida e inténtelo de nuevo. |
| `1402-500` | Error interno | Se ha producido un error interno desconocido. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1403-400` | Solicitud incorrecta | El tiempo de inicio ha pasado y ya no puede cambiar la frecuencia a una vez. |
| `1404-400` | Solicitud incorrecta | Ha pasado el tiempo de inicio y ya no puede actualizar el relleno. |

## Excepciones de Flow Service (1600-1699)

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1600-400` | Solicitud incorrecta | No se pudo procesar la solicitud. {detailedMessage} |
| `1601-500` | Error interno | Se ha producido un error interno desconocido. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1602-404` | Recurso no encontrado | No se ha encontrado el recurso solicitado. {detailedMessage} |
| `1603-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo. Póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1604-504` | Se ha agotado el tiempo de espera de la puerta de enlace | Se ha agotado el tiempo de espera de la puerta de enlace. Inténtelo de nuevo. Póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1605-401` | No autorizado | El usuario no está autorizado. {detailedMessage} |
| `1606-403` | Prohibido | No se permite la operación solicitada. {detailedMessage} |
| `1607-412` | Error de condición previa | La condición definida por los encabezados If-Unmodified-Since o If-None-Match no se cumple. {detailedMessage} |

## Errores de zona de aterrizaje de datos

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1700-500` | Error interno | Se ha producido un error interno desconocido. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1701-400` | Solicitud incorrecta | La zona de aterrizaje proporcionada está inactiva. Actívela e inténtelo de nuevo. |
| `1702-400` | Solicitud incorrecta | El SAS Type={sasType} proporcionado para la zona de aterrizaje no está permitido. Indique uno válido e inténtelo de nuevo. |
| `1703-400` | Solicitud incorrecta | No se permite actualizar las credenciales. |
| `1704-400` | Solicitud incorrecta | Las claves devueltas para storageAccountName={accountName} en subscriptionId={subscriptionId} y resourceGroupName={resourceGroupName} no tienen el formato correcto. Compruebe su solicitud e inténtelo de nuevo. Póngase en contacto con soporte si el problema persiste. |
| `1705-400` | Solicitud incorrecta | La acción de zona de aterrizaje de datos proporcionada no es compatible. Indique una válida e inténtelo de nuevo. |
| `1706-400` | Solicitud incorrecta | La configuración de activaciones permitidas no está configurada correctamente para landing zone={landingZoneType}. Inténtelo de nuevo y póngase en contacto con el servicio de atención al cliente si el problema persiste. |
| `1707-400` | Solicitud incorrecta | No se pudo iniciar el servicio porque la configuración de la zona de aterrizaje no puede ser nula o estar vacía. Asegúrese de ello e inténtelo de nuevo. |
| `1708-400` | Solicitud incorrecta | La configuración del contenedor no puede ser nula en landingZoneType={landingZoneType}. Asegúrese de que no lo sea e inténtelo de nuevo. |
| `1709-400` | Solicitud incorrecta | Los detalles de SAS no pueden ser nulos para {tokenConfig} en landingZoneType={landingZoneType}. Proporcione un SAS válido en la configuración e inténtelo de nuevo. |
| `1710-400` | Solicitud incorrecta | La zona de aterrizaje proporcionada del tipo: {landingZoneUseCase} no es compatible. Indique uno válido e inténtelo de nuevo. |
| `1711-400` | Solicitud incorrecta | No se encontraron los detalles de SAS para la zona de aterrizaje de datos proporcionada del tipo: {landingZoneUseCase}. Compruebe si se facilitan detalles. |
| `1712-400` | Solicitud incorrecta | La acción de zona de aterrizaje proporcionada: {actionType} no está permitido. Indique una válida e inténtelo de nuevo. |
| `1713-400` | Solicitud incorrecta | El {OperationType} no está permitido para el {tokenType} proporcionado. Compruebe su solicitud e inténtelo de nuevo. |
| `1714-400` | Solicitud incorrecta | clientId={clientId} no tiene permiso para realizar esta operación. Compruebe su solicitud con permisos e inténtelo de nuevo. |
