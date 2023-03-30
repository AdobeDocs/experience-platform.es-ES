---
title: Mensajes de error del servicio de flujo
description: Obtenga información sobre los mensajes de error que pueden encontrarse al utilizar el servicio de flujo para los orígenes.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Mensajes de error del servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de varias fuentes distintas dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen con varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Este documento proporciona un catálogo de mensajes de error, descripciones y resoluciones sugeridas con respecto al servicio de flujo.

## Errores de validación internos en el servicio de flujo

La siguiente tabla describe los errores relacionados con la validación interna en el servicio de flujo.

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1100-400` | Solicitud no válida | No se pudo procesar la solicitud. Error del proveedor de flujo: No tiene derecho a esta operación. |
| `1101-404` | Recurso no encontrado | No se encuentra el recurso solicitado. Error del proveedor de flujo: El recurso con un id determinado no existe. |
| `1102-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1103-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1104-504` | Tiempo de espera de la puerta de enlace | Se ha producido un tiempo de espera de puerta de enlace. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1400-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1401-400` | Solicitud no válida | Los parámetros de límite y recuento no se pueden proporcionar juntos en la misma solicitud. Proporcione solo el límite o el parámetro de recuento e inténtelo de nuevo. |
| `1402-400` | Solicitud no válida | La acción &quot;finalizar&quot; solo se admite para solicitudes del proveedor. |
| `1403-400` | Falta el encabezado | Falta el encabezado &quot;If-Match&quot; en la solicitud. Proporcione el encabezado e inténtelo de nuevo. |
| `1404-412` | La versión no coincide | La versión suministrada &#39;v1&#39; no coincide con la versión actual de la entidad &#39;cc01fc2c-0000-0200&#39;. Compruebe que la versión proporcionada coincide con la versión actual en la entidad e inténtelo de nuevo. |
| `1405-400` | Solicitud no válida | El cuerpo de la solicitud no puede ser nulo ni estar vacío. Proporcione un cuerpo de solicitud e inténtelo de nuevo. |
| `1406-400` | Solicitud no válida | La suboperación &#39;progress&#39; no se puede aplicar con otras suboperaciones. Actualice la lista de suboperaciones e inténtelo de nuevo. |
| `1407-400` | Solicitud no válida | El estado fallido no se puede usar con la variable `progress` subOp. Elimine el `progress` subOp o utilice status=&#39;inProgress&#39; e inténtelo de nuevo. |
| `1408-400` | Solicitud no válida | El porcentaje completado debe ser 100 para los estados completados o fallidos. Actualice el porcentaje completado e inténtelo de nuevo. |
| `1409-400` | Solicitud no válida | La operación &quot;finalizar&quot; no se puede aplicar en el estado actual habilitado para finalizar. Actualice la operación e inténtelo de nuevo. |
| `1410-400` | Solicitud no válida | `State` no está permitido en la solicitud de creación de flujo. |
| `1411-400` | Solicitud no válida | No se puede recuperar entityId. Solicitud no válida recibida con la ruta &#39;baseConnections/123&#39;. |
| `1412-400` | Solicitud no válida | Versión de asignación no válida en la solicitud. Proporcione la versión de asignación correcta. |
| `1413-400` | Solicitud no válida | El ID de especificación proporcionado no es válido. Proporcione un ID de especificación válido e inténtelo de nuevo. |
| `1414-400` | Solicitud no válida | No se puede actualizar la especificación de conexión de una conexión. |
| `1415-400` | Solicitud no válida | No se encontró la especificación auth &#39;authConnection&#39; para la especificación de conexión id ba6e206f-f233-ab16. |
| `1416-400` | Solicitud no válida | Eliminar o Actualizar solo se puede aplicar en conexión con estado habilitado, deshabilitado o inicializando. |
| `1417-400` | Solicitud no válida | Eliminar o actualizar en conexiones en `initializing` no se permiten con UserToken. |
| `1418-400` | Solicitud no válida | La conexión base con el ID 35dcaad3-122a-4278 no se puede eliminar porque la conexión base se está utilizando en uno o varios flujos. Asegúrese de que los flujos correspondientes se eliminen antes de eliminar una conexión base. |
| `1419-400` | Solicitud no válida | Error al validar la asignación con id 45d90285d2d249acb87a72a2f12f7401, versión 0. Esto puede deberse a permisos inadecuados en los campos asignados. Compruebe la asignación o póngase en contacto con su administrador. |
| `1420-400` | Solicitud no válida | No se puede actualizar el estado actual de desactivación. |
| `1421-400` | Solicitud no válida | La actualización de estado actual no se puede realizar en transición. |
| `1422-400` | Solicitud no válida | La acción disable no se puede aplicar en el estado actual {state}. Actualice la acción e inténtelo de nuevo. |
| `1423-400` | Solicitud no válida | Se proporcionó un campo baseSpec no gestionado en ConnectionSpecFiltering. Actualice el campo {field} e inténtelo de nuevo. |
| `1424-400` | Solicitud no válida | OrderBy no es compatible con la consulta entre entornos limitados. |
| `1425-400` | Solicitud no válida | Error al hacer coincidir el esquema en el conjunto de datos de destino 64ef1a3c0ef con el esquema en la asignación 91ac5a2c0eb. El esquema con el mismo id y la misma versión debe utilizarse tanto en la asignación como en el conjunto de datos de destino. |
| `1426-400` | Solicitud no válida | El token de usuario no tiene autorización para crear o actualizar la especificación de conexión. Asegúrese de que el token de usuario esté autorizado e inténtelo de nuevo. |
| `1427-400` | Solicitud no válida | El token de usuario no tiene autorización para crear o actualizar ejecuciones de flujo. Asegúrese de que el token de usuario esté autorizado e inténtelo de nuevo. |
| `1428-400` | Solicitud no válida | No se ha encontrado la ejecución del flujo del predecesor con el id aa6a206f-f233-4c2d. |
| `1429-400` | Solicitud no válida | No se encuentra el flujo del predecesor con el id aa6a206f-f233-4c2d. |
| `1430-400` | Solicitud no válida | Flujo no encontrado con id aa6a206f-f233-4c2d. |
| `1431-400` | Solicitud no válida | La matriz vacía &quot;campos&quot; no está permitida en la directiva. |
| `1432-400` | Solicitud no válida | El orden de clasificación especificado no es correcto, anteponga + para orden ascendente y - para orden descendente en fieldName. |
| `1433-400` | Solicitud no válida | Campo incorrecto= #id pasado en orderBy, por ejemplo: +nombre, -nombre, nombre. |
| `1434-400` | Solicitud no válida | Se recibió la operación &quot;mover&quot; no admitida. Utilice uno de los tipos de operación compatibles y vuelva a intentarlo. |
| `1435-400` | Solicitud no válida | Subacción &#39;inversa&#39; no admitida. Utilice uno de los tipos de subacciones compatibles y vuelva a intentarlo. |
| `1436-400` | Solicitud no válida | Suboperación no admitida PROGRESS recibida para habilitar la operación. |
| `1437-400` | Solicitud no válida | Se recibió el valor de estado &quot;iniciado&quot; no admitido. Actualice el valor del estado e inténtelo de nuevo. |
| `1438-400` | Solicitud no válida | Se ha recibido un &quot;promedio&quot; de operación agregada no admitida. |
| `1439-400` | Recurso no encontrado | No se encuentra el recurso de flujos 3f4ae131-b384-4e73 solicitado. Compruebe el ID del recurso antes de intentarlo de nuevo. |
| `1440-400` | Solicitud no válida | El operador &#39;~&#39; no está implementado. |
| `1441-400` | Solicitud no válida | La función agregada &quot;average&quot; no está implementada. |
| `1442-400` | Solicitud no válida | Agregación no permitida en el id de campo. |
| `1443-400` | Solicitud no válida | El operador &#39;&lt;=&#39; no está permitido para varios valores. |
| `1444-400` | Solicitud no válida | El flujo 3f4ae131-b384-4e73 no está en estado esperado pendiente. |
| `1445-400` | Solicitud no válida | La función de conexión del PATCH no está habilitada. |
| `1446-400` | Solicitud no válida | El ID de flujo no puede ser nulo ni estar vacío. Actualice el ID de flujo e inténtelo de nuevo. |
| `1447-400` | Solicitud no válida | Se encontraron flujos activos que contenían id aa6a206f-f233-4c2d. |
| `1448-400` | Solicitud no válida | Operator >= no es compatible con el id de campo. |
| `1449-400` | Solicitud no válida | Conexiones de campo no válidas en parámetros de filtro. |
| `1450-400` | Solicitud no válida | Operador no válido> en parámetros de filtro. |
| `1451-400` | Solicitud no válida | Parámetros testParam no válidos proporcionados en parámetros de consulta. |
| `1452-400` | Solicitud no válida | Valor no válido 1676643256,1676643210 para el campo creadoEn. |
| `1453-400` | Solicitud no válida | Valor de consulta no válido creadoAt== proporcionado en el parámetro de consulta. |
| `1454-400` | Solicitud no válida | Se ha proporcionado el tipo de valor de filtro no gestionado. |
| `1455-400` | Solicitud no válida | Se ha producido un error al validar las instrucciones del parche: Falta el campo &quot;keyWhatDoesNotExist&quot;. |
| `1456-400` | Solicitud no válida | La eliminación y finalización de estado no es un valor válido. Los valores permitidos son [habilitado, deshabilitado, inicializar]. |
| `1457-400` | Solicitud no válida | La actualización de la operación no se puede aplicar en la eliminación y finalización del estado. |
| `1458-400` | Solicitud no válida | La eliminación de la operación no se puede aplicar en la eliminación y finalización del estado. |

{style="table-layout:auto"}


## Errores de verificación del token de usuario para la autorización

La siguiente tabla describe los errores relacionados con la verificación del token de usuario para la autorización

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `2000-401` | Token de autorización no válido | El token de autorización no tiene acceso a esta organización o la organización no existe. Asegúrese de que la organización existe o póngase en contacto con el administrador para obtener acceso. |
| `2001-401` | Falta el encabezado o está vacío | Falta el encabezado x-gw-ims-org-id o está vacío. Actualice el valor del encabezado e inténtelo de nuevo. |
| `2002-401` | Falta el encabezado | Falta el encabezado x-gw-ims-org-id en la solicitud. Actualice el valor del encabezado e inténtelo de nuevo. |
| `2100-404` | Espacio aislado no encontrado | No se encontró el simulador para pruebas con el nombre &quot;dev&quot;. Asegúrese de que el nombre del simulador de pruebas sea correcto e inténtelo de nuevo. |
| `2101-404` | Espacio aislado no encontrado | No se encontró el simulador para pruebas con el nombre &quot;dev&quot;. Error de la API de administración de espacio aislado: Espacio aislado con el nombre &quot;dev&quot; no presente. Compruebe si existe algún recurso. |
| `2102-500` | Error al obtener el simulador de pruebas por nombre | Se produjo un problema al recuperar un simulador de pruebas con el nombre &quot;dev&quot;. Error de la API de administración de espacio aislado: Algo salió mal. Inténtelo de nuevo. |
| `2103-404` | Espacio aislado no encontrado | No se encontró el simulador para pruebas con el ID 8da3ef09-b469-404a y el identificador dev. Compruebe que los valores de ID y de nombre del simulador para pruebas son correctos e inténtelo de nuevo. |
| `2104-500` | Obtención de entorno limitado por error de identificador | Hubo un problema al recuperar un simulador para pruebas con el id. &#39;8da3ef09-b469-404a&#39; y el nombre &#39;dev&#39;. Error de la API de administración de espacio aislado: Algo salió mal. Inténtelo de nuevo. |
| `2105-400` | Falta el encabezado | Falta el encabezado x-sandbox-name en la solicitud. Agregue el encabezado en la solicitud e inténtelo de nuevo. |
| `2106-404` | Obtener error de entorno limitado predeterminado | No se encontró la información predeterminada del simulador de pruebas. |
| `2107-500` | Obtener error de entorno limitado predeterminado | Se produjo un problema al recuperar un entorno limitado predeterminado. Error de la API de administración de espacio aislado: Algo salió mal. Inténtelo de nuevo. |
| `2108-500` | Obtener el error de entornos limitados activos | Se produjo un problema al recuperar un simulador de pruebas activo. Error de la API de administración de espacio aislado: Algo salió mal. Inténtelo de nuevo. |
| `2110-400` | Encabezados no permitidos | El encabezado x-sandbox-id no está permitido con el token de usuario. Actualice el encabezado e inténtelo de nuevo. |
| `2111-403` | Encabezados con valor restringido | El encabezado x-sandbox-name con valor * está restringido con el token de usuario. Actualice el encabezado y el valor e inténtelo de nuevo. |
| `2112-400` | Encabezados con un valor diferente no permitido | Los encabezados x-sandbox-name y x-sandbox-id deben tener el valor * para la consulta entre entornos limitados. Actualice los encabezados y vuelva a intentarlo. |
| `2113-400` | Encabezados con valor no permitido | Los encabezados x-sandbox-id y x-sandbox-name con valor * no están permitidos para la solicitud. Actualice los encabezados y vuelva a intentarlo. |
| `2114-400` | Token vacío | Token vacío proporcionado. Proporcione un token e inténtelo de nuevo. |
| `2115-400` | Token no válido | Se proporcionó un token no válido. Proporcione un token válido e inténtelo de nuevo. |
| `2116-500` | Error interno | Se ha producido un error interno durante la descodificación sin conexión del token al portador para la resolución del ámbito. |
| `2117-500` | Error interno | Se ha producido un error interno al comprobar los permisos del usuario. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `2118-403` | Falta permiso | Falta la escritura del permiso. Póngase en contacto con el administrador para resolver los permisos y vuelva a intentarlo. |
| `2119-400` | Falta el parámetro de consulta | El contexto de solicitud no contiene el parámetro de consulta requerido specId. Proporcione el parámetro de consulta que falta e inténtelo de nuevo. |
| `2120-403` | Prohibido | No tiene permisos suficientes para realizar la operación. Póngase en contacto con el administrador para resolver los permisos y vuelva a intentarlo. |
| `2121-403` | Prohibido | El administrador de permisos se niega en el recurso Origen empresarial. Póngase en contacto con el administrador para resolver los permisos y vuelva a intentarlo. |
| `2200-500` | Error de solicitud de servicio externo | Hubo un problema al llamar al servicio Catálogo para validar el esquema. |
| `2250-500` | Error de solicitud de servicio externo | Se produjo un problema al llamar al servicio de preparación de datos para validar la asignación. |

{style="table-layout:auto"}
