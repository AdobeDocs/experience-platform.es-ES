---
title: Mensajes de error de Flow Service
description: Obtenga información acerca de los mensajes de error que pueden surgir al utilizar Flow Service para las fuentes.
exl-id: af79c547-25d0-459a-8de7-eb14206a8694
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 35%

---

# Mensajes de error de Flow Service

Flow Service se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen a varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Este documento proporciona un catálogo de mensajes de error, descripciones y resoluciones sugeridas con respecto a Flow Service.

## Errores de validación interna en Flow Service

La siguiente tabla describe los errores relacionados con la validación interna en Flow Service.

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `1100-400` | Solicitud no válida | No se ha podido procesar la solicitud. Error del proveedor de flujo: no tiene derecho a esta operación. |
| `1101-404` | Recurso no encontrado | No se ha encontrado el recurso solicitado. Error del proveedor de flujo: El recurso con el ID proporcionado no existe. |
| `1102-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1103-503` | Servicio no disponible | El servicio no está disponible temporalmente. Inténtelo nuevamente más tarde. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1104-504` | Se ha agotado el tiempo de espera de la puerta de enlace | Se ha producido un tiempo de espera de la puerta de enlace. Inténtelo nuevamente más tarde. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1400-500` | Error interno | Se ha producido un error interno. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `1401-400` | Solicitud no válida | Los parámetros limit y count no se pueden combinar en la misma solicitud. Proporcione únicamente uno e inténtelo de nuevo. |
| `1402-400` | Solicitud no válida | La acción &quot;finalizar&quot; solo se admite para solicitudes de proveedor. |
| `1403-400` | Falta el encabezado | Falta el encabezado &quot;If-Match&quot; en la solicitud. Proporcione el encabezado e inténtelo de nuevo. |
| `1404-412` | Versión no coincidente | La versión &quot;v1&quot; proporcionada no coincide con la versión actual en la entidad &quot;cc01fc2c-0000-0200&quot;. Asegúrese de que la versión proporcionada coincida con la versión actual en la entidad e inténtelo de nuevo. |
| `1405-400` | Solicitud no válida | El cuerpo de la solicitud no puede ser nulo ni estar vacío. Proporcione un cuerpo de solicitud e inténtelo de nuevo. |
| `1406-400` | Solicitud no válida | La suboperación &quot;en curso&quot; no se puede aplicar con otras suboperaciones. Actualice la lista de suboperaciones e inténtelo de nuevo. |
| `1407-400` | Solicitud no válida | No se puede usar el estado con la operación secundaria `progress`. Elimine la operación secundaria `progress` o use el estado=&#39;en curso&#39; e inténtelo de nuevo. |
| `1408-400` | Solicitud no válida | El porcentaje completado debe ser 100 para los estados Completado o Error. Actualice el porcentaje e inténtelo de nuevo. |
| `1409-400` | Solicitud no válida | La operación &#39;finalize&#39; no se puede aplicar en el estado actual habilitado-finalizando. Actualice la operación e inténtelo de nuevo. |
| `1410-400` | Solicitud no válida | `State` no está permitido en la solicitud de creación de flujo. |
| `1411-400` | Solicitud no válida | No se puede recuperar entityId. Solicitud no válida recibida con la ruta &#39;baseConnections/123&#39;. |
| `1412-400` | Solicitud no válida | Versión de Mapping no válida en la solicitud. Proporcione la versión de mapping correcta. |
| `1413-400` | Solicitud no válida | La ID de especificación proporcionada no es válida. Proporcione un ID de especificación válido e inténtelo de nuevo. |
| `1414-400` | Solicitud no válida | No se puede actualizar la especificación de conexión de una conexión. |
| `1415-400` | Solicitud no válida | No se ha encontrado la especificación de autenticación &quot;authConnection&quot; para la ID de especificación de conexión ba6e206f-f233-ab16. |
| `1416-400` | Solicitud no válida | Eliminar o Actualizar solo se puede aplicar en una conexión que tenga el estado habilitado, deshabilitado o inicializándose. |
| `1417-400` | Solicitud no válida | No se permite eliminar o actualizar conexiones en estado `initializing` con UserToken. |
| `1418-400` | Solicitud no válida | No se puede eliminar la conexión base con el ID 35dcaad3-122a-4278 porque la conexión base se está utilizando en uno o más flujos. Asegúrese de que los flujos correspondientes se eliminen antes de eliminar una conexión base. |
| `1419-400` | Solicitud no válida | Error al validar la asignación con ID 45d90285d2d249acb87a72a2f12f7401, versión 0. Esto puede deberse a permisos inadecuados en los campos asignados. Compruebe su asignación o póngase en contacto con el administrador. |
| `1420-400` | Solicitud no válida | No se puede actualizar el estado actual de deshabilitación. |
| `1421-400` | Solicitud no válida | La actualización del estado actual no puede ser transicional. |
| `1422-400` | Solicitud no válida | No se puede aplicar la acción deshabilitada en el estado actual {state}. Actualice la acción e inténtelo de nuevo. |
| `1423-400` | Solicitud no válida | Se ha proporcionado un campo baseSpec no controlado en ConnectionSpecFiltering. Actualice el campo {field} e inténtelo de nuevo. |
| `1424-400` | Solicitud no válida | OrderBy no es compatible con la consulta entre zonas protegidas. |
| `1425-400` | Solicitud no válida | Error al hacer coincidir el esquema del conjunto de datos de destino 64ef1a3c0ef con el esquema de la asignación 91ac5a2c0eb. Se debe utilizar un esquema con el mismo ID y versión tanto en la asignación como en el conjunto de datos de destino. |
| `1426-400` | Solicitud no válida | El token de usuario no tiene autorización para crear o actualizar la especificación de conexión. Asegúrese de que el token de usuario tenga autorización e inténtelo de nuevo. |
| `1427-400` | Solicitud no válida | El token de usuario no está autorizado para crear/actualizar ejecuciones de flujo. Asegúrese de que esté autorizado e inténtelo de nuevo. |
| `1428-400` | Solicitud no válida | No se ha encontrado la ejecución del flujo de predecesoras con el ID aa6a206f-f233-4c2d. |
| `1429-400` | Solicitud no válida | No se ha encontrado el flujo de la predecesora con el ID aa6a206f-f233-4c2d. |
| `1430-400` | Solicitud no válida | Flujo no encontrado con el ID aa6a206f-f233-4c2d. |
| `1431-400` | Solicitud no válida | No se permite &#39;fields&#39; de matriz vacía en la directiva. |
| `1432-400` | Solicitud no válida | El orden especificado no es correcto, anteponga + para un orden ascendente y - para un orden descendente en fieldName. |
| `1433-400` | Solicitud no válida | Campo incorrecto= #id se ha pasado en orderBy; por ejemplo, +name, -name, name. |
| `1434-400` | Solicitud no válida | Se ha recibido la operación no compatible &#39;mover&#39;. Utilice uno de los tipos de operación admitidos e inténtelo de nuevo. |
| `1435-400` | Solicitud no válida | Se ha recibido una subacción &#39;inversa&#39; no admitida. Utilice uno de los tipos de subacciones admitidos e inténtelo de nuevo. |
| `1436-400` | Solicitud no válida | Se ha recibido un PROGRESO de suboperación no compatible para la operación habilitar. |
| `1437-400` | Solicitud no válida | Se ha recibido el valor de estado no admitido &quot;iniciado&quot;. Actualice el valor del estado e inténtelo de nuevo. |
| `1438-400` | Solicitud no válida | Se ha recibido una operación agregada no admitida &#39;promedio&#39;. |
| `1439-400` | Recurso no encontrado | No se ha encontrado el recurso de flujos solicitado 3f4ae131-b384-4e73. Compruebe el ID del recurso antes de intentarlo de nuevo. |
| `1440-400` | Solicitud no válida | Operador &#39;~&#39; no implementado. |
| `1441-400` | Solicitud no válida | Función de agregado &#39;average&#39; no implementada. |
| `1442-400` | Solicitud no válida | No se permite la agregación en el ID de campo. |
| `1443-400` | Solicitud no válida | El operador &#39;&lt;=&#39; no se permite para varios valores. |
| `1444-400` | Solicitud no válida | El flujo 3f4ae131-b384-4e73 no está en el estado esperado pendiente. |
| `1445-400` | Solicitud no válida | Funcionalidad de conexión PATCH no habilitada. |
| `1446-400` | Solicitud no válida | El ID de flujo no puede ser nulo ni estar vacío. Actualice el ID de flujo e inténtelo de nuevo. |
| `1447-400` | Solicitud no válida | Se han encontrado flujos activos que contienen el ID aa6a206f-f233-4c2d. |
| `1448-400` | Solicitud no válida | Operador >= no compatible con el ID de campo. |
| `1449-400` | Solicitud no válida | Conexiones de campo no válidas en los parámetros de filtro. |
| `1450-400` | Solicitud no válida | Operador no válido.> en parámetros de filtro. |
| `1451-400` | Solicitud no válida | Parámetros no válidos testParam proporcionados en los parámetros de consulta. |
| `1452-400` | Solicitud no válida | Valor no válido 1676643256,1676643210 para el campo createdAt. |
| `1453-400` | Solicitud no válida | Valor de consulta createdAt== proporcionado en el parámetro de consulta no válido. |
| `1454-400` | Solicitud no válida | Se ha proporcionado un tipo de valor de filtro no controlado. |
| `1455-400` | Solicitud no válida | Se ha producido un error al validar las instrucciones de parche: Falta el campo &quot;keyWhatDoesNotExist&quot;. |
| `1456-400` | Solicitud no válida | La eliminación-finalización del estado no es un valor válido. Los valores permitidos son [enabled, disabled, initializing]. |
| `1457-400` | Solicitud no válida | No se puede aplicar la actualización de operación en estado delete-finalize. |
| `1458-400` | Solicitud no válida | La eliminación de la operación no se puede aplicar en estado delete-finalize. |

{style="table-layout:auto"}


## Errores de verificación del token de usuario para la autorización

La siguiente tabla describe los errores relacionados con la verificación del token de usuario para la autorización

| Código de error | Título | Mensaje detallado |
| --- | --- | --- |
| `2000-401` | Token de autorización no válido | El token de autorización no tiene acceso a esta organización o la organización no existe. Asegúrese de que la organización existe o póngase en contacto con el administrador para obtener acceso. |
| `2001-401` | Falta el encabezado o está vacío | Falta el encabezado x-gw-ims-org-id o está vacío. Actualice el valor del encabezado e inténtelo de nuevo. |
| `2002-401` | Falta el encabezado | Falta el encabezado x-gw-ims-org-id en la solicitud. Actualice el valor del encabezado e inténtelo de nuevo. |
| `2100-404` | Zona protegida no encontrada | No se ha encontrado la zona protegida con el nombre &quot;dev&quot;. Asegúrese de que el nombre de la zona protegida sea correcto e inténtelo de nuevo. |
| `2101-404` | Zona protegida no encontrada | No se ha encontrado la zona protegida con el nombre &quot;dev&quot;. Error de la API de administración de zona protegida: La zona protegida con el nombre &quot;dev&quot; no está presente. Compruebe si el recurso existe. |
| `2102-500` | Error de obtención de zona protegida por nombre | Se ha producido un error al recuperar una zona protegida con el nombre &quot;dev&quot;. Error de la API de administración de zona protegida: Se ha producido un error. Inténtelo de nuevo. |
| `2103-404` | Zona protegida no encontrada | No se ha encontrado la zona protegida con ID 8da3ef09-b469-404a y el nombre dev. Asegúrese de que los valores de ID y nombre de la zona protegida sean correctos e inténtelo de nuevo. |
| `2104-500` | Error de obtención de zona protegida por identificador | Se ha producido un error al recuperar una zona protegida con ID &#39;8da3ef09-b469-404a&#39; y nombre &#39;dev&#39;. Error de la API de administración de zona protegida: Se ha producido un error. Inténtelo de nuevo. |
| `2105-400` | Falta el encabezado | Falta el encabezado x-sandbox-name en la solicitud. Agregue el encabezado a la solicitud e inténtelo de nuevo. |
| `2106-404` | Error al obtener zona protegida predeterminada | No se encontró la información predeterminada de la zona protegida. |
| `2107-500` | Error al obtener zona protegida predeterminada | Se ha producido un error al recuperar una zona protegida predeterminada. Error de la API de administración de zona protegida: Se ha producido un error. Inténtelo de nuevo. |
| `2108-500` | Error al obtener zona protegida activa | Error al recuperar una zona protegida activa. Error de la API de administración de zona protegida: Se ha producido un error. Inténtelo de nuevo. |
| `2110-400` | Encabezados no permitidos | El encabezado x-sandbox-id no se permite con el token de usuario. Actualice el encabezado e inténtelo de nuevo. |
| `2111-403` | Encabezados con valor restringido | El encabezado x-sandbox-name con valor * está restringido con el token de usuario. Actualice el encabezado y el valor e inténtelo de nuevo. |
| `2112-400` | No se permiten encabezados con valores diferentes | Los encabezados x-sandbox-name y x-sandbox-id deben tener el valor * para la consulta entre zonas protegidas. Actualice los encabezados e inténtelo de nuevo. |
| `2113-400` | Encabezados con valor no permitido | Los encabezados x-sandbox-id y x-sandbox-name con valor * no están permitidos para la solicitud. Actualice los encabezados e inténtelo de nuevo. |
| `2114-400` | Token vacío | Token vacío proporcionado. Proporcione un token e inténtelo de nuevo. |
| `2115-400` | Token no válido | Token proporcionado no válido. Proporcione un token válido e inténtelo de nuevo. |
| `2116-500` | Error interno | Se ha producido un error interno durante la descodificación sin conexión del token de portador para la resolución del ámbito. |
| `2117-500` | Error interno | Se ha producido un error interno al comprobar los permisos del usuario. Inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `2118-403` | Falta el permiso | Falta la escritura con permiso. Póngase en contacto con el administrador para resolver los permisos e inténtelo de nuevo. |
| `2119-400` | Falta el parámetro de consulta | El contexto de la solicitud no contiene el parámetro de consulta specId requerido. Proporcione el parámetro de consulta que falta e inténtelo de nuevo. |
| `2120-403` | Prohibido | No tiene permisos suficientes para llevar a cabo la operación. Póngase en contacto con el administrador para resolver los permisos e inténtelo de nuevo. |
| `2121-403` | Prohibido | El administrador de permisos se ha denegado en el recurso Enterprise Source. Póngase en contacto con el administrador para resolver los permisos e inténtelo de nuevo. |
| `2200-500` | Error de solicitud de servicio externo | Se ha producido un problema al llamar al servicio de catálogo para validar el esquema. |
| `2250-500` | Error de solicitud de servicio externo | Se ha producido un problema al llamar al servicio de preparación de datos para validar la asignación. |

{style="table-layout:auto"}
