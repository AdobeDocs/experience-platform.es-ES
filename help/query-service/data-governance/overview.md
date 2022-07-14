---
title: Control de datos en el servicio de consulta
description: Esta descripción general abarca los principales elementos del control de datos en el servicio de consulta de Experience Platform.
feature: Data Governance
source-git-commit: ec063a0f5600729d3575f98898ade04443f29f2a
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 0%

---

# Control de datos en el servicio de consulta

Adobe Experience Platform reúne los datos de varios sistemas empresariales y le permite limpiar, moldear, manipular y enriquecer los datos a través del servicio de consulta según sus necesidades. Esto permite a los especialistas en marketing identificar, comprender y captar a los clientes de una mejor manera. Garantizar una gestión adecuada de los datos es un aspecto crítico de la gestión de la información personal, ya que ciertos datos pueden estar sujetos a restricciones de uso basadas en políticas organizativas y normativas legales. Es fundamental garantizar que los datos introducidos y sus operaciones relacionadas cumplan las políticas de uso de datos definidas.

El control de datos dentro de Query Service permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Esto desempeña un papel clave a la hora de garantizar que las políticas de uso se hayan aplicado según las regulaciones definidas por su empresa.

Se recomienda a las organizaciones que realizan habitualmente el procesamiento de datos que describan, practiquen y hagan cumplir estas directrices para crear un entorno que respete la privacidad para todos los usuarios.

Las siguientes categorías son fundamentales para cumplir con las regulaciones de cumplimiento de los datos al utilizar el servicio de consulta:

1. Seguridad
1. Auditoría
1. Uso de datos
1. Privacidad
<!-- 1. Data hygiene -->

Este documento examina cada una de las diferentes áreas de gobierno y muestra cómo facilitar el cumplimiento de los datos al utilizar el servicio de consulta. Consulte la [información general sobre gobernanza, privacidad y seguridad](../../landing/governance-privacy-security/overview.md) para obtener información más amplia sobre cómo Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de normas.

## Seguridad

La seguridad de los datos es el proceso para proteger los datos de accesos no autorizados y garantizar el acceso seguro durante todo su ciclo de vida. El acceso seguro se mantiene en Experience Platform mediante la aplicación de funciones y permisos mediante funciones como el control de acceso basado en roles y el control de acceso basado en atributos. Las credenciales, SSL y el cifrado de datos también se utilizan para garantizar la protección de datos en Platform.

La seguridad con respecto al servicio de consulta se divide en las siguientes categorías:

* [Control de acceso](#access-control): El acceso se controla mediante funciones y permisos, incluidos conjuntos de datos y permisos a nivel de columna.
* Protección de datos mediante [conectividad](#connectivity): Los datos se protegen mediante Platform y clientes externos al lograr una conexión limitada con credenciales que caducan o credenciales que no caducan.
* Protección de datos mediante [cifrado y claves a nivel de sistema](#encryption): La seguridad de los datos se garantiza mediante cifrado cuando los datos están en reposo.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### Control de acceso {#access-control}

El control de acceso en Adobe Experience Platform le permite utilizar [Adobe Admin Console](https://adminconsole.adobe.com/) para administrar el acceso a las funciones del servicio de consulta mediante permisos basados en funciones. Del mismo modo, se puede controlar el acceso a atributos de datos específicos mediante la administración de etiquetas en esquemas y campos de datos.

Esta sección describe los permisos de control de acceso requeridos que un usuario debe tener para utilizar completamente las funciones del servicio de consulta. Consulte los documentos de [administración de permisos](../../access-control/ui/permissions.md) y [administración de usuarios](../../access-control/ui/users.md) para obtener instrucciones detalladas sobre la asignación del acceso a un perfil de producto.

#### Permisos relevantes

Los permisos de control de acceso relevantes se definen en las tablas siguientes según su nivel de alcance.

**Permisos de ejecución de consultas**

Para ejecutar consultas dentro del servicio de consulta, se debe asignar una función a un usuario con el siguiente permiso:

| Permiso | Descripción |
|---|---|
| [!UICONTROL Administrar consultas] | Este permiso permite a los usuarios ejecutar la exploración de datos y las consultas por lotes, que pueden leer un conjunto de datos existente o escribir datos en conjuntos de datos. Esto incluye ambas `CREATE TABLE AS SELECT` (`CTAS`) y `INSERT INTO AS SELECT` (`ITAS`). |

**Permisos del conjunto de datos**

Esta sección sirve como guía del acceso basado en recursos necesario para acceder a los conjuntos de datos mientras se consultan los datos a través del servicio de consulta.

A través de la interfaz Permisos puede definir el control de acceso basado en recursos para un conjunto de datos y un esquema con los siguientes permisos:

| Permiso | Descripción |
|---|---|
| [!UICONTROL Administrar conjuntos de datos] | Este permiso proporciona acceso de solo lectura para esquemas y permite el acceso para leer, crear, editar y eliminar conjuntos de datos para su uso con el servicio de consulta. |
| [!UICONTROL Ver conjuntos de datos] | Este permiso permite acceso de solo lectura para conjuntos de datos y esquemas para su uso con el servicio de consulta. |

#### Control de acceso para columnas/campos

La función de control de acceso basado en atributos permite a los usuarios del servicio de consulta restringir el acceso a los datos críticos del usuario. El acceso se puede conceder o restringir en función de los permisos asignados a una función. El acceso de los usuarios a columnas individuales se controla mediante las etiquetas de uso de datos relevantes y los conjuntos de permisos aplicados a las funciones asignadas a los usuarios.

El etiquetado de grupos de campos de esquema y clases con etiquetas de uso de datos aplica restricciones de uso de datos a todos los esquemas con los mismos grupos de campos y clases. Consulte la descripción general sobre [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener información completa sobre esta función.

Esta función le permite conceder derechos de acceso sobre columnas confidenciales a los grupos de usuarios que elija. El control de acceso en una columna puede restringir las capacidades de lectura y escritura de un tipo concreto de usuario.

El control de acceso para las columnas se puede aplicar a nivel de esquema tanto para los esquemas estándar como para los específicos. Aplique etiquetas de uso de datos a esquemas XDM para restringir el acceso a una o más columnas. El etiquetado de datos se aplica de forma coherente, incluso para conjuntos de datos creados mediante Query Service utilizando un esquema predefinido o un esquema ad hoc generado como parte de la operación CTAS.

Una vez que se ha aplicado el nivel de acceso adecuado mediante etiquetas y funciones, se produce el siguiente comportamiento del sistema cuando un usuario intenta acceder a los datos no accesibles:

1. Si a un usuario se le ha denegado el acceso a una de las columnas de un esquema, también se le deniega el permiso de lectura o escritura en la columna restringida. Esto se aplica a los siguientes escenarios comunes:

   * **Caso 1**: Cuando un usuario intenta ejecutar una consulta que solo afecta a una columna restringida, el sistema genera un error que indica que la columna no existe.
   * **Caso 2**: Cuando un usuario intenta ejecutar una consulta con varias columnas, incluida una columna restringida, el sistema solo devuelve el resultado de todas las columnas no restringidas.

1. Si un usuario intenta acceder a un campo calculado, se le requiere que tenga acceso a todos los campos utilizados en la composición o que el sistema también deniegue el acceso al campo calculado.

#### Controles de acceso para vistas

El servicio de consultas permite utilizar ANSI SQL estándar para [`CREATE VIEW`](../sql/syntax.md#create-view) instrucciones. Para flujos de trabajo de datos muy confidenciales, debe aplicar los controles adecuados al crear vistas.

La variable `CREATE VIEW` palabra clave define una vista de una consulta, pero la vista no se materializa físicamente. En su lugar, la consulta se ejecuta cada vez que se hace referencia a la vista en una consulta. Cuando un usuario crea una vista desde un conjunto de datos, las reglas de control de acceso basadas en roles y atributos para el conjunto de datos principal son **not** aplicado jerárquicamente. Como resultado, se deben establecer permisos explícitamente en cada una de las columnas cuando se crea una vista.

### Conectividad {#connectivity}

Se puede acceder al servicio de consulta a través de la interfaz de usuario de Platform o formando una conexión con clientes compatibles externos. El acceso a todos los frentes disponibles está controlado por un conjunto de credenciales.

#### Conectividad mediante clientes externos

El acceso al servicio de consulta mediante un cliente de terceros requiere credenciales para la autorización. Estas credenciales son obligatorias para acceder al servicio de consulta con cualquiera de los clientes externos compatibles. Puede conectarse a clientes externos mediante una de las acciones siguientes: [credenciales que caducan](#expiring-credentials) o [credenciales que no caducan](#non-expiring-credentials).

#### Tiempo de conexión limitado mediante credenciales de expiración {#expiring-credentials}

[Credenciales de caducidad](../ui/credentials.md) permitir a los usuarios formar una conexión temporal con un cliente externo. Este conjunto de credenciales solo es válido durante 24 horas. La caducidad de estos tipos de credenciales se puede ver junto con la pestaña de credenciales en el panel del servicio de consultas.

![La pestaña de credenciales del espacio de trabajo del servicio de consulta con las credenciales caducadas resaltadas.](../images/data-governance/overview/expiring-credentials.png)

#### Credenciales que no caducan {#non-expiring-credentials}

[Credenciales que no caducan](../ui/credentials.md#non-expiring-credentials) permite formar una conexión permanente con un cliente externo, facilitando la conexión al servicio de consulta sin necesidad de una contraseña manual.

Para activar la opción de generar credenciales que no caduquen, debe seguir el esquema [flujo de trabajo previo](../ui/credentials.md#prerequisites). Como parte de este proceso, el administrador de su organización debe configurar los permisos para el perfil del producto, lo que le otorga al administrador el control sobre qué cuentas tienen acceso para utilizar credenciales que no caduquen.

Se pueden asignar funciones a las cuentas de usuario técnicas permitidas con credenciales no caducadas para garantizar un control de datos adecuado definiendo el ámbito de su acceso de lectura y escritura en función de sus responsabilidades y necesidades. Consulte la sección anterior de [uso de permisos basados en funciones mediante control de acceso](#access-control) para administrar el acceso al servicio de consulta.

Una vez completado el flujo de trabajo previo, los usuarios autorizados ahora pueden [generar las credenciales de conexión necesarias](../ui/credentials.md#generate-credentials).

#### Cifrado de datos SSL

Para aumentar la seguridad, el servicio de consulta proporciona compatibilidad nativa con conexiones SSL para cifrar comunicaciones cliente/servidor. Platform admite varias opciones SSL para adaptarse a sus necesidades de seguridad de datos y equilibrar la sobrecarga de procesamiento del cifrado y el intercambio de claves.

Consulte la guía de [Opciones SSL para conexiones de cliente de terceros con servicio de consulta](../clients/ssl-modes.md) para obtener más información, incluido cómo conectarse mediante el `verify-full` Valor del parámetro SSL.

### Cifrado {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

El cifrado es el uso de un proceso algorítmico para transformar datos en texto codificado e ilegible para garantizar que la información esté protegida y sea inaccesible sin una clave de descifrado.

El cumplimiento de los datos del servicio de consulta garantiza que los datos siempre estén cifrados. Los datos en tránsito siempre son compatibles con HTTPS y los datos en reposo se cifran en un almacén de Azure Data Lake mediante claves de nivel de sistema. Consulte la documentación sobre [cómo se cifran los datos en Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html) para obtener más información. Para obtener más información sobre cómo se cifran los datos en reposo en el almacenamiento de Azure Data Lake, consulte [documentación oficial de Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## Auditoría {#audit}

El servicio de consulta registra la actividad de los usuarios y la categoriza en diferentes tipos de registro. Registra la información de suministro en **who** performed **what** acción y **when**. Cada acción registrada en un registro contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y atributos adicionales relevantes para el tipo de acción.

Un usuario de Platform puede solicitar cualquiera de las categorías de registro que desee. Esta sección proporciona detalles sobre el tipo de información capturada para el servicio de consulta y a la que se puede acceder a esta información.

### Registros de consultas {#query-logs}

La interfaz de usuario de registros de consulta permite supervisar y revisar los detalles de ejecución de todas las consultas que se han ejecutado mediante el Editor de consultas o la API del servicio de consultas. Esto aporta transparencia a las actividades del servicio de consulta, lo que le permite comprobar los metadatos para **all** las consultas que se han ejecutado en el servicio de consulta. Incluye todo tipo de consultas, ya sea una consulta exploratoria, por lotes o programada.

Se puede acceder a los registros de consulta a través de la interfaz de usuario de Platform en la [!UICONTROL Registros] de la pestaña [!UICONTROL Consultas] espacio de trabajo.

![La pestaña Registro de consultas con el panel de detalles resaltado.](../images/data-governance/overview/queries-log.png)

### Registros de auditoría {#audit-logs}

Los registros de auditoría contienen información más detallada que los registros de consulta y permiten filtrar los registros en función de atributos como usuario, fecha, tipo de consulta, etc. Más allá de los detalles disponibles en la interfaz de usuario del registro de consultas, los registros de auditoría almacenan detalles sobre usuarios individuales junto con sus datos de sesión o la conectividad con un cliente de terceros.

Al proporcionar un registro exacto de las acciones de los usuarios, una pista de auditoría puede ayudar a solucionar problemas y ayudar a su empresa a cumplir de manera eficaz con las políticas de administración de datos corporativos y los requisitos regulatorios. Los registros de auditoría proporcionan un registro de todas las actividades de Platform. Con los registros de auditoría puede auditar las acciones del usuario relacionadas con la ejecución de consultas, las plantillas y las consultas programadas para aumentar la transparencia y visibilidad de las acciones realizadas por los usuarios en el servicio de consulta.

La tabla siguiente indica las categorías de consulta capturadas por los registros de auditoría y los tipos de acción que registran:

| Categoría | Tipo de acción |
|---|---|
| Consulta | Ejecutar |
| Plantilla de consulta | Crear, eliminar, actualizar |
| Consulta programada | Crear, eliminar, actualizar |

A continuación se muestra una lista de tres registros de servidor ampliados que contienen más detalles que los que se encuentran dentro de los registros de consulta. Los registros ampliados se encuentran dentro de las categorías de consulta de registros de auditoría:

1. **Registros de metaconsulta**: Cuando se ejecuta una consulta, se ejecutan varias subconsultas de servidor asociadas (como el análisis). Estos tipos de consultas se conocen como consultas de &quot;metadatos&quot;. Los detalles pertinentes se encuentran en los registros de auditoría.
1. **Registros de sesión**: El sistema crea un registro de entrada de sesión para un usuario cuando inicia sesión en el servicio de consulta, independientemente de si ejecuta una consulta.
1. **Registros de conexión de cliente de terceros**: Se genera un registro de auditoría de conectividad cuando un usuario conecta correctamente Query Service con un cliente de terceros.

Consulte la [información general sobre registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md) para obtener más información sobre cómo los registros de auditoría pueden ayudar a su organización a abordar el cumplimiento de los datos.

## Uso de datos {#data-usage}

El marco de control de datos de Platform proporciona una manera uniforme de utilizar los datos de forma responsable en todas las soluciones, servicios y plataformas de Adobe. Coordina el enfoque sistémico para capturar, comunicar y usar metadatos en todo Adobe Experience Cloud. A su vez, esto ayuda a los responsables del tratamiento de datos a etiquetar los datos según las acciones de marketing necesarias y las restricciones impuestas a esos datos a partir de estas acciones de marketing deseadas. Consulte la descripción general sobre [etiquetas de uso de datos](../../data-governance/labels/overview.md) para obtener más información sobre cómo la administración de datos le permite aplicar etiquetas de uso de datos a conjuntos de datos y campos.

Se recomienda trabajar para lograr el cumplimiento de los datos en todas las etapas del recorrido de los datos. Con este fin, los conjuntos de datos derivados que utilizan esquemas ad hoc deben etiquetarse adecuadamente como parte del marco de control de datos. Existen dos tipos de conjuntos de datos derivados formados por el servicio de consulta: conjuntos de datos que utilizan un esquema estándar y conjuntos de datos que utilizan un esquema ad hoc.

>[!NOTE]
>
>Los conjuntos de datos que se crean mediante el servicio de consulta se denominan &quot;conjuntos de datos derivados&quot;.

Como los esquemas ad hoc los crea un usuario individual para un propósito específico, los campos de esquema XDM tienen un espacio de nombres para ese conjunto de datos en particular y no están destinados a utilizarse en distintos conjuntos de datos. Como resultado, los esquemas ad hoc no son visibles de forma predeterminada en la interfaz de usuario del Experience Platform. Aunque no hay diferencia en la aplicación de etiquetas de uso de datos entre esquemas estándar y específicos, los esquemas ad hoc creados por el servicio de consulta con el propósito de etiquetar primero deben ser visibles en la interfaz de usuario de Platform. Consulte la guía de [descubrimiento de esquemas ad hoc en la interfaz de usuario de Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) para obtener más información.

Una vez que haya accedido al esquema, puede [aplicar etiquetas a campos individuales](../../xdm/tutorials/labels.md). Una vez que se ha etiquetado un esquema, todos los conjuntos de datos que se derivan de ese esquema heredan esas etiquetas. Desde aquí puede configurar políticas de uso de datos que restrinjan la activación de datos con ciertas etiquetas a determinados destinos. Para obtener más información, consulte la descripción general de [políticas de uso de datos](../../data-governance/policies/overview.md).

## Privacidad {#privacy}

[Privacy Service](../../privacy-service/home.md) le ayuda a administrar las solicitudes de los clientes para acceder a sus datos y eliminarlos de acuerdo con las normas legales de privacidad. Para ello, busca en los datos identificadores preexistentes y accede a esos datos o los elimina en función del trabajo de privacidad solicitado. Los datos deben etiquetarse correctamente para que el servicio pueda determinar a qué campos acceder o eliminar durante los trabajos de privacidad. Los datos que están sujetos a solicitudes de privacidad deben contener información de identidad del cliente para enlazar los distintos datos con la persona individual a la que se aplica la solicitud de privacidad. El servicio de consulta puede enriquecer los datos que utiliza con un identificador único con el fin de satisfacer los trabajos de privacidad.

Las solicitudes de privacidad se pueden enviar al lago de datos o al almacén de datos de perfil. Los registros eliminados del lago de datos no resultan en la eliminación de perfiles que se hicieron de esos registros. Además, un trabajo de privacidad para eliminar información personal del lago de datos no elimina su perfil, por lo que cualquier información (que contenga ese ID de perfil) ingerida después de completar el trabajo de privacidad actualiza ese perfil como de costumbre. Esto reafirma la necesidad de identificar correctamente los datos utilizados en los esquemas específicos.

Consulte la documentación del Privacy Service para obtener más información sobre [datos de identidad para solicitudes de privacidad](../../privacy-service/identity-data.md) y cómo configurar sus operaciones de datos y aprovechar las tecnologías de Adobe para recuperar de forma eficaz la información de identidad adecuada para las solicitudes de privacidad de los clientes.

Las funciones del servicio de consulta para la administración de datos simplifican y optimizan el proceso de categorización de datos y cumplimiento de las regulaciones de uso de datos. Una vez identificados los datos, el servicio de consulta le permite asignar la identidad principal en todos los conjuntos de datos de salida. You **must** agregue identidades al conjunto de datos para facilitar las solicitudes de privacidad de datos y trabajar para el cumplimiento de los datos.

Los campos de datos del esquema se pueden configurar como un campo de identidad a través de la interfaz de usuario de Platform y el servicio de consulta también le permite [marcar las identidades principales utilizando el comando SQL &quot;ALTER TABLE&quot;](../sql/syntax.md#alter-table). Configuración de una identidad mediante el `ALTER TABLE` es especialmente útil cuando los conjuntos de datos se crean con SQL en lugar de directamente desde un esquema a través de la interfaz de usuario de Platform. Consulte la documentación para obtener instrucciones sobre cómo [definir campos de identidad en la interfaz de usuario](../../xdm/ui/fields/identity.md) al utilizar esquemas estándar.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
