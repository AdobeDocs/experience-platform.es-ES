---
title: Administración de datos en Query Service
description: Esta descripción general abarca los principales elementos del control de datos en el servicio de consultas de Experience Platform.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '3129'
ht-degree: 0%

---

# Gobernanza de datos en el servicio de consultas

Adobe Experience Platform reúne datos de varios sistemas empresariales y le permite limpiar, dar forma, manipular y enriquecer los datos mediante el servicio de consultas según sus necesidades. Esto permite a los especialistas en marketing identificar, comprender y atraer a los clientes de una manera mejor. Garantizar una administración adecuada de los datos es un aspecto crítico del tratamiento de la información personal, ya que determinados datos pueden estar sujetos a restricciones de uso basadas en políticas organizativas y regulaciones legales. Es fundamental asegurarse de que los datos ingeridos y sus operaciones relacionadas cumplan con las políticas de uso de datos definidas.

El control de datos dentro del servicio de consulta le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Esto desempeña un papel clave a la hora de garantizar que las políticas de uso se hayan aplicado según las regulaciones definidas por su empresa.

Se recomienda a las organizaciones que realizan el procesamiento de datos de forma rutinaria que describan, practiquen y apliquen estas directrices para crear un entorno con conciencia de privacidad para todos los usuarios.

Las siguientes categorías son fundamentales para cumplir con las regulaciones de cumplimiento de datos al utilizar el servicio de consulta:

1. Seguridad
1. Auditoría
1. Uso de datos
1. Privacidad
1. Higiene de datos

Este documento examina cada una de las diferentes áreas de gobernanza y muestra cómo facilitar el cumplimiento de los datos al utilizar el servicio de consulta. Consulte [información general sobre administración, privacidad y seguridad](../../landing/governance-privacy-security/overview.md) para obtener información más amplia sobre cómo Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las normas.

## Seguridad {#security}

La seguridad de los datos es el proceso de proteger los datos contra el acceso no autorizado y garantizar un acceso seguro durante todo su ciclo de vida. El acceso seguro se mantiene en Experience Platform mediante la aplicación de funciones y permisos mediante funciones como el control de acceso basado en funciones y el control de acceso basado en atributos. Las credenciales, SSL y el cifrado de datos también se utilizan para garantizar la protección de datos en Platform.

La seguridad con respecto al servicio de consultas se divide en las siguientes categorías:

* [Control de acceso](#access-control): el acceso se controla mediante funciones y permisos que incluyen permisos de nivel de columna y conjunto de datos.
* Proteger datos mediante [conectividad](#connectivity): Los datos se protegen mediante Platform y clientes externos si se logra una conexión limitada con credenciales que caducan o credenciales que no caducan.
* Protección de datos mediante [cifrado y claves administradas por el cliente (CMK)](#encryption-and-customer-managed-keys): el acceso se controla mediante cifrado cuando los datos están en reposo.

### Control de acceso {#access-control}

El control de acceso en Adobe Experience Platform le permite usar [Adobe Admin Console](https://adminconsole.adobe.com/) para administrar el acceso a las características del servicio de consultas mediante permisos basados en funciones. Del mismo modo, se puede controlar el acceso a atributos de datos específicos mediante la administración de etiquetas en esquemas y campos de datos.

En esta sección se describen los permisos de control de acceso necesarios que debe tener un usuario para utilizar completamente las funciones del servicio de consulta. Consulte los documentos sobre [administración de permisos](../../access-control/ui/permissions.md) y [administración de usuarios](../../access-control/ui/users.md) para obtener instrucciones detalladas sobre cómo asignar acceso a un perfil de producto.

#### Permisos relevantes

Los permisos de control de acceso relevantes se definen en las tablas siguientes según su nivel de ámbito.

**Permisos de ejecución de consultas**

Para ejecutar consultas en el servicio de consultas, se debe asignar a un usuario una función con el siguiente permiso:

| Permiso | Descripción |
|---|---|
| [!UICONTROL Administrar consultas] | Este permiso permite a los usuarios ejecutar consultas de exploración de datos y consultas por lotes, que pueden leer un conjunto de datos existente o escribir datos en conjuntos de datos. Esto incluye consultas `CREATE TABLE AS SELECT` (`CTAS`) y `INSERT INTO AS SELECT` (`ITAS`). |

**Permisos de conjuntos de datos**

Esta sección sirve como guía para el acceso basado en recursos necesario para acceder a los conjuntos de datos al consultar datos a través del servicio de consulta.

A través de la interfaz Permisos, puede definir el control de acceso basado en recursos para un conjunto de datos y esquema con los siguientes permisos:

| Permiso | Descripción |
|---|---|
| [!UICONTROL Administrar conjuntos de datos] | Este permiso proporciona acceso de solo lectura a los esquemas y permite leer, crear, editar y eliminar conjuntos de datos para su uso con el servicio de consultas. |
| [!UICONTROL Ver conjuntos de datos] | Este permiso permite el acceso de solo lectura para conjuntos de datos y esquemas para su uso con el servicio de consulta. |

#### Control de acceso para columnas/campos

La función de control de acceso basado en atributos permite a los usuarios del servicio de consultas restringir el acceso a datos de usuario críticos. El acceso se puede conceder o restringir según los permisos asignados a una función. El acceso de los usuarios a columnas individuales está controlado por las etiquetas de uso de datos relevantes y los conjuntos de permisos aplicados a las funciones asignadas a los usuarios.

Al etiquetar grupos y clases de campos de esquema con etiquetas de uso de datos, se aplican restricciones de uso de datos a todos los esquemas con los mismos grupos de campos y clases. Consulte la descripción general de [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener información completa sobre esta característica.

Esta función le permite conceder derechos de acceso sobre columnas confidenciales a los grupos de usuarios que elija. El control de acceso de una columna puede restringir las capacidades de lectura y escritura de un tipo concreto de usuario.

El control de acceso para columnas se puede aplicar en el nivel de esquema para esquemas estándar y ad hoc. Aplique etiquetas de uso de datos a esquemas XDM para restringir el acceso a una o más columnas. El etiquetado de datos se aplica de forma coherente, incluso para conjuntos de datos creados mediante el servicio de consultas utilizando un esquema predefinido o un esquema ad hoc generado como parte de la operación CTAS.

Una vez que se ha aplicado el nivel de acceso adecuado mediante etiquetas y funciones, se produce el siguiente comportamiento del sistema cuando un usuario intenta acceder a los datos no accesibles:

1. Si se ha denegado a un usuario el acceso a una de las columnas de un esquema, también se deniega al usuario el permiso para leer o escribir en la columna restringida. Esto se aplica a los siguientes escenarios comunes:

   * **Caso 1**: Cuando un usuario intenta ejecutar una consulta que afecta solamente a una columna restringida, el sistema genera un error que indica que la columna no existe.
   * **Caso 2**: Cuando un usuario intenta ejecutar una consulta con varias columnas, incluida una columna restringida, el sistema devuelve únicamente el resultado de todas las columnas no restringidas.

1. Si un usuario intenta acceder a un campo calculado, debe tener acceso a todos los campos utilizados en la composición o el sistema también deniega el acceso al campo calculado.

#### Controles de acceso para vistas

El servicio de consultas proporciona la capacidad de usar ANSI SQL estándar para instrucciones [`CREATE VIEW`](../sql/syntax.md#create-view). Para flujos de trabajo de datos muy confidenciales, debe aplicar los controles adecuados al crear vistas.

La palabra clave `CREATE VIEW` define una vista de una consulta, pero la vista no se materializa físicamente. En su lugar, la consulta se ejecuta cada vez que se hace referencia a la vista en una consulta. Cuando un usuario crea una vista a partir de un conjunto de datos, las reglas de control de acceso basadas en roles y atributos para el conjunto de datos principal se aplican **no** jerárquicamente. Como resultado, debe establecer explícitamente permisos en cada una de las columnas cuando se cree una vista.

#### Crear restricciones de acceso basadas en el campo en conjuntos de datos acelerados {#create-field-based-access-restrictions-on-accelerated-datasets}

Con la [capacidad de control de acceso basada en atributos](../../access-control/abac/overview.md), puede definir ámbitos organizativos o de uso de datos en conjuntos de datos de hechos y dimensiones en el [almacén acelerado](../data-distiller/sql-insights/send-accelerated-queries.md). Esto permite a los administradores administrar el acceso a segmentos específicos y administrar mejor el acceso dado a usuarios o grupos de usuarios.

Para crear restricciones de acceso basadas en campos en conjuntos de datos acelerados, puede utilizar consultas CTAS del servicio de consulta para crear conjuntos de datos acelerados y estructurarlos en función de esquemas XDM o esquemas ad hoc existentes. Los administradores pueden [agregar y editar etiquetas de uso de datos para el esquema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) o [esquema ad hoc](./ad-hoc-schema-labels.md#edit-governance-labels). Puede aplicar, crear y editar etiquetas a sus esquemas desde el área de trabajo [!UICONTROL Etiquetas] en la interfaz de usuario de [!UICONTROL Esquemas].

Las etiquetas de uso de datos también se pueden [aplicar o editar directamente en el conjunto de datos](../../data-governance/labels/user-guide.md#add-labels) a través de la interfaz de usuario de conjuntos de datos, o crear desde el área de trabajo de control de acceso [!UICONTROL Etiquetas]. Consulte la guía sobre cómo [crear una etiqueta nueva](../../access-control/abac/ui/labels.md) para obtener más información.

El acceso de los usuarios a columnas individuales se puede controlar mediante las etiquetas de uso de datos adjuntas y los conjuntos de permisos aplicados a las funciones asignadas a los usuarios.

### Conectividad {#connectivity}

Se puede acceder al servicio de consultas a través de la interfaz de usuario de Platform o formando una conexión con clientes compatibles externos. El acceso a todos los frentes disponibles se controla mediante un conjunto de credenciales.

#### Conectividad a través de clientes externos

El acceso al servicio de consultas mediante un cliente de terceros requiere credenciales de autorización. Estas credenciales son obligatorias para acceder al servicio de consulta con cualquiera de los clientes externos compatibles. Puede conectarse a clientes externos usando [credenciales que caducan](#expiring-credentials) o [credenciales que no caducan](#non-expiring-credentials).

#### Tiempo de conexión limitado mediante credenciales que caducan {#expiring-credentials}

[Las credenciales caducan](../ui/credentials.md) y permiten a los usuarios formar una conexión temporal con un cliente externo. Este conjunto de credenciales solo es válido durante 24 horas. La caducidad de estos tipos de credenciales se puede ver junto con la pestaña de credenciales en el panel del servicio de consulta.

![Se ha resaltado la ficha de credenciales en el área de trabajo del servicio de consultas con credenciales que caducan.](../images/data-governance/overview/expiring-credentials.png)

#### Credenciales que no caducan {#non-expiring-credentials}

[Las credenciales que no caducan](../ui/credentials.md#non-expiring-credentials) le permiten formar una conexión permanente con un cliente externo, lo que facilita la conexión al servicio de consultas sin necesidad de una contraseña manual.

Para habilitar la opción de generar credenciales que no caduquen, debe seguir el [flujo de trabajo de requisitos previos](../ui/credentials.md#prerequisites) descrito. Como parte de este proceso, el administrador de la organización debe configurar permisos para el perfil del producto, lo que permite al administrador controlar qué cuentas tienen acceso para utilizar credenciales que no caducan.

Se pueden asignar funciones a las cuentas de usuario técnicas permitidas con credenciales que no caducan para garantizar un control de datos adecuado definiendo el ámbito de su acceso de lectura y escritura en función de sus responsabilidades y necesidades. Consulte la sección anterior sobre [uso de permisos basados en roles mediante el control de acceso](#access-control) para administrar el acceso al servicio de consultas.

Una vez completado el flujo de trabajo de requisitos previos, los usuarios autorizados ahora pueden [generar las credenciales de conexión necesarias](../ui/credentials.md#generate-credentials).

#### Cifrado de datos SSL

Para aumentar la seguridad, el servicio de consultas proporciona compatibilidad nativa con conexiones SSL para cifrar las comunicaciones cliente/servidor. Platform admite varias opciones SSL para satisfacer sus necesidades de seguridad de datos y equilibrar la sobrecarga de procesamiento del cifrado y el intercambio de claves.

Consulte la guía sobre las [opciones SSL disponibles para conexiones de clientes de terceros al servicio de consultas](../clients/ssl-modes.md) para obtener más información, incluido cómo conectarse mediante el valor del parámetro SSL `verify-full`.

### Cifrado y claves administradas por el cliente (CMK) {#encryption-and-customer-managed-keys}

El cifrado es el uso de un proceso algorítmico para transformar datos en texto codificado e ilegible para garantizar que la información esté protegida e inaccesible sin una clave de descifrado.

El cumplimiento de los datos del servicio de consultas garantiza que los datos siempre estén cifrados. Los datos en tránsito siempre son compatibles con HTTPS y los datos en reposo se cifran en un almacén de Azure Data Lake mediante claves de sistema. Consulte la documentación sobre [cómo se cifran los datos en Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md) para obtener más información. Para obtener detalles sobre cómo se cifran los datos en reposo en Azure Data Lake Storage, consulte la [documentación oficial de Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

Los datos en tránsito siempre son compatibles con HTTPS y, de manera similar, cuando los datos están en reposo en el lago de datos, el cifrado se realiza con la clave de administración del cliente (CMK), que ya es compatible con la administración de lago de datos. La versión admitida actualmente es TLS1.2. Consulte la [documentación de claves administradas por el cliente (CMK)](../../landing/governance-privacy-security/customer-managed-keys/overview.md) para obtener información sobre cómo configurar sus propias claves de cifrado para los datos almacenados en Adobe Experience Platform.


## Auditoría {#audit}

El servicio de consulta registra la actividad del usuario y clasifica esa actividad en diferentes tipos de registro. Los registros proporcionan información sobre **quién** realizó **qué** acción y **cuándo**. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción.

Un usuario de Platform puede solicitar cualquiera de las categorías de registro. Esta sección proporciona detalles sobre el tipo de información capturada para el servicio de consultas y dónde se puede acceder a esta información.

### Registros de consultas {#query-logs}

La interfaz de usuario de registros de consultas permite supervisar y revisar los detalles de ejecución de todas las consultas que se han ejecutado mediante el Editor de consultas o la API del servicio de consultas. Esto aporta transparencia a las actividades del Servicio de consultas, lo que le permite comprobar los metadatos de **todas** las consultas que se han ejecutado en el Servicio de consultas. Incluye todos los tipos de consultas, ya sean exploratorias, por lotes o programadas.

Se puede acceder a los registros de consultas a través de la IU de Platform en la pestaña [!UICONTROL Registros] del área de trabajo [!UICONTROL Consultas].

![Pestaña Registro de consultas con el panel de detalles resaltado.](../images/data-governance/overview/queries-log.png)

### Registros de auditoría {#audit-logs}

Los registros de auditoría contienen información más detallada que los registros de consulta y permiten filtrar registros en función de atributos como usuario, fecha, tipo de consulta, etc. Más allá de los detalles disponibles en la IU del registro de consultas, los registros de auditoría almacenan detalles de usuarios individuales junto con sus datos de sesión o conectividad con un cliente de terceros.

Al proporcionar un registro exacto de las acciones de los usuarios, una pista de auditoría puede ayudar a solucionar problemas y ayudar a su empresa a cumplir de forma eficaz con las políticas de administración de datos corporativos y los requisitos regulatorios. Los registros de auditoría proporcionan un registro de todas las actividades de la plataforma. Mediante los registros de auditoría puede auditar las acciones de los usuarios relacionadas con la ejecución de consultas, las plantillas y las consultas programadas para aumentar la transparencia y la visibilidad de las acciones realizadas por los usuarios en el servicio de consultas.

La siguiente tabla indica las categorías de consultas capturadas por los registros de auditoría y los tipos de acciones que registran:

| Categoría | Tipo de acción |
|---|---|
| Consulta | Ejecutar |
| Plantilla de consulta | Crear, eliminar, actualizar |
| Consulta programada | Crear, eliminar, actualizar |

A continuación se muestra una lista de tres registros de servidor extendidos que contienen más detalles que los que se encuentran dentro de los registros de consulta. Los registros extendidos se encuentran dentro de las categorías de consulta de registros de auditoría:

1. **Registros de metaconsultas**: cuando se ejecuta una consulta, se ejecutan varias subconsultas de backend asociadas (como el análisis). Estos tipos de consultas se conocen como consultas de &quot;metadatos&quot;. Sus detalles relevantes se pueden encontrar en los registros de auditoría.
1. **Registros de sesión**: el sistema crea un registro de entrada de sesión para un usuario cuando inicia sesión en el Servicio de consultas, independientemente de si ejecuta o no una consulta.
1. **Registros de conexión de cliente de terceros**: se genera un registro de auditoría de conectividad cuando un usuario conecta correctamente el servicio de consultas a un cliente de terceros.

Consulte la [descripción general de los registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md) para obtener más información sobre cómo los registros de auditoría pueden ayudar a su organización a cumplir con los datos.

## Uso de datos {#data-usage}

El marco de trabajo de control de datos de Platform proporciona una forma uniforme de utilizar los datos de forma responsable en todas las soluciones de Adobe, servicios y plataformas. Coordina el enfoque sistémico para capturar, comunicar y utilizar metadatos en toda la Adobe Experience Cloud. Esto, a su vez, ayuda a los responsables del tratamiento de datos a etiquetar los datos según las acciones de marketing necesarias y las restricciones impuestas a esos datos por estas acciones de marketing previstas. Consulte la descripción general de [etiquetas de uso de datos](../../data-governance/labels/overview.md) para obtener más información sobre cómo el control de datos le permite aplicar etiquetas de uso de datos a conjuntos de datos y campos.

Se recomienda trabajar para que los datos cumplan los requisitos en cada fase del recorrido de los datos. Para ello, los conjuntos de datos derivados que utilizan esquemas ad hoc deben etiquetarse adecuadamente como parte del marco de trabajo de control de datos. Existen dos tipos de conjuntos de datos derivados formados por el servicio de consulta: conjuntos de datos que utilizan un esquema estándar y conjuntos de datos que utilizan un esquema ad hoc.

>[!NOTE]
>
>Los conjuntos de datos que se crean mediante el servicio de consultas se denominan &quot;conjuntos de datos derivados&quot;.

Dado que un usuario individual crea esquemas ad hoc para un propósito específico, los campos de esquema XDM tienen un espacio de nombres para ese conjunto de datos en particular y no están pensados para su uso en diferentes conjuntos de datos. Como resultado, los esquemas ad hoc no son visibles de forma predeterminada en la interfaz de usuario de Experience Platform. Aunque no hay diferencia en la aplicación de etiquetas de uso de datos entre esquemas estándar y ad hoc, los esquemas ad hoc creados por el servicio de consultas con el fin de etiquetar deben hacerse visibles primero en la interfaz de usuario de Platform. Consulte la guía sobre [descubrimiento de esquemas ad hoc en la interfaz de usuario de Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) para obtener más información.

Una vez que haya obtenido acceso al esquema, puede [aplicar etiquetas a campos individuales](../../xdm/tutorials/labels.md). Una vez etiquetado un esquema, todos los conjuntos de datos que se derivan de él heredan esas etiquetas. Desde aquí, puede configurar políticas de uso de datos que puedan restringir la activación de datos con determinadas etiquetas a determinados destinos. Para obtener más información, consulte la descripción general de [políticas de uso de datos](../../data-governance/policies/overview.md).

## Privacidad {#privacy}

[Privacy Service](../../privacy-service/home.md) le ayuda a administrar las solicitudes de los clientes para acceder a sus datos y eliminarlos de acuerdo con las normas legales de privacidad. Para ello, busca en los datos identificadores preexistentes y accede a esos datos o los elimina en función del trabajo de privacidad solicitado. Los datos deben etiquetarse correctamente para que el servicio determine a qué campos acceder o eliminar durante los trabajos de privacidad. Los datos sujetos a solicitudes de privacidad deben contener información de identidad del cliente para vincular los distintos fragmentos de datos con la persona individual a la que se aplica la solicitud de privacidad. El servicio de consultas puede enriquecer los datos que utiliza con un identificador único para satisfacer los trabajos de privacidad.

Las solicitudes de privacidad se pueden enviar al lago de datos o al almacén de datos de perfil. Los registros eliminados del lago de datos no provocan la eliminación de perfiles realizados desde esos registros. Además, un trabajo de privacidad para eliminar información personal del lago de datos no elimina su perfil, por lo que cualquier información (que contenga ese ID de perfil) ingerida después de la finalización del trabajo de privacidad actualiza ese perfil con normalidad. Esto reafirma la necesidad de identificar correctamente los datos utilizados en esquemas específicos.

Consulte la documentación del Privacy Service para obtener más información sobre [datos de identidad para solicitudes de privacidad](../../privacy-service/identity-data.md) y cómo configurar las operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad del cliente.

Las funciones del servicio de consulta para el control de datos simplifican y optimizan el proceso de categorización de datos y el cumplimiento de las regulaciones de uso de datos. Una vez identificados los datos, el servicio de consultas permite asignar la identidad principal en todos los conjuntos de datos de salida. Usted **debe** agregar identidades al conjunto de datos para facilitar las solicitudes de privacidad de datos y trabajar en pos del cumplimiento de los datos.

Los campos de datos de esquema se pueden establecer como un campo de identidad a través de la interfaz de usuario de Platform y el servicio de consulta también le permite [marcar las identidades principales mediante el comando SQL &#39;ALTER TABLE&#39;](../sql/syntax.md#alter-table). La configuración de una identidad mediante el comando `ALTER TABLE` resulta especialmente útil cuando los conjuntos de datos se crean mediante SQL en lugar de hacerlo directamente desde un esquema a través de la IU de Platform. Consulte la documentación para obtener instrucciones sobre cómo [definir campos de identidad en la interfaz de usuario](../../xdm/ui/fields/identity.md) al utilizar esquemas estándar.

## Higiene de datos {#data-hygiene}

La &quot;higiene de los datos&quot; se refiere al proceso de reparación o eliminación de datos que pueden estar obsoletos, ser inexactos, tener un formato incorrecto, estar duplicados o ser incompletos. Estos procesos garantizan que los conjuntos de datos sean precisos y coherentes en todos los sistemas. Es importante garantizar una higiene de los datos adecuada en cada paso del recorrido de los datos e incluso desde la ubicación inicial de almacenamiento de datos. En el servicio de consultas de Experience Platform, se trata del lago de datos o del almacén acelerado.

Puede asignar una identidad a un conjunto de datos derivado para permitir su administración de datos siguiendo los servicios centralizados de higiene de datos de Platform.

Por el contrario, cuando se crea un conjunto de datos agregado en el almacén acelerado, los datos agregados no se pueden utilizar para derivar los datos originales. Como resultado de esta agregación de datos, se elimina la necesidad de aumentar las solicitudes de higiene de los datos.

Una excepción a este escenario es el caso de la eliminación. Si se solicita una eliminación de higiene de datos en un conjunto de datos y antes de que se complete la eliminación, se ejecuta otra consulta de conjunto de datos derivado, entonces el conjunto de datos derivado capturará información del conjunto de datos original. En este caso, debe tener en cuenta que si se ha enviado una solicitud para eliminar un conjunto de datos, no debe ejecutar ninguna consulta de conjunto de datos recién derivada utilizando el mismo origen de conjunto de datos.

Consulte la [descripción general de la higiene de los datos](../../hygiene/home.md) para obtener más información sobre la higiene de los datos en Adobe Experience Platform.
